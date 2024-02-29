# Configuration

## Test OBS Studio setup

To verify that OBS Studio is setup correctly for **OBSSnazControl** to work, perform the following tests:

- Start OBS
- Prepare scene
- Start recording
- Pause recording
- Resume recording
- Stop recording

## Configuring Snaz

- Configure Chrono's (Chrono Up) to generate file with text (timestamp) as required

## Configuring OBS

- Activate OBS's websocket server using *Tools -> WebSocket Server Settings*
- In order to be able to pause and resume recording, make sure all recordings settings do not depend on streaming setting (e.g. encoder etc.)

## Configuring OBSSnazControl

OBSSnazControl's configuration parameters are stored in `OBSSnazControl.exe.config` file.

### Change regex used to identify Snaz and OBS Studio window in `OBSSnazControl.exe.config`

To change the regular expressions used to identify Snaz and OBS Studio windows, the following parameters in the App.config file can be changed:

```xml
<add key="snaz.window.title.regex" value="^Snaz \d+\.\d+\.\d+.*$" />
<add key="obs.window.title.regex" value="^OBS \d+\.\d+\.\d+.*$" />
```

### Configure OBS Studio's web socket server settings in `OBSSnazControl.exe.config`

After configuring OBS Studio's websocket server, the OBSSnazControl's related configuration parameters must be set accordingly in `OBSSnazControl.exe.config`:

```xml
<add key="obs.websocket.ip-address" value="<webSocketServerName>" />
<add key="obs.websocket.port" value="<webSocketPort>" />
<add key="obs.websocket.password" value="<webSocketPassword>"/>
```