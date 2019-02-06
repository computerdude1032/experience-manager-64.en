---
title: Integrating AEM 3D with Autodesk 3ds Max
seo-title: Integrating AEM 3D with AutoDesk 3ds Max
description: You can optionally integrate AEM 3D with Autodesk 3ds Max software to enable support for native 3ds Max files (.MAX). Rendering by way of 3ds Max is not supported at this time.
seo-description: You can optionally integrate AEM 3D with Autodesk 3ds Max software to enable support for native 3ds Max files (.MAX). Rendering by way of 3ds Max is not supported at this time.
uuid: b7e00cc5-1039-46a4-a26f-de7cc87b9431
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
content-type: reference
topic-tags: 3D
discoiquuid: 68112bf6-edaa-4ff2-84b7-dc3231105c47
index: y
internal: n
snippet: y
---

# Integrating AEM 3D with Autodesk 3ds Max{#integrating-aem-d-with-autodesk-ds-max}

>[!NOTE]
>
>This task is optional and pertains to Windows only.

You can optionally integrate AEM 3D with Autodesk 3ds Max software to enable support for native 3ds Max files (.MAX). Rendering by way of 3ds Max is not supported at this time.

See [Advanced configuration settings](../../assets/using/advanced-config-3d.md).

See also [Integrating AEM 3D with AutoDesk Maya](../../assets/using/integrate-maya-with-3d.md).

To integrate AEM 3D with Autodesk 3ds Max:

1. Install Autodesk 3ds Max software on the same servers where AEM Author nodes are installed.

   Following installation, verify that you can open and use Maya and that there are no licensing issues.

   >[!NOTE]
   >
   >To avoid access denied issues, install 3ds Max using the same admin user account as AEM.

1. In 3ds Max, click **Customize **&gt; **Plug-in Manager**.

   Locate **`FBXMAX.DLU`** and verify that its **Status** is "loaded".

   Close the Plug-In Manager dialog box and 3ds Max.

1. Update the conversion script.

   AEM uses a command line script to invoke the 3ds Max command line utility **`3dsmaxcmd.exe`**. You must edit this script if you installed a version other than 3ds Max 2016, or if you installed 3ds Max to a non-standard location, or if you installed AEM on a different partition or drive.

    1. Open CRXDE Lite and navigate to **/libs/settings/dam/v3D/scripts/max**.
    1. Double-click `export-fbx.bat` to open it.
    1. Edit the first line of the script as needed to reflect the location of the `3dsmaxcmd.exe` utility. For example, if 3ds Max 2017 is used and AEM is installed on a different disk drive:

   ![](assets/image2018-6-22_13-35-8.png)

1. Near the upper-left corner of the CRXDE Lite page, tap or click **Save All**.

   Near the upper-left corner of the CRXDE Lite page, tap or click **Save All**.

1. Remove the working folder (only necessary if a previous attempt was made to ingest a .MAX file).

    1. In CRXDE Lite, navigate to `/libs/settings/dam/v3D/Paths/maxWorkPath`. By default, the value of this setting is `./MaxWork`, which is relative to the AEM install root folder.
    
    1. Log onto the server itself and use **File Explorer** to navigate to the AEM install root folder.
    1. Delete the **MaxWork** folder--including its entire contents--if it exists.  
       The folder is re-created automatically the next time a .MAX file is ingested.

1. Enable 3ds Max for ingestion by doing the following:

    1. In CRXDE Lite, navigate to `/libs/settings/dam/v3D/assetTypes/max` and set the **Enabled** property to true:

   ![](assets/image2018-6-22_13-50-50.png)

1. Near the upper-left corner of the CRXDE Lite page, tap or click **Save All**.

### Testing the integration of AEM 3D with Autodesk 3ds Max {#testing-the-integration-of-aem-d-with-autodesk-ds-max}

1. Open AEM Assets, then upload the .MAX file located in `sample-3D-content/models`** **to the **test3d** folder.

   Note that sample-3D-content.zip was previously downloaded for validating the basic 3D functionality.

1. Return to the Card view and observe the message banners shown on the uploaded assets.

   The Converting Format banner is displayed while 3ds Max is converting the native 3ds Max format to .FBX.

1. After processing is finished, open `logo-sphere.max` in the Detail view.

   The Preview experience is the same as with **logo_sphere.fbx**.
