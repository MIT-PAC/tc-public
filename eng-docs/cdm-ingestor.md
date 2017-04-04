# ClearScope CDM Ingestor

## Summary

### Running the Ingestor

Log into Ingestor box as `darpa` user:

1. `$ cd ~/ta1-integration-clearscope`

1. `$ adb devices` (verify that device is in list of attached devices)

1. Launch the Ingestor:
   ```
   java -jar target/ta1-integration-clearscope-1.0-SNAPSHOT-jar-with-dependencies.jar \
       -usb \
       ta1-clearscope-cdm17 -ks 10.0.6.9:9092 \
       -psf ../ta3-serialization-schema/avro/TCCDMDatum.avsc
   ```
   
Note: The last command should be run in a manner such that it will
continue to run after logout (`tmux` or `screen` are nice).

#### Kafta Addresses for TA2 Teams

* RIPE Kafka cluster:   10.0.50.9:9092
* MARPLE Kafka cluster: 10.0.50.19:9092
* ADAPT Kafka cluster:  10.0.50.24:9092

### Bringing down the Ingestor

1. `$ adb reboot` (to reboot the phone) or `$ adb shell su root 'svc
power shutdown'` (to power down the phone).

2. control-c (or otherwise kill) the Ingestor.

## Background

* `.cst` files are the output format of the ClearScope provenance
  system.  They are human readable and give the stream of tag events
  from a device for a particular time interval.

* The CDM Ingestor converts ClearScope's cst provenance format to the
  CDM format of provenance records.

* The Ingestor has the functionality to connect to a device via USB,
  and read the cst provenance stream from the device and create CDM
  records in real-time.

* A ClearScope Android device has multiple modes for recording tag
  streams.  During boot, and until otherwise directed, the device will
  write the tag stream to a protected file on the device.  The default
  location for the file is:

   `/data/provmsgr/prov-output`

 This file can be read with the adb command:

   `$ adb shell su -c cat /data/provmsgr/prov-output`

 This command will direct the contents of the tag file to standard out.


## ClearScope CDM Ingestor

To read and convert the stream of tags in real time, you use the
ClearScope CDM Ingestor (or just Ingestor).  The current expected mode
of operation is for the Ingestor to be executed shortly after the
phone is booted, while connected via USB to a server.  

The ingestor will perform the following when it is run:

1. Change the mode of the device provenance communicator to stream
mode.  The tag events will no longer be written to the file described
above.

1. Spawn a thread to buffer the stream of tags from the phone.

1. Read and convert the tags written to the tag file (describing boot
and early phone operation) in a thread.

1. Once the file tag events are all converted, the Ingestor will then
switch to reading from the live stream over USB.

The above should all be seamless to the user.

The Ingestor is located at:

`/home/mgordon/ta1-integration-clearscope`

We recommend that you run java with at least 4GB of maximum heap space.  See below.

To execute the Ingestor, change to the above directory and issue the
following command:

```
$ adb devices         # verify that devices is listed

$ adb root            # make sure adb is running as root to allow access to prov stream

$ java -Xmx8g -Xms1g -jar target/ta1-integration-clearscope-1.0-SNAPSHOT-jar-with-dependencies.jar \
  -usb file:cdm_files/last-run.cdm -psf \
  ../ta3-serialization-schema/avro/TCCDMDatum.avsc
```

The `-usb` option directs the Ingestor to read the tag stream from the
device with the steps given above.  This command writes the converted
CDM records to the files `cdm_files/last-run.cdm`.

Please wait until you see this output:

`Done reading from boot provenance stream file...switching to FIFO`

This output signals that the device is ready for the engagement traffic.

There are many other options for the Ingestor that were provided by
BBN, for example to connect to a Kafka server.  Please see their
documentation for further information.

Note that it is assumed that the once the Ingestor is executed in USB
mode, the phone will not be disconnected from the Ingestor until is
recording is finished.  If you want to stop recording, it is
recommended at this point to reboot the phone. To do this, open a new
terminal window, and issue the `adb reboot` command to reboot the
phone.  You can then kill the Ingestor (with `control-c`).

### Run with Kafka

```
       java -jar $(CDM_CLEARSCOPE_JAR) \
               -usb \
               ta1-clearscope-bovia-cdm13 -ks 10.0.6.9:9092 \
               -psf ../ta3-serialization-schema/avro/TCCDMDatum.avsc



```

## Other Modes of the Provenance Communicator

You can issue ADB commands to control where the tag stream generated
by the ClearScope system is directed.  At boot, the tag stream is
written to a file as described above.

1. To direct the tag stream to /dev/null (which in practice discards
the tag stream):

 `$ adb shell su -c /system/bin/provmsgr direct-to-dev-null`

1. To direct the tag stream to the Android log:

 `$ adb shell su -c /system/bin/provmsgr direct-to-log`

1. To direct to the `/data/provmsgr/prov-output` file:

 `$ adb shell su -c /system/bin/provmsgr direct-to-file`






