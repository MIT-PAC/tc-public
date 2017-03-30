# Additional Device Setup

In order to install an application, debug an application, and run our
system tests, additional device setup is required.  Follow the steps
below:

(These instructions assume you have already flashed the phone with the
ClearScope system image)

1. Become a developer: Settings -> About Phone.  Click "Build Number"
section 7 times.  You will see a confirmation that you are a
developer.

1. Go back to home screen.  Settings -> Developer Options.  Make sure
that Developer mode is on (the top toggle).

1. Enable "Stay Awake" toggle.

1. Enable "USB debugging" toggle.

1. Enable "Allow Mock Locations" toggle.

## First time using device

1. Enable developer mode as above
2. Enable USB debugging
3. Enable "OEM Unlocking"
3. Plug into computer
4. Trust computer as USB debugger
5. `adb reboot bootloader`
5. `fastboot oem unlock` (Press Power button on phone to accept OEM unlock)




