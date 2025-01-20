<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Windows PowerShell Lab</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 20px;
        }
        h1, h2, h3 {
            color: #333;
        }
        code {
            display: block;
            background: #f4f4f4;
            padding: 10px;
            margin: 10px 0;
            border-left: 4px solid #007acc;
            white-space: pre-wrap;
            font-family: Consolas, monospace;
        }
        .screenshot {
            color: #007acc;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <h1>Windows PowerShell Lab: User Management and System Information Automation</h1>

    <h2>Objective</h2>
    <ul>
        <li>Automate user account creation.</li>
        <li>Gather system information.</li>
        <li>Perform bulk file operations using PowerShell scripting.</li>
    </ul>

    <h2>Lab Summary (Resume Bullet Points)</h2>
    <ul>
        <li>Automated Active Directory user account creation and management using PowerShell scripts.</li>
        <li>Extracted system information (CPU, RAM, disk space) using PowerShell commands.</li>
        <li>Created and executed scripts to perform bulk file operations, including renaming and moving files.</li>
        <li>Demonstrated ability to work with loops, conditional logic, and PowerShell cmdlets for automation tasks.</li>
    </ul>

    <h2>Step-by-Step Instructions</h2>

    <h3>1. Create a New User in PowerShell</h3>
    <p>Open PowerShell with administrative privileges and run the following command to create a local user account:</p>
    <code>
$Password = ConvertTo-SecureString "Password123!" -AsPlainText -Force<br>
New-LocalUser -Name "LabUser" -Password $Password -FullName "Lab User Account" -Description "Test account created via PowerShell"
    </code>
    <p class="screenshot">Screenshot: Take a screenshot of the command execution and the confirmation of the new user creation.</p>

    <h3>2. Gather System Information</h3>
    <p>Run the following script to gather system information:</p>
    <code>
Get-ComputerInfo | Select-Object CsName, OsName, WindowsVersion, WindowsBuildLabEx, OsArchitecture
    </code>
    <p>For more detailed hardware info, run:</p>
    <code>
Get-WmiObject -Class Win32_ComputerSystem<br>
Get-WmiObject -Class Win32_OperatingSystem
    </code>
    <p class="screenshot">Screenshot: Capture the output showing system and hardware details.</p>

    <h3>3. Automate Bulk File Operations</h3>
    <p>Create a folder for testing:</p>
    <code>
New-Item -ItemType Directory -Path C:\TestLab
    </code>
    <p>Populate it with sample files:</p>
    <code>
1..10 | ForEach-Object {
    New-Item -Path C:\TestLab -Name "File$_.txt" -ItemType File
}
    </code>
    <p>Rename all files in the folder:</p>
    <code>
Get-ChildItem -Path C:\TestLab -Filter *.txt | ForEach-Object {
    Rename-Item -Path $_.FullName -NewName ($_.BaseName + "_Renamed.txt")
}
    </code>
    <p>Move all files to a subdirectory:</p>
    <code>
New-Item -ItemType Directory -Path C:\TestLab\SubFolder<br>
Get-ChildItem -Path C:\TestLab -Filter *_Renamed.txt | Move-Item -Destination C:\TestLab\SubFolder
    </code>
    <p class="screenshot">Screenshot: Take a screenshot of the directory before and after the renaming/moving process.</p>

    <h3>4. Export Data to a CSV File</h3>
    <p>Export system processes to a CSV file:</p>
    <code>
Get-Process | Select-Object Name, CPU, Id, StartTime | Export-Csv -Path C:\TestLab\Processes.csv -NoTypeInformation
    </code>
    <p>Open the file in Notepad or Excel to confirm:</p>
    <code>
Invoke-Item C:\TestLab\Processes.csv
    </code>
    <p class="screenshot">Screenshot: Capture the content of the exported CSV file.</p>

    <h3>5. Cleanup</h3>
    <p>Remove all files and folders created during the lab:</p>
    <code>
Remove-Item -Path C:\TestLab -Recurse -Force
    </code>
    <p>Remove the test user account:</p>
    <code>
Remove-LocalUser -Name "LabUser"
    </code>
    <p class="screenshot">Screenshot: Show the cleanup commands and confirm the user and folder are deleted.</p>

</body>
</html>
