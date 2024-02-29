# Using OBSSnazControl

## Prerequisites

**OBSSnazControl** is a **64-bit** application. It requires:

- Microsoft Windows 10 or later,
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

> [!IMPORTANT]
> Do not click the mouse or touch the keyboard after activating a button on **OBSSnazControl** as long as the Snaz window is performing any action.
> Snaz is controlled by simulating keystrokes. If you activate any other window than the Snaz window using mouse or keyboard, the keystrokes will not be sent to the Snaz application.

### Starting recording and "Chrono UP"
If the "Start" button is activated, **OBSSnazControl** starts the recording in OBS as well as the Snaz "Chrono up". While recording is active, the start button's text changes to "Pause".

### Pausing and resuming recording and "Chrono Up"
By pressing the "Pause" button during an active recording session, **OBSSnazControl** synchronuously pauses recording in OBS Studio and the Snaz "Chrono UP". If paused, the button's text changes to "Resume". Pressing the "Resume" button causes OBS to resume recording and synchronously resumes Snaz' "Chrono Up".

### Stopping recording
Activating the "Stop" button immediately stops recording in OBS and also halts the Snaz "Chrono Up". In OBS Studio stopping a recording will result in the recording being saved to disk.

### Exiting OBSSnazControl
If the user presses the "Exit" button, **OBSSnazControl** will be terminated.