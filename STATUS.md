# AudioBookBinder Fork Status

## Completed

- [x] Merged upstream/master (Swift CLI rewrite, cleanup)
- [x] Issue #19: Original Quality mode — use source file's sample rate/channels/bitrate
  - `ConfigNames.h`: `kConfigUseOriginalQuality` key
  - `AudioFile.h/.m`: `sourceSampleRate`, `sourceChannels`, `sourceBitrate` properties
  - `AudioBinder.h/.m`: `useOriginalQuality` property, per-volume override logic
  - `AudioBookBinderAppDelegate.m`: default `NO`
  - `AudioBinderWindowController.m`: reads from `NSUserDefaults`
  - `abbinder.swift`: `-O` flag

## In Progress

- [ ] GUI checkbox for "Use Original Quality" in `AudioBinderWindow.xib` + `PrefsController`

## Planned (from open issues)

- [ ] Issue #11: Auto-select best compression method
  - New `QualityDetector` class (new file, zero conflict)
  - New config key `kConfigAutoQuality`
  - Logic in `AudioBinder.m` to pick optimal settings from source files
- [ ] Issue #23: Fix splitting large m4a files (duration > max volume length)
  - Fix in `AudioBinder.m` `convert` method
- [ ] Issue #36: Fix "Can't create output file" error
  - Fix in `AudioBinder.m` `openOutFile` method

## Architecture Notes

- Keep changes in shared Objective-C core + Swift CLI to minimize upstream overlap
- Avoid touching GUI/XIB files unless necessary
- Branching: `master` tracks upstream, feature work on separate branches
