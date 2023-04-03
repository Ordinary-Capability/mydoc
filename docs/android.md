# Source Compile
## CTS
### Android12 CTS Build from Source Code
1. Get source code
    skip
2. Compile CTS
    ```
    source build/envsetup.sh
    lunch aosp_arm-eng
    m cts -j18
    ```
    Find result in *out* directory.
### RUN CTS
To run a test plan on a single device:
1. Make sure you have at least one device connected
2. Launch the cts-tradefed console by running the **cts-tradefed**. If you've
downloaded and extracted the CTS zip, the script can be found at **android-cts/tools/cts-tradefed**.
Or else if you are working from the Android source tree and have run make cts,
the script can be found at
**out/host/linux-x86/cts/android-cts/tools/cts-tradefed**
3. Type:**run cts** to run the default CTS plan

4. Some other useful commands are
    ```
    run cts --module <module_name>
    run cts --module <module_name> --test <test_name>
    run cts --shard-count <number of shards>
    run cts --help
    ```
    Note: when run cts shard, all connected devices must be running the same build.
