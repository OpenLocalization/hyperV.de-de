
#Export und Import virtuellen Maschinen

Sie können verwenden den Export und importieren Funktionalität schnell Duplizieren von virtuellen Maschinen oder von einem Host auf einen anderen verschieben.
Du musst nicht exportieren Sie eine virtuelle Maschine um es importieren können.
Sie können kopieren Sie einfach einen virtuellen Computer und die zugehörigen Dateien auf dem neuen Host, und verwenden Sie dann die **Virtuelle Maschine importieren** Assistent zum Angeben des Speicherorts der Dateien.
Das registriert die virtuelle Maschine mit Hyper-V und macht es verwertet werden.

##Virtuelle Maschinen exportieren

Eine einfache Möglichkeit, virtuelle Maschinen zu importierende vorzubereiten ist die **Virtuellen Computer exportieren** -Assistent.

1.  In Hyper-V-Manager wählen Sie eine oder mehrere virtuelle Computer mit der rechten Maustaste auf Ihre Auswahl und wählen Sie **Export**.
2.  Klicken Sie auf **Durchsuchen** im Dialog und wählen Sie wo Sie möchten, setzen Sie die exportierte VM(s) und klicken Sie dann auf **Wählen Sie Ordner**.
3.  In der **Virtuellen Computer exportieren** Dialogfeld, klicken Sie auf **Export**.

Informationen zur Verwendung von Windows PowerShell, um virtuelle Maschinen zu exportieren finden Sie unter [Export-VM](https://technet.microsoft.com/library/hh848491.aspx)

##Importieren von virtuellen Maschinen

1.  In **Hyper-V-Manager**, in der **Aktion** im Menü klicken **Virtuelle Maschine importieren**.
2.  Klicken Sie im Abschnitt Ordner suchen auf Durchsuchen, und navigieren Sie zu dem die VM-Dateien befinden.
    <!--zu prüfen, ob dies behoben - ist dieses Verhalten ist ein Bug aus meiner Sicht--> Bitte beachten Sie, dass mithilfe des Assistenten können Sie eine VM zu einem Zeitpunkt importieren und musst die VM-Ordner anstelle von den allgemeinen Exportordner auswählen.
    Klicken Sie auf **Nächste** Wenn fertig.
3.  Wählen Sie den virtuellen Computer zu importieren, und klicken Sie dann auf **Nächste**.
4.  Im Abschnitt wählen Sie Import-Typ können Sie den virtuellen Computer zu importieren:
    
    *   **Registrieren** -Nutzt die vorhandene eindeutige ID des virtuellen Computers, und registriert sie vor Ort.
        Wählen Sie diese Option, wenn die Dateien der virtuellen Maschinen bereits an der richtigen Stelle sind.
    *   **Wiederherstellen** -Eindeutige ID der ursprünglichen virtuellen Maschine verwendet und auch kopiert die Dateien der virtuellen Maschine auf den standardmäßigen Speicherort für den Host angegeben.
    *   **Kopie** -Erstellt eine neue eindeutige Kennung für die virtuelle Maschine und auch kopiert die Dateien der virtuellen Maschine auf den standardmäßigen Speicherort für den Host angegeben.
5.  Klicken Sie nach Auswahl die VM importieren, **Nächste**.
6.  Im Abschnitt wählen Sie Ziel können Sie wählen, wo Sie die Dateien für den virtuellen Computer gespeichert oder lassen sie in ihrem aktuellen Speicherort.
    Wenn Sie fertig sind, klicken Sie auf **Nächste**.
7.  Im Speicherordner auswählen können Sie einen anderen Ort zu speichern Sie die Datei .vhdx oder lassen Sie sie auswählen, wo sie sind.
    Wenn Sie fertig sind, klicken Sie auf **Nächste**.
8.  Wenn Sie die VM importieren abgeschlossen haben, sehen Sie die Seite "Zusammenfassung", beschreibt, in dem die neuen VM-Dateien befinden.

Der VM Import-Assistent führt Sie auch durch die Schritte der Adressierung Inkompatibilitäten beim Importieren der virtuelle Computer auf den neuen Host — so kann dieser Assistent mit Konfiguration helfen, die physische Hardware, wie z. B. Arbeitsspeicher, virtuelle Switches und virtuelle Prozessoren zugeordnet ist.

Um einen virtuellen Computer zu importieren, führt der Assistent die folgenden:

1.  Erstellt eine Kopie der Konfigurationsdatei des virtuellen Computers.
    Dies geschieht als Vorsichtsmaßnahme für den Fall, dass ein unerwarteter Neustart auf dem Host, wie z. B. von einem Stromausfall auftritt.
2.  Überprüft die Hardware.
    Informationen in der Konfigurationsdatei der virtuellen Maschine ist im Vergleich zu Hardware auf dem neuen Host.
3.  Erstellt eine Liste von Fehlern.
    Diese Liste gibt Was muss neu konfiguriert werden und bestimmt, welche Seiten weiter im Assistenten angezeigt werden.
4.  Zeigt die relevanten Seiten einer Kategorie zu einem Zeitpunkt.
    Der Assistent erklärt jede Inkompatibilität, mit denen Sie die virtuelle Maschine neu konfigurieren, so dass es kompatibel mit dem neuen Host.
5.  Entfernt die Kopie der Konfigurationsdatei.
    Nachdem der Assistent dies tut, kann die virtuelle Maschine gestartet werden.

Neben dem Assistenten umfasst das Hyper-V-Modul für Windows PowerShell Cmdlets für den Import von virtuellen Maschinen.
Weitere Informationen finden Sie unter [Import-VM](https://technet.microsoft.com/library/hh848495.aspx).


