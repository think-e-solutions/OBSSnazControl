# Configuration

## Test OBS Studio setup

To verify that OBS Studio is setup correctly for **OBSSnazControl** to work, perform the following tests:

1. Start OBS
2. Prepare scene
3. Start recording
4. Pause recording
5. Resume recording
6. Stop recording

## Configuring Snaz

- Configure Chrono's (Chrono Up) to generate file with text (timestamp) as required

## Configuring OBS

- Activate OBS's websocket server using *Tools -> WebSocket Server Settings*
- In order to be able to pause and resume recording, make sure all recordings settings do not depend on streaming setting (e.g. encoder etc.)

## Configuring OBSSnazControl

OBSSnazControl's configuration parameters are stored in `OBSSnazControl.exe.config` file.

### Configure OBS Studio's web socket server settings in `OBSSnazControl.exe.config`

After configuring OBS Studio's websocket server, the OBSSnazControl's related configuration parameters must be set accordingly in `OBSSnazControl.exe.config`:

```xml
<add key="obs.websocket.ip-address" value="<webSocketServerName>" />
<add key="obs.websocket.port" value="<webSocketPort>" />
<add key="obs.websocket.password" value="<webSocketPassword>"/>
```