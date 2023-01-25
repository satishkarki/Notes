# Power Shell Script to unshare the remote printer

I have a Windows Server 2019 which I am using as a print server (\\\TESTDC01). To test script below, I made some virtual printers and shared them over the network. 



These shared printers can be accessed from a Win10 machine as \\\TESTDC01\TestPrinter1, \\\TESTDC01\TestPrinter2, and so on. Once the script runs, sharing will be disabled and it will be inaccessible in Win10, but it will not delete the printer from server.

Make sure to login as an admin, before running the script.

```powershell
#Import the CSV file contating the list of printers
$printers=Import-Csv -Path "C:\Users\satish.karki\Desktop\Printerlist.csv"

#My Print Server
$printServer="TESTDC01"

#Loop through each printer in the list
Write-Host "The name of printers in the list is"
foreach ($printer in $printers){
    Write-Host "$($printer.PrinterName)"
    $printerPath="\\"+$printServer+"\"+$printer.PrinterName
    Set-Printer -Name $printerPath -Shared $false -ShareName $printerPath
}
Write-Host "The printers are unshared"
```

