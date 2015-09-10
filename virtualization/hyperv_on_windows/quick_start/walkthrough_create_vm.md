ms.ContentId: 3C63F9A8-30E4-40F4-BC7B-A001C1E90779
title: Step 4: Create a Windows virtual machine from an .iso file

#Step 4: Create a Windows virtual machine from an .iso file

For this step, if you already have a .iso file for a supported 64-bit operating system, you can use that.
If not, you can download the .iso for [Windows 8.1 Enterprise](http://www.microsoft.com/en-us/evalcenter/evaluate-windows-8-1-enterprise) and choose the 64-bit edition.

1.  In Hyper-V Manager, click on the **Action** menu > **New** > **Virtual machine**.
2.  In the virtual machine wizard, make the following choices:
    
    <table>
      <tr>
        <th caps_internal_Id="17378e71-09a5-4e57-8347-7701e3ddcf61">Page</th>
        <th caps_internal_Id="96f4bd16-5e7f-496b-9f85-ece4cd068c62">Entry</th>
      </tr>
      <tr>
        <td caps_internal_Id="9dc25c31-8288-434e-b833-902d868b140b">Name:</td>
        <td>Type in <b caps_internal_Id="7207cfe1-d8d2-4b6f-86dc-47b1bf7ec0b2">Windows Walkthrough VM</b></td>
      </tr>
      <tr>
        <td caps_internal_Id="cae6fb03-2358-4664-bb77-5d62d57dd476">Generation:</td>
        <td>
          <b caps_internal_Id="08c8c2ca-a20e-4d26-b364-36c5c47ee9d1">Generation 2</b>
        </td>
      </tr>
      <tr>
        <td caps_internal_Id="c37b9e94-754b-42a0-891f-89e2e4b3b863">Startup Memory:</td>
        <td>
          <b caps_internal_Id="b3f50451-eab4-477a-8226-5b0668db8cb6">1024</b> and leave dynamic memory selected</td>
      </tr>
      <tr>
        <td caps_internal_Id="0da193c3-96c6-4473-8de2-8d4c64d954fa">Configure Networking:</td>
        <td>
          <b caps_internal_Id="f3f43ee5-c114-4bdb-95d6-e8038779833a">External</b> (this is the virtual switch you created in Step 3)</td>
      </tr>
      <tr>
        <td caps_internal_Id="a5028acd-c82a-46bf-927f-b96eb0661fb8">Connect virtual hard disk:</td>
        <td>
          <b caps_internal_Id="2734a738-99b6-40e5-9d2d-b6207f538cc3">Create a virtual hard disk</b> (keep the other default values) </td>
      </tr>
      <tr>
        <td caps_internal_Id="77803214-a0a5-4e12-b703-df1b4327bd71">Installation Options:</td>
        <td>
          <b caps_internal_Id="f8f3c9e7-82d6-406a-9948-5498bbb9dd5f">Install an operating system from a bootable CD/DVD-ROM</b>. Under <b caps_internal_Id="3d903005-fff3-4251-a433-3a2b17dccbf2">Media</b>, select <b caps_internal_Id="65bb6e58-8230-413c-8bdf-f8a6c7df070e">Image file (iso)</b> and then click <b caps_internal_Id="7be0009c-5ab0-4951-8bcd-62b5ccdad654">Browse</b> to point to the .iso file.</td>
      </tr>
    </table>
3.  When everything looks right, click **Finish**.

> **Note:** If you only have 32-bit version of Windows, you need to choose Generation 1 in the **Generation** section of the wizard.
> Generation 2 VMs only support 64-bit operating systems.
> 

##Next Step:

[Step 5: Connect to the virtual machine and finish the installation](walkthrough_vmconnect.md)


