# Source Compile
## Android12 CTS Build from Source Code
1. Get source code
    skip
2. Compile CTS
    ```
    source build/envsetup.sh
    lunch aosp_arm-eng
    m cts -j18
    ```
    Find result in *out* directory.