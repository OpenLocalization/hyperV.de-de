#PowerShell-Snippets

PowerShell ist ein genial Skripting, Automatisierung und Management-Tool für Hyper-V.  Hier ist eine Toolbox zu erkunden einige der tollen Dinge tun kann!

Alle Hyper-V-Management erfordert ausführen als Administrator übernehmen also alle Skripts und Ausschnitte als Administrator werden, von einem Hyper-V-Administrator-Konto ausgeführt müssen.

Wenn Sie sich nicht sicher, ob Sie die richtigen Berechtigungen haben, geben `Get-VM` und wenn es ohne Fehler ausgeführt wird, sind Sie bereit zu gehen.

##PowerShell-Direct-Werkzeuge

Alle Skripte und Ausschnitte in diesem Abschnitt wird auf die folgenden Grundlagen verlassen.

**Anforderungen** :  

*   PowerShell-Direct.
    Windows 10-Guest und Host-Betriebssystem.

**Allgemeine Variablen** :  
`$VMName` --Dies ist ein String mit dem VMName.
Finden Sie eine Liste der verfügbaren VMs mit `Get-VM``$cred` --Die Anmeldeinformationen für das Betriebssystem des Gastes.
Kann mit aufgefüllt werden `$cred = Get-Credential`

###Prüfen Sie, ob der Gast gestartet wurde

Hyper-V-Manager geben nicht Sie Einblick in das Gastbetriebssystem, oft ist es schwierig zu wissen, ob der Gast OS gebootet hat.

Verwenden Sie diesen Befehl, um festzustellen, ob der Gast gestartet ist.

``` PowerShell
if((Invoke-Command -VMName $VMName -Credential $cred {"Test"}) -ne "Test"){Write-Host "Not Booted"} else {Write-Host "Booted"}


```

**Outcome**  
Prints a friendly message declaring the state of the guest OS.


### Script locking until the guest has booted

The following function waits uses the same principle to wait until PowerShell is available in the guest (meaning the OS has booted and most services are running) then returns.

``` PowerShell
function waitForPSDirect([string]$VMName, $cred){
   Write-Output "[$($VMName)]:: Waiting for PowerShell Direct (using $($cred.username))"
   while ((Invoke-Command -VMName $VMName -Credential $cred {"Test"} -ea SilentlyContinue) -ne "Test") {Sleep -Seconds 1}}

```

**Ergebnis**  
Prints a friendly message and locks until the connection to the VM succeeds.
Erfolgreich im Hintergrund.

###Skript sperren, bis der Gast ein Netzwerk hat

Mit PowerShell-Direct ist es möglich, angeschlossen an eine PowerShell-Sitzung in einer virtuellen Maschine vor der virtuellen Maschine erhalten hat eine IP-Adresse erhalten.

''' PowerShell

#Warten Sie DHCP

während ((Get-NetIPAddress |?
AddressFamily - Eq IPv4 |?
IPAddress -ne 127.0.0.1).SuffixOrigin -ne "Dhcp") {sleep -Milliseconds 10}
```

** Ergebnis **
Locks until a DHCP lease is recieved.
Da dieses Skript kein bestimmtes Subnetz oder IP-Adresse, auf der Suche nach ist es funktioniert egal welche Netzwerkkonfiguration verwenden Sie.
Erfolgreich im Hintergrund.

##Verwalten von Anmeldeinformationen mit PowerShell

Hyper-V-Skripts erfordern häufig die Behandlung von Anmeldeinformationen für einen oder mehrere virtuelle Maschinen, Hyper-V-Host oder beides.

Es gibt mehrere Möglichkeiten, Sie können dies erreichen, beim Arbeiten mit PowerShell Direct oder Norm PowerShell-Remoting:

1.  Die erste (und einfachste) Weg soll haben dieselben Anmeldeinformationen in der und der Gast oder lokale und remote-Host gültig sein.
    Dies ist ganz einfach, wenn Sie sich mit Ihrem Microsoft-Konto - anmelden oder wenn Sie in einer Domänenumgebung.
    In diesem Szenario können Sie nur ausführen `Invoke-Command -VMName "test" {get-process}`.
2.  Let PowerShell prompt you for credentials  
    If your credentials do not match you will automatically get a credential prompt allowing you to provide the appropriate credentials for the virtual machine.
3.  Speichern von Anmeldeinformationen in einer Variablen für die Wiederverwendung.
    Running a simple command like this:  
    ` PowerShell
    $localCred = Get-Credential
    `
    And then running something like this:
    ``` PowerShell
    Invoke-Command -VMName "test" -Credential $localCred  {get-process}


  ```
  Will mean that you only get prompted once per script/PowerShell session for your credentials.

4. Code your credentials into your scripts.  **Don't do this for any real workload or system**
 > Warning:  _Do not do this in a production system.  Do not do this with real passwords._

  You can hand craft a PSCredential object with some code like this:  
  ``` PowerShell
  $localCred = New-Object -typename System.Management.Automation.PSCredential -argumentlist "Administrator", (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force) 

  ```

Grob unsicher- aber für Testzwecke.
Jetzt erhalten Sie keine Aufforderungen überhaupt in dieser Sitzung.


