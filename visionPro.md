[//]: # (#visionPro)

## calibration
1. calibration only need do once. Immediately disconnect all arguments needed for `CalibNPointToNPoints` to calibrate after calibration is done, but let the input/output images for `CalibNPointToNPoints` continue to flow.

## patInspect
1. Takes the same input image as `PMAlign` and the pose output of `PMAlign`

## trigger mode
1. [!image](images/visionPro_triggerMode.png)

# Scripting
## terminals
1. define terminal within `toolGroup`
```vb
MyBase.toolGroup.DefineScriptTerminal(a_private_instance, the_name_string_to_shown_in_quickBuild, is_input_or_not)
```
2. get input terminal value
```vb
MyBase.toolGroup.GetScriptTerminalData(the_name_string_to_shown_in_quickBuild,a_private_instance)
```
3. communicate with terminal inside toolBlocks, easier way
```vb
Me.Inputs.<name_already_set_in_GUI> = ...
Me.Outputs.<name_already_set_in_GUI> = ...
```

## special variables within UserScript
1. `result` and `message` within `GroupRun`
- Assignment of `result` has the effect of `resultAnalysis`
- `message` is the string that shows in the status bar within the toolBlock/group

## add annotations to lastrun_image
```vb
MyBase.toolGroup.AddGraphicToRunRecord()
```