#Schritt 7: Exportieren Sie und importieren Sie eine virtuelle Maschine

Schnell können einen virtuellen Computer zu kopieren oder verschieben eine virtuellen Maschine mit dem Exportieren und Importieren von Funktionalität.

##Export der VM

Exportieren einer virtuellen Maschine exportiert alle Stücke der VM, einschließlich den Checkpoints.

1.  In Hyper-V-Manager mit der rechten Maustaste den virtuellen Computer, und wählen Sie **Export**.
    
    !(media/select_export1.png)
2.  Klicken Sie auf **Durchsuchen** im Dialog box und navigieren Sie zu C:\Users\Public und klicken Sie auf **Wählen Sie Ordner**.
3.  In der **Virtuellen Computer exportieren** Dialogfeld, stellen Sie sicher, dass der Pfad in Ordnung aussieht und dann auf **Export**.
    
    !(media/click_export.png)
4.  Während die VM exportiert wird, können Sie den Fortschritt im Abschnitt Status sehen:
    
    !(media/export_progress.png)

##Funktionierte der Export?

Um sicherzustellen, dass die virtuelle Maschine exportiert wurde, rechtsklicken Sie auf Ihre **Start** Menü und wählen Sie **Datei-Explorer**.

1.  Navigieren Sie zu C:\Users\Public\Windows Exemplarische Vorgehensweise VM.
2.  Sehen Sie einen anderen Ordner namens Windows Walkthrough VM und in diesem Ordner sollte drei Ordner mit den Dateien für Ihre exportierten virtuellen Maschine:
    
    *   Momentaufnahmen
    *   Virtuelle Festplatten
    *   Virtuelle Maschinen 
    
    !(media/export_confirm.png)

##Die VM importieren

Bevor wir die VM importieren, werden wir die ursprüngliche VM löschen.
Mit der rechten Maustaste auf die VM und wählen Sie **Löschen**.

1.  In **Hyper-V-Manager**, in der **Aktion** im Menü klicken **Virtuelle Maschine importieren**.
2.  In der **Suchen Sie den Ordner** Abschnitt, klicken Sie auf Durchsuchen und navigieren Sie zu C:\Users\Public\Windows Exemplarische Vorgehensweise VM und dann auf **Nächste**.
3.  In der **Wählen Sie virtuellen Computer importieren** Bildschirm klicken **Nächste**.
4.  In der **Wählen Sie Importtyp** Abschnitt, wählen Sie **Registrieren Sie die virtuelle Maschine im Ort** und klicken Sie dann auf **Nächste**.
5.  In der **Wählen Sie Ziel** Abschnitt behalten Sie die Standardeinstellung, und klicken Sie **Nächste**.
6.  Verlassen Sie im Speicherordner auswählen den Standardpfad zu und auf **Nächste**.
7.  Auf der Übersichtsseite sehen Sie eine Liste der Pfade, wo die neuen VM-Dateien gespeichert werden.
    Klicken Sie auf **Fertig stellen** um den Import zu starten.

##Funktionierte der Import?

Um sicherzustellen, dass der Import gearbeitet haben, doppelklicken Sie einfach die VM in **Hyper-V-Manager** und starten Sie VMConnect um die VM zu überprüfen.

##Nächster Schritt:

[Schritt 8: Experimentieren Sie mit Windows Powershell](walkthrough_powershell.md)


