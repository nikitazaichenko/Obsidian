Для того, чтобы даже с административным правами  к Hyper-V серверу мог подключаться Veeam необходимо изменить несколько параметров в том числе и отключить UAC

- HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System

If the LocalAccountTokenFilterPolicy registry entry doesn't exist, follow these steps:

On the Edit menu, point to New, and then select DWORD Value.  
Type LocalAccountTokenFilterPolicy, and then press ENTER.

In the Value data box, type 1, and then select OK.

- HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System,
    
      EnableLUA  
    

In the Value data box, type 0, and then select OK.

- GPO Computer Configuration\Windows Settings\Security Settings\Local Policies\Security Options 
    
    User Account Control: Admin Approval Mode for the Built-in Administrator account - Disable
    

Reboot