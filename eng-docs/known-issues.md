# Known Issues with ClearScope Device

* Cannot download and dynamically load dex classes.

* ClearScope does not support running of non-instrumented Android dex classes

* Applications cannot use Google Play libraries.  Google Play services cannot be installed on the instrumented device.

* All "native" method in Java must be declared (or used) as final.
