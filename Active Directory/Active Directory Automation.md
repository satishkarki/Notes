# Active Directory Automation



* Step 1 Install RSAT on AD joined machine

  ```powershell
  # Confirm RSAT is enabled
  Get-WindowsCapability -Name RSAT* -Online | Select-Object -Property DisplayName, State
  
  #Output	
  DisplayName																						State
  RSAT: Active Directory Domain Services and Lightweight Directory Services Tools 				Installed
  ```

  

* Step 2 Import Active Directory module

  ```powershell
  Import-Module ActiveDirectory
  ```

* Step 3 