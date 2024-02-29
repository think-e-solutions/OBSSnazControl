# Know issues/traps

## No OBS Studio or Snaz "instance" found although both programs are running

If **OBSSnazControl** does not find the OBS Studio and Snaz window "instances", one reason can be that the regular expressions used for matching the applications' window titles are incorrect and do thererfore not match the window titles. Another cause maybe that OBS Studio or Snaz changed the title that's being displayed in newer versions.

In such a case, change the regular expressions used to identify OBS Studio and Snaz window titles in `OBSSnazControl.exe.config`.

To change the regular expressions used to identify Snaz and OBS Studio windows, the following parameters in the `OBSSnazControl.exe.config` file can be changed:

```xml
<add key="snaz.window.title.regex" value="^Snaz \d+\.\d+\.\d+.*$" />
<add key="obs.window.title.regex" value="^OBS \d+\.\d+\.\d+.*$" />
```

## Multiple OBS Studio or Snaz "instances" found

If multiple application windows matching the regular expressions for the OBS Studio or Snaz main application window are found, **OBSSnazControl** reports an error.

If this is the case, check for e.g. browser tabs and desktop shortcuts that match the window regular expressions.

> [!TIP]
> If a desktop shortcut with a name matching regular expression `Snaz .*` exists, startup fails with an error message stating that multiple windows exist matching regular expression `Snaz .*`.

## Recording encoding setting in OBS Studio prevents start of recording

Under certain circumstances, the encoding chosen for recordings in OBS Studio can prevent the start of a recording.

In any case, test recording in OBS (standalone) first, to see whether it's working as expected.