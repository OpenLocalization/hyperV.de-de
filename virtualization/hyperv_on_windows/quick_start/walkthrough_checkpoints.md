#Schritt 6: Experiment mit checkpoints

Kontrollpunkte sind ein hilfreiches Werkzeug, wenn Sie den aktuellen Status einer virtuellen Maschine zu speichern, bevor Sie eine Änderung wie Anwenden eines Updates, Software installieren oder Ändern einer Einstellung möchten.
Wenn die Änderung Probleme verursacht, können Sie wiederherstellen den Prüfpunkt und zurück.

There are two types of checkpoints:  
**Produktion-Kontrollpunkte**: Vor allem auf Servern in Produktionsumgebungen eingesetzt.
**Norm-Kontrollpunkte**: In Entwicklungs- oder Testumgebungen verwendet

Produktion-Kontrollpunkte sind Standard für Hyper-V auf Windows 10.

##Den Prüfpunkt-Typ ändern

Wir beginnen, durch Ausprobieren den älteren Stil der Prüfpunkte, **Norm-Kontrollpunkte**.
Da die Produktion der Standard sind, müssen wir rufen die Einstellungen für den virtuellen Computer, und ändern Sie den Typ der Prüfpunkt.

1.  Mit einem Rechtsklick **Windows Walkthrough VM** und wählen Sie **Einstellungen**.
2.  In der **Verwaltung** Abschnitt, wählen Sie **Prüfpunkte**.
3.  Wählen Sie **Norm-Kontrollpunkte**.
    Der Dialog sollte wie folgt aussehen:
    
    !(media/standard1.png)
4.  Klicken Sie auf **Okay** um das Dialogfeld zu schließen.

##Offen Notepad Prüfpunkte zu testen

Um zu sehen, was passiert mit jeder Art von Prüfpunkt, werden wir eine Anwendung in der VM ausführen.

1.  Mit einem Rechtsklick **Windows Walkthrough VM** und wählen Sie **Verbinden**.
2.  Öffnen Sie in der virtuellen Maschine **Notizblock** durch Anklicken der **Start** Menü und tippen **Notizblock** und wählen sie dann aus den Ergebnissen.
3.  Geben Sie im Editor **Dies ist ein Test der Prüfpunkte.** Die Datei sollte so aussehen:
    
    !(media/standard_notepad.png)
4.  Speichern Sie die Datei als **Test.txt**, aber nicht schließen Sie den Editor.
    Lassen Sie es auf dem virtuellen Computer ausgeführt.

##Erstellen Sie einen standard-checkpoint

1.  Um den Prüfpunkt zu erstellen, klicken Sie auf die !(media/checkpoint_button.png)**Prüfpunkt** Schaltfläche in der Menüleiste.
2.  Geben Sie im Dialogfeld Name Prüfpunkt **Standard**.
    Der Dialog sollte wie folgt aussehen:
    
    !(media/save_standard.png)
3.  Wenn der Prozess abgeschlossen ist, erscheint der Prüfpunkt unter **Prüfpunkte** in der **Hyper-V-Manager**.
    
    !(media/standard_complete.png)

##Erstellen eines Checkpoints Produktion

Jetzt müssen wir ändern, ändern Sie den Typ des Prüfpunkts, die wir wollen zurück zu nehmen **Produktion-Kontrollpunkte** vor der Einnahme eines zweiten Checkpoints.

1.  Mit der rechten Maustaste den virtuellen Computer, und klicken Sie auf **Einstellungen**.
2.  In der **Verwaltung** Abschnitt, wählen Sie **Prüfpunkte**.
3.  Wählen Sie **Produktion-Kontrollpunkte**.
4.  Deaktivieren Sie die Option Herbst-zurück.
    Wenn das System einen Checkpoint Produktion nehmen kann nicht, wollen wir statt einen Norm Checkpoint fehlschlagen lassen.
    
    !(media/production.png)
5.  Klicken Sie auf **Okay** um das Dialogfeld zu schließen.
6.  Der rechten Maustaste auf den virtuellen Computer erneut, und wählen Sie **Verbinden**.
7.  Geben Sie im Editor in der VM eine weitere Zeile, die liest **Dies ist ein Test von einem Checkpoint Produktion** und speichern Sie die Datei erneut.
8.  Klicken Sie auf die !(media/checkpoint_button.png)**Prüfpunkt** Schaltfläche in der Menüleiste.
9.  Wenn gefragt, nennen Sie es **Produktion** und klicken Sie dann auf **Ja**.
    
    !(media/production_CheckpointName.png)
10.  VMConnect zu schließen.
    Die VM wird weiter ausgeführt, Sie nur wird nicht verbunden sein, es nicht mehr.
11.  In Hyper-V-Manager wird Ihre Liste von Checkpoints nun so aussehen:
    
    !(media/production_complete.png)

##Anwenden der Norm checkpoint

1.  In **Hyper-V-Manager**, in der **Prüfpunkte** Abschnitt der rechten Maustaste auf diejenige mit dem Titel **Standard** und klicken Sie auf **Gelten**.
2.  Klicken Sie im Popup-dialog **Checkpoint zu erstellen und anwenden**.
    
    !(media/apply_standard.png)
3.  Wenn das fertig, Ihre Liste von Checkpoints jetzt wird etwa wie folgt aussehen:
    
    !(media/standard_applied.png)
4.  Wenn dies abgeschlossen ist, mit der rechten Maustaste den virtuellen Computer und dann auf **Verbinden** der VM verbinden.
5.  Beim Anschließen an die VM die VM sollte laufen, mit Notepad geöffnet, aber die Linie über Produktion Prüfpunkte werden fehlende:
    
    !(media/standard_applied_notepad.png)
6.  VMConnect zu schließen, aber die VM laufen lassen.

##Anwenden der Produktion-checkpoint

Nun gehen Sie wir zurück zu Hyper-V Manager und wenden Sie Checkpoint Produktion an und sehen Sie, wie unsere VM danach aussieht.

1.  Klicken Sie im Abschnitt Checkpoints derjenige mit dem Titel **Produktion-Checkpoint** und klicken Sie auf **Gelten**.
2.  Wählen Sie im Popup-dialog **Checkpoint zu erstellen und anwenden**.
3.  Wenn dies abgeschlossen ist, mit der rechten Maustaste den virtuellen Computer und dann auf **Verbinden** die VM zu starten.
4.  Sie werden bemerken, dass die VM nicht ausgeführt wird.
    Klicken Sie auf die !(media/start.png) Start-Taste in der Menüleiste auf die VM gestartet.
5.  Öffnen Sie in Editor öffnen test.txt.
    Sie sollten die Zeile in der Datei zum Testen Produktion Kontrollpunkte sehen:
    
    !(media/production_notepad.png)

##Umbenennen eines Checkpoints

1.  Maustaste auf dem letzten Checkpoint in der Struktur, und klicken Sie auf Umbenennen.
2.  Name der Prüfpunkt **Streichen Sie mich**.
    
    !(media/delete_me.png)

##Löschen eines Checkpoints

Vorherige Schritt hat wahrscheinlich Sie gegeben einen Hinweis, was wir als nächstes tun werde.
Wir werden den Prüfpunkt zu löschen, den Sie gerade umbenannt.

1.  Maustaste auf dem Checkpoint benannt **Streichen Sie mich** und klicken Sie auf **Prüfpunkt löschen**.
    
    !(media/delete_checkpoint.png)
2.  Klicken Sie im Dialogfeld Warnung **Löschen**.
    
    !(media/delete_warn.png)
3.  Nach dem Checkpoint gelöscht wird, sollte die Liste wie folgt aussehen:
    
    !(media/after_delete.png)

##Nächster Schritt:

[Schritt 7: Exportieren Sie und importieren Sie eine virtuelle Maschine](walkthrough_export_import.md)


