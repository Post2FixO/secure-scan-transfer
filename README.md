# secure-scan-transfer

Easy and secure scanning from public scanners to remote file systems.

## Intro

**secure-scan-transfer** is a PowerShell script that secures scanning from public office space scanners, directly to internet connected workstations or servers. While cloud sync desktop clients provide an easy way to sync scans to a computer, copies can remain accessible on shared scanners and in cloud storage. This script actively monitors cloud-synced folders, moving any incoming files to local folders, automatically deleting scans from cloud storage and therefore from the publicly accessible interfaces of shared scanners.

The ability to use cloud integrations that are encrypted by default eliminates the need to rely on outdated, less secure scanner protocols such as SMB or FTP, which often require additional security layers like site 2 site VPNs that can still expose files on local networks. **secure-scan-transfer** allows admins to utilize easy to setup advanced and secure direct scanning to remote computers.

## Running the Script

To start the script, open PowerShell and run the following command:

```powershell
powershell -ExecutionPolicy Bypass -File "path_to_your_script.ps1"
```

This method (`-ExecutionPolicy Bypass`) allows the script to run without changing the global execution policy permanently. It bypasses the policy only for the current session, ensuring that your script can execute while maintaining stricter security policies by default.

## Setup Instructions

### Prerequisites

- Windows OS with PowerShell.
- Read/write access to the specified source and destination directories.
- Cloud sync client installed (e.g., Google Drive for Desktop, Dropbox).

### Configuration Steps

1. **Set the User Account**: Specify the username of the account on the local machine where files will be moved.

    ```powershell
    $user = "your_username"
    ```

2. **Select Your Cloud Service**: Uncomment the line corresponding to the cloud service where your scanner uploads documents.

    ```powershell
    $service = "My Drive"  # For Google Drive for Desktop
    #$service = "DropBox"  # Uncomment if using Dropbox
    ```

3. **Define Source and Destination Folders**: Replace `<source folder>` and `<destination folder>` with the actual folder names where your scanner uploads files and where you want them to be moved.

    ```powershell
    $folderPairs = @(
        @{ Source = "C:\Users\$user\$service\<source folder>"; Destination = "C:\Users\$user\<destination folder>" },
    )
    ```

4. **Add Additional Folder Pairs** as needed by copying the line in the `$folderPairs` array and adjusting the paths accordingly.

## Usage Notes

- **Monitoring**: Once started, the script will continuously monitor the specified source folders and move new files to the designated folders, showing activity logs.
- **Management**: The PowerShell terminal can be minimized but should remain running in the background to maintain functionality (intil further integration).
- **Stopping the Script**: To stop the script, press `Ctrl+C` in the PowerShell window.
