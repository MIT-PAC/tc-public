# ClearScope High-Level Category Descriptions

## Purpose

This document provides an English description for each of the source
/ sink high-level categories used by ClearScope's CDM output.  The
categories are provided in the `enum SrcSinkType` of CDMv17, and each
`SrcSinkObject` has a `SrcSinkType`.  

##ACCESSIBILITY_SERVICE

Accessibility services are intended to assist users with disabilities
in using Android devices and apps. They run in the background and
receive callbacks by the system when AccessibilityEvents are
fired. Such events denote some state transition in the user interface,
for example, the focus has changed, a button has been clicked, etc.  

An application can register to help with accessibility or it can query
/ influence the registered accessibility apps.

##ACTIVITY_MANAGEMENT

Control instrumentation of DEX code that is associated with an Activity.

##ALARM_SERVICE

Alarms give you a way to perform time-based operations outside the
lifetime of your application. For example, you could use an alarm to
initiate a long-running operation, such as starting a service once a
day to download a weather forecast.

Examples of calls include setting alarm and passing code to run at
alarm firing.

##ANDROID_TV

Access to the Android TV provider, if available on the device.  

##AUDIO_IO

Access to and communication with the AudioService for controlling
volume, querying audio state (e.g., is the speaker phone on?), setting
ringtones, play audio clips and ringtones, and callbacks for audio
changes (like volume changes).

##BACKUP_MANAGER

Acesss to and communication with the BackupManager.  The interface
through which an application interacts with the Android backup service
to request backup and restore operations.  Android's backup service
allows you to copy your persistent application data to remote "cloud"
storage, in order to provide a restore point for the application data
and settings. 

##BINDER

Un-categorized Binder communication.

##BLUETOOTH

Access to and communication with the Bluetooth services including
low-level Bluetooth connections, and high-level services over
Bluetooth like Bluetooth headset service.

##BOOT_EVENT

An event and data that concerns boot events and ordering.

##BROADCAST_RECEIVER_MANAGEMENT

Activity Manager calls that service Broadcast receivers including
un/registering a receiver, sending a broadcast intent, and finishing a
receiver. 

##CAMERA

Access to, callbacks from, and communication with the CameraService.  

##CLIPBOARD

Access to system clipboard.

##COMPONENT_MANAGEMENT

Management of local and remote components of Android applications.
For example, starting a local or remote Activity.

##CONTENT_PROVIDER

Communication to and from a Content Provider, including registering
data observers, sync, and callbacks.

##CONTENT_PROVIDER_MANAGEMENT

##DATABASE

Registering for notification for changes in a database.

##DEVICE_ADMIN

Querying and setting device policies such as resetting password,
proxy, minimum password length.

##DEVICE_SEARCH

Accesses to the Search Manager to perform or update global device text
search. 

##DEVICE_USER

Accesses to the User Manager that provides an interface to querying
and writing user settings such as setting user icon and if a user is
restricted. 

##DISPLAY

Access to the Display Manager that provides access to remote displays
over the network.

##DROPBOX

Access to the Dropbox Manager for adding and querying a Dropbox account.

##EMAIL

Access to the global Email Service for sending email and searching email.

##EXPERIMENTAL

Access to experimental features of the device such as Strict Mode and
RPC performance modes.

##FILE

Posix calls for opening, closing, writing and reading files on the
file system. 

##FILE_SYSTEM_MANAGEMENT

Access to the Mount service on the device which provides access to
mounting of file systems and connected file system devices such as USB
drives.  Methods include requests for mounting, querying mount state,
querying usages stats on mount point, and encrypting / decrypting
storage.  

##FINGERPRINT

Access to fingerprint sensor service including enrollment, callbacks,
and error processing.

##FLASHLIGHT

Turn on / off flashlight and query the state of the flashlight.

##HDMI

Access to, control off, and data transfer with devices connected
through the HDMI port of the device.  

##IDLE_DOCK_SCREEN

Access to the Dream Manager and Service.  Dreams are interactive
screensavers launched when a charging device is idle, or docked in a
desk dock.

##IMS

IP Multimedia Core Network Subsystem accesses the standard interface
for voice and other multimedia services over IP.  Methods in this
category control voice call actions, voice calls, callbacks for voice
and multimedia calls, and information for current connections.

##INFRARED

Access to and transfers over the consumer IR hardware if present on
device.

##INSTALLED_PACKAGES

Access to package (app) installer, manager, and launchers.  Actions
include installing packages, deleting packages, modification of
installed packages callbacks, checking for application permissions,
app UID, keys, intent filters, etc.

##JSSE_TRUST_MANAGER

Access to Java Secure Socket Extension trust manager access.  

##KEYCHAIN

Access to device keychain and keystore for installing, querying, and
deleting key pairs and certificates.

##KEYGUARD

Access to various methods and services for unlocking the device from
locked state.  This includes access to Face Lock (if available), key
guards (key codes and passwords), and other widgets for locking /
unlocking.  Methods include callbacks for various states of the
keyguard  / keylock and for accessing settings of the keyguard /
keylock.  

##LOCATION

Access to the various services and sensors for querying and setting
the device location.  Methods include callbacks for location changes,
setting the preferred location determination mechanism, determining
country from cell tower information, access to underlying GPS
hardware.  Also included is access to the device geofencing services
and hardware for adding and callbacks for geofences.

##MACHINE_LEARNING

Access to machine learning services.  Mostly undocumented, the
functionality of the services is not clear.

##MEDIA_LOCAL_MANAGEMENT

Access to the Media Browser service that enables apps to browse local
media files on the device.  Media browse services enable applications
to browse media content provided by an application and ask the
application to start playing it. 

##MEDIA_LOCAL_PLAYBACK

Access to media sessions for playing media local to the device.
Actions includes setting file for playback, setting volume, adding
files to queue, callbacks for state of playback / user commands,
querying / setting media information for files (e.g., artist, song
name, etc.), and controlling / querying state of playback.


##MEDIA_NETWORK_CONNECTION

Provides APIs that let you interact directly with connected cameras
and other devices, using the PTP (Picture Transfer Protocol) subset of
the MTP (Media Transfer Protocol) specification.  Also provides access
to system service for fetching possibly cached remote content from Internet
via HTTP.  

##MEDIA_REMOTE_PLAYBACK

Access to various services for controlling media playback on connected
devices such as remote displays.  Services include the remote service
which allows the device to act as a remote control for a connected
device.  The media router APIs enable a broad range of media output to
playback equipment connected to Android devices through wireless and
wired means. 

##NETWORK

Posix system calls for opening, closing, sending on, and receiving
from network sockets.  

##NETWORK_MANAGEMENT

Access to various services that control or monitor network
connectivity.  These services include:

* Network Management Service provides access to methods for setting
  and querying a connection's state including firewall state and other
  configuration. 

* Connectivity Manager with actions such as querying network
  information and capabilities, VPN, tethering, and proxies, and
  switching between networks.

* Ethernet Manager provides access to wired ethernet if available.
  Setting configuration.

* Network event observer provides callbacks for various changes in
  network state including DNS changes and route changes.

* Network Policy Manager provides mechanisms for setting and querying
  basic network policies based on UID.

* Network Stats and Scores: Access to various networks statistics such
  as bytes per app.

* WifiManager provides access to Wifi networks available including
  list of access points, current access point configuration, and
  Wifi hardware access.

##NFC

Access to the NFC hardware if available on device.  Methods includes
creating and sending an NFC message, and callbacks for receiving NFC
messages.  

##NOTIFICATION

Access to the notification manager.  Notifications can take different
forms: A persistent icon that goes in the status bar and is accessible
through the launcher, (when the user selects it, a designated Intent
can be launched), Turning on or flashing LEDs on the device, or
Alerting the user by flashing the backlight, playing a sound, or
vibrating.  

##PAC_PROXY

Access to proxy auto-config service for phone for apps that include
PAC files to set proxy setting per connection.

##PERMISSIONS

Access to the services that interact with application permission and
restrictions:

* Restrictions Manager provides a mechanism for apps to query
  restrictions imposed by an entity that manages the user. Apps can
  also send permission requests to a local or remote device
  administrator to override default app-specific restrictions or any
  other operation that needs explicit authorization from the
  administrator.

* Apps Ops Manage allows fine-grained control over application
  permissions, such as revoking a single permission for an app.  

##PERSISTANT_DATA

Access to service for reading and writing data blocks to a persistent
partition.

##POWER_MANAGEMENT

Provides access to the following services:

* Power Manager provides control and queries of various power
  management features of the device including sleeping, screen
  brightness, and power save mode.

* Battery Stats provides access to state and history regarding device
  battery, sensors and hardware battery utilization, and jobs battery
  utilization. 

##PRINT_SERVICE

Access to the Android printing services:

* Print Manager: System level service for accessing the printing
  capabilities of the device. 

* Print Service: Print services are plug-in components that know how
  to talk to printers via some standard protocols. These services
  serve as a bridge between the system and the printers. 

##PROCESS_MANAGEMENT

Methods for accessing information and setting configuration for
application processes including application scheduling priority,
callback for remote component lifecycle changes (resuming, not
responding, process death), and process statistics.  

##RPC

General RPC that cannot be categorized specifically such as sending an
Intent and receiving an Intent, sending a cancellation signal, and
sending messages with a payload to/from a bound service.

##SCREEN_AUDIO_CAPTURE

Access to the Media Projection Service that allow screen and audio
capture sessions.

##SERIAL_PORT

Access to serial port on the device if present.

##SERVICE_MANAGEMENT

Methods for managing service components of app or remote
applications.  The calls include listing available services, starting
/ stopping services, binding / unbinding services, and publishing
services.  Also methods for scheduling the previous calls.

##SMS_MMS

Method for access the SMS/MMS capabilities of the device.  These
include callback for message receipt / sending, enabling / disabling
cell broadcast, querying state of telephony systems, and sending /
receiving message data.

##SPEECH_INTERACTION

Access to various services that provide speech input and speech to
text (and vice versa) capabilities on the device:

* Callbacks for sound triggers and word recognition

* Voice interaction sessions

* Text to speech service

##STATUS_BAR

The status bar is the sliver of notification area at the top of the
Android screen.  Methods in this category provide access to the status
bar including sending updates and changing state of the bar.  Also,
various callback are defined for notification of changes to the status
bar. 

##SYNC_FRAMEWORK

The sync component encapsulates the code for the tasks that transfer
data between the device and a server.  

##TELEPHONY

Method for interacting with services that abstract the various
telephony subsystems on the device:

* Carrier Messaging: Sending and receiving SMS/MMS messaging and
  callbacks. 

* Connection Service: Provides apps the ability to make phone calls
  (VoIP or otherwise) and calls to be integrated into the built-in
  phone app.

* In-Call Service: This service is implemented by any app that wishes
  to provide the user-interface for managing phone calls. Telecom
  binds to this service while there exists a live (active or incoming)
  call, and uses it to notify the in-call app of any live and recently
  disconnected calls. An app must first be set as the default phone
  app (See getDefaultDialerPackage()) before the telecom service will
  bind to its InCallService implementation.

* Telecom Manager / Service / Registry: Provides access to information about
  active calls and registration/call-management functionality. Apps
  can use methods in this class to determine the current call state.

* Video Provider: Video calling

* Phone state: monitoring changes in specific telephony states on the
  device, including service state, signal strength, message waiting
  indicator (voicemail), and others.

* Sip Services

##TEXT_SERVICES

Global services for modifying user text input including the spell
checker.  

##THREADING

This is an API for scheduling various types of jobs against the
framework that will be executed in an application's own process 

##TIME_EVENT

Events associated with system time including change date/time, query
date/time, and change timezone. 

##UI

Methods for interacting with the user interface including:

* Window Manager

* Input Manager: Central system API to the overall input method
  framework (IMF) architecture, which arbitrates interaction between
  applications and the current input method.  This includes both the
  app and system services.

* UI Mode Manager for changing UI modes, e.g., night mode, car mode,
  etc. 

##UI_AUTOMATION

Methods for interacting with the device's UI by simulation user actions
and introspection of the screen content. It relies on the platform
accessibility APIs to introspect the screen and to perform some
actions on the remote view tree. It also allows injecting of arbitrary
raw input events simulating user interaction with keyboards and touch
devices.  

##UI_RPC

Methods for interacting with a remote apps UI components.

##UID_EVENT

Calls of the following:

* Methods for notification of user switching events.

* RPC calls for querying the UID of an RPC, listing processes by UID,
  and killing app by UID.

##USAGE_STATS

Access to Usage Stats Manager.  Provides access to device usage
history and statistics. Usage data is aggregated into time intervals:
days, weeks, months, and years.  

##USB

Access to device USB Manager for access to USB connections including
USB debugging and low-level device interaction via USB.

##USER_ACCOUNTS_MANAGEMENT

Access to services that control user account information on device and
various other account services (e.g., facebook accounts, google
accounts):

* Account manager: provides access to a centralized registry of the
  user's online accounts. The user enters credentials (username and
  password) once per account, granting applications access to online
  resources with "one-click" approval.

* Account Authenicator: services for creating authentication routines
  for accounts.

##VIBRATOR

Access to the vibrator hardware on the device.

##WAKE_LOCK

Advisory wakelock-like mechanism by which processes that should not be
interrupted for OTA/update purposes can so advise the OS. This is
particularly relevant for headless or kiosk-like operation.

##WALLPAPER_MANAGER

Provides access to the system wallpaper. With WallpaperManager, you
can get the current wallpaper, get the desired dimensions for the
wallpaper, set the wallpaper, and more.  

##WAP

Processing WAP Push messages. A WAP Push message is a binary encoded
XML file that can direct a mobile phone to content on the web.  WAP
Push messages are used to send ringtones, wallpapers and games to
mobile phones after the user has sent a paid SMS to a provider.

##WEB_BROWSER

Various RPC calls into the default web browser including certificate
information, remote key stores, eyes free displaying, and web view
updates.

##WIDGETS

Access to App Widgets framework. App Widgets are miniature application
views that can be embedded in other applications (such as the Home
screen) and receive periodic updates.  

##GATEKEEPER

The Gatekeeper subsystem performs device pattern/password
authentication in a Trusted Execution Environment (TEE). Gatekeeper
enrolls and verifies passwords via an HMAC with a hardware-backed
secret key. Additionally, Gatekeeper throttles consecutive failed
verification attempts and must refuse to service requests based on a
given timeout and a given number of consecutive failed attempts.

##MIDI

Provides mechanisms for sending and receiving messages using the standard
MIDI event protocol over USB, Bluetooth LE, and virtual (inter-app)
transports.

##TEST

AIDL, Binder, or other AOSP test RPC.
