---
title: Uppgraderingsberedskap
titleSuffix: Configuration Manager
description: Integrera Uppgraderingsberedskap med Configuration Manager för att få åtkomst till Windows 10 Upgrade Compatibility data och mål enheter för uppgradering eller reparation.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/31/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 18d8b66a7b9f5ad889645cbc8e48ebcbfe6550a9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715048"
---
# <a name="integrate-upgrade-readiness-with-configuration-manager"></a>Integrera Uppgraderingsberedskap med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

> [!Important]  
> Windows Analytics-tjänsten dras tillbaka den 31 januari 2020. Mer information finns i [KB 4521815: pensionering i Windows Analytics den 31 januari 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).
>
> Desktop Analytics är utvecklingen av Windows Analytics. Mer information finns i [Vad är Desktop Analytics](../../../desktop-analytics/overview.md).

Om din Configuration Manager plats hade en anslutning till Uppgraderingsberedskap måste du ta bort den och konfigurera om klienter.

## <a name="remove-upgrade-readiness-connection"></a><a name="bkmk_remove"></a>Ta bort Uppgraderingsberedskap anslutning

1. Öppna Configuration Manager-konsolen som en användare med rollen **Fullständig administratör** .

1. Gå till arbets ytan **Administration** , expandera **Cloud Services**och välj noden **Azure-tjänster** .

1. Ta bort Windows Analytics-tjänsten.

## <a name="reconfigure-clients"></a>Konfigurera om klienter

### <a name="unenroll-devices"></a>Avregistrera enheter

Börja med att granska platsens standard-eller anpassade klient enhets inställningar i **Windows Analytics** -gruppen. Inaktivera till exempel följande inställning: **Hantera inställningar för Windows-telemetri med Configuration Manager**.

> [!IMPORTANT]
> Om du planerar att använda Desktop Analytics konfigurerar den Windows-diagnostikens data inställningar på klienter. Använd guiden anslutning för Azure-tjänster om du vill konfigurera inställningarna för användning med Desktop Analytics. Mer information finns i [så här ansluter du Configuration Manager med Desktop Analytics](../../../desktop-analytics/connect-configmgr.md).

På registrerade enheter tar du bort värdet CommercialID från följande Windows-register nycklar:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Data konfiguration för Windows-diagnostik

Om du inte vill att enheterna ska kunna skicka diagnostikdata:

- Windows 10: ange nivån för diagnostikdata till **säkerhet**
- Windows 7 SP1 eller 8,1: inaktivera den **kommersiella data inloggnings nyckeln**

Ange dessa värden med någon av följande metoder:

- Grup princip, i **dator konfiguration** > **administrativa mallar** > **Windows Components** > **data insamling och för hands versioner** av Windows-komponenter
- Hantering av mobila enheter (MDM), till exempel [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

Mer information finns i [Konfigurera Windows-diagnostikdata i din organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> När du tillämpar dessa ändringar slutar enheterna omedelbart att skicka diagnostikdata. Det kan ta 24-48 timmar för Microsoft att sluta bearbeta insikter för din arbets yta. Microsoft tar bort dessa data från sina moln tjänster inom 30 dagar eller mindre.

<!--
Upgrade Readiness is a part of [Windows Analytics](https://docs.microsoft.com/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness). It allows you to assess and analyze the readiness of devices in your environment for an upgrade to Windows 10. Integrate Upgrade Readiness with Configuration Manager to access client upgrade compatibility data in the Configuration Manager console. Then use this data to create collections, and target devices for upgrade or remediation.



## Configure clients

Upgrade Readiness relies on Windows Analytics data. In order for Upgrade Readiness to receive sufficient data, configure the following prerequisites:

- Configure all clients with a *commercial ID key*  

- Configure Windows 10 clients for Windows Analytics to report at least basic level data  

- For clients running Windows 7 or 8.1:  

    - Install the updates as described in [Get started with Upgrade Readiness](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)  

    - Enable Windows Analytics client settings  

Configure these settings using Configuration Manager client settings. For more information, see [Use Windows Analytics](monitor-windows-analytics.md).

> [!NOTE]  
> Deploying the correct prerequisite updates and configuring client settings should be sufficient in most environments. If you encounter issues with Upgrade Readiness not receiving data from devices in your environment, then some of these issues may be addressed by using the [Upgrade Readiness deployment script](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-deployment-script). 



## Connect Configuration Manager to Upgrade Readiness

Use the [Azure services wizard](../../servers/deploy/configure/azure-services-wizard.md) to simplify the process of configuring Azure services you use with Configuration Manager. To connect Configuration Manager with Upgrade Readiness, create an Azure Active Directory (Azure AD) app registration of type *Web app / API* in the [Azure portal](https://portal.azure.com). For more information about how to create an app registration, see [Register your application with your Azure AD tenant](/azure/active-directory/active-directory-app-registration). 

In the Azure portal, give following permissions to your newly registered web app:
- *Reader* permissions to the resource group that contains the Log Analytics workspace with your Upgrade Readiness data
- *Contributor* permissions to the Log Analytics workspace that hosts your Upgrade Readiness data

The Azure services wizard uses this app registration to allow Configuration Manager to communicate securely with Azure AD and connect your infrastructure to your Upgrade Readiness data.

> [!IMPORTANT]  
> Grant permissions to the app itself, not to an Azure AD user identity. It's the registered app that accesses the data on behalf of your Configuration Manager infrastructure. To grant the permissions, search for the name of the app registration in the **Add users** area when assigning the permission. 
> 
> This process is the same as when providing Configuration Manager with permissions to Log Analytics. These steps must be completed before the app registration is imported into Configuration Manager with the *Azure services wizard*.
> 
> For more information, see [Connect Configuration Manager to Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm).


### Use the Azure Wizard to create the connection

Follow the instructions in [Configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) to create a connection to Upgrade Readiness by importing the web app registration you created above. 

If the web app import was successful and the correct permissions are assigned in the Azure portal, the *Configuration* page pre-populates the following values:   
-  Azure subscriptions  
-  Azure resource group  
-  Windows Analytics workspace  

More than one resource group or workspace is available in the following circumstances: 
- If the registered Azure AD web app has *Contributor* permissions on more than one resource group   
- If the selected resource group has more than one Log Analytics workspace  



## View and use Upgrade Readiness information in Configuration Manager

After you've integrated Upgrade Readiness with Configuration Manager, you can view the analysis of your clients' upgrade readiness.

1. In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Upgrade Readiness** node.  

2. Review the data. For example:  
    - The upgrade readiness state  
    - The percent of Windows devices that are reporting data  

3. Filter the dashboard to view data for devices in specific collections.  

4. View the devices in a particular readiness state, and then create a dynamic collection for those devices. Then use that collection to upgrade those devices, or take action to remediate devices that are in a blocked state.  

> [!Note]  
> The site synchronizes data with Upgrade Readiness once a week. To manually trigger synchronization:
> 1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node.  
> 2. Select the Upgrade Readiness connection from the list.  
> 3. In the ribbon, select the option to synchronize.  



## Next steps

- [Upgrade Windows to the latest version](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)  
- [Create a task sequence to upgrade an OS](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)  
- [Create phased deployments](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)  
