#Schritt 1: Stellen Sie sicher, dass Ihre Maschine Hyper-V ausgeführt werden können

Nur Windows 10 Pro und Windows 10 Enterprise unterstützt Hyper-V.

> Wenn Sie Windows 10 Home--ausführen können Sie in der Aktivierungs-Seite befindet sich in den Sicherheitseinstellungen auf Win 10 Pro aktualisieren.
> Der Link "Gehe um zu speichern" gelangen Sie zu einer Seite für die Aktualisierung.
> 

Hyper-V ist nicht verfügbar in Windows 10 Mobile / Windows 10 Mobile Enterprise

Hyper-V erfordert mindestens 4 GB RAM, aber Sie brauchen mehr, wenn Sie mehrere virtuelle Computer gleichzeitig ausführen möchten.

Ab Windows 10, erfordert Hyper-V einen 64-Bit-Prozessor mit Second Level Address Translation (Stab).

##Überprüfen Sie die Hardware-Kompatibilität

Um Kompatibilität zu überprüfen, öffnen Sie PowerShell oder eine Windows-Eingabeaufforderung (cmd.exe) und Typ: `systeminfo.exe`.
Dadurch erhalten Sie Informationen über Ihren Computer.

Alle Elemente unter **Hyper-V-Anforderungen** muss den Wert wenn verfügen **Ja**.

!(media\systeminfo.png)

Relevanten Bereichen:

*   `OS Name` --Windows 8 oder höher und Beruf oder Enterprise muss sein.
*   `Hyper-V Requirements` --all dies muß wahr (Wert "Yes"), aber einige können im BIOS eingestellt werden.
    
    *   `VM Monitor Mode Extensions` --Eigenschaft der Hardware.
        Hyper-V kann nicht auf diesem Computer ausführen.
    *   `Virtualization Enabled in Firmware` --Kann im BIOS aktiviert werden
    *   `Second Level Address Translation` --Eigenschaft der Hardware.
        Hyper-V kann nicht auf diesem Computer ausführen.
    *   `Data Execution Prevention Available` --Kann im BIOS aktiviert werden

Wenn Hyper-V bereits aktiviert ist, liest der Abschnitt über die Hyper-V-Anforderungen:  


```
Hyper-V Requirements: A hypervisor has been detected. Features required for Hyper-V will not be displayed.

```


##Nächster Schritt:

[Schritt 2: Installieren von Hyper-V](walkthrough_install.md)


