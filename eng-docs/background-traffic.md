# Benign Background Traffic

## Summary 

This document describes the background service pre-installed on the
ClearScope devices for generating benign background HTTP page loads. 

## Configuration

### Timeout between loads

The service currently loads a webpage every 10 seconds.

### Urls To Load

The service expects a file with urls to load, one url per line.
Example: 

```
http://wetransfer.com
http://far-far-star.com
http://spoonuniversity.com
http://fishwrapper.com
http://uberhavoc.com
http://jungroup.com
http://holidayinn.com
http://outback.com
http://thepointsguy.com
http://curejoy.com
http://bouche.me
http://guim.co.uk
http://bryantstratton.edu
http://firefox.com
```

The services expects this file to be on the device here:

`/data/user/0/edu.mit.clearscope.benigntraffic/files/cs-benign-traffic-urls.txt`

So to push a urls file to the device:

`$ adb push [path-to-urls-file-on-ingestor-machine] /data/user/0/edu.mit.clearscope.benigntraffic/files/cs-benign-traffic-urls.txt`


## Start 

`$ adb shell am startservice edu.mit.clearscope.benigntraffic/.WebLoadService`

## Stop 

`$ adb shell am force-stop edu.mit.clearscope.benigntraffic`

## Notes

The service does not follow redirects.  
