# RcPi
`In Plain English`

### Major Keys 🔑
When connected to 'Lambda Group', RcPi has ip address `192.168.1.27`.


### Please Read
`<LTE-IP-ADDRESS>`  or similar means replace everything _including_ the brackets

To Open a Shell in the RcPi execute `ssh pi@192.168.1.27`

To find the `ip-address` of the LTE Modem, you'll run the command `ifconfig` in a shell within the RcPi.


### What's Happening Behind the Scenes On Boot

From [Intel's mavlink-router](https://github.com/intel/mavlink-router) we get `mavlink-routerd` which we use to broadcast mavlink data from the specified serial port. 
`mavlink-routerd -e 0.0.0.0:14550 /dev/serial/by-id/usb-3D_Robotics_PX4_FMU_v5.x_0-if00`

From [Shortstheory's adaptive-streaming](https://github.com/shortstheory/adaptive-streaming) we get `stream_server` which we use to stream video from connected cameras, which in this application is a Raspberry Pi Camera. 
`/home/pi/Desktop/adaptive-streaming/build/stream_server wlan0`

### Note ⚠️
For UART instead of USB connections to the flight controller, you'll need to follow the instructions in the [mavlink-router](https://github.com/intel/mavlink-router) project.
For LTE connections, you'll need to change the interface from `wlan0` to whatever the interface is from `ifconfig` for the LTE Modem.

## How to Use with QGroundControl 

### Telemetry 

Click on the purple QGroundControl icon 'Q' to access the Application Settings

Navigate to Application Settings > Comm Links > Add (at the bottom) 

In the `Type` field use `TCP`
In the `Host Address` field use `<LTE-IP-ADDRESS>`
In the `Tcp Port` field use `5760`

### Video Stream

Navigate to Application Settings > General > (Scroll To)  Video

`Video Source` must be changed to `RSTP Video Stream`

`RSTP URL` should be set to  `rtsp://192.168.1.27:8554/cam0` or similar (wait at least 1 minute before trying a new URL if it doesn't work )

####  Note ⚠️
I think RcPi may only support one stream client at a time
Video streaming is more ficle than Telemetry, only try video streaming setup after you've gotten Telemetry up and running.
Wait one (1) minute before trying a different `RSTP URL` If  `cam0` doesn't work after a minute, you should try `cam1` through `cam3` as well. 



