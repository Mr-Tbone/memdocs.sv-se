---
title: Hantera samlingar
titleSuffix: Configuration Manager
description: Utför vanliga hanterings uppgifter för samlingar i Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2fc8347ae766cbd16075ef4170efa2f8042371f8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714341"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>Hantera samlingar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd översikts informationen i den här artikeln för att hjälpa dig att utföra hanterings uppgifter för samlingar i Configuration Manager.  

> [!NOTE]  
>  Information om hur du skapar Configuration Manager samlingar finns i [skapa samlingar](create-collections.md).



## <a name="how-to-manage-device-collections"></a><a name="bkmk_device"></a>Hantera enhets samlingar  

Välj **Enhetssamlingar** på arbetsytan **Tillgångar och efterlevnad**, välj den samling som du vill hantera och välj sedan en hanteringsaktivitet.  


#### <a name="show-members"></a>Visa medlemmar
Visar alla resurser som är medlemmar i den valda samlingen på en tillfällig nod under noden **Enheter** .


#### <a name="add-selected-items"></a>Lägga till valda objekt
Innehåller följande alternativ: 

- **Lägg till markerade objekt i befintlig enhets samling**: öppnar dialog rutan **Välj samling** . Välj den samling som du vill lägga till medlemmar i den valda samlingen i. Den valda samlingen tas med i den här samlingen med hjälp av en medlemskapsregel av typen **Inkludera samlingar** .  

- **Lägg till markerade objekt i ny enhets samling**: öppnar **guiden skapa enhets samling** där du kan skapa en ny samling. Den valda samlingen tas med i den här samlingen med hjälp av en medlemskapsregel av typen **Inkludera samlingar** .  


Mer information finns i [så här skapar du samlingar](create-collections.md).


#### <a name="install-client"></a>Installera klient
Öppnar **guiden Installera klient**. Den här guiden använder push-installation av klienter för att installera en Configuration Manager-klient på alla datorer i den valda samlingen. Mer information finns i [push-installation av klienter](../../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).


#### <a name="run-script"></a>Kör skript
Öppnar guiden **Kör skript** för att köra ett PowerShell-skript på alla klienter i samlingen. Mer information finns i [skapa och köra PowerShell-skript](../../../../apps/deploy-use/create-deploy-scripts.md).


#### <a name="manage-affinity-requests"></a>Begäran om att hantera tillhörigheter
Öppnar dialog rutan **Hantera begär Anden om mappning mellan användare och enhet** . Godkänn eller avvisa väntande begär Anden om att upprätta mappningar mellan användare och enheter för enheter i den valda samlingen. Mer information finns i [Länka användare och enheter med mappning mellan användare och enhet](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)


#### <a name="clear-required-pxe-deployments"></a>Rensa nödvändiga PXE-distributioner
Tar bort nödvändiga PXE-startdistributioner från alla medlemmar i den valda samlingen. Mer information finns i [använda PXE för att distribuera Windows via nätverket](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).


#### <a name="update-membership"></a>Uppdatera medlemskap
Utvärderar medlemskapet för den valda samlingen. Den här uppdateringen kan ta en stund för samlingar med många medlemmar. Använd åtgärden **Uppdatera** för att uppdatera visningen med de nya medlemmarna i samlingen när uppdateringen har slutförts.


#### <a name="add-resources"></a>Lägg till resurser
Öppnar dialog rutan **Lägg till resurser i samling** . Sök efter nya resurser som ska läggas till i den valda samlingen. Ikonen för den valda samlingen visar en timglas symbol medan uppdateringen pågår.


#### <a name="client-notification"></a>Klientmeddelande
Mer information finns i [klient meddelanden](../client-notification.md).


#### <a name="endpoint-protection"></a>Slutpunktsskydd
Mer information finns i [klient meddelanden](../client-notification.md).


#### <a name="export"></a>Exportera
Öppnar **guiden Exportera samlingar** som hjälper dig att exportera den här samlingen till en Managed Object Format fil (MOF). Den här filen kan sedan arkiveras eller importeras på en annan Configuration Manager webbplats. När du exporterar en samling exporteras inte refererade samlingar. En refererad samling refereras till av den valda samlingen med hjälp av en regel för att **Inkludera** eller **exkludera** .


#### <a name="copy"></a>Kopiera
Skapar en kopia av den valda samlingen. Den nya samlingen använder den valda samlingen som en begränsande samling.


#### <a name="refresh"></a>Uppdatera
Uppdatera vyn.


#### <a name="delete"></a>Ta bort
Tar bort den valda samlingen. Du kan också ta bort alla resurser i samlingen från platsdatabasen. 

Du kan inte ta bort samlingarna som är inbyggda i Configuration Manager. En lista över de inbyggda samlingarna finns i [Introduktion till samlingar](introduction-to-collections.md#built-in-collections).


#### <a name="simulate-deployment"></a>Simulera distribution
Öppnar **Guiden simulera program distribution**. Med den här guiden kan du testa resultatet av en program distribution utan att installera eller avinstallera programmet. Mer information finns i [så här simulerar du program distributioner](../../../../apps/deploy-use/simulate-application-deployments.md).


#### <a name="deploy"></a>Distribuera
Du kan välja mellan följande alternativ:  

- **Program**: öppnar **guiden distribuera program vara**. Välj och konfigurera en program distribution till den valda samlingen. Mer information finns i [distribuera program](../../../../apps/deploy-use/deploy-applications.md).  

- **Program**: öppnar **guiden distribuera program vara**. Välj och konfigurera en paket-och program distribution för den valda samlingen. Mer information finns i [paket och program](../../../../apps/deploy-use/packages-and-programs.md).  

- **Konfigurations bas linje**: öppnar dialog rutan **distribuera konfigurations bas linjer** . Konfigurera distributionen av en eller flera konfigurations bas linjer till den valda samlingen. Mer information finns i [så här distribuerar du konfigurations bas linjer](../../../../compliance/deploy-use/deploy-configuration-baselines.md).  

- **Aktivitetssekvens**: öppnar **guiden distribuera program vara**. Välj och konfigurera en aktivitetssekvensdistribution för den valda samlingen. Mer information finns i [Hantera aktivitetssekvenser för att automatisera uppgifter](../../../../osd/deploy-use/deploy-a-task-sequence.md).  

- **Program uppdateringar**: öppnar **guiden distribuera program uppdateringar**. Konfigurera distributionen av program uppdateringar till resurser i den valda samlingen. Mer information finns i [hantera program uppdateringar](../../../../sum/understand/software-updates-introduction.md).  


#### <a name="clear-server-group-deployment-locks"></a>Rensa distributions lås för Server grupp
Frigör alla Server grupps distributions lås för samlingen manuellt. Mer information finns i [tjänst a Server Group](../../../../sum/deploy-use/service-a-server-group.md).


#### <a name="move"></a>Flytta
Flytta den valda samlingen till en annan mapp i noden **enhets samlingar** . 


#### <a name="properties"></a>Egenskaper
Mer information finns i [samlings egenskaper](#BKMK_CollProp).  


## <a name="how-to-manage-user-collections"></a><a name="bkmk_user"></a>Hantera användar samlingar  

Välj **Användarsamlingar** på arbetsytan **Tillgångar och efterlevnad**, välj den samling som du vill hantera och välj sedan en hanteringsaktivitet.  

> [!Note]  
> Följande åtgärder är tillgängliga i användar samlingar, men beteendena är desamma som med enhets samlingar. Förutom de som gäller för användar samlingar och användare i. Mer information finns i motsvarande åtgärd under [Hantera enhets samlingar](#bkmk_device).  

- **Visa medlemmar**  
- **Lägga till valda objekt**  
    - **Lägg till markerade objekt i befintlig användar samling**  
    - **Lägg till markerade objekt i ny användar samling**  
- **Begäran om att hantera tillhörigheter**  
- **Uppdatera medlemskap**  
- **Lägg till resurser**  
- **Exportera**  
- **Exemplar**  
- **Uppdatera**  
- **Ta bort**  
- **Simulera distribution**  
- **Distribuera**  
    - **Program**  
    - **Program**  
    - **Konfigurations bas linje**
- **Flytta**  
- **Egenskaper**


##  <a name="collection-properties"></a><a name="BKMK_CollProp"></a> Samlingsegenskaper  

När du öppnar dialog rutan **Egenskaper** för en samling kan du Visa och konfigurera följande alternativ:  

#### <a name="general"></a>Allmänt
Visa och konfigurera allmän information om den valda samlingen inklusive samlingens namn och den begränsande samlingen.

#### <a name="membership-rules"></a>Medlemskapsregler
Konfigurera medlemskaps reglerna som definierar medlemskapet för den här samlingen. Mer information finns i [så här skapar du samlingar](create-collections.md).  

#### <a name="power-management"></a>Energisparfunktioner
Konfigurera hanterings planer för energispar funktioner som du har tilldelat till datorer i den valda samlingen. Mer information finns i [Introduktion till energispar funktioner](../power/introduction-to-power-management.md).  

#### <a name="deployments"></a>Distributioner
Visar all program vara som du har distribuerat till medlemmar i den valda samlingen.  

#### <a name="maintenance-windows"></a>Underhållsperioder
Visa och konfigurera underhålls fönster som tillämpas på medlemmar i den valda samlingen. Mer information finns i [använda underhålls](use-maintenance-windows.md)perioder.

#### <a name="collection-variables"></a>Collection-variabler
Konfigurera variabler som gäller för den här samlingen och som kan användas av aktivitetssekvenser. Mer information finns i [så här anger du variabler för aktivitetssekvens](../../../../osd/understand/using-task-sequence-variables.md#bkmk_set).  

#### <a name="distribution-point-groups"></a>Distributionsplatsgrupper
Koppla en eller flera distributions plats grupper till medlemmar i den valda samlingen. Mer information finns i [Hantera innehåll och innehålls infrastruktur](../../../servers/deploy/configure/manage-content-and-content-infrastructure.md).

#### <a name="aad-group-sync"></a>Synkronisering av AAD-grupp
Synkronisera samlings medlemskaps resultat till Azure Active Directory grupper. Den här synkroniseringen är en [för hands versions funktion](../../../servers/manage/pre-release-features.md) som börjar i version 1906. Mer information finns i [skapa samlingar](create-collections.md#bkmk_aadcollsync).

#### <a name="security"></a>Säkerhet
Visar de administrativa användare som har behörighet till den valda samlingen genom associerade roller och säkerhetsomfattningar. Mer information finns i [grunderna i rollbaserad administration](../../../understand/fundamentals-of-role-based-administration.md).  

#### <a name="alerts"></a>Aviseringar 
Konfigurera när aviseringar genereras för klient status och Endpoint Protection. Mer information finns i [så här konfigurerar du klient status](../../deploy/configure-client-status.md) och [hur du övervakar Endpoint Protection](../../../../protect/deploy-use/monitor-endpoint-protection.md).  
## <a name="using-powershell"></a><a name="bkmk_powershell"></a>Använda PowerShell

PowerShell kan användas för att hantera samlingar.  Mer information finns i:

* [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection)
* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Kopiera – CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/copy-cmcollection)
* [Remove-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollection)
* [Importera – CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmcollection)
* [Exportera – CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmcollection)
* [Get-CMCollectionMember](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmember)
* [Get-CMCollectionSetting](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionsetting)
* [Invoke-CMCollectionUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/invoke-cmcollectionupdate)
* [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule)
* [Set-CMCollectionPowerManagement](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollectionpowermanagement)
* [Get-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmembershiprule)
* [Remove-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionmembershiprule)
* [Get-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectiondirectmembershiprule)
* [Get-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionquerymembershiprule)
* [Get-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionincludemembershiprule)
* [Add-CMCollectionToAdministrativeUser](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontoadministrativeuser)
* [Remove-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionquerymembershiprule)
* [Remove-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectiondirectmembershiprule)
* [Get-CMCollectionExcludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionexcludemembershiprule)
* [Add-CMCollectionToDistributionPointGroup](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontodistributionpointgroup)
* [Remove-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionincludemembershiprule)
* [Remove-CMCollectionExcludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionexcludemembershiprule)
* [Remove-CMCollectionFromAdministrativeUser](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionfromadministrativeuser)
