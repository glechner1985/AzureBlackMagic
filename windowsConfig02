# Create RAID0
$storagePoolName = 'DataLUN'
$storsageSubsystemId = (Get-StorageSubSystem)[0].uniqueID
$vDiskName = 'DataStore01'
New-StoragePool -FriendlyName $storagePoolName `
                -StorageSubSystemUniqueId $storsageSubsystemId `
                -PhysicalDisks (Get-PhysicalDisk -CanPool $true)
New-VirtualDisk -FriendlyName $vDiskName `
                -StoragePoolFriendlyName $storagePoolName -useMaximumSize `
                -ResiliencySettingName Simple                     
$diskNumber = (Get-VirtualDisk -FriendlyName $vDiskName | Get-Disk).Number
Initialize-Disk -Number $diskNumber
New-Partition -DiskNumber $diskNumber -UseMaximumSize -AssignDriveLetter
$driveLetter = (Get-Partition | where {$_.DiskNumber -eq $diskNumber -and $_.Type -ne 'Reserved'}).DriveLetter
Format-Volume -DriveLetter $driveLetter -FileSystem NTFS -NewFileSystemLabel $vDiskName

# Install Cholocatey
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

# Install 7zip
choco install 7zip -y
# Install Notepad++
choco install notepadplusplus -y
# Install putty
choco install putty.install -y
# Install additional software
choco install curl -y --force
