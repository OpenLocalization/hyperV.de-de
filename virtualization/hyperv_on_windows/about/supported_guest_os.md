#Unterstützte Windows-Gäste

Dieser Artikel listet die Windows-Betriebssysteme als Gäste in Hyper-V unter Windows unterstützt, sowie Informationen zu Integrationsservices bietet.

> Neue Windows-10 führt als ein Gast-Betriebssystem auf Windows 8.1 und Windows Server 2012 R2 Hyper-V-Hosts.
> 

##Was bedeutet unterstützt?

Unterstützung bedeutet, dass Microsoft diese Host/Gast-Kombinationen getestet hat.
Probleme mit diesen Kombinationen können die Aufmerksamkeit von Product Support Services erhalten.

Microsoft bietet Unterstützung für Gastbetriebssysteme auf folgende Weise:

*   Probleme in Microsoft-Betriebssystemen gefunden und unterstützen bei der Integration, die Dienste von Microsoft unterstützt werden.
*   Für Probleme in anderen Betriebssystemen, die vom Hersteller Betriebssystems auf Hyper-V ausgeführt beglaubigt sind, wird die Unterstützung durch den Hersteller bereitgestellt.
*   Für Fragen, die in anderen Betriebssystemen gefunden sendet Microsoft das Problem auf die heterogenen Supportcommunity, [TSANet](http://www.tsanet.org/).

##Was sind Integrationsdienste und warum sind sie wichtig?

Hyper-V enthält Integrationsservices für unterstützte Gastbetriebssysteme.
Integrationsdienste verbessern die Interaktion zwischen dem Host-System und der virtuellen Maschine.

Einige Betriebssysteme (einschließlich verschiedene Versionen von Windows) haben die Integrationsservices integriert, während andere Integrationsdienste über Windows Update zur Verfügung stellen.

##Unterstützte Gast-Betriebssysteme der Windows Server

10-Windows-Hyper-V-Hosts:

| Gast-Betriebssystem| Maximale Anzahl der virtuellen Prozessoren| Integrationsservices| Hinweise| |
| -----                                | -----                                     | -----                     | -----     | ----- |
| Windows Server technische Vorschau| 64| Built-in| | | |
| Windows Server 2012 R2| 64| Built-in| | | |
| Windows Server 2012| 64| Built-in| | | |
| Windows Server 2008 R2 mit Servicepack 1 (SP 1)| 64| Installieren Sie die Integrationsservices, nachdem Sie das Betriebssystem des virtuellen Computers eingerichtet.| Datacenter, Enterprise, Standard und Web-Editionen.| |
| Windows Server 2008 mit Servicepack 2 (SP 2)| 4| Installieren Sie die Integrationsservices, nachdem Sie das Betriebssystem des virtuellen Computers eingerichtet.| Datacenter, Enterprise, Standard und Web-Editionen (32-Bit und 64-Bit).| |
| Windows Home Server 2011| 4| Installieren Sie die Integrationsservices, nachdem Sie das Betriebssystem des virtuellen Computers eingerichtet.| |
| Windows Small Business Server 2011| Essentials-Edition - 2, Standard Edition - 4| Installieren Sie die Integrationsservices, nachdem Sie das Betriebssystem des virtuellen Computers eingerichtet.| Essentials und Standard-Editionen.| |

##Unterstützte Windows-Gastbetriebssystemen

10-Windows-Hyper-V-Hosts:

| Gast-Betriebssystem| Maximale Anzahl der virtuellen Prozessoren| Integrationsservice| Hinweise| |
| ----- | ----- | ----- | ----- | ----- |
| Windows 10| 32| Built-in| | |
| 8.1 für Windows| 32| Built-in| | |
| Windows 8| 32| Die Integrationsservices zu aktualisieren, nachdem Sie das Betriebssystem auf dem virtuellen Computer einrichten.| | |
| Windows 7 mit Servicepack 1 (SP 1)| 4| Die Integrationsservices zu aktualisieren, nachdem Sie das Betriebssystem auf dem virtuellen Computer einrichten.| Ultimate, Enterprise und Professional Edition (32-Bit und 64-Bit).| |
| Windows 7| 4| Die Integrationsservices zu aktualisieren, nachdem Sie das Betriebssystem auf dem virtuellen Computer einrichten.| Ultimate, Enterprise und Professional Edition (32-Bit und 64-Bit).| |
| Windows Vista mit Servicepack 2 (SP2)| 2| Installieren Sie die Integrationsservices, nachdem Sie das Betriebssystem des virtuellen Computers eingerichtet.| Business, Enterprise und Ultimate, einschließlich N und KN-Editionen.| |
 Windows-10 ist ein Gast-Betriebssystem auf Windows 8.1 und Windows Server 2012 R2 Hyper-V-Hosts.

##Linux und BSD gratis

10-Windows-Hyper-V-Hosts:

| Gast-Betriebssystem| |
| -----|------|
| [CentOS und RedHat Enterprise Linux ](https://technet.microsoft.com/library/dn531026.aspx)| |
| [Debian virtuellen Maschinen auf Hyper-V](https://technet.microsoft.com/library/dn614985.aspx)| |
| [SUSE](https://technet.microsoft.com/en-us/library/dn531027.aspx)| |
| [Oracle Linux](https://technet.microsoft.com/en-us/library/dn609828.aspx)| |
| [Ubuntu](https://technet.microsoft.com/en-us/library/dn531029.aspx)| |
| [FreeBSD](https://technet.microsoft.com/library/dn848318.aspx)| |
Gibt es Einschränkungen um spezielle Kernel-Versionen.
Weitere Informationen, einschließlich Supportinformationen zu früheren Versionen von Hyper-V finden Sie unter [Linux und FreeBSD virtuellen Maschinen auf Hyper-V](https://technet.microsoft.com/library/dn531030.aspx).


