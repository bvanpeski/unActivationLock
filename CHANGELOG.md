# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.5.2] - 2023-06-05
### Changed
- Changed wording in logging output for the edge case scenario where an Activation Lock is detected but it cannot find a user with an associated FindMy token.

## [1.5.1] - 2023-03-01
### Changed
- Fixed applescript dialog to resolve issue where it would not execute in certain situations.

## [1.5] - 2023-02-01
### Added
- Added ability to always prompt user to log out of Find My regardless of activation lock status.
- Script now grabs the iCloud email address of the user who activation locked the device.
- Added user input for sleep timer between prompts.
- Added user input for number of attempts to make before giving up.
- Added System Settings activate command to account for edge cases where System Settings would launch behind other windows.
- Added SwiftDialog support (Thanks to Trevor Sysock @BigMacAdmin)
### Changed
- Changed open url to open directly to the iCloud portion of AppleID. This is using a deprecate url scheme and will probably stop working on the next major version of macOS. (thanks @kspitzer14)
- Changed default icon to FindMy.icns
- Changed timeout from number of seconds to number of attempts.

## [1.4] - 2023-01-22
### Changed
- Cleaned up LOGGING for better legibility.

## [1.3] - 2023-01-18
### Changed
- Updated dialog with new icon (Thanks to Trevor Sysock @BigMacAdmin)

## [1.2] - 2022-10-22
### Added
- Added graceful exit if current user is not associated with lock.
- Added activation lock user lookup for scenarios where a machine may have more than one local user.

## [1.0] - 2022-08-11
### Added
- First go at a solution for solving activation lock issues.
