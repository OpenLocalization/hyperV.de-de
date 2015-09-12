#Schritt 8: Experimentieren Sie mit Windows PowerShell

Nun, da Sie durch die Grundlagen der Bereitstellung von Hyper-V, virtuelle Maschinen erstellen und verwalten diese virtuellen Computer gegangen sind, lassen Sie uns, wie Sie viele dieser Aktivitäten mit PowerShell automatisieren können.

###Zurückgeben einer Liste der Hyper-V-Kommandos

1.  Klicken Sie auf die Windows-Schaltfläche Start, Typ **PowerShell**.
2.  Führen Sie den folgenden Befehl, um eine durchsuchbare Liste der PowerShell-Befehle zur Verfügung, mit dem Hyper-V-PowerShell-Modul anzuzeigen.
    
    ```powershell
    get-command –module hyper-v | out-gridview


```
  You get something like this:

  ![](media\command_grid.png)

3. To learn more about a particular PowerShell command use `get-help`. For instance running the following command will return information about the `get-vm` Hyper-V command.

  ```powershell
get-help get-vm

```

 Die Ausgabe zeigt, wie strukturieren den Befehl, was sind die erforderlichen und optionalen Parametern und der Aliase, die Sie verwenden können.

!(media\get_help.png)

###Zurückgeben einer Liste der virtuellen Maschinen

Nutzung der `get-vm` Befehl, um eine Liste der virtuellen Computer zurückgeben.

1.  Führen Sie den folgenden Befehl in die PowerShell:
    
    `powershell
    get-vm
    `
    This displays something like this:
    
    !(media\get_vm.png)
2.  Zurück nur eingeschaltet virtuellen Maschinen hinzufügen einen Filter, der `get-vm` Befehl.
    Mit den Befehl Where-Object kann ein Filter hinzugefügt werden.
    Weitere Informationen zum Filtern finden Sie unter der [Mit Hilfe der Where-Object](https://technet.microsoft.com/en-us/library/ee177028.aspx) Dokumentation.
    
    ```powershell
    get-vm | where {$_.State –eq ‘Running’}


 ```
3.  To list all virtual machines in a powered off state, run the following command. This command is a copy of the command from step 2 with the filter changed from ‘Running’ to ‘Off’.

 ```powershell
 get-vm | where {$_.State –eq ‘Off’}

 ```


###Starten und Herunterfahren der virtuellen Maschinen

1.  Um einen bestimmten virtuellen Computer zu starten, führen Sie den folgenden Befehl mit Namen der virtuellen Maschine:
    
    ```powershell
    Start-vm –Name virtual machine name


 ```

2. To start all currently powered off virtual machines, get a list of those machines and pipe the list to the 'start-vm' command:

  ```powershell
 get-vm | where {$_.State –eq ‘Off’} | start-vm

 ```

1.  Führen Sie diese Schritte aus, um alle ausgeführten virtuellen Computer herunterzufahren:
    
    ```powershell
    get-vm | where {$_.State –eq ‘Running’} | stop-vm


 ```

### Create a VM checkpoint

To create a checkpoint using PowerShell, select the virtual machine using the `get-vm` command and pipe this to the `checkpoint-vm` command. Finally give the checkpoint a name using `-snapshotname`. The complete command will look like the following:

 ```powershell
 get-vm -Name VM Name | checkpoint-vm -snapshotname name for snapshot

 ```

Hier ist beispielsweise ein Prüfpunkt mit dem Namen DEMOCP:

!(media\POSH_CP2.png)

###Erstellen einer neuen virtuellen Maschine

Das folgende Beispiel veranschaulicht das Erstellen Sie einer neuen virtuelle Maschine in der PowerShell Integrated Scripting Environment (ISE).
Dies ist ein einfaches Beispiel und enthalten zusätzliche PowerShell-Funktionen und erweiterte VM-Bereitstellungen auf erweitert werden konnte.

1.  Öffnen Sie die PowerShell ISE klicken Sie auf Start, geben Sie **PowerShell-ISE**.
2.  Führen Sie den folgenden Code zum Erstellen einer virtuellen Maschine.
    Finden Sie unter der [Neue VM](https://technet.microsoft.com/en-us/library/hh848537.aspx) Dokumentation für detaillierte Informationen über den Befehl New-VM.
    
    ```powershell
    $VMName = "VMNAME"
    
    $VM = @{
     Name = $VMName 
     MemoryStartupBytes = 2147483648
     Generation = 2
     NewVHDPath = "C:\Virtual Machines\$VMName\$VMName.vhdx"
     NewVHDSizeBytes = 53687091200
     BootDevice = "VHD"
     Path = "C:\Virtual Machines\$VMName "
     SwitchName = (get-vmswitch).Name[0]
    }
    
    New-VM @VM
    ```

##Einpacken und Verweise

Dieses Dokument hat einige einfache Schritte, Explorer das Hyper-V-PowerShell-Modul sowie einige Beispielszenarien gezeigt.
Weitere Informationen über die Hyper-V-PowerShell-Module finden Sie unter der [Hyper-V-Cmdlets in Windows PowerShell-Referenz](https://technet.microsoft.com/%5Clibrary/Hh848559.aspx).


