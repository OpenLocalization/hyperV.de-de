ms.ContentId: 347fa279-d588-4094-90ec-8c2fc241f5b6
title: Manage Windows Server Containers with Docker

#Schnellstart: Windows Server Container und Docker

In diesem Artikel gehen durch die Grundlagen der Verwaltung von Windows Server-Container mit Docker.
Angesprochenen Themen umfassen Windows Server Container und Windows-Server-Container-Abbilder erstellen, Entfernen von Windows-Server-Container und Container-Bilder und schließlich Bereitstellen einer Anwendung in einem Windows-Server-Container.
Die gewonnenen Erkenntnisse in dieser exemplarischen Vorgehensweise sollten Sie beginnen, zu erforschen, Bereitstellung und Verwaltung von Windows-Server-Containers mit Docker aktivieren.

Haben Sie Fragen?
Auf Bitten der [Windows-Container-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers).

> **Hinweis:** Mit PowerShell erstellt Windows-Container können mit Docker und umgekehrt nicht derzeit verwaltet werden.
> Erstellen von Containern mit PowerShell finden Sie  [Schnellstart: Windows Server Container und PowerShell](./manage_powershell.md).
> < Br / >< Br / > Wenn Sie mehr wissen möchten [Lesen Sie die FAQ](../about/faq.md#WhydoIhavetopickbetweenDockerandPowerShellforWindowsServerContainermanagement).
> 

##Voraussetzungen

Durchführung dieser exemplarischen müssen die folgenden Elemente vorhanden sein.

*   Windows Server 2016 TP3 oder später mit der Container-Funktion von Windows Server konfiguriert.
    Wenn Sie das Handbuch für die Einrichtung abgeschlossen haben, ist dies die VM, die in Azure oder Hyper-V erstellt wurde.
*   Dieses System müssen an ein Netzwerk angeschlossen und auf das Internet zugreifen.

Benötigen Sie die Container-Funktion konfigurieren, finden Sie unter den folgenden Handbüchern: [Container-Setup in Azure](./azure_setup.md) oder [Container-Setup in Hyper-V](./container_setup.md).

##Grundlegende Behältermanagement mit Docker

In diesem erste Beispiel werden die Grundlagen der erstellen und Entfernen von Windows-Server-Container und Windows-Server-Container-Bilder mit Docker spazieren.

Spaziergang durch Protokoll in Ihrem Host-System von Windows Server Container zunächst sehen Sie eine Windows-Eingabeaufforderung.

!(media/cmd.png)

Eine PowerShell-Sitzung zu starten, durch Eingabe von `powershell`.
Sie wissen, dass Sie bei die Eingabeaufforderung aus Änderungen sind in einer PowerShell-Sitzung `C:\directory>` An `PS C:\directory>`.


```
C:\> powershell
Windows PowerShell
Copyright (C) 2015 Microsoft Corporation. All rights reserved.

PS C:\>

```


> Dieser Schnellstart wird auf Docker Befehle konzentriert, aber einige Schritte wie Verwaltung von Firewall-Regeln und das Kopieren von Dateien mit PowerShell-Befehle ausgeführt werden.
> In dieser exemplarischen Vorgehensweise in einer PowerShell-Sitzung durcharbeiten.
> 

Als Nächstes stellen Sie sicher, dass Ihr System eine gültige IP-Adresse verwendet hat. `ipconfig` und beachten Sie diese Adresse für die spätere Verwendung.


```
ipconfig

Ethernet adapter Ethernet 3:

   Connection-specific DNS Suffix  . :
   IPv6 Address. . . . . . . . . . . : 2601:600:8f01:84eb::e
   IPv6 Address. . . . . . . . . . . : 2601:600:8f01:84eb:a8c1:a3e:96b7:ffcb
   Link-local IPv6 Address . . . . . : fe80::a8c1:a3e:96b7:ffcb%5
   IPv4 Address. . . . . . . . . . . : 192.168.1.25

```

Wenn Sie von einer Azure-VM anstatt arbeiten `ipconfig` Du musst die öffentliche IP-Adresse der Azure Virtual Machine zu erhalten.

!(media/newazure9.png)

###Schritt 1 - erstellen Sie einen neuen Container

Bevor Sie einen Windows-Server-Container mit Docker erstellen, benötigen Sie den Namen oder die ID des Bildes Windows Server Container Exsisitng.

Bis alle Bilder geladen auf dem Container-Host verwenden, finden Sie unter der `docker images` Befehl.

``` PowerShell
docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
windowsservercore   latest              9eca9231f4d4        30 hours ago        9.613 GB
windowsservercore   10.0.10254.0        9eca9231f4d4        30 hours ago        9.613 GB


```

Now, use `docker run` To create a new Windows Server Container. This command as seen below will instruct the Docker daemon to create a new container named ‘dockerdemo’ from the image ‘windowsservercore’ and open an interactive (-it) console session (cmd) with the container.

``` PowerShell
docker run -it --name dockerdemo windowsservercore cmd

```

Wenn der Befehl abgeschlossen ist werden Sie in einer Konsolensitzung auf dem Container arbeiten.

Arbeiten in einem Container ist nahezu identisch mit der Arbeit mit Windows auf einer virtuellen oder physischen Maschine installiert.
Sie können Befehle wie ausführen `ipconfig` um die IP-Adresse des Containers zurückzugeben, `mkdir` Erstellen Sie ein neues Verzeichnis oder `powershell` um eine PowerShell-Sitzung zu starten.
Gehen Sie voran und nehmen Sie eine Änderung an dem Container wie das Erstellen einer Datei oder eines Ordners.
Der folgende Befehl erstellt z. B. eine Datei die Netzwerk Konfigurationsdaten über den Container enthält.

``` PowerShell
ipconfig > c:\ipconfig.txt


```

You can read the contents of the file to ensure the command completed successfully. Notice that the IP address contained in the text file matches that of the container.

``` PowerShell
type c:\ipconfig.txt

Ethernet adapter vEthernet (Virtual Switch-94a3e12ad262b3059e08edc4d48fca3c8390e38c3b219023d4a0a4951883e658-0):

   Connection-specific DNS Suffix  . : 
   Link-local IPv6 Address . . . . . : fe80::cc1f:742:4126:9530%18
   IPv4 Address. . . . . . . . . . . : 172.16.0.2
   Subnet Mask . . . . . . . . . . . : 255.240.0.0
   Default Gateway . . . . . . . . . : 172.16.0.1

```

Nun, da der Container geändert wurde, führen Sie folgendermaßen vor, um die Konsole Sitzung setzen Sie Sie wieder in der Konsolensitzung des Container-Hosts zu stoppen.

``` PowerShell
exit


```

Finally to see a list of containers on the container host use the `docker ps –a` command. Notice from the output that a container named 'dockerdemo' has been created.

``` PowerShell
docker ps -a

CONTAINER ID        IMAGE               COMMAND        CREATED             STATUS                     PORTS     NAMES
4f496dbb8048        windowsservercore   "cmd"          2 minutes ago       Exited (0) 2 minutes ago             dockerdemo

```


###Schritt 2 - Erstellen Sie ein neues Container-Bild

Ein Bild kann nun von dieser Container gemacht werden.
Dieses Bild verhält sich wie eine Momentaufnahme des Containers und kann viele Male erneut bereitgestellt werden.

Erstellen Sie ein neues Bild, führen Sie den folgenden.
Dieser Befehl weist die Docker-Engine erzeugt ein neues Bild mit dem Namen 'Newcontainerimage', die alle Änderungen an den 'Deckerdemo'-Container enthalten wird.

``` PowerShell
docker commit dockerdemo newcontainerimage


```

To see all images on the host, run `docker images`. Notice that a new image has been created with the name 'newcontainerimage'.

``` PowerShell
docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
newcontainerimage   latest              4f8ebcf0a334        2 minutes ago       9.613 GB
windowsservercore   latest              9eca9231f4d4        30 hours ago        9.613 GB
windowsservercore   10.0.10254.0        9eca9231f4d4        30 hours ago        9.613 GB

```


###Schritt 3 - Erstellen Sie neuen Container aus Bild

Nun, da Sie eine benutzerdefinierte Container-Bild haben, stellen Sie einen neuen Container mit dem Namen 'Newcontainer' aus 'Newcontainerimage' und öffnen Sie eine interaktive Shell-Sitzung mit dem Container.

``` PowerShell
docker run –it --name newcontainer newcontainerimage cmd


```

Take a look at the c:\ drive of this new container and notice that the ipconfig.txt file is present.

Exit the newly created container to return to the container hosts console session.

``` PowerShell
exit

```

Diese Übung hat gezeigt, dass ein Bild aus einem modifizierten Container alle Änderungen enthält.
Während hier im Beispiel wird eine einfache Dateiänderung war, würde dasselbe gelten, wenn man Software in den Container, z. B. einen Webserver zu installieren.
Mit diesen Methoden benutzerdefinierte Abbilder erstellt werden, die Anwendung bereit Container bereitstellen wird.

###Schritt 4 - Container entfernen und Bilder

Notwendig, um einen Container zu entfernen, nachdem es nicht mehr ist Nutzung der `docker rm` Befehl.
Der folgende Befehl entfernt die Container-Name 'Newcontainer'.

``` PowerShell
docker rm newcontainer


```
To remove container images when they are no longer needed use the `docker rmi` command. You cannot remove an image if it is referenced by an existing container.

The following command removes the container image named 'newcontainerimage'.
``` PowerShell
docker rmi newcontainerimage

Untagged: newcontainerimage:latest
Deleted: 4f8ebcf0a334601e75070a92294d993b0f182abb6f4c88740c75b05093e6acff

```


##Host ein Web-Server in einem Container

Das nächste Beispiel zeigen einen praktischeren Anwendungsfall für Windows-Server-Container.
In dieser Übung enthaltenen Schritte führen Sie durch die Erstellung eines Web Server Container-Image, die verwendet werden kann, für die Bereitstellung von Webanwendungen, die innerhalb einer Windows-Server-Container gehostet.

###Schritt 1 - Download-Web-Server-Software

Vor dem Erstellen eines Container-Bild im Web benötigen Serversoftware heruntergeladen und auf dem Container-Host inszeniert werden.
Wir werden die Nginx für Windows-Software für dieses Beispiel verwenden.
**Hinweis** Dieser Schritt benötigen die Container-Host mit dem Internet verbunden sein.
Wenn dieser Schritt eine Konnektivität oder Name Auflösung Fehlerüberprüfung der Netzwerk-Konfiguration des Hosts Container produziert.

Führen Sie den folgenden Befehl auf dem Container-Host die Verzeichnisstruktur zu erstellen, die in diesem Beispiel verwendet wird.

``` PowerShell
mkdir c:\build\nginx\source


```

Run this command on the container host to download the nginx software to 'c:\nginx-1.9.3.zip'.

``` PowerShell
wget -uri 'http://nginx.org/download/nginx-1.9.3.zip' -OutFile "c:\nginx-1.9.3.zip"

```

Schließlich wird der folgende Befehl die Nginx-Software zum 'C:\build\nginx\source' entpacken.

``` PowerShell
Expand-Archive -Path C:\nginx-1.9.3.zip -DestinationPath C:\build\nginx\source -Force


```

### Step 2 - Create Web Server Image
In the previous example, you manually created, updated and captured a container image. This example will demonstrate an automated method for creating container images using a Dockerfile. Dockerfiles contain instructions that the Docker engine uses to build and modify a container, and then commit the container to a container image. 
For more information on dockerfiles, see [Dockerfile reference](https://docs.docker.com/reference/builder/).

Use the following command to create an empty dockerfile.

``` PowerShell
new-item -Type File c:\build\nginx\dockerfile

```

Öffnen Sie die Dockerfile mit dem Notepad.


```
notepad.exe c:\build\nginx\dockerfile

```

Kopieren Sie und fügen Sie den folgenden Text in den Editor, speichern Sie die Datei und schließen Editor.

``` PowerShell
FROM windowsservercore
LABEL Description="nginx For Windows" Vendor="nginx" Version="1.9.3"
ADD source /nginx


```

At this point the dockerfile will be in 'c:\build\nginx' and the nginx software extracted to 'c:\build\nginx\source'. 
You are now ready to build the web server container image based on the instructions in the dockerfile. To do this, run the following command on the container host.

``` PowerShell
docker build -t nginx_windows C:\build\nginx

```

Dieser Befehl weist die Hafenarbeiter-Engine, die am Dockerfile zu verwenden `C:\build\nginx` Erstellen Sie ein Bild mit dem Namen 'Nginx_windows'.

Die Ausgabe wird so aussehen:

!(media/docker1.png)

Wenn abgeschlossen, schauen Sie sich die Bilder auf dem Rechner mit der `docker images` Befehl.
Es erscheint ein neues Bild mit dem Namen 'Nginx_windows'.
``` PowerShell
docker images

REPOSITORY-TAG-ID ERSTELLT VIRTUELLE BILDGRÖßE

nginx_windows       latest              d792268338d0        5 seconds ago       9.613 GB
windowsservercore   10.0.10254.0        9eca9231f4d4        35 hours ago        9.613 GB
windowsservercore   latest              9eca9231f4d4        35 hours ago        9.613 GB


```

### Step 3 – Configure Networking for Container Application
Because you will be hosting a website inside of a container a few networking related configurations need to be made. First a firewall rule needs to be created on the container host that will allow access to the website. In this example we will be accessing the site through port 80. Run the following script to create this firewall rule. This script can be copied into the VM. 

``` powershell
if (!(Get-NetFirewallRule | where {$_.Name -eq "TCP80"})) {
    New-NetFirewallRule -Name "TCP80" -DisplayName "HTTP on TCP/80" -Protocol tcp -LocalPort 80 -Action Allow -Enabled True
}

```

Als nächstes Wenn Sie von Azure arbeiten und nicht bereits einen virtuellen Computer-Endpunkt erstellt haben musst du jetzt erstellen.
Weitere Informationen über Azure VM Endpunkte finden Sie in diesem Artikel: [Einrichten von Azure-VM-Endpunkte](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-set-up-endpoints/).

###Schritt 4 - Web-Server bereit Container bereitstellen

Stellen Sie einen Windows Server-Container auf führen Sie den folgenden Befehl 'Nginx_windows'-Container basiert.
Dies erstellt einen neuen Container mit dem Namen 'Nginxcontainer' und starten eine Konsolensitzung auf dem Container.
Der 80:80 – p als Bestandteil dieser Befehl erstellt eine Portzuordnung zwischen Port 80 auf dem Host an Port 80 für den Container.

``` powershell
docker run -it --name nginxcontainer -p 80:80 nginx_windows cmd


```
Once working inside the container, the nginx web server can be started and web content staged. To start the nginx web server, change to the nginx installation directory.

``` powershell
cd c:\nginx\nginx-1.9.3

```

Starten Sie den Webserver Nginx.
``` powershell
start nginx


```
### Step 5 – Access the Container Hosted Website

With the web server container created, you can now checkout the application hosted in the container. To do so, open up a browser on different machine and enter `http://containerhost-ipaddress`. Notice here that you will be browsing to the IP Address of the Container Host and not the container itself. If you are working from an Azure Virtual Machine this will be the public IP address or Cloud Service name. 

If everything has been correctly configured, you will see the nginx welcome page.

![](media/nginx.png)

At this point, feel free to update the website. Copy in your own sample website, or run the following command in the container to replace the nginx welcome page with a ‘Hello World’ web page.

```powershell
powershell wget -uri 'https://raw.githubusercontent.com/Microsoft/Virtualization-Documentation/master/doc-site/virtualization/windowscontainers/quick_start/SampleFiles/index.html' -OutFile "C:\nginx\nginx-1.9.3\html\index.html"

```

Nachdem die Website aktualisiert wurde, wechseln Sie zurück in `http://containerhost-ipaddress`.

!(media/hello.png)

> **Hinweis:** Wenn Sie wollen, ändern Sie die Docker Daemon-Einstellungen (z.B. sein, daß den Port zu ändern, es hört auf, zu einem Container eine Remoteverbindung herstellen), musst du die Datei "C:\ProgramData\docker\runDockerDaemon.cmd" in den Container zu bearbeiten und dann Sie zum Neustarten des Dienstes mit PowerShell müssen, Verwendung `Restart-Service docker`.
> 

##Video-Anleitung

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Deploying-and-Managing-Windows-Server-Containers-with-Docker/player" width="800" height="450" allowFullScreen="true" frameBorder="0" scrolling="no" caps_internal_Id="53b62060-d5e0-47be-ad29-350eb19f5830" />

##Die nächsten Schritte

Nun, da Sie Container eingerichtet und eine Einführung in die Werkzeuge haben, gehen Sie Ihrer eigenen Containerbetrieb Anwendungen zu bauen.

Denken Sie daran, dies ist ein **Vorschau** Es gibt einige Bugs, und wir haben eine Menge Arbeit.
[Diese Seite](../about/work_in_progress.md) enthält viele unserer bekannten Fragen.

Beachten Sie, dass gibt es einige bekannte Docker-Befehle [funktionieren nicht](../about/work_in_progress.md#DockermanagementDockercommandsthatdontworkwithWindowsServerContainers) und einige, die nur [teilweise arbeiten](../about/work_in_progress.md#DockermanagementDockercommandsthatpartiallyworkwithWindowsServerContainers)

Wir sind auch die Überwachung der [Foren](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers) sehr eng.

Es gibt auch vorgefertigte Proben auf [GitHub](https://github.com/Microsoft/Virtualization-Documentation/tree/master/windows-server-container-samples).

-----------------------------------
[Back to Container Home](../containers_welcome.md)   
[Known Issues for Current Release](../about/work_in_progress.md)


