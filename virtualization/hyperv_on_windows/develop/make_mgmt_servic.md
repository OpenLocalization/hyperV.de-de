#Machen Sie einen neuen Management-service

Dieses Dokument stellt VM-Diensten, das auf Hyper-V-Steckdosen und wie man mit ihnen beginnen.

!(../media/2.png)

##Was ist ein VM-Service?

VM sind Dienste, die die Hyper-V-Hosts und virtuelle Maschinen auf dem Host zu erstrecken.

Hyper-V jetzt (Windows 10 and Server 2016 +) bietet eine nicht-Netz-Verbindung, die Sie Dienstleistungen umfassen die Host/virtuelle Maschine-Grenze unter Beibehaltung der grundsätzlichen Anforderungen der Hyper-V um Mieter/Hoster Isolation, Kontrolle, erstellen kann und diagnostizierbar.

Hyper-V bietet weiterhin einen Basissatz von in-Box-Service (Integrationsservices) für Grundlagen (z. B. Zeit Sync) und für allgemeine Anfragen, die wir erhalten, aber jetzt kann jeder schreiben und einen VM-Dienst bereitstellen, wie gebraucht.

PowerShell-Direct ist ein in-Box-Beispiel eines VM-Dienstes.

##Was ist eine Hyper-V-Steckdose?

Hyper-V-Steckdosen sind wie TCP Sockets mit keine Abhängigkeit von Vernetzung.
Mithilfe von Hyper-V-Sockets, Dienste können unabhängig von der Netzwerkstapel ausgeführt und alle Datenfluss bleibt an Host-Speicher.

##System-Anforderungen

**Unterstützte Host-Betriebssystem**

*   Windows 10
*   Windows Server technische Vorschau 3
*   Zukünftige Versionen (Server-2016 +)

**Unterstützte Gastbetriebssystem**

*   Windows 10
*   Windows Server technische Vorschau 3
*   Zukünftige Versionen (Server-2016 +)
*   Linux

##Möglichkeiten und Grenzen

Kernel mode or user mode  
Data stream only    
No block memory so not the best for backup/video  

##Erste Schritte

Dieses Handbuch setzt voraus, dass Sie mit Socket-Programmierung in C/C++ vertraut bist.

###Schritt 1: Registrieren Sie Ihren Dienst auf dem Hyper-V-host

Um einen benutzerdefinierten Dienst integriert mit Hyper-V zu verwenden, muss der neue Dienst mit dem Hyper-V-Host-Registrierung registriert werden.

Mit der Registrierung des Diensts in der Registrierung erhalten Sie:

*   WMI-Management für aktivieren, deaktivieren und Auflisten der verfügbaren Dienste
*   Auf der Liste der Dienste mit virtuellen Maschinen direkt kommunizieren darf.

** Registrierung Speicherort und Informationen **


```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Virtualization\VirtualDevices\6C09BB55-D683-4DA0-8931-C9BF705F6480\GuestCommunicationServices\

```

Position in der Registrierung sehen Sie mehrere GUIDS.
Das sind unsere Dienstleistungen in-Box.

Informationen in der Registrierung pro Dienst:

*   `Service GUID`
    
    *   `ElementName (REG_SZ)` --Dies ist der Dienst-Anzeigename

Um Ihren eigenen Service zu registrieren, erstellen Sie einen neuen Registrierungsschlüssel, die mit Ihren eigenen GUID und angezeigter Name.

Der Registrierungseintrag wird so aussehen:


```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Virtualization\GuestCommunicationServices\
    999E53D4-3D5C-4C3E-8779-BED06EC056E1\
        ElementName REG_SZ  VM Session Service
    YourGUID\
        ElementName REG_SZ  Your Service Friendly Name

```


> ** Tipp: **  To generate a GUID in PowerShell and copy it to the clipboard, run:  
> ``` PowerShell
> [System.Guid]::NewGuid().ToString() | clip.exe
> 


```

<!-- How do customers know this worked -->

### Step 2 - Create a simple host-side service



### Step 3 - Create a simple guest-side service

## More information about AF_HYPERV
Since Hyper-V sockets do not depend on a networking stack, TCP/IP, DNS, etc. the socket end point needed a non-IP, not hostname, format that still describes the connection.  In lieu of an IP or hostname, AF_HYPERV endpoints rely heavily on two GUIDS:  
* VM ID – this is the unique ID assigned per VM.  A VM’s ID can be found using the following PowerShell snippet.
```PowerShell
(Get-VM -Name vmname).Id

```

*   Service ID-GUID, unter denen der Dienst in der Hyper-V-Host-Registrierung registriert ist.
    Finden Sie unter [Registrieren einen neuen Service](#GettingStarted).

For connections from a service on the host to the service on a VM:  
VMID and Service ID
For connections from a service on a VM to the service on the host:  
Zero GUID and Service ID

##Unterstützten Socket-Befehle

Socket()
Bind()
Connect ()
Send()
Listen()
Accept()


