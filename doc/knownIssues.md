# Know issues/traps

### Multiple OBS Studio or Snaz "instances" found
If more than one application window matching the regular expressions for the OBS Studio or Snaz main application window are found, **OBSSnazControl** reports an error.
If this is the case, check for e.g. browser tabs and desktop shortcuts that match the window regular expressions.

> [!TIP]
> If a desktop shortcut with a name matching regular expression `Snaz .*` exists, startup fails with an error message stating that multiple windows exist matching regular expression `Snaz .*`.

### Recording encoding setting in OBS Studio prevents start of recording
Under certain circumstances, the encoding chosen for recordings in OBS Studio can prevent the start of a recording.

In any case, test recording in OBS (standalone) first, to see whether it's working as expected.