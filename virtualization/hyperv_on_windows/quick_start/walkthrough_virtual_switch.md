#Schritt 3: Erstellen Sie einen virtuellen switch

Ein virtueller Switch können Sie eine Netzwerkverbindung für den virtuellen Computer erstellen.
Sie werden genau wie die Netzwerkkarte (NIC) auf dem physischen Computer verwendet.

In diesem Beispiel wollen wir einen externen Schalter zu erstellen.
Der externe Schalter können Ihre virtuelle Maschine auf den Host zugreifen Netzwerkadapter des Computers.
Wenn Ihr Host-Computer mit dem Internet verbunden ist, wird auch Ihre virtuelle Maschine sein.

Wir werden auch die Umstellung auf dem Host diese Netzwerkkarte Teilen ermöglichen festlegen.
Dies macht es also sowohl die virtuellen Maschinen und der Host im gleiche Netzwerk verwenden kann.


1.  Klicken Sie im Hyper-V-manager **Virtual Switch-Manager**.
    
    !(media/virtual_switch_manager1.png)
2.  Wählen Sie **Neue virtuelle Netzwerk-switch**.
    
    !(media/new_switch.png)
3.  Wählen Sie **Externe** und **Erstellen von virtuellen Switch**.
    
    !(media/new_switch_createbutton.png)
4.  Unter **Name**, Typ **Externe**.
5.  Unter **Externes Netzwerk**, wählen Sie den richtigen Netzwerk-Adapter (es wird wahrscheinlich nur eine Option sein).
6.  Wählen Sie **Verwaltungsbetriebssystem diese Netzwerkkarte Teilen zu ermöglichen** und klicken Sie auf **Okay**.
    
    !(media/share_nic.png)
7.  Sie erhalten eine Warnung, dass Ihr Netzwerk trennen könnte, während der virtuelle Switch erstellt wird.
    Klicken Sie einfach **Ja**.
    Ihr Netzwerk wird für kurze Zeit nicht erreichbar.
    
    !(media/network_warning.png)

##Nächster Schritt:

[Schritt 4: Erstellen einer virtuellen Windows-Maschine aus einer .iso-Datei](walkthrough_create_vm.md)


