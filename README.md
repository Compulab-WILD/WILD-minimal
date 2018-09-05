WILD Minimal - WiFi RTT proof-of-concept for Android 9 Pie<br/>
Revision: 0.1 24-Aug-2018<br/>
Designed for ranging to Compulab WILD FTM Responders and tested with Google Pixel<br/>
"WILD" stands for WiFi Indoor Location Device<br/>
(C) Compulab 2018 https://www.fit-iot.com<br/>
Written by Irad Stavi irad@compulab.co.il<br/>
Special thanks to Prof. Berthold K.P. Horn of MIT CSAIL http://people.csail.mit.edu/bkph/ for his insightful advice<br/>
<br/>
What the program does:<br/>
1. Get permissions<br/>
2. WiFi Scan to detect APs<br/>
3. Every 2 seconds send a ranging request to APs found in scan that are FTM responders and display the ranging results of each in a table<br/>
<br/>
The program is written to be as simple as possible - a self contained activity with nearly sequential execution.<br/>
Below is the flow in a nutshell:<br/>
    onCreate: Requests permissions and starts 'repeat' which is called every 2 seconds.<br/>
repeat: runs a simple state machine: permission_is_granted --(do scan)--> wifi_scan_is_requested --(scan-results received)--> wifi_scan_is_done.<br/>
then repeat starts calling range() every 2 seconds.<br/>
range: build a 'ranging request' and send. onRangingResults will be called asynchronously when results are ready.<br/>
onRangingResults: Display the ranging results in a table (MAC address, measured range, standard deviation, signal strength)<br/>

APK installation instructions (may be helpful if you never installed an APK before. If you did - you can skip :)
------------------------------------------------------------------------------------------------------------

    - Go to https://github.com/Compulab-WILD/WILD-minimal
    - Download everything
    - Look at the APK directory for the APK file

    - Enable "developer mode" on the phone https://www.verizonwireless.com/support/knowledge-base-215055/
    - Download and install ADB (found in SDK manager) https://developer.android.com/studio/command-line/adb
    - Find where ADB is installed. In my case C:\android-sdk-tools\platform-tools
    - Copy wild-minimal.apk to the directory where ADB is

    - Connect the phone with USB cable to your host
    - Identify the ID of the phone by
    > adb devices
    - Type command (assuming your phone ID is 01234567890ABCDEF)
    > adb -s 01234567890ABCDEF install wild-minimal.apk
    - Now you should have "WILD minimal" app on the phone

