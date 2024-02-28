# OBSSnazControl

**OBSSnazControl** is a very simple but useful utility for Microsoft(R) Windows(R) to synchronize a [Snaz](https://github.com/JimmyAppelt/Snaz) "Chrono Up" with [OBS Studio](https://obsproject.com) if the OBS Studio recording needs to be started, paused, resumed and finally stopped.

## Objective
Users of OBS Studio may want to display information about the time that has passed since recording was started. A very simple way to achieve this is to use the "Text (GDI+)" source in OBS Studio and configure it to display time information read from a text file. The text file would need to contain the time elapsed since the recording was started. Such file can, for example, be generated by Snaz's "Chrono Up" functionality.

However, if recording in OBS Studio is paused and resumed later, the Snaz "Chrono Up" will continue to run while the recording is paused. Consequently, the time displayed in OBS will be out of sync, once the recording is resumed.

Whenever OBS's recording state changes, Snaz's "Chrono Up"'s state must be changed accordingly to avoid this problem.

## Solution
**OBSSnazControl** solves the out-of-sync problem between OBS Studio and Snaz. When started, it shows a very simple application window with three buttons. Initially those buttons are called "Start", "Stop" and "Exit".

### Starting recording and "Chrono UP"
If the "Start" button is activated, **OBSSnazControl** starts the recording in OBS as well as the Snaz "Chrono up". While recording is active, the start button's text changes to "Pause".

### Pausing and resuming recording and "Chrono Up"
By pressing the "Pause" button during an active recording session, **OBSSnazControl** synchronuously pauses recording in OBS Studio and the Snaz "Chrono UP". If paused, the button's text changes to "Resume". Pressing the "Resume" button causes OBS to resume recording and synchronously resumes Snaz' "Chrono Up".

### Stopping recording
Activating the "Stop" button immediately stops recording in OBS and also halts the Snaz "Chrono Up". In OBS Studio stopping a recording will result in the recording being saved to disk.

### Exiting OBSSnazControl
If the user presses the "Exit" button, **OBSSnazControl** will be terminated.

## How OBSSnazControl works
**OBSSnazControl** makes use of two main technologies: OBS Studio's websocket API and simulation of keystrokes.

### Controlling OBS Studio
At start-up **OBSSnazControl** checks whether OBS is running by inspecting all windows' titles. If any of the window titles matches a configurable regular expresssion that is considered to match only OBS Studio's main window title, **OBSSnazControl** assumes OBS Studio is running and attempts to establish the websocket connection to it. If the connection fails, it will show an error.

For communication with OBS Studio, **OBSSnazControl** uses OBS's websocket API (see [obs-websocket-dotnet](https://www.nuget.org/packages/obs-websocket-dotnet)).

### Controlling Snaz
Controlling Snaz is a bit more complicated than controlling OBS Studio. Snaz does not offer any APIs for direct interaction with it's UI.

All actions to control the state of "Chrono Up" in Snaz are performed by sending simulated keytstrokes to Snaz based on `Sendkeys.SendWait(String)` method. The Snaz Window must be the active foreground window, when keystroke sequences are sent by **OBSSnazControl**. **OBSSnazControl** ensures in-time activation of the Snaz window. However, it therefore requires a valid window handle for the Snaz application. This window handle is obtained at start-up by inspecting all windows' titles and finding the one matching a configurable regular expression when **OBSSnazControl** is started (see [Configuration](#configuration)).

> [!IMPORTANT]
> Because of the method used to control Snaz it's very important that users do not change the state of the Snaz window while **OBSSnazControl** is active. 

## Configuration

### Prerequisites
- OBS Studio's websocket server must be activated

## Tests to perform
- Start OBS
- Prepare scene
- Start recording
- Pause recording
- Resume recording
- Stop recording

> [!IMPORTANT]
> Do not click the mouse or touch the keyboard after activating a button on **OBSSnazControl** as long as the Snaz window is performing any action.
> Snaz is controlled by simulating keystrokes. If you activate any other window than the Snaz window using mouse or keyboard, the keystrokes will not be sent to the Snaz application.

### Configuring Snaz

- Configure Chrono's (Chrono Up) to generate file with text (timestamp) as required

### Configuring OBS
- Activate OBS's websocket server using *Tools -> WebSocket Server Settings*
- In order to be able to pause and resume recording, make sure all recordings settings do not depend on streaming setting (e.g. encoder etc.)

### Configuring OBSSnazControl
OBSSnazControl's configuration parameters are stored in `OBSSnazControl.exe.config` file.

#### Change regex used to identify Snaz and OBS Studio window
To change the regular expressions used to identify Snaz and OBS Studio windows, the following parameters in the App.config file can be changed:

```xml
<add key="snaz.window.title.regex" value="^Snaz \d+\.\d+\.\d+\..*$" />
<add key="obs.window.title.regex" value="^OBS \d+\.\d+\.\d+\..*$" />
```

#### Configure OBS Studio's web socket server settings
After configuring OBS Studio's websocket API (*Tools -> WebSocket Server Settings*), the OBSSnazControl's related configuration parameters must be set accordingly in App.config:

```xml
<add key="obs.websocket.ip-address" value="<webSocketServerName>" />
<add key="obs.websocket.port" value="<webSocketPort>" />
<add key="obs.websocket.password" value="<webSocketPassword>"/>
```

## Using OBSSnazControl

## Prerequisites
**OBSSnazControl** is a 64-bit application. It requires:

- Microsoft(R) Windows(R) 10 or later,
- Snaz 1.12.7.0 or later,
- OBS Studio 27.0.0 or later.

**OBSSnazControl** has recnetly been tested with OBS Studio 30.0.2 and Snaz 1.12.7.0.

## Testing OBS Studio's setup 
To verify that OBS Studio is setup correctly for **OBSSnazControl** to work, perform the following tests:

- Start OBS
- Prepare scene
- Start recording
- Pause recording
- Resume recording
- Stop recording

## Starting OBSSnazControl
When using **OBSSnazControl**, it's important to ensure the correct startup sequence of OBS Studio, Snaz and **OBSSnazControl**.

> [!Important]
> Please start applications in the following Order
> 1. OBS Studio
> 2. Snaz
> 3. **OBSSnazControl**

If **OBSSnazControl** is started before  OBS Studio and Snaz are active, **OBSSnazControl** initialization will fail and show an error message stating that OBS Studio and Snaz seem to be not running.

## Know issues/traps

### Multiple OBS Studio or Snaz "instances" found
If more than one application window matching the regular expressions for the OBS Studio or Snaz main application window are found, **OBSSnazControl** reports an error.
If this is the case, check for e.g. browser tabs and desktop shortcuts that match the window regular expressions.

> [!TIP]
> If a desktop shortcut with a name matching regular expression `Snaz .*` exists, startup fails with an error message stating that multiple windows exist matching regular expression `Snaz .*`.

### Recording encoding setting in OBS Studio prevents start of recording
Under certain circumstances, the encoding chosen for recordings in OBS Studio can prevent the start of a recording.

In any case, test recording in OBS (standalone) first, to see whether it's working as expected.

