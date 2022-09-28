# gstreamer-klv-plugins-release
GStreamer klv plugins

- klvdecode - MISB Klv decoder  
- klvencode - MISB Klv encoder  

## MisbCore

**gstreamer-klv-plugins** use the [MisbCore](https://www.impleotv.com/content/misbcore/help/index.html) library. You MUST set the library path, so the plugins could find it.

The path is set in **MISBCORE_LIB_PATH** environment variable.  
By default, the **MisbCore** library will work in demo mode, so it will only process tags < 15.  
In order to lift demo restrictions you should apply the license.  

The license file path and the key are set in **MISBCORE_LICENSE_FILE** and **MISBCORE_LICENSE_KEY** respectively. 
You can set the environment variables by using **export** command. 
```
export MISBCORE_LIB_PATH=/home/myuser/libraries/MisbCoreNativeLib.so
```
To permanently setup the system-wide environment variables you can add them to the **/etc/environment** file. Note, you need to use **admin** or **sudo** to modify it.  
```
MISBCORE_LIB_PATH=/home/myuser/libraries/MisbCoreNativeLib.so
MISBCORE_LICENSE_FILE=/home/myuser/licenses/misbCore/MisbCore-Decode.lic
MISBCORE_LICENSE_KEY=0C203E11-847A7BF1-00B8B052-0B9F984C
```
### Testing plugin

```
gst-launch-1.0 filesrc location=~/Movies/2tpacket.bin ! klvdecode ! fakesink dump=TRUE
```

```
gst-launch-1.0 filesrc location=~/Movies/2t.ts ! tsdemux name=demux demux. ! queue ! h264parse ! 'video/x-h264, stream-format=byte-stream' ! avdec_h264 ! autovideosink demux. ! 'meta/x-klv' ! klvdecode ! queue ! fakesink dump=TRUE
```

