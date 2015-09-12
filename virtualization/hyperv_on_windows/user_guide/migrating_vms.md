#Migrieren und Aktualisieren von virtuellen Maschinen

Wenn Sie virtueller Maschinen auf Maschinenebene Windows 10, die ursprünglich mit Hyper-V in Windows 8.1 oder früher erstellt wurden verschieben, werden nicht Sie möglicherweise die neue virtuelle Maschine-Features verwenden, bis Sie die virtuelle Maschine Konfigurationsversion manuell aktualisieren.

Um die Konfigurationsversion zu aktualisieren, den virtuellen Computer Herunterfahren Sie, und wählen Sie dann zum Upgrade Konfiguration des virtuellen Computers in Hyper-V Manager.
Sie können auch eine erhöhte öffnen Windows PowerShell-Eingabeaufforderung, und geben:

 ```PowerShell
Update-VmVersion <vmname> | <vmobject>


```



## How do I check the configuration version of the virtual machines running on Hyper-V? 

To find the configuration version, open an elevated Windows PowerShell command prompt, and run the following command:

**Get-VM * | Format-Table Name, Version**

The PowerShell command produces the following sample output:


```

Name State CPUUsage(%) MemoryAssigned(M)-Uptime-Status-Version

Atlantis ausgeführt 0-1024 00:04:20.5910000 funktioniert normal 5.0

SGC VM      Running         0       538                 00:02:44.8350000    Operating normally      6.2
```

##Was passiert, wenn ich nicht die Konfiguration der Version aktualisieren?

Wenn Sie virtuelle Computer, die Sie mit einer früheren Version von Hyper-V erstellt verfügen, einige Funktionen funktioniert möglicherweise nicht mit diesen virtuellen Maschinen bis Sie die VM-Version zu aktualisieren.

Minimale Version von VM-Konfiguration für Hyper-V-Neuerungen:

| **Name des Features**| **Mindestversion VM**| |
| :------------------------------------- | -----------------: ||
| Heiße hinzufügen/entfernen-Speicher| 6.0| |
| Heiße hinzufügen/entfernen-Netzwerkadapter| 5.0| |
| Secure Boot für Linux-VMs| 6.0| |
| Produktion-Checkpoints| 6.0| |
| PowerShell-Direct| 6.2| |
| Virtuelle Trusted Platform Module (vTPM)| 6.2| |
| Virtuelle Maschine Gruppierung| 6.2| |

##Virtuelle Maschine Konfigurationsversion

Beim Verschieben oder eine virtuelle Maschine auf einen Host mit Hyper-V auf Windows 10 von Windows 8.1-Host zu importieren, ist nicht die Konfigurationsdatei des virtuellen Computers automatisch aktualisiert.
Dadurch kann die virtuelle Maschine auf einem Host mit Windows 8.1 zurück verschoben werden.
Sie müssen nicht Zugriff auf virtuelle Maschine Neuerungen, bis Sie die virtuelle Maschine Konfigurationsversion manuell aktualisieren.

Die VM-Konfiguration-Version stellt dar, welche Version von Hyper-V-Konfiguration des virtuellen Computers gespeicherten Zustand und snapshot-Dateien, die mit kompatibel ist.
Virtuelle Maschinen mit Konfiguration der Version 5 sind kompatibel mit Windows 8.1 und Windows 8.1 und Windows 10 ausführen.
Virtuelle Maschinen mit Konfiguration der Version 6 sind kompatibel mit Windows 10 und läuft nicht auf Windows 8.1.

Es ist nicht notwendig, um alle virtuellen Computer gleichzeitig zu aktualisieren.
Sie können wählen, um bestimmte virtuelle Maschinen bei Bedarf zu aktualisieren.
Allerdings müssen Sie nicht Zugriff auf neue virtuelle Maschine Funktionen, bis Sie die Konfigurations-Version für jeden virtuellen Computer manuell aktualisieren.

----------------
**Important **

• Nachdem Sie die virtuelle Maschine Konfigurationsversion aktualisieren, können nicht Sie die virtuelle Maschine an einen Host verschieben, die ausgeführt Windows 8.1 wird.

• Die virtuelle Maschine Konfigurationsversion ab Version 6 auf Version 5 downgrade nicht möglich.

• Sie müssen den virtuellen Computer für die Konfiguration des virtuellen Computers aktualisieren deaktivieren.

• Nach dem Upgrade der virtuellen Maschine verwendet das Format der neuen Konfigurationsdatei.
Weitere Informationen finden Sie unter neue virtuelle Maschine Konfigurations-Dateiformat.

--------

##Was passiert, wenn ich ein der Version einer virtuellen Maschine Upgrade?

Wenn Sie manuell aktualisieren, die Konfigurationsversion einer virtuellen Maschine auf Version 6.x, ändern Sie die Dateistruktur, die zum Speichern der virtuellen Maschinen-Konfiguration und Checkpoint-Dateien verwendet wird.

Aktualisierten virtuellen Maschinen verwendet ein neues Format für Konfiguration, zur Steigerung der Effizienz des Lesens und Schreibens von Daten zur Konfiguration der virtuellen Maschine vorgesehen ist.
Das Upgrade reduziert auch das Potenzial für die Beschädigung von Daten beim Ausfall eines Speicher.

Die folgende Tabelle listet die Binärdatei Standorte und Erweiterungsinformationen für eine aktualisierte virtuelle Maschine.

| **VM-Konfiguration und Checkpoint-Dateien (Version 6.x)**| **Beschreibung**| |
|:---------------|:----------------||
| **Konfiguration des virtuellen Computers**| Konfigurationsinformationen werden in einem binären Dateiformat gespeichert, das die .vmcx-Erweiterung verwendet.| |
| **Status des virtuellen Computers-Runtime**| Zustandsdaten Runtime werden in ein binäres Dateiformat gespeichert, das die .vmrs-Erweiterung verwendet.| |
| **Virtuelle Festplatte virtuelle Maschine**| Die virtuelle Festplatte-Dateien für den virtuellen Computer.Sie verwenden die Dateierweiterungen VHD oder .vhdx.| |
| **Automatische virtuelle Festplatte-Dateien**| Die differenzierende virtuelle Maschine Kontrollpunkte verwendeten Datenträgerdateien.Sie verwenden die .avhdx-Datei-Erweiterungen.| |
| **Prüfpunktdateien**| Prüfpunkte werden in mehreren Checkpoint-Dateien gespeichert.Jedem Checkpoint erstellt eine Konfigurationsdatei und Runtime-Statusdatei.Checkpoint-Dateien verwenden, die .vmrs und .vmcx Dateierweiterungen.Diese neuen Dateiformate werden auch für Produktion Checkpoints und Norm Prüfpunkte verwendet.| |
Nachdem Sie die Konfiguration des virtuellen Computers aktualisiert Version zu Version 6.x, es ist nicht möglich, downgrade von Version 6.x auf Version 5.

Die virtuelle Maschine muss deaktiviert werden, um die Konfiguration des virtuellen Computers zu aktualisieren.

Die folgende Tabelle listet die Datei Standardspeicherorte für neue oder aktualisierte virtuelle Maschinen.

| **Dateien des virtuellen Computers (Version 6.x)**| **Beschreibung**| |
|:-----|:-----||
| **Konfigurationsdatei der virtuellen Maschine**| C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Maschinen| |
| **Virtuelle Maschine Runtime-Statusdatei**| C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Maschinen| |
| **Checkpoint-Dateien (.vmrs, .vmcx)**| C:\ProgramData\Microsoft\Windows\Snapshots| |
| **Virtuelle Festplattendatei (.vhd/.vhdx)**| C:\Users\Public\Documents\Hyper-V\Virtual Hard Disks| |
| **Automatische virtuelle Festplatte-Dateien (.avhdx)**| C:\Users\Public\Documents\Hyper-V\Virtual Hard Disks| |


