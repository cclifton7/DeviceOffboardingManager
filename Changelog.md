## Version 0.2.3 - 8/29/2025 (Fork) ##
- **SCCM Integration**: DeviceOffboardingManager will now query\offboard SCCM devices
  - The SCCM console must be installed on the device that is running DeviceOffboardingManager
  - User must have appropriate access to SCCM
- **Added Settings Menu**
  - Toggle SCCM Management On/Off
  - Toggle Automatic MS Graph authentication On/Off
- **Ability to save Encrypted JSON for Application Registration Secret for Automatic Authentication to MS Graph**
  - Added button to save authentication method when using App Registration Secret
  - JSON is encrypted and saved to %LOCALAPPDATA%\DeviceOffboardingManager
  - Encrypted JSON is bound to the device it was created on.
- **Added Animated Loading Window**
  - Animated loading menu will show when Dashboard is compiling and device searches
- **Misc**
  - Updated Entra ID Icon
  - Adjusted window sizes to prevent having to scroll

## Version 0.2.2 - 7/26/2025

- **Fixed Autopilot Device Removal by Serial Number**: Enhanced offboarding process to properly retrieve and use serial numbers for Autopilot device removal (Issue #45)
  - Captures serial number from Intune device data during offboarding
  - Extracts serial number from Entra ID device physicalIds when available
  - Ensures devices searched by name can be properly removed from Autopilot
  - Fixes "BadRequest" API error when searching Autopilot devices by displayName
- **Fixed Critical Error with Duplicate Entra ID Devices**: Enhanced offboarding to handle duplicate device records in Entra ID (Issue #44)
  - Processes all duplicate devices instead of just the first one
  - Validates serial numbers to avoid deleting wrong duplicates
  - Provides detailed logging for each duplicate device processed
  - Reports partial success when some duplicates fail to delete
  - Prevents critical errors when multiple devices share the same name
- **Export Selected Devices to CSV**: Added new feature to export only selected device names to CSV (Issue #43)
  - Added "Export Selected" button next to existing "Export Results" button
  - Exports device names along with all metadata (serial number, OS, user, service status)
  - Button is enabled/disabled based on device selection
  - Allows easy transfer of device information to other systems for cleanup
  - Maintains consistent export format with existing export functionality
- **Enhanced Dialog Error Handling**: Added comprehensive error handling for all dialog windows (Issue #42)
  - Added null checks before calling ShowDialog() on all windows
  - Wrapped all ShowDialog() calls in try-catch blocks
  - Added error handling for window creation with XamlReader.Load()
  - Provides user-friendly error messages when dialogs fail to load
  - Prevents "null-valued expression" errors during offboarding

## Version 0.2.1 - 6/29/2025

- **Fixed Autopilot Device Removal**: Enhanced Autopilot device removal to use displayName as fallback when serial number is unavailable (Issue #34)
  - Added search by displayName for Autopilot devices
  - Improved handling of pre-provisioned Autopilot devices that may not be in Intune
  - Better error messages indicating why removal might fail
- **Fixed CSV Bulk Import**: CSV bulk import now automatically triggers device search after import (Issue #32)
  - Created centralized `Invoke-DeviceSearch` function for consistent search behavior
  - Added automatic search execution after CSV file selection
  - Improved validation for empty files and whitespace
- **Enhanced Device Search**: Improved device search to handle Autopilot-only devices (Related to Issue #34)
  - Devices existing only in Autopilot service are now properly displayed
  - Serial numbers are populated from any available source (Intune or Autopilot)
  - Fixed handling of devices that exist in Autopilot but not in Intune
- **Input Validation**: Added trimming of newlines and whitespace from search input to prevent accidental multi-line entries (Related to Issue #34)
- **Enhanced Bulk Import UI**: Replaced file dialog with professional modal interface for bulk device import
  - Added visual CSV template with example device identifiers
  - Implemented downloadable template CSV functionality
  - Added file preview showing first 10 devices before import
  - Improved error handling with clear visual feedback
  - Enhanced user experience with modern, consistent styling
- **Dynamic Version Display**: Added automatic version number display in window title
- **Improved Changelog Display**: Enhanced markdown rendering in changelog modal
  - Added support for **bold text** formatting
  - Added support for `inline code` formatting
  - Properly handles nested list indentation
  - Mixed formatting (bold, italic, code) now renders correctly
  - Improved visual styling with appropriate fonts and colors
- **Fixed Date Parsing Issues**: Implemented culture-invariant date parsing across the entire application
  - Fixed Autopilot last contact date showing 1/1/0001 12:00AM (Issue #31)
  - Fixed Playbook_1.ps1 date parsing error with culture-specific formats (Issue #30)
  - Fixed Dashboard date parsing errors causing multiple log entries (Issue #16)
  - Added `ConvertTo-SafeDateTime` helper function for consistent date handling
  - Updated all playbooks to use culture-invariant date parsing
  - Replaced all DateTime::Parse calls with safe parsing that handles multiple formats

## Version 0.2 - 6/20/2025

- **Improved Bulk Offboarding**: Removed individual device confirmation dialogs when offboarding multiple devices (Issue #28)
- **Offboarding Summary**: Added a comprehensive summary dialog that shows results for all devices after bulk offboarding
- **Enhanced Logging**: Added detailed logging for all offboarding operations to help troubleshoot issues
- **Better Error Handling**: Errors are now collected and displayed in the summary instead of interrupting the process
- **Fixed Playbook Downloads**: All 5 playbooks now download and execute correctly (Issue #26)
- **Enabled Additional Playbooks**: Enabled Intune Not in Autopilot, Corporate Devices, Personal Devices, and Stale Device Report playbooks
- **Selective Service Offboarding**: Added checkboxes to select/deselect specific services (Entra ID, Intune, Autopilot) during offboarding (Issue #25)
- **Service Selection Validation**: Added validation to ensure at least one service is selected before offboarding
- **Fixed BitLocker Permission Documentation**: Added missing BitlockerKey.Read.All permission to prerequisites (Issue #24)
- **Improved BitLocker Error Handling**: Added specific error messages when BitLocker permissions are missing
- **Fixed Entra ID Permission**: Updated Device.Read.All to Device.ReadWrite.All to enable device deletion from Entra ID (Issue #23)
- **Export to CSV Feature**: Added export functionality for device lists (Issue #20)
  - Export search results to CSV
  - Export playbook results to CSV
  - Includes all device details in a clean format
- **Clickable Dashboard Cards**: Made all dashboard cards interactive with export functionality
  - Click on any stale device card (30/90/180 days) to view and export the device list
  - Click on personal or corporate device cards to view and export those lists
  - Click on Intune, Autopilot, or Entra ID total device cards to view all devices from that service
  - Each card shows a modal with the device details and export button

## Version 0.1.1 - 1/18/2025

- **Improved Performance**: Intune data is being retrieved concurrently through threaded API calls for enhanced performance.
- **Check for available Update**: Implemented a Version Checker to notify you of available updates.
- **Select “All” Devices**: Added a new checkbox to select all devices from the search results.

## Version 0.1 - 1/11/2025

- Initial Release "Hello World!"
