---
title: Teknisk för hands version 1709
titleSuffix: Configuration Manager
description: Lär dig mer om de funktioner som finns i teknisk för hands version 1709 för Configuration Manager.
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b3cb491ff3bfb10935566c33e321542435d2e0af
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692918"
---
# <a name="capabilities-in-technical-preview-1709-for-configuration-manager"></a>Funktioner i Technical Preview 1709 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1709. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. Innan du installerar den här versionen av Technical Preview kan du läsa [Technical Preview för Configuration Manager](../../core/get-started/technical-preview.md) för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Kända problem i den här tekniska för hands versionen:**
- **Det går inte att uppdatera till för hands version 1709 när du har en plats server i passivt läge**. När du kör för hands version 1706, 1707 eller 1708 och har en [primär plats server i passivt läge](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), måste du avinstallera plats servern för passivt läge innan du kan uppdatera för hands versionen till version 1709. Du kan installera om den passiva läges plats servern efter att platsen har kört version 1709.

  Så här avinstallerar du plats servern för passivt läge:
  1. I-konsolen går du till **Administration**  >  **Översikt**  >  **plats konfigurations**  >  **servrar och plats system roller**och väljer sedan plats servern för passivt läge.
  2. I fönstret **plats system roller** högerklickar du på **plats Server** rollen och väljer sedan **ta bort roll**.
  3. Högerklicka på plats servern för passivt läge och välj sedan **ta bort**.
  4. När plats servern har avinstallerats startar du om tjänsten **CONFIGURATION_MANAGER_UPDATE**på den aktiva primära plats servern.


**Följande är nya funktioner som du kan prova med den här versionen.**  

## <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Förbättrad VPN-profil i Configuration Manager-konsolen
<!-- 1313282 -->
I den här versionen har vi uppdaterat guiden VPN-profil och egenskaps sidor för att Visa inställningar som är lämpliga för den valda plattformen. Specifikt:

- Varje plattform har sitt eget arbets flöde, vilket innebär att nya VPN-profiler bara innehåller inställningen som stöds av plattformen.
- Sidorna för **plattformar som stöds** visas nu efter sidan **Allmänt** .  Nu väljer du plattform innan du anger egenskaps värden.
- När plattformen är inställd på **Android**, **Android for Work**eller **Windows Phone 8,1**behövs inte sidan **plattformar som stöds** och visas inte.
- Det Configuration Manager klientbaserade arbets flödet har kombinerats med klientbaserade Windows 10-arbetsflöden (hybrid Mobile Device). de har stöd för samma inställningar.
- Varje plattforms arbets flöde innehåller bara de inställningar som är lämpliga för det arbets flödet.  Android-arbetsflödet innehåller till exempel inställningar som är lämpliga för Android. inställningar som är lämpliga för iOS eller Windows 10 Mobile visas inte längre i Android-arbetsflödet.
- För Windows 8,1-enheter markeras inställningar som hanteras av Configuration Manager tydligt.
- Den automatiska VPN-sidan är föråldrad och har tagits bort.

Dessa ändringar gäller för nya VPN-profiler.  

För att minimera kompatibiliteten är befintliga VPN-profiler oförändrade.  När du redigerar en befintlig profil visas inställningarna som de gjorde när profilen skapades.  

### <a name="try-it-out"></a>prova!

Skapa en ny VPN-profil med den vanliga processen. Observera att den första sidan i guiden VPN-profils alternativ har ändrats.

1. Gå till **till gångar och efterlevnad**  >  **Översikt**  >  **kompatibilitetsinställningar inställningar**  >  **företags resurs åtkomst**  >  **VPN-profiler** och välj sedan **skapa VPN-profil**.
2. Ange ett namn på sidan **Allmänt** och välj något av följande alternativ under **Ange vilken typ av VPN-profil du vill skapa**:

    - Windows 10  
    - Windows 8,1  
    - Windows Phone 8.1  
    - iOS och macOS  
    - Android  
    - Android for Work  

3. Om du väljer **Windows 8,1**har du också möjlighet att skapa en **ny profil** eller **Importera från en fil**.
4. Slutför guiden för att slutföra skapandet av profilen.

När du väljer olika plattformar ser du till att endast de inställningar som är relevanta för den valda plattforms visningen visas.

## <a name="co-management-for-windows-10-devices"></a>Samhantering för Windows 10-enheter    
<!-- 1350871 -->
Många kunder vill hantera Windows 10-enheter på samma sätt som de hanterar mobila enheter med en förenklad, lägre kostnad, molnbaserad lösning. Det kan dock vara svårt att göra över gången från traditionell hantering till modern hantering. Från och med Windows 10, version 1607 (även kallat uppdatering av årsdagen) kan du ansluta en Windows 10-enhet till en lokal Active Directory (AD) och molnbaserad Azure AD samtidigt (hybrid Azure AD). Samhantering drar nytta av den här förbättringen och gör att du samtidigt kan hantera Windows 10-enheter med hjälp av både Configuration Manager och Intune. Det är en lösning som ger en brygga från traditionell till modern hantering och ger dig en sökväg för att göra över gången med en stegvis metod. 

### <a name="prerequisites"></a>Förutsättningar
Du måste ha följande krav på plats innan du kan aktivera samhantering. Det finns allmänna krav och olika krav för befintliga Configuration Manager klienter och enheter som inte är klienter.

### <a name="known-issues"></a>Kända problem
När du har skapat en princip för samtidig hantering kan du inte redigera principen. Du kan ändra principen genom att ta bort den och sedan återskapa den med de inställningar som du behöver. 

#### <a name="general-prerequisites"></a>Allmänna krav
Följande är allmänna krav som du kan använda för att aktivera samhantering:  

- Teknisk för hands version för Configuration Manager version 1709
- Azure AD 
- EMS-eller Intune-licens för alla användare
- Intune-prenumeration &#40;MDM-auktoritet i Intune inställt på **intune**&#41;

   > [!Note]  
   > Om du har en hybrid MDM-miljö (Intune integrerad med Configuration Manager) kan du inte aktivera samhantering.

#### <a name="additional-prerequisites-for-existing-configuration-manager-clients"></a>Ytterligare krav för befintliga Configuration Manager-klienter
- Windows 10, version 1709 (höst Creators Update) och senare
- Hybrid Azure AD-ansluten (ansluten till AD och Azure AD)

#### <a name="additional-prerequisites-for-new-windows-10-devices"></a>Ytterligare krav för nya Windows 10-enheter
- Windows 10, version 1709 (höst Creators Update) och senare
- [Cloud Management Gateway](../clients/manage/manage-clients-internet.md#cloud-management-gateway) i Configuration Manager

### <a name="workloads-you-can-switch-to-intune"></a>Arbets belastningar som du kan växla till Intune
När du har aktiverat samhantering fortsätter Configuration Manager att hantera alla arbets belastningar. När du bestämmer dig för att du är redo kan du starta Intune med att hantera tillgängliga arbets belastningar. I den här versionen kan du använda Intune för att hantera följande arbets belastningar.   

#### <a name="compliance-policies"></a>Efterlevnadsprinciper
Efterlevnadsprinciper definierar de regler och inställningar som en enhet måste följa för att anses vara kompatibla med principerna för villkorlig åtkomst. Du kan också använda efterlevnadsprinciper för att övervaka och åtgärda enheters efterlevnadsproblem oberoende av villkorlig åtkomst.

#### <a name="windows-update-for-business-policies"></a>Windows Update för affärs principer
Med Windows Update för affärs principer kan du konfigurera regler för avstängning för Windows 10-funktions uppdateringar eller kvalitets uppdateringar för Windows 10-enheter som hanteras direkt av Windows Update för företag. Mer information finns i [konfigurera Windows Update för principer för avstängning av företag](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Fjärråtgärder som är tillgängliga i Intune på Azure för samhanterade enheter
När en Windows 10-enhet är aktive rad för samhantering har du följande fjärråtgärder som är tillgängliga från Intune på Azure:  
- [Fabriks återställning](/intune/devices-wipe#wipe)
- [Selektiv rensning](/intune/apps-selective-wipe)
- [Ta bort enheter](/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Starta om enheten](/intune/device-restart)
- [Ny start](/intune/device-fresh-start)

### <a name="prepare-intune-for-co-management"></a>Förbereda Intune för samhantering
Innan du växlar arbets belastningar från Configuration Manager till Intune skapar du de profiler och principer du behöver i Intune för att se till att enheterna fortsätter att vara skyddade.
Du kan skapa objekt i Intune baserat på de objekt som du har i Configuration Manager. Eller, om din aktuella strategi baseras på en äldre eller traditionell hantering, kanske du vill gå tillbaka till de principer och profiler som du behöver för modern hantering. Använd följande resurser för att skapa principer och profiler.    
<!-- - [Device compliance policies](/intune/compliance-policy-create-windows)  -->
- [Windows Update för affärs principer](/intune/windows-update-for-business-configure)  
- [Enhetens konfigurationsprofiler](/intune/device-profile-create)  

### <a name="architectural-overview-for-co-management"></a>Arkitektur översikt för samhantering
Följande diagram ger en översikt över samhantering och hur den passar in i befintliga konfigurations-och Intune-infrastrukturer.

![Arkitektur diagram för samhantering](./media/co-management-arch-cm1709tp.svg)

### <a name="scenarios-to-enable-co-management"></a>Scenarier för att aktivera samhantering  
Du kan aktivera samhantering för både Windows 10-enheter som har registrerats i Microsoft Intune och befintliga Windows 10 Configuration Manager-klienter. Båda scenarierna resulterar i Windows 10-enheter som hanteras samtidigt av Configuration Manager och Intune, samt anslutna till AD och Azure AD.  

#### <a name="devices-enrolled-in-intune"></a>Enheter som har registrerats i Intune  
När Windows 10-enheter har registrerats i Intune kan du installera Configuration Manager-klienten på enheterna (med ett särskilt kommando rads argument) för att förbereda klienterna för samhantering. Sedan aktiverar du samhantering från Configuration Manager-konsolen för att börja flytta vissa arbets belastningar till Intune för vissa Windows 10-enheter.  

För Windows 10-enheter som ännu inte har registrerats i Intune kan du använda automatisk registrering i Azure för att registrera enheterna. För nya Windows 10-enheter kan du använda Windows autopilot för att konfigurera OOBE (out of Box Experience) som innehåller automatisk registrering som registrerar enheter i Intune.  

#### <a name="configuration-manager-clients"></a>Configuration Manager klienter
När du har Windows 10-enheter som är Configuration Manager-klienter kan du registrera dessa enheter och aktivera samhantering från Configuration Manager-konsolen. Configuration Manager utlöser automatisk registrering i Intune baserat på klient information för Azure AD.  

### <a name="prepare-windows-10-devices-for-co-management"></a>Förbereda Windows 10-enheter för samhantering
Du kan aktivera samhantering på Windows 10-enheter som är anslutna till AD och Azure AD och som registrerats i Intune och en klient i Configuration Manager. För nya Windows 10-enheter och enheter som redan har registrerats i Intune installerar du Configuration Manager-klienten innan de kan samhanteras. För Windows 10-enheter som redan Configuration Manager-klienter kan du registrera enheterna med Intune och aktivera samhantering i Configuration Manager-konsolen.

#### <a name="command-line-to-install-configuration-manager-client"></a>Kommando rad för att installera Configuration Manager-klient
Skapa en app i Intune för Windows 10-enheter som inte redan Configuration Manager-klienter. Använd följande kommando rad när du skapar appen i nästa avsnitt:

ccmsetup.msi CCMSETUPCMD = "/MP: &#60;*URL för Cloud Management Gateway ömsesidig auth-slutpunkt*&#62;/CCMHOSTNAME =&#60;*URL för Cloud Management Gateway ömsesidigt auth* *-* slutpunkt&#62; SMSSiteCode =&#60;*platskod*&#62; SMSMP = https: &#47;/&#60;*FQDN för mp*&#62; AADTENANTID =&#60;*AAD klient-ID*&#62; AADTENANTNAME =&#60;*klient* ORGANISATIONs namn&#62; AADCLIENTAPPID =&#60;-ID *för AAD-integrering*&#62; AADRESOURCEURI = https: &#47;

Om du till exempel har följande värden:

- **URL för moln hanterings-gatewayens ömsesidiga auth-slutpunkt**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Använd värdet **MutualAuthPath** i vyn **VProxy_Roles** SQL för **URL: en för en slut punkts värde för molnbaserad autentisering i Cloud Management Gateway** .

- **FQDN för hanterings plats (MP)**: sccmmp.Corp.contoso.com    
- **Platskod**: PS1    
- **Azure AD-klient-ID**: 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Namn på Azure AD-klient organisation**: contoso    
- **Azure AD-klientens app-ID**: bef323b3-042f-41a6-907A-f9faf0d1XXXX     
- **AAD-resurs-ID-URI**: ConfigMgrServer    

  > [!Note]    
  > Använd **identifierar** -värdet som finns i **vSMS_AAD_Application_Ex** SQL-vyn för **URI-värdet för AAD-resurs-ID** .

Använd följande kommando rad:

ccmsetup.msi CCMSETUPCMD = "/MP: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 CCMHOSTNAME = contoso. cloudapp. net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode = PS1 SMSMP = https:/&#47;sccmmp.corp.contoso.com AADTENANTID = 72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME = contoso AADCLIENTAPPID = &#47;bef323b3-042f-41a6-907a f9faf0d1XXXX

> [!Tip]
>Du kan hitta kommando rads parametrarna för din webbplats med hjälp av följande steg:     
> 1. I Configuration Manager-konsolen går du till **Administration**  >  **Översikt**  >  **Cloud Services**  >  **samhantering**.  
> 2. På fliken Start går du till gruppen hantera och väljer **Konfigurera samhantering** för att öppna guiden för att skapa en gemensam hantering.    
> 3. På sidan prenumeration klickar du på **Logga** in och loggar in på din Intune-klient och klickar sedan på **Nästa**.    
> 4. På sidan Aktivering klickar du på **Kopiera** i avsnittet enheter som har **registrerats i Intune** för att kopiera kommando raden till Urklipp och sedan Spara kommando raden som ska användas i proceduren för att skapa appen.  
> 5. Klicka på **Avbryt** om du vill avsluta guiden.

#### <a name="new-windows-10-devices"></a>Nya Windows 10-enheter
För nya Windows 10-enheter kan du använda autopilot-tjänsten för att konfigurera out of Box-upplevelsen, vilket innefattar att ansluta enheten till AD och Azure AD, samt registrera enheten i Intune. Skapa sedan en app i Intune för att distribuera Configuration Manager-klienten.  
1. Aktivera autopilot för de nya Windows 10-enheterna. Mer information finns i [Översikt över Windows autopilot](/windows/deployment/windows-10-auto-pilot).  
2. Konfigurera automatisk registrering i Azure AD för att enheterna ska registreras automatiskt i Intune. Mer information finns i [registrera Windows-enheter för Microsoft Intune](/intune/windows-enroll).
3. Skapa en app i Intune med Configuration Manager klient paketet och distribuera appen till Windows 10-enheter som du vill samhantera. Använd [kommando raden för att installera Configuration Manager-klienten](#command-line-to-install-configuration-manager-client) när du går igenom stegen för att [Installera klienter från Internet med hjälp av Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure).   

#### <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Windows 10-enheter som inte har registrerats i Intune eller en Configuration Manager-klient
För Windows 10-enheter som inte är registrerade i Intune eller som har Configuration Manager-klienten, kan du använda automatisk registrering för att registrera enheten i Intune. Skapa sedan en app i Intune för att distribuera Configuration Manager-klienten.
1. Konfigurera automatisk registrering i Azure AD för att enheterna ska registreras automatiskt i Intune. Mer information finns i [registrera Windows-enheter för Microsoft Intune](/intune/windows-enroll).  
2. Skapa en app i Intune med Configuration Manager klient paketet och distribuera appen till Windows 10-enheter som du vill samhantera. Använd [kommando raden för att installera Configuration Manager-klienten](#command-line-to-install-configuration-manager-client) när du går igenom stegen för att [Installera klienter från Internet med hjälp av Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

#### <a name="windows-10-devices-enrolled-in-intune"></a>Windows 10-enheter som har registrerats i Intune
För Windows 10-enheter som redan har registrerats i Intune skapar du en app i Intune för att distribuera Configuration Manager-klienten. Använd [kommando raden för att installera Configuration Manager-klienten](#command-line-to-install-configuration-manager-client) när du går igenom stegen för att [Installera klienter från Internet med hjälp av Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

### <a name="switch-configuration-manager-workloads-to-intune"></a>Växla Configuration Manager-arbetsbelastningar till Intune
I föregående avsnitt har du för berett Windows 10-enheter för samhantering. De här enheterna är nu anslutna till AD och Azure AD och de registreras i Intune och har Configuration Manager-klienten. Du har troligen fortfarande fortfarande Windows 10-enheter som är anslutna till AD och har Configuration Manager-klienten, men inte anslutit till Azure AD eller registrerat i Intune. Följande procedur innehåller steg för att aktivera samhantering, förbereda resten av dina Windows 10-enheter (Configuration Manager klienter utan Intune-registrering) för samhantering, och gör att du kan börja växla vissa Configuration Manager arbets belastningar till Intune.

1. I Configuration Manager-konsolen går du till **Administration**  >  **Översikt**  >  **Cloud Services**  >  **samhantering**.    
2. På fliken Start går du till gruppen hantera och väljer **Konfigurera samhantering** för att öppna guiden för att skapa en gemensam hantering.    
3. På sidan prenumeration klickar du på **Logga** in och loggar in på din Intune-klient och klickar sedan på **Nästa**.   
4. Konfigurera följande inställningar på sidan mellanlagring och klicka sedan på **Nästa**:
    - **Pilot grupp**: pilot gruppen innehåller en eller flera samlingar som du väljer. Använd den här gruppen som en del av den stegvisa distributionen av samhantering. Du kan börja med en liten test samling och sedan lägga till fler samlingar i pilot gruppen när du distribuerar samhantering till fler användare och enheter. Du kan när som helst ändra samlingarna i gruppen pilot genom att använda egenskaperna för samhantering.
    - **Produktion**: när du väljer den här inställningen aktive ras alla Windows 10-enheter som stöds för samhantering. Konfigurera **undantags gruppen** med en eller flera samlingar. Enheter som är medlemmar i någon av samlingarna i den här gruppen undantas från att använda samhantering. 
5. På sidan Aktivering väljer du antingen **pilot** eller **alla** (beroende på inställningarna som du konfigurerade på sidan mellanlagring) för att aktivera automatisk registrering i Intune och klickar sedan på **Nästa**. När du väljer **pilot**registreras endast Configuration Manager-klienter som är medlemmar i pilot gruppen automatiskt i Intune. På så sätt kan du aktivera samhantering på en delmängd av klienter för att först testa samhantering och distribuera samhantering med hjälp av en stegvis metod. 
6. På sidan arbets belastningar väljer du om du vill växla Configuration Manager arbets belastningar som ska hanteras av Intune och klicka sedan på **Nästa**. Använd skjutreglagen för att välja om du vill växla arbets belastningen till pilot gruppen eller för alla Windows 10-klienter (beroende på vilka inställningar du konfigurerade på sidan mellanlagring). 
7. Slutför guiden för att aktivera samhantering.  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->

## <a name="see-also"></a>Se även
Information om hur du installerar eller uppdaterar den tekniska för hands versionen finns i [teknisk för hands version för Configuration Manager](technical-preview.md).