# secure-scans-to-workstations
Secure scans to workstations from public scanners

## Overview

secure-scans-to-workstations is a PowerShell script designed to securely transfer scanned documents from shared scanners to private workstations or servers. By leveraging cloud service scanner integrations and their desktop clients, the script swiftly relocates scans from cloud-synced folders to local folders, simultaneously deleting them from the shared scanners and cloud services. This method ensures that sensitive documents remain inaccessible in cloud storage or through scanner interfaces in publicly accessible areas like shared office spaces. Addressing the principal security risks associated with cloud-integrated scanners, the script bypasses the need for complex network setups or outdated protocols like SMB or FTP, which often require VPNs for secure remote network connections and can inadvertently expose files on local networks. secure-scans-to-workstations provides an efficient and secure solution for document management, enhancing privacy while maintaining ease of use for administrators and users alike.

## Key Features

- **Secure File Transfer**: Automatically moves files from cloud-synced directories to a private file system, ensuring that scanned documents are not accessible to unauthorized users.
- **Privacy Enhancement**: Files are removed from public or shared cloud directories immediately after being scanned, minimizing the risk of data exposure.
- **Ease of Setup**: Uses native cloud sync clients without the need for complex network configurations, making it simple and straightforward to implement.

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

### Running the Script

To start the script, open PowerShell and run the following command:

```powershell
powershell -ExecutionPolicy Bypass -File "path_to_your_script.ps1"
```

#### Why Use This Method?

This method (`-ExecutionPolicy Bypass`) allows the script to run without changing the global execution policy permanently. It bypasses the policy only for the current session, ensuring that your script can execute while maintaining stricter security policies by default.

## Usage Notes

- **Monitoring**: Once started, the script will continuously monitor the specified source folders and move new files to the designated destinations.
- **Management**: The PowerShell terminal can be minimized but should remain running in the background to maintain functionality.
- **Stopping the Script**: To stop the script, press `Ctrl+C` in the PowerShell window.

---

This README provides a clear and concise explanation of what the script does, how to set it up, and how to run it, tailored for users who may not be familiar with PowerShell or the details of your specific setup.
