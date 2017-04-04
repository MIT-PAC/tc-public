# Engagement 1 Notes

TA3 and TA5 should read this document to learn our assumptions and
limitations for Engagement 1.

## Expected Procedure for Engagement

0. Please read notes below.

1. Connect device to Ingestor machine via USB.

1. Run Ingestor in usb mode, and wait 5 minutes for the Ingestor to
ingest the boot stream.  [More documentation](cdm-ingestor.md).

1. Run apps.  Remember that each app needs to be
[instrumented](instrumenting-new-app.md) before installed on the
device.

1.  If anything goes wrong, the device will need to be reflashed or
rebooted before reusing, and the Ingestor rerun.

## Notes for Engagement 1

* During the initial few minutes of the Ingestor run, the device
  should not be used because the Ingestor is receiving the provenance
  stream from booting and is inundated with this data.  A few minutes
  should be enough.

* The device should only be rebooted if an error has occurred.

* If you cancel the Ingestor, the device may stop responding since the
  device is expecting the Ingestor to read and pop the provenance
  event stream.  If you cancel the Ingestor, you will need to reboot
  the phone.

* java.nio.ByteBuffer and subclasses are not supported for tag
  propagation.  Please do not use them in engagement applications.

* Cannot run system tests while using the Ingestor in USB mode.

