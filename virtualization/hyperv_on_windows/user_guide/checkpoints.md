#Verwendung von Prüfpunkten virtuelle Computer in einen früheren Zustand wiederherstellen

Prüfpunkte bieten eine schnelle und einfache Möglichkeit, den virtuellen Computer in einen früheren Zustand wiederherzustellen.
Dies ist besonders hilfreich, wenn Sie zu einer virtuellen Maschine ändern und Sie in der Lage, zu den gegenwärtigen Zustand Rollback Wenn Ursache Probleme ändern möchten.

##Aktivieren oder Deaktivieren von Prüfpunkten

1.  In **Hyper-V-Manager**, klicken Sie mit der rechten Maustaste auf den virtuellen Computer, und klicken Sie auf **Einstellungen**.
2.  In der **Verwaltung** Abschnitt, wählen Sie **Prüfpunkte**.
3.  Damit können Kontrollpunkte dieser virtuellen Maschine abgenommen werden, stellen Sie sicher, dass Checkpoints aktivieren ausgewählt ist--ist dies das Standardverhalten.
    Um die Prüfpunkte zu deaktivieren, deaktivieren Sie die **Checkpoints aktivieren** das Kontrollkästchen.
4.  Klicken Sie auf **Gelten** um Ihre Änderungen zu übernehmen.
    Wenn Sie fertig sind, klicken Sie auf **Okay** um das Dialogfeld zu schließen.

##Wählen Sie Standard oder Produktion Prüfpunkte

Es gibt zwei Arten von Checkpoints:

*   **Produktion-Kontrollpunkte** --Als eine Form der Sicherung vor allem auf Servern in Produktionsumgebungen verwendet.
*   **Norm-Kontrollpunkte** --In Entwicklungs- oder Testumgebungen verwendet, um Rollback zu ermöglichen, wenn eine Änderung fehlschlägt.

Beide Arten von Checkpoints wiederherstellen eine virtuelle Maschine auf einen früheren Zustand.

Produktion-Kontrollpunkte erstellt ein anwendungskonsistente-Checkpoint einer virtuellen Maschine.
Das bedeutet, dass die gespeicherte virtuelle Maschine mit keine Anwendungszustand fortgesetzt wird.

Norm Prüfpunkte (früher bekannt als Snapshots) erfassen den genaue Speicherstatus Ihrer virtuellen Maschine.
Das bedeutet, dass die virtuelle Maschine mit wiederhergestellt werden sollen **genau** den gleichen Zustand, in dem Checkpoint zu genauen Anwendungszustand abgenommen wurde.
Norm-Kontrollpunkte können Informationen über Client-Verbindungen, Transaktionen und den externen Netzwerk-Status enthalten.
Diese Informationen möglicherweise nicht gültig, wenn der Prüfpunkt angewendet wird.
Darüber hinaus werden ein Checkpoint in einem Absturz des Programms getroffen wird, Wiederherstellen von diesen Prüfpunkt in der Mitte dieser Absturz.

Das Vorhandensein einer Norm-Checkpoint für eine virtuelle Maschine kann die Datenträgerleistung des virtuellen Computers auswirken.
Wir empfehlen nicht mit Norm Prüfpunkte auf virtuellen Maschinen, wenn Leistung oder die Verfügbarkeit des Speicherplatzes wichtig ist.

Anwenden eines Checkpoints Produktion umfasst Offlinestatus das Gast-Betriebssystem gebootet.
Dies bedeutet, dass kein Staat oder Sicherheit Anwendungsinformationen als Teil der Checkpoint-Prozess erfasst wird.

Die folgende Tabelle zeigt wann Produktion Prüfpunkte oder Norm Kontrollstellen, je nach Zustand des virtuellen Computers zu verwenden.

| **Zustand der virtuellen Maschine**| **Produktion-Checkpoint**| **Norm-Checkpoint**|
|:-----|:-----|:-----|
| **Ausführen von Integration Services**| Ja| Ja|
| **Ohne Integrationsservices ausführen**| Nicht| Ja|
| **Offline - keine gespeicherten Zustand**| Ja| Ja|
| **Offline - mit gespeicherten Zustand**| Nicht| Ja|
| **Angehalten**| Nicht| Ja|
Um den Unterschied zwischen Standard- und Produktion Checkpoints zu sehen, betrachten Sie die [Prüfpunkte Exemplarische Vorgehensweise](../quick_start/walkthrough_checkpoints.md).

##Legen Sie einen Prüfpunkt Standardtyp

1.  In **Hyper-V-Manager**, klicken Sie mit der rechten Maustaste auf den virtuellen Computer, und klicken Sie auf **Einstellungen**.
2.  In der **Verwaltung** Abschnitt, wählen Sie **Prüfpunkte**.
3.  Wählen Sie entweder Produktion Prüfpunkte oder Norm Prüfpunkte.
    Wenn Sie Produktion Prüfpunkte wählen, können Sie auch angeben, ob der Host einen Norm Prüfpunkt ergreifen sollten, wenn ein Prüfpunkt Produktion nicht gefasst werden kann.
    Wenn Sie dieses Kontrollkästchen deaktivieren und ein Checkpoint Produktion kann nicht genommen werden, wird kein Prüfpunkt ausgewählt.
4.  Wenn Sie möchten den Speicherort zu ändern, in dem die Konfigurationsdateien für den Prüfpunkt gespeichert werden, ändern Sie den Pfad in der **Speicherort der Prüfpunkt-Datei** Abschnitt.
5.  Klicken Sie auf **Gelten** um Ihre Änderungen zu übernehmen.
    Wenn Sie fertig sind, klicken Sie auf **Okay** um das Dialogfeld zu schließen.

Das Standardverhalten in Windows 10 für neue virtuelle Computer ist Produktion Kontrollpunkte mit Fallback auf Norm Prüfpunkte erstellt werden.

##Erstellen eines Checkpoints

Um einen Checkpoint zu erstellen

1.  In **Hyper-V-Manager**, unter **Virtuelle Maschinen**, wählen Sie die virtuelle Maschine.
2.  Klicken Sie mit der rechten Maustaste auf den virtuellen Computer, und klicken Sie dann auf **Prüfpunkt**.
3.  Wenn der Prozess abgeschlossen ist, erscheint der Prüfpunkt unter **Prüfpunkte** in der **Hyper-V-Manager**.

##Anwenden eines Checkpoints

Wenn Sie Ihren virtuellen Computer zu einem früheren-Zeitpunkt wiederherstellen möchten, können Sie ein vorhandenes Checkpoint anwenden.

1.  In **Hyper-V-Manager**, unter **Virtuelle Maschinen**, wählen Sie die virtuelle Maschine.
2.  Im Abschnitt Checkpoints Maustaste dem Checkpoint, die Sie verwenden möchten und klicken Sie auf **Gelten**.
3.  Es erscheint ein Dialogfenster mit den folgenden Optionen: 


```
**Create Checkpoint and Apply**: Creates a new checkpoint of the virtual machine before it applies the earlier checkpoint. 

**Apply**: Applies only the checkpoint that you have chosen. You cannot undo this action.

**Cancel**: Closes the dialog box without doing anything.

```


##Löschen eines Checkpoints

Um einen Checkpoint sauber zu löschen: 

1.  In **Hyper-V-Manager**, wählen Sie die virtuelle Maschine.
2.  In der **Prüfpunkte** Abschnitt, mit der rechten Maustaste des Prüfpunkts, den Sie löschen möchten, und klicken Sie auf Löschen.
    Sie können auch einen Checkpoint und alle nachfolgenden Checkpoints löschen.
    Dazu mit der rechten Maustaste des frühesten Prüfpunkts, den Sie verwenden möchten, löschen Sie, und klicken Sie dann auf **** Löschen Checkpoint** Unterstruktur **.
3.  Sie möglicherweise aufgefordert, sicherzustellen, dass den Prüfpunkt löschen möchten.
    Bestätigen Sie, dass es der richtige Checkpoint, und klicken Sie auf **Löschen**.
4.  Die Dateien .avhdx und .vhdx Zusammenführen werden, und wenn Sie fertig sind, wird die .avhdx-Datei aus dem Dateisystem gelöscht werden.

> **Tipp:** Verwenden Sie Windows Powershell einen Prüfpunkt löschen Sie mithilfe der **Entfernen-VMSnapshot** Cmdlet.
> 

Prüfpunkte werden als .avhdx-Dateien in demselben Speicherort wie die .vhdx-Dateien für den virtuellen Computer gespeichert.
Sie sollten die .avhdx-Dateien nicht direkt löschen.

##Ändern wo Prüfpunkt Einstellungen und Speichern des Zustands Dateien werden gespeichert

Wenn die virtuelle Maschine keine Checkpoints verfügt, können Sie ändern, in dem die Prüfpunkt-Konfiguration und gespeicherten Zustand Dateien gespeichert werden.

1.  In **Hyper-V-Manager**, klicken Sie mit der rechten Maustaste auf den virtuellen Computer, und klicken Sie auf **Einstellungen**.
2.  In der **Verwaltung** Abschnitt, wählen Sie **Prüfpunkte** oder **Speicherort der Prüfpunkt-Datei**.
3.  In **Speicherort der Prüfpunkt-Datei**, geben Sie den Pfad zu dem Ordner, wo Sie die Dateien speichern möchten.
4.  Klicken Sie auf **Gelten** um Ihre Änderungen zu übernehmen.
    Wenn Sie fertig sind, klicken Sie auf **Okay** um das Dialogfeld zu schließen.

Der standardmäßige Speicherort zum Speichern der Konfiguration Prüfpunktdateien ist: % systemroot%\ProgramData\Microsoft\Windows\Hyper-V\Snapshots.


##Umbenennen eines Checkpoints

1.  In **Hyper-V-Manager**, wählen Sie die virtuelle Maschine.
2.  Maustaste auf dem Checkpoint, und wählen Sie dann **Benennen Sie**.
3.  Geben Sie den neuen Namen für den Prüfpunkt.
    Es muss weniger als 100 Zeichen, und das Feld darf nicht leer sein.
4.  Klicken Sie auf **GEBEN SIE** Wenn Sie fertig sind.

Standardmäßig ist der Name von einem Checkpoint der Name der virtuellen Maschine kombiniert mit Datum und Uhrzeit, die der Prüfpunkt getroffen wurde.
Dies ist das standard-Format:


```
virtual_machine_name (MM/DD/YYY –hh:mm:ss AM\PM)

```

Namen sind auf 100 Zeichen oder weniger beschränkt, und der Name darf nicht leer sein.


