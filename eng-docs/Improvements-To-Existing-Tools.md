# Improvements To Existing Android Tools

## dexdump

* `$ dexdump -C dexfile.dex` print a numbered list of classes that you
  can grep.  Remember number for class in interest.

* `$ dexdump -Q <class-num> -d dexfile.dex` to decompile entire class (all
  methods).

* `$ dexdump -M <class-num> -d dexfile.dex` to numbered list all methods of
  class designated by <class-num>.  Assume <method-num> is the number
  for the method of interest.

* `$ dexdump -Q <class-num>.<method-num> -d dexfile.dex` to decompile
  only the method of interest in the class.

## adb

### To force install an application (uninstall existing version on
    device if necessary)

1. `$ adb install -f <apk_file>`
