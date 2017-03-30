# Engagement 1 Notes

TA3 and TA5 should read this document to learn our assumptions and
limitations for Engagement 1.

## Expected Procedure for Engagement

0. Please read notes below.

1. Build new image on build VM.

2. Flash image to device.

3. Run Clearscope unit and system tests and verify all tests pass.  Do
not run Ingestor (Ingestor and unit tests cannot be run at same
time). 

4. Reflash device for engagement.  Remove device from USB.  Wait for
the device to boot, and come to the lock screen.

5. Connect device to Ingestor machine via USB.

6. Run Ingestor in usb mode, and wait 5 minutes for the Ingestor to
ingest the boot stream.  [More documentation](cdm-ingestor.md).

7. Run apps, [background scripts](background-traffic.md), etc.
Remember that each app needs to be
[instrumented](instrumenting-new-app.md) before installed on the
device.

8.  If anything goes wrong, the device will need to be reflashed
before reusing.  See below.

## Notes for Engagement 1

* During the initial few minutes of the Ingestor run, the device
  should not be used because the Ingestor is receiving the provenance
  stream from booting and is inundated with this data.  The USB
  connection in the VM is quite slow, and you should wait until the
  Ingestor ingests the boot record.  A few minutes should be enough.

* Do not reboot the device during the engagement.  The device cannot
  be rebooted without re-flashing.  This means that if a device
  rebooted, the previous boots tag definitions will be invalid.

  If the phone needs to be rebooted, it will need to be reflashed, and
  the streams from the separate sessions (before and after reboot)
  should be reported to TA2 as separate runs.

* If you cancel the Ingestor, the device may stop responding since the
  device is expecting the Ingestor to read and pop the provenance
  event stream.  If you cancel the Ingestor, you will need to reflash
  the device (see above).

* Video recording via the camera is not support because of an issue
  with the kernel device driver for the camera.  This is present on a
  non-instrumented AOSP fresh system, and is not a limitation of
  ClearScope.

* The background scripts sometimes fail to connect to the phone on the
  first run after a reflash.  If this happens, just rerun the
  background script.

* java.nio.ByteBuffer and subclasses are not supported for tag
  propagation.  Please do not use them in engagement applications.

* Cannot run system tests while using the Ingestor in USB mode.

## Changes needed for VM

1.clean rebuild