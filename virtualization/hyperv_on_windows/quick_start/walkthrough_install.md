#Schritt 2: Installieren von Hyper-V unter Windows 10

Hyper-V kann mit installiert werden [Programme und Funktionen](#UsingProgramsandFeatures) oder [Windows Powershell](#UsingPowerShell).

##Programme und Funktionen

1.  Mit der rechten Maustaste die **Windows** Schaltfläche und klicken Sie dann auf **Programme und Funktionen**.
    
    !(media\programs_and_features.png)
2.  Klicken Sie auf **Aktivieren Sie oder Deaktivieren der Windows-features**.
3.  Wählen Sie **Hyper-V**, klicken Sie **Okay**
    
    !(media\hyper-v_feature_selected.png)
4.  Wenn die Installation abgeschlossen ist, müssen Sie den Computer neu starten.
    
    !(media\restart.png)

##Mithilfe von PowerShell

Weitere Informationen finden Sie in der PowerShell Hilfe [Aktivieren-WindowsOptionalFeature](https://technet.microsoft.com/library/hh852172.aspx).

1.  Klicken Sie auf die **Windows** Button und Suche nach **Windows PowerShell**.
2.  Mit einem Rechtsklick **Windows PowerShell** und klicken Sie dann auf **Als Administrator ausführen**.
3.  Geben Sie Folgendes an der Eingabeaufforderung den Windows Powerhshell, und drücken Sie dann die **Geben Sie** key:  
    ` PowerShell
    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
    `
4.  Wenn die Installation abgeschlossen ist, starten Sie den Computer.

##Woher weiß ich die Hyper-V richtig installiert?

Nach dem Neustart Ihres Computer-Start der Hyper-V-Manager-Tool.

1.  Klicken Sie auf die **Windows** Button und Typ **Hyper-V**.
2.  Klicken Sie auf **Hyper-V-Manager** in der Liste.
3.  Die Hyper-V-Manager-Anwendung sollte beginnen.

##Nächsten Schritt

[Schritt 3: Erstellen Sie einen virtuellen switch](walkthrough_virtual_switch.md)


