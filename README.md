WILD Minimal - WiFi RTT proof-of-concept for Android 9 Pie
Revision: 0.1 24-Aug-2018
Designed for ranging to Compulab WILD FTM Responders and tested with Google Pixel
"WILD" stands for WiFi Indoor Location Device
(C) Compulab 2018 https://www.fit-iot.com
Written by Irad Stavi irad@compulab.co.il
Special thanks to Prof. Berthold K.P. Horn of MIT CSAIL http://people.csail.mit.edu/bkph/ for his insightful advice

What the program does:
1. Get permissions
2. WiFi Scan to detect APs
3. Every 2 seconds send a ranging request to APs found in scan that are FTM responders and display the ranging results of each in a table

The program is written to be as simple as possible - a self contained activity with nearly sequential execution
Below is the flow in a nutshell:
onCreate: Requests permissions and starts 'repeat' which is called every 2 seconds
repeat: runs a simple state machine: permission_is_granted --(do scan)--> wifi_scan_is_requested --(scan-results received)--> wifi_scan_is_done
    then repeat starts calling range() every 2 seconds
range: build a 'ranging request' and send. onRangingResults will be called asynchronously when results are ready.
onRangingResults: Display the ranging results in a table (MAC address, measured range, standard deviation, signal strength)
