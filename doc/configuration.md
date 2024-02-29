# Configuration

## Test OBS Studio setup

To verify that OBS Studio is setup correctly for **OBSSnazControl** to work, perform the following tests:

1. Start OBS
2. Prepare scene
3. Start recording
4. Pause recording
5. Resume recording
6. Stop recording

## Configuring OBS Studio

- Activate OBS's websocket server using *Tools -> WebSocket Server Settings*
- In order to be able to pause and resume recording, make sure all recordings' settings do not depend on streaming setting (e.g. encoder etc.)

## Configuring Snaz

- Configure Chrono's (Chrono Up) to generate file with text (timestamp) as required

## Configuring OBSSnazControl

OBSSnazControl's configuration parameters are stored in `OBSSnazControl.exe.config` file located in the **OBSSnazControl** installation folder.

> [!Important]
> Files inside the `Program Files` directory of Microsoft Windows can only be modified with administrative privileges. Unfortunately, Notepad - the default app that one would likely use to modify an XML file like `OBSSnazControl.exe.config` on a system that does not have any other editors installed - cannot save files to the `Program Files` directory. If you don't have another editor capable of elevating a user's permission (e.g. Notepad++), save the modified file to a different location and then move it to the `Progam Files` folder using Windows explorer.

### Configure OBS Studio's web socket server settings in `OBSSnazControl.exe.config`

After configuring OBS Studio's websocket server (see [Configuring OBS Studio](#Configuring-OBS-Studio)), the OBSSnazControl's related configuration parameters must be set accordingly in `OBSSnazControl.exe.config`:

```xml
<add key="obs.websocket.ip-address" value="<webSocketServerName>" />
<add key="obs.websocket.port" value="<webSocketPort>" />
<add key="obs.websocket.password" value="<webSocketPassword>"/>
```