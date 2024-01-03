# Intune Manage Windows Features

## Introduction
This repository provides tools and scripts for managing Windows Features on devices enrolled in Microsoft Intune, using PowerShell. It simplifies enabling or disabling specific Windows Features across your organization's devices.

## Contents
- `Generate_XML.ps1`: Script to generate XML configuration files.
- `IntuneWinAppUtil.exe`: Utility for packaging applications for Intune.
- `Package_Sources`: Contains the main PowerShell script and XML configuration template.
- `README.md`: This document.

## Prerequisites
- Access to Microsoft Intune with administrative privileges.
- Basic understanding of PowerShell scripting.
- Windows environment for running the scripts.

## Getting Started

### Step 1: Configure XML
Edit `Windows_Features_Config_File.xml` in the `Package_Sources` folder to define the Windows features to be managed.

#### XML Configuration Examples
```xml
<Windows_Features>
    <Feature>
        <Feature_Name>Microsoft-Hyper-V</Feature_Name>
        <Feature_Restart_Status>True</Feature_Restart_Status>
        <Feature_Status>Enable</Feature_Status>
    </Feature>
    <Feature>
        <Feature_Name>Windows-Defender-ApplicationGuard</Feature_Name>
        <Feature_Restart_Status>False</Feature_Restart_Status>
        <Feature_Status>Disable</Feature_Status>
    </Feature>
    <Feature>
        <Feature_Name>Containers</Feature_Name>
        <Feature_Restart_Status>False</Feature_Restart_Status>
        <Feature_Status>Default</Feature_Status>
    </Feature>
    <!-- Additional features can be added here -->
</Windows_Features>
```

### Step 2: Generate Configuration Files
Run `Generate_XML.ps1` to produce XML configuration files based on your setup.

### Step 3: Package for Intune
- Use `IntuneWinAppUtil.exe` for packaging the application.
- Open a command prompt in the directory where `IntuneWinAppUtil.exe` is located.
- Execute the utility with the following command:
  ```
  IntuneWinAppUtil.exe -c <source_folder> -s <setup_file> -o <output_folder>
  ```
  - `-c`: Path to the folder containing the files to be packaged (e.g., `Package_Sources`).
  - `-s`: The setup file to be run (e.g., `Manage_Windows_Features.ps1`).
  - `-o`: Path to the folder where the .intunewin package will be created.

### Step 4: Upload to Intune
- Log into the Intune portal and upload the generated package as a Win32 app.
- Set up the app by providing details like name, description, publisher, and program configurations.

### Step 5: Deployment
Assign the uploaded app to the appropriate user or device groups within your organization.

## Testing
Test the configuration on a limited number of devices before applying it organization-wide.

## Support
For issues or questions, please refer to the original documentation or open an issue in this repository.
