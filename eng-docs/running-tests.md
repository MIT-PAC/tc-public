# Running ClearScope Unit and System Tests on a Device

## THESE TESTS CURRENTLY DO NOT RUN ON THE TA3 MACHINE

This documents provides instructions for running our system and units
tests on a device flashed with the ClearScope system image.  At this
time only the Nexus 6 is supported.

**For each of the tests scripts below, the phone must be connected via USB, and the phone must be unlocked (screen on).**

## Run Unit Tests

1. `$ run-unit-tests-tc`

## Run System Tests

### With prompt for phone connected and unlocked; requires user to press key.

Cannot be running the Ingester when the system test run.

1. `$ run-system-tests-tc`  


