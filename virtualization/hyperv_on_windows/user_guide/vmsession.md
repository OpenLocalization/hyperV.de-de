#Verwalten von Windows PowerShell direkten

PowerShell-Direct können Sie die Remoteverwaltung eines Windows 10 oder virtuelle Maschine Windows Server Technical Preview von einem Windows 10 oder Windows Server technische Vorschau Hyper-V-Host.
PowerShell-Direct ermöglicht PowerShell Management innerhalb eines Virtual machine unabhängig von der Netzwerkkonfiguration oder remote-Management-Einstellungen auf entweder die Hyper-V-Host oder der virtuellen Maschine.
Dies erleichtert für Hyper-V-Administratoren automatisieren und script-Virtual Machine-Management und Konfiguration.

Es gibt zwei Möglichkeiten zum Ausführen von PowerShell-Direct:  

*   Erstellen Sie und beenden Sie eine Sitzung des PowerShell-Direct mit PSSession cmdlets
*   Run-Skript oder mit dem Cmdlet Invoke-Command Befehl

Wenn Sie ältere virtuelle Maschinen verwalten, verwenden Verbindung mit virtuellen Computern (VMConnect) oder [Konfigurieren eines virtuellen Netzwerks für die virtuelle Maschine](http://technet.microsoft.com/library/cc816585.aspx).

##Erstellen Sie und beenden Sie eine Sitzung des PowerShell-Direct mit PSSession cmdlets

1.  Öffnen Sie Windows PowerShell auf dem Hyper-V-Host als Verwalter.
2.  Run the one of the following commands to create a session by using the virtual machine name or GUID:  
    ``` PowerShell
    Enter-PSSession -VMName VMName
    Enter-PSSession -VMGUID VMGUID


```

4. Run whatever commands you need to. These commands run on the virtual machine that you created the session with.
5. When you're done, run the following command to close the session:  
``` PowerShell
Exit-PSSession 

```


> Hinweis: Wenn Sie die Sitzung sind nicht anschließen, stellen Sie sicher Sie verwenden Anmeldeinformationen für den virtuellen Computer, die Sie an--nicht den Hyper-V-Host herstellen.
> 

Mehr über diese Cmdlets finden Sie unter [Geben Sie-PSSession](http://technet.microsoft.com/library/hh849707.aspx) und [Exit-PSSession](http://technet.microsoft.com/library/hh849743.aspx).

##Run-Skript oder mit dem Cmdlet Invoke-Command Befehl

Können Sie die [Invoke-Command](http://technet.microsoft.com/library/hh849719.aspx) Cmdlet einen vordefinierten Satz von Befehlen auf dem virtuellen Computer ausgeführt.
Hier ist ein Beispiel für die Verwendung von des Cmdlets Invoke-Command wobei PSTest Name der virtuellen Maschine und das Skript (foo.ps1) ausgeführt wird, auf Laufwerk C: im Ordner Skript / drive:

 ``` PowerShell
 Invoke-Command -VMName PSTest -FilePath C:\script\foo.ps1 


 ```

To run a single command, use the **-ScriptBlock** parameter:

 ``` PowerShell
 Invoke-Command -VMName PSTest -ScriptBlock { cmdlet } 

 ```


##Was ist erforderlich, um PowerShell direkt verwenden?

Eine direkte PowerShell-Sitzung auf einem virtuellen Computer zu erstellen,

*   Die virtuelle Maschine muss lokal auf dem Host ausgeführt werden und gebootet.
*   Sie müssen in den Hostcomputer als Hyper-V-Administrator angemeldet sein.
*   Sie müssen gültige Benutzeranmeldeinformationen für die virtuelle Maschine angeben.
*   Das Host-Betriebssystem muss Windows 10 Windows Server Technical Preview oder eine höhere Version ausgeführt.
*   Der virtuelle Computer muss Windows 10 Windows Server Technical Preview oder eine höhere Version ausgeführt.

Können Sie die [Get-VM](http://technet.microsoft.com/library/hh848479.aspx) Cmdlet überprüfen, ob die Anmeldeinformationen, die Sie verwenden die Hyper-V-Administratorrolle haben und sehen die VMs werden lokal auf dem Host ausgeführt und gebootet.

##Was können Sie mit PowerShell-Direct?

Finden Sie unter [PowerShell-Direct-Ausschnitte](../develop/powershell_snippets.md) zahlreiche Beispiele der Verwendung PowerShell direkt in Ihrer Umgebung sowie Tipps und Tricks für Hyper-V-Skripten mit PowerShell.


