#Einführung in Hyper-V unter Windows 10 (Beta3)

Ob Sie ein Softwareentwickler, eine ITPro oder ein Techenthusiast sind, müssen viele von Ihnen mehrere Betriebssysteme, gelegentlich auf vielen verschiedenen Computern ausführen.
Nicht alle von uns haben Zugriff auf eine vollständige Suite von Labs, um diese Maschinen zu Haus, und Virtualisierung wird als ein Raum und Zeit sparen.

Hier ist ein Diagramm:

![Bild](media/ProductionCheckpoints.png)

##Verwendungsmöglichkeiten für Virtualisierung

Virtualisierung ermöglicht es jedem leicht mehrere Testumgebungen bestehend aus viele Betriebssysteme, Software-Konfigurationen und Hardwarekonfigurationen zu pflegen.
Hyper-V bietet Virtualisierung auf Windows sowie einen einfachen Mechanismus, um schnell zwischen diesen Umgebungen ohne zusätzliche Hardwarekosten wechseln.

Hyper-V kann in vielerlei Hinsicht zum Beispiel verwendet werden:

*   Eine Testumgebung, bestehend aus mehreren virtuellen Maschinen kann auf einem einzigen Desktop oder Laptop-Computer erstellt werden.
    Sobald die Prüfung abgeschlossen ist, können diese virtuellen Computer exportiert und dann in einem anderen Hyper-V-System importiert.
*   Hyper-V können auf ihrem Computer Entwickler die Software auf mehreren Betriebssystemen testen.
    Beispielsweise wenn Sie eine Anwendung, die auf ein Linux-Betriebssystem, Windows 8 und Windows 7 getestet werden müssen haben, können mehrere virtuelle Maschinen auf Ihrem Entwicklungssystem, enthält jedes dieser Betriebssysteme erstellt werden.
*   Hyper-V können Sie um virtuelle Maschinen aus einer Hyper-V-Bereitstellung zu beheben.
    Sie können export eine virtuellen Maschine aus der Produktionsumgebung, öffnen Sie es auf Ihrem Desktop mit Hyper-V, Ihre erforderlichen Fehlerbehebung durchführen und dann wieder in der Produktionsumgebung zu exportieren.
*   Virtuellen Netzwerke verwenden, erstellen Sie eine Multi-machine Umgebung für Test, Entwicklung, Demonstration, die Auswirkungen auf das Produktionsnetzwerk sicher ist.
*   Enthusiasten können sie experimentieren mit anderen Betriebssystemen.
    Hyper-V macht es sehr leicht zu erziehen und verschiedene Betriebssysteme abzureißen.
*   Hyper-V können auf einem Laptop Sie für den Nachweis von älterer Versionen von Windows oder nicht-Windows-Betriebssystemen.

##System-Anforderungen

Hyper-V erfordert ein 64-Bit-System, Second Level Address Translation (Stab) verfügt. SLAT ist ein Feature in der aktuellen Generation von 64-Bit-Prozessoren von Intel & AMD vorhanden. Sie benötigen auch eine 64-Bit-Version von Windows 8 oder höher und mindestens 4 GB RAM. Hyper-V unterstützt die Erstellung von 32-Bit- und 64-Bit-Betriebssystemen in den virtuellen Maschinen.

Hyper-V dynamische Speicher ermöglicht Speicher benötigt von der VM zugewiesen und de dynamisch zugeteilt werden (Angabe eines Minimum und Maximum) und ungenutzten Speicher zwischen VMs zu teilen.
3 oder 4 VMs können auf eine Maschine mit 4 GB RAM ausgeführt, aber Sie benötigen mehr RAM für 5 oder mehr VMs.
Am anderen Ende des Spektrums können Sie auch große VMs mit 32 Prozessoren und 512 GB RAM, je nach physischer Hardware erstellen.

##Betriebssysteme, die in einer virtuellen Maschine ausgeführt werden können

Der Begriff "Gast" bezieht sich auf eine virtuelle Maschine und "Host" bezieht sich auf den Computer mit der virtuellen Maschine.
Hyper-V unter Windows unterstützt viele verschiedene Gast-Betriebssysteme, einschließlich der verschiedenen Versionen von Linux, FreeBSD und Windows.
Informationen darüber, welche Betriebssysteme als Gäste in Hyper-V unter Windows unterstützt werden, finden Sie unter [Unterstützte Windows-Gast-Betriebssysteme](supported_guest_os.md) und [Linux und FreeBSD virtuellen Maschinen auf Hyper-V](https://technet.microsoft.com/library/dn531030.aspx).

##Unterschiede zwischen Hyper-V auf Windows und Hyper-V unter Windows Server

Es gibt einige Funktionen, die anders in Hyper-V unter Windows funktionieren als Hyper-V unter Windows Server ausgeführt.
Dazu gehören die folgenden:

*   Das Speicher-Management-Modell unterscheidet sich für Hyper-V unter Windows.
    Hyper-V-Speicher erfolgt auf einem Server mit der Annahme, die ausschließlich der virtuellen Maschinen auf dem Server ausgeführt werden.
    In Hyper-V unter Windows ist Speicher verwaltet, mit der Maßgabe, dass die meisten Client-Rechner laufende Software zusätzlich zu laufenden virtuellen Maschinen sind.
    Beispielsweise könnte ein Entwickler Visual Studio als auch mehrere virtuelle Maschinen auf dem gleichen Computer ausgeführt werden.
*   SR-IOV auf einem 64-Bit-Gast funktioniert normal, aber 32-Bit nicht und wird nicht unterstützt.

###Windows Server-Features nicht Avilable in Windows Hyper-V

Es gibt einige Features, die in Hyper-V auf Server enthalten, die in Hyper-V unter Windows nicht enthalten sind.
Dazu gehören die folgenden:

*   Die Remote FX-Fähigkeit, GPUs zu virtualisieren 
*   Live-Migration virtueller Maschinen von einem Host zu einem anderen
*   Hyper-V Replica
*   Virtuelle Fibre-Channel
*   SR-IOV-Vernetzung
*   Gemeinsam genutzt. VHDX

> **Warnung**: Virtuelle Maschinen auf Hyper-V ausgeführt wird können nicht automatisch verarbeiten Verschieben von einem drahtgebundenen auf eine drahtlose Verbindung.
> Sie müssen die Netzwerkadaptereinstellungen für virtuelle Maschinen ändern manuell.
> 

##Einschränkungen

Mit Virtualisierung Einschränkungen haben.
Funktionen oder Anwendungen, die bestimmte Hardware abhängen funktioniert nicht gut in einer VM.
Z. B. Spiele oder Programme, die Verarbeitung mit GPUs benötigen (ohne Softwarefallbacks) funktioniert möglicherweise nicht gut.
Auch hätte für Anwendungen auf Sub 10ms Timer, wie Latenz-Sensitive hochpräzise Anwendungen wie live-Musik mixen apps, etc. Fragen in einer virtuellen Maschine ausgeführt.
Die Wurzel OS läuft auch auf dem Hyper-V Virtualisierungsschicht, aber es ist spezielle, auf die sie direkten Zugriff auf die Hardware.
Deshalb Anwendungen spezielle Hardware-Anforderungen weiterhin ungehindert in die Wurzel OS funktionieren aber Wartezeit-Sensitive, hochpräzisen apps hätte noch Probleme in der Wurzel OS laufen.

Zur Erinnerung musst du eine gültige Lizenz für alle Betriebssysteme können in den VMs-Test verwendeten.

##Nächster Schritt:

[Exemplarische Vorgehensweise Hyper-V auf Windows 10](..\quick_start\walkthrough.md)

Abreise [Was ist neu](whats_new.md) in Hyper-V auf Windows 10.


