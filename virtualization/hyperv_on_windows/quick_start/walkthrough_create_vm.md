#Schritt 4: Erstellen einer virtuellen Windows-Maschine aus einer .iso-Datei

Für diesen Schritt haben Sie bereits eine .iso-Datei für eine unterstützte 64-Bit-Betriebssystem können, das Sie.
Wenn dies nicht der Fall sein, können Sie die .iso für herunterladen [8.1 Windows Enterprise](http://www.microsoft.com/en-us/evalcenter/evaluate-windows-8-1-enterprise) und wählen Sie die 64-Bit-Edition.

1.  In Hyper-V-Manager, klicken Sie auf die **Aktion** Menü > **Neu** > **Virtuelle Maschine**.
2.  Stellen Sie im virtuellen Computer-Assistenten die folgenden Auswahlmöglichkeiten:
    
    <table>
      <tr>
        <th caps_internal_Id="ccf51af6-281f-4b63-ad5c-fa388626f192">Page</th>
        <th caps_internal_Id="62587968-25f5-4744-8c04-1dbf454b1873">Entry</th>
      </tr>
      <tr>
        <td caps_internal_Id="09f573ce-f477-4f2b-935f-d1b2ff399ae0">Name:</td>
        <td>Type in <b caps_internal_Id="dbad4087-1e32-42b7-8923-664c91af67d8">Windows Walkthrough VM</b></td>
      </tr>
      <tr>
        <td caps_internal_Id="2c1fb44c-cd79-4cb4-94e4-b753ea763f2b">Generation:</td>
        <td>
          <b caps_internal_Id="d622cbcf-91bf-48c5-ba6f-079e22c21b44">Generation 2</b>
        </td>
      </tr>
      <tr>
        <td caps_internal_Id="fd540478-f84b-4e2e-810e-7bd5fda7cea4">Startup Memory:</td>
        <td>
          <b caps_internal_Id="e124a5a3-6a46-4331-ac3a-0be34ff02c96">1024</b> and leave dynamic memory selected</td>
      </tr>
      <tr>
        <td caps_internal_Id="12357368-5093-4fe9-bf22-ee93ca5e49c0">Configure Networking:</td>
        <td>
          <b caps_internal_Id="1370e443-2fd9-4baa-b69d-849512ab7c86">External</b> (this is the virtual switch you created in Step 3)</td>
      </tr>
      <tr>
        <td caps_internal_Id="9ac9e23b-6518-49b0-b04d-688d3bdb6f75">Connect virtual hard disk:</td>
        <td>
          <b caps_internal_Id="6b73792b-8c64-4835-9fe2-02c3f0667f5d">Create a virtual hard disk</b> (keep the other default values) </td>
      </tr>
      <tr>
        <td caps_internal_Id="0300269c-ca01-4734-84fc-4a45c84da81c">Installation Options:</td>
        <td>
          <b caps_internal_Id="1bd6e0f6-ca10-403d-984d-e735796137cf">Install an operating system from a bootable CD/DVD-ROM</b>. Under <b caps_internal_Id="aebc7ac8-72ed-42a9-a64e-75ef0728000c">Media</b>, select <b caps_internal_Id="f64cd4b0-afa6-44bb-a830-048bddb8e00c">Image file (iso)</b> and then click <b caps_internal_Id="37d6ac07-cb5d-4619-bd75-95fe9e8b24f8">Browse</b> to point to the .iso file.</td>
      </tr>
    </table>
3.  Wenn alles gut aussieht, klicken Sie **Fertig stellen**.

> **Hinweis:** Wenn Sie nur 32-Bit-Version von Windows haben, musst du Generation 1 in wählen die **Erstellung der** Abschnitt des Assistenten.
> Generation 2 VMs nur unterstützen 64-Bit-Betriebssysteme.
> 

##Nächster Schritt:

[Schritt 5: Verbinden Sie mit dem virtuellen Computer und schließen die Installation ab](walkthrough_vmconnect.md)


