# How OBSSnazControl works

**OBSSnazControl** makes use of two main technologies: OBS Studio's websocket API and simulation of keystrokes.

## How OBSSnazControl interacts with OBS Studio

At start-up **OBSSnazControl** checks whether OBS is running by inspecting all windows' titles. If any of the window titles matches a configurable regular expresssion that is considered to match only OBS Studio's main window title, **OBSSnazControl** assumes OBS Studio is running and attempts to establish the websocket connection to it. If the connection fails, it will show an error.

For communication with OBS Studio, **OBSSnazControl** uses OBS's websocket API (see [obs-websocket-dotnet](https://www.nuget.org/packages/obs-websocket-dotnet)).

## How OBSSnazControl interact with Snaz

Controlling Snaz is a bit more complicated than controlling OBS Studio. Snaz does not offer any APIs for direct interaction with it's UI.

All actions to control the state of "Chrono Up" in Snaz are performed by sending simulated keytstrokes to Snaz based on `Sendkeys.SendWait(String)` method. The Snaz Window must be the active foreground window, when keystroke sequences are sent by **OBSSnazControl**. **OBSSnazControl** ensures in-time activation of the Snaz window. However, it therefore requires a valid window handle for the Snaz application. This window handle is obtained at start-up by inspecting all windows' titles and finding the one matching a configurable regular expression when **OBSSnazControl** is started (see [Configuration](#configuration)).