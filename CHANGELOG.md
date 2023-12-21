# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## v 1.6 | 2023-12-21
### Changed
`CHANGED` -  Modified all open and osascript commands to run as the currently logged in user to catch edge cases where the `open` command failed to open System Settings.

## v 1.5.2 | 2023-06-05
### Changed
`CHANGED` - Changed wording in logging output for the edge case scenario where an Activation Lock is detected but it cannot find a user with an associated FindMy token.

## v 1.5.1 | 2023-03-01
### Changed
`CHANGED` - Fixed applescript dialog to resolve issue where it would not execute in certain situations.

## v 1.5 | 2023-02-01
`ADDED` - Added ability to always prompt user to log out of Find My regardless of activation lock status.

`ADDED` - Script now grabs the iCloud email address of the user who activation locked the device.

`ADDED` - Added user input for sleep timer between prompts.

`ADDED` - Added user input for number of attempts to make before giving up.

`ADDED` - Added System Settings activate command to account for edge cases where System Settings would launch behind other windows.

`ADDED` - Added SwiftDialog support (Thanks to Trevor Sysock @BigMacAdmin)
### Changed
`CHANGED` - Changed open url to open directly to the iCloud portion of AppleID. This is using a deprecate url scheme and will probably stop working on the next major version of macOS. (thanks @kspitzer14)

`CHANGED` - Changed default icon to FindMy.icns

`CHANGED` - Changed timeout from number of seconds to number of attempts.

## v 1.4 | 2023-01-22
`CHANGED` -  Cleaned up LOGGING for better legibility.

## v 1.3 | 2023-01-18
`CHANGED` - Updated dialog with new icon (Thanks to Trevor Sysock @BigMacAdmin)

## v 1.2 | 2022-10-22
`ADDED` - Added graceful exit if current user is not associated with lock.

`ADDED` - Added activation lock user lookup for scenarios where a machine may have more than one local user.

## v 1.0 | 2022-08-11
### Added
`ADDED` - First go at a solution for solving activation lock issues.
