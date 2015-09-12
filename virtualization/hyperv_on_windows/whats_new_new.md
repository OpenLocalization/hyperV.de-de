#Was ist neu in Hyper-V auf Windows 10

In diesem Thema erläutert die neue und geänderte Funktionen in Hyper-V auf Windows 10 ®.

##Windows PowerShell-Direct

Es gibt jetzt eine einfache und zuverlässige Art des Host-Betriebssystems Windows PowerShell-Befehlen in einer virtuellen Maschine ausführen.
Es gibt keine Netzwerk- oder Firewall-Anforderungen oder spezielle Konfiguration.
Es funktioniert unabhängig von Ihrer remote-Management-Konfiguration.
Um es zu verwenden, müssen Sie Windows 10 oder Windows Server Technical Preview auf dem Host und das Gastbetriebssystem der virtuellen Maschine ausführen.

Um eine direkte PowerShell-Sitzung zu erstellen, verwenden Sie einen der folgenden Befehle:

``` PowerShell
Enter-PSSession -VMName VMName
Invoke-Command -VMName VMName -ScriptBlock { commands }


```

Today, Hyper-V administrators rely on two categories of tools for connecting to a virtual machine on their Hyper-V host:
- Remote management tools such as PowerShell or Remote Desktop
- Hyper-V Virtual Machine Connection (VM Connect)

Both of these technologies work well, but each have trade-offs as your Hyper-V deployment grows. VMConnect is reliable, but it can be hard to automate. Remote PowerShell is powerful, but can be difficult to setup and maintain. 

Windows PowerShell Direct provides a powerful scripting and automation experience with the simplicity of VMConnect. Because Windows PowerShell Direct runs between the host and virtual machine, there is no need for a network connection or to enable remote management. You do need guest credentials to log into the virtual machine.

#### Requirements
- You must be connected to a Windows 10 or Windows Server Technical Preview host with virtual machines that run Windows 10 or Windows Server Technical Preview as guests.
- You need to be logged in with Hyper-V Administrator credentials on the host.
- You need User credentials for the virtual machine.
- The virtual machine you want to connect to must be running and booted.


## Hot add and remove for network adapters and memory

You can now add or remove a Network Adapter while the virtual machine is running, without downtime. This works for generation 2 virtual machines running both Windows and Linux operating systems. 

You can also adjust the amount of memory assigned to a virtual machine while it's running, even if you haven’t enabled Dynamic Memory. This works for both generation 1 and generation 2 virtual machines.

## Production checkpoints

Production checkpoints allow you to easily create “point in time” images of a virtual machine, which can be restored later on in a way that is completely supported for all production workloads. This is achieved by using backup technology inside the guest to create the checkpoint, instead of using saved state technology. For production checkpoints, the Volume Snapshot Service (VSS) is used inside Windows virtual machines. Linux virtual machines flush their file system buffers to create a file system consistent checkpoint. If you want to create checkpoints using saved state technology, you can still choose to use standard checkpoints for your virtual machine. 


> **Important:** The default for new virtual machines will be to create production checkpoints with a fallback to standard checkpoints. 


## Hyper-V Manager improvements

- **Alternate credentials support** – You can now use a different set of credentials in Hyper-V manager when you connect to another Windows 10 Technical Preview remote host. You can also save these credentials so it's easier to log on later. 

- **Down-level management** - You can now use Hyper-V manager to manage more versions of Hyper-V. With Hyper-V manager in Windows 10 Technical Preview, you can manage computers running Hyper-V on Windows Server 2012, Windows 8, Windows Server 2012 R2 and Windows 8.1.

- **Updated management protocol** - Hyper-V manager has been updated to communicate with remote Hyper-V hosts using the WS-MAN protocol, which permits CredSSP, Kerberos or NTLM authentication. When you use CredSSP to connect to a remote Hyper-V host, it allows you to perform a live migration without first enabling constrained delegation in Active Directory. WS-MAN-based infrastructure also simplifies the configuration necessary to enable a host for remote management. WS-MAN connects over port 80, which is open by default.


## Connected Standby works 

When Hyper-V is enabled on a computer that uses the Always On/Always Connected (AOAC) power model, the Connected Standby power state is now available.

In Windows 8 and 8.1, Hyper-V caused computers that used the Always On/Always Connected (AOAC) power model (also known as InstantON) to never sleep. See this [KB article](
https://support.microsoft.com/en-us/kb/2973536) for a full discription.


## Linux secure boot 

More Linux operating systems, running on generation 2 virtual machines, can now boot with the secure boot option enabled.  Ubuntu 14.04 and later, and SUSE Linux Enterprise Server 12, are enabled for secure boot on hosts that run the Technical Preview. Before you boot the virtual machine for the first time, you must specify that the virtual machine should use the Microsoft UEFI Certificate Authority.  At an elevated Windows Powershell prompt, type:

    Set-VMFirmware vmname -SecureBootTemplate MicrosoftUEFICertificateAuthority

For more information on running Linux virtual machines on Hyper-V, see [Linux and FreeBSD Virtual Machines on Hyper-V](http://technet.microsoft.com/library/dn531030.aspx).


## Virtual Machine Configuration Version 

When you move or import a virtual machine to a host running Hyper-V on Windows 10 from host running Windows 8.1, the virtual machine’s configuration file isn't automatically upgraded. This allows the virtual machine to be moved back to a host running Windows 8.1. You won't have access to new virtual machine features until you manually update the virtual machine configuration version. 

The virtual machine configuration version represents what version of Hyper-V the virtual machine’s configuration, saved state, and snapshot files it's compatible with. Virtual machines with configuration version 5 are compatible with Windows 8.1 and can run on both Windows 8.1 and Windows 10. Virtual machines with configuration version 6 are compatible with Windows 10 and won't run on Windows 8.1.

#### How do I check the configuration version of the virtual machines running on Hyper-V? 

From an elevated command prompt, run the following command:

``` PowerShell
Get-VM * | Format-Table Name, Version

```


####Wie aktualisiere ich die Konfigurationsversion einer virtuellen Maschine?

Führen Sie aus einer Eingabeaufforderung von Windows PowerShell einen der folgenden Befehle aus:

``` PowerShell
Update-VmConfigurationVersion <vmname>


```

Or

``` PowerShell
Update-VmConfigurationVersion <vmobject>

```

** Wichtig: **

*   Nach einem upgrade die virtuellen Maschine Konfigurationsversion Verschieben nicht möglich die virtuelle Maschine auf einen Host, die ausgeführt Windows 8.1 wird.
*   Sie können die virtuelle Maschine Konfigurationsversion ab Version 6 auf Version 5 nicht herabsetzen.
*   Sie müssen den virtuellen Computer für die Konfiguration des virtuellen Computers aktualisieren deaktivieren.
*   Nach der Aktualisierung wird die virtuelle Maschine das Format der neuen Konfigurationsdatei verwendet.
    Weitere Informationen finden Sie unter neue virtuelle Maschine Konfigurations-Dateiformat.

##Neue virtuelle Maschine Konfigurations-Dateiformat

Virtuelle Maschinen haben jetzt ein neues Dateiformat für die Konfiguration zur Steigerung der Effizienz des Lesens und Schreibens von Daten zur Konfiguration der virtuellen Maschine vorgesehen ist.
Es ist auch entworfen, um das Potenzial für die Beschädigung von Daten zu reduzieren, wenn ein Speicher-Fehler vorliegt.
Die neuen Konfigurationsdateien verwenden die. VMCX Erweiterung für VM-Konfigurationsdaten und die. VMRS Endung Laufzeit Zustandsdaten.

> **Wichtig:** Die. VMCX Datei ist ein binäres Format.
> Direktes Bearbeiten der. VMCX oder. VMRS Datei wird nicht unterstützt.
> 

##Integrationsdienste geliefert über Windows Update

Aktuelles zu Integrationsservices für Windows-Gäste sind jetzt über Windows Update verteilt.

Integrationskomponenten (auch genannt Integrationsdienste) sind der Gruppe der synthetischen Treiber ermöglichen eine virtuelle Maschine mit dem Host-Betriebssystem zu kommunizieren.
Sie kontrollieren die Dienste von Zeit Sync bis hin zu Gast-Datei kopieren.
Wir haben gesprochen, Kunden über Integration-Komponenteninstallation und Update im vergangenen Jahr zu entdecken, dass sie während der Aktualisierung ein häufiger Problempunkt sind.

In der Vergangenheit kamen alle Versionen von Hyper-V mit neuen Integrationskomponenten.
Aktualisieren den Hyper-V-Host benötigt, aktualisieren die Integrationskomponenten in der virtuellen Maschinen als auch.
Die neue Integrationskomponenten wurden aufgenommen mit dem Hyper-V-Host, dann wurden sie in den virtuellen Maschinen mit vmguest.iso installiert.
Dieser Prozess benötigt einen Neustart der virtuellen Maschine und konnte nicht mit anderen Windows-Updates zusammengefasst werden.
Da der Hyper-V-Administrator bieten Ihnen vmguest.iso und der virtuellen Computer-Administrator installieren mussten musste, benötigt Integration-Komponentenupdate, der Hyper-V-Administrator haben die Administratoranmeldeinformationen in den virtuellen Maschinen--was nicht immer der Fall.

Maschinell bearbeitet in Windows 10 und künftig alle Integration, die Komponenten an virtuellen geliefert werden zusammen mit anderen wichtigen Updates über Windows Update.

Gibt es Updates heute für ausgeführten virtuellen Computer zur Verfügung:

*   Windows Server 2012
*   Windows Server 2008 R2
*   Windows 8
*   Windows 7

Der virtuellen Maschine muss mit Windows Update oder WSUS-Server verbunden werden.
Künftig werden Integration Komponentenupdates eine Kategorie-ID haben in dieser Version sind sie als KBs aufgeführt.

Lesen Sie mehr über wie wir Anwendbarkeit bestimmen, sehen dies [Blog-post](http://blogs.technet.com/b/virtualization/archive/2014/11/24/integration-components-how-we-determine-windows-update-applicability.aspx).

Finden Sie unter [Dieses blog](http://blogs.msdn.com/b/virtual_pc_guy/archive/2014/11/12/updating-integration-components-over-windows-update.aspx) Beitrag für eine ausführliche Anleitung zum Installieren von Integrationsservices.

> **Wichtig:** Das ISO-Abbild Datei vmguest.iso ist nicht mehr erforderlich, für die Aktualisierung von Integrationskomponenten.
> Es hat nicht mit Hyper-V auf Windows 10 aufgenommen.
> 

##Nächsten Schritt

[Spaziergang durch Hyper-V unter Windows 10](..\quick_start\walkthrough.md)


