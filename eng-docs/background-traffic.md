# Generating Background Traffic

## THE BACKGROUND TRAFFIC FRAMEWORK HAS NOT BEEN UPGRADED TO WORK ON ANDROID 6.0.1. BACKGROUND TRAFFIC GENERATION WILL NOT WORK CURRENTLY ON THE TA3 MACHINES.

## General notes

If you have just flashed the phone, sometimes, you need to disconnect
and reconnect the USB connection.

## Loading Web Pages

### Prerequisites

1. You should follow all setup in [Additional Device
Setup](additional-device-setup.md).

1. The device is connected via ADB (use `adb devices` to confirm
connection). 

1. The device needs a data connection (wifi, cellular data, etc.).

1. Navigate to www.google.com.  Two modal dialogs should pop up.
   1. Accept location queries
   1. Decline to download the Google app.
   
1. The device is in on the home screen in portrait orientation.

### Script

The script to load web pages is on the VM at:

`/home/clearscope/TC/tc-scripts/background-traffic/load-web-pages.py`

It has the following usage:

```
usage: load-web-pages.py [-h] [-g] [-f FILE] [-u URL] [-l LOOP]

Load webpage url(s) on connected device via ADB.

optional arguments:
  -h, --help            show this help message and exit
  -g, --gui             Send over GUI interaction commands instead of Intent
                        (slower)
  -f FILE, --file FILE  Read URLs from file, one URL per line
  -u URL, --url URL     URL to load
  -l LOOP, --loop LOOP  Loop over URL(s) LOOP times, -1 is infinite
```

### Discussion

The script supports both Intent-based commands and GUI commands.
Intent-based operation will construct an Intent string, and inject
into the phone, with no button presses. GUI interaction will send a
stream of screen presses and events over ADB to load each webpage. 

### Tests

There are two test files that include 15 and 1000 web pages,
top15-websites and top1000-websites, respectively.

`$ python load-web-pages.py -l 2 -f top15-websites -g`

Will load each url from the top 15 websites file using GUI mode,
looping through the from start to end twice.

## Composing and Sending Emails

### Prerequisites

1. You should follow all setup in [Additional Device
Setup](additional-device-setup.md).

1. You must have a valid email account already set up with the
device.  If you launch the Mail app, it will ask you to create an
email account.  You should test sending from this account to make sure
you have set up the outgoing server correctly.

1. The device needs to unlocked and on the home screen.

### Script

The script to load web pages is on the VM at:

`/home/clearscope/TC/tc-scripts/background-traffic/compose-and-send-emails.py`

```
usage: compose-and-send-emails.py [-h] [-f FILE] [-l LOOP]

Compose and send emails on connected device via ADB.

optional arguments:
  -h, --help            show this help message and exit
  -f FILE, --file FILE  File to load for emails. Each line is an email with
                        for: to_address|subject|body
  -l LOOP, --loop LOOP  Loop over the email file LOOP times
```

### Discussion

The script is extremely slow, e.g., it takes 1 minute to send each
email, as the script creates screen and button presses for all input. 

### Tests

There is a test file of 100 short email messages in the file
`100-emails`.

You can run the script with the test input with:

`$ python compose-and-send-emails.py -f 100-emails`


