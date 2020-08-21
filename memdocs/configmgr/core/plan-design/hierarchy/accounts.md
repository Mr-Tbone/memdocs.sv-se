---
title: Konton som används
titleSuffix: Configuration Manager
description: Identifiera och hantera de Windows-grupper, konton och SQL-objekt som används i Configuration Manager.
ms.date: 05/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 17c22027ffc28f2e04e95b8223de27b8f26489fd
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698494"
---
# <a name="accounts-used-in-configuration-manager"></a>Konton som används i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd följande information för att identifiera de Windows-grupper, konton och SQL-objekt som används i Configuration Manager, hur de används och eventuella krav.  

- [Windows-grupper som skapas och används i Configuration Manager](#bkmk_groups)  
  - [Konfigurations Manager_CollectedFilesAccess](#configmgr_collectedfilesaccess)  
  - [Konfigurations Manager_DViewAccess](#configmgr_dviewaccess)  
  - [Configuration Manager fjärr styrnings användare](#configmgr_rcusers)  
  - [SMS-administratörer](#sms-admins)  
  - [SMS_SiteSystemToSiteServerConnection_MP_ &lt; SiteCode\>](#bkmk_remotemp)  
  - [SMS_SiteSystemToSiteServerConnection_SMSProv_ &lt; SiteCode\>](#bkmk_remoteprov)  
  - [SMS_SiteSystemToSiteServerConnection_Stat_ &lt; SiteCode\>](#bkmk_remotestat)  
  - [SMS_SiteToSiteConnection_ &lt; SiteCode\>](#bkmk_filerepl)  

- [Konton som används i Configuration Manager](#bkmk_accounts)
  - [Konto för Active Directory grupp identifiering](#active-directory-group-discovery-account)  
  - [Active Directory konto för system identifiering](#active-directory-system-discovery-account)  
  - [Konto för Active Directory användar identifiering](#active-directory-user-discovery-account)  
  - [Active Directory skogs konto](#active-directory-forest-account)  
  - [Konto för certifikat registrerings plats](#certificate-registration-point-account)  
  - [Avbilda operativ system avbildnings konto](#capture-os-image-account)  
  - [Konto för push-installation av klient](#client-push-installation-account)  
  - [Konto för registrerings plats anslutning](#enrollment-point-connection-account)  
  - [Anslutnings konto för Exchange Server](#exchange-server-connection-account)  
  - [Konto för hanterings plats anslutning](#management-point-connection-account)  
  - [Konto för multicast-anslutning](#multicast-connection-account)  
  - [Konto för nätverks åtkomst](#network-access-account)  
  - [Paket åtkomst konto](#package-access-account)  
  - [Konto för repor ting Services-plats](#reporting-services-point-account)  
  - [Konton för tillåtna visnings program för fjärrverktyg](#remote-tools-permitted-viewer-accounts)  
  - [Konto för plats installation](#site-installation-account)
  - [Konto för installation av plats system](#site-system-installation-account)  
  - [Server konto för plats systemets proxyserver](#site-system-proxy-server-account)  
  - [Konto för SMTP-server anslutning](#smtp-server-connection-account)  
  - [Anslutnings konto för program uppdaterings plats](#software-update-point-connection-account)  
  - [Käll plats konto](#source-site-account)  
  - [Konto för käll plats databas](#source-site-database-account)  
  - [Konto för domän anslutning för aktivitetssekvens](#task-sequence-domain-join-account)  
  - [Anslutnings konto för nätverks katalog för aktivitetssekvens](#task-sequence-network-folder-connection-account)  
  - [Kör som-konto för aktivitetssekvens](#task-sequence-run-as-account)  

- [Användar objekt som Configuration Manager använder i SQL](#bkmk_sqlusers)
  - [smsdbuser_ReadOnly](#smsdbuser_readonly)
  - [smsdbuser_ReadWrite](#smsdbuser_readwrite)
  - [smsdbuser_ReportSchema](#smsdbuser_reportschema)

- [Databas roller som Configuration Manager använder i SQL](#bkmk_sqlroles)
  - [smsdbrole_AITool](#smsdbrole_aitool)
  - [smsdbrole_AIUS](#smsdbrole_aius)
  - [smsdbrole_AMTSP](#smsdbrole_amtsp)
  - [smsdbrole_CRP](#smsdbrole_crp)
  - [smsdbrole_CRPPfx](#smsdbrole_crppfx)
  - [smsdbrole_DMP](#smsdbrole_dmp)
  - [smsdbrole_DmpConnector](#smsdbrole_dmpconnector)
  - [smsdbrole_DViewAccess](#smsdbrole_dviewaccess)
  - [smsdbrole_DWSS](#smsdbrole_dwss)
  - [smsdbrole_EnrollSvr](#smsdbrole_enrollsvr)
  - [smsdbrole_extract](#smsdbrole_extract)
  - [smsdbrole_HMSUser](#smsdbrole_hmsuser)
  - [smsdbrole_MCS](#smsdbrole_mcs)
  - [smsdbrole_MP](#smsdbrole_mp)
  - [smsdbrole_MPMBAM](#smsdbrole_mpmbam)
  - [smsdbrole_MPUserSvc](#smsdbrole_mpusersvc)
  - [smsdbrole_siteprovider](#smsdbrole_siteprovider)
  - [smsdbrole_siteserver](#smsdbrole_siteserver)
  - [smsdbrole_SUP](#smsdbrole_sup)
  - [smsdbrole_WebPortal](#smsdbrole_webportal)
  - [smsschm_users](#smsschm_users)

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a><a name="bkmk_groups"></a> Windows-grupper som Configuration Manager skapar och använder  

Configuration Manager skapas automatiskt och i många fall upprätthålls automatiskt följande Windows-grupper:  

> [!NOTE]  
> När Configuration Manager skapar en grupp på en dator som är en domän medlem är gruppen en lokal säkerhets grupp. Om datorn är en domänkontrollant är gruppen en lokal domän grupp. Den här typen av grupp delas mellan alla domänkontrollanter i domänen.  


### <a name="configuration-manager_collectedfilesaccess"></a><a name="configmgr_collectedfilesaccess"></a> Konfigurations Manager_CollectedFilesAccess

Configuration Manager använder den här gruppen för att ge åtkomst till att visa filer som samlats in av program varu inventering.  

Mer information finns i [Introduktion till program varu inventering](../../clients/manage/inventory/introduction-to-software-inventory.md).

#### <a name="type-and-location"></a>Typ och plats
Den här gruppen är en lokal säkerhetsgrupp som skapas på den primära platsservern.

När du avinstallerar en plats tas inte gruppen bort automatiskt. Ta bort den manuellt när du har avinstallerat en plats.

#### <a name="membership"></a>Medlemskap
Configuration Manager hanterar grupp medlemskapet automatiskt. Medlemmar är administrativa användare som fått behörighet att **Visa insamlade filer** för det skyddbara objektet **Samling** genom en tilldelad säkerhetsroll.

#### <a name="permissions"></a>Behörigheter
Den här gruppen har som standard behörigheten **läsa** till följande mapp på plats servern: `C:\Program Files\Microsoft Configuration Manager\sinv.box\FileCol`  


### <a name="configuration-manager_dviewaccess"></a><a name="configmgr_dviewaccess"></a>Konfigurations Manager_DViewAccess  

Den här gruppen är en lokal säkerhets grupp som Configuration Manager skapar på plats databas servern eller databas replik servern för en underordnad primär plats. Platsen skapar den när du använder distribuerade vyer för databasreplikering mellan platser i en hierarki. Den innehåller plats servern och SQL Server dator konton för den centrala administrations platsen.

Mer information finns i [data överföringar mellan platser](data-transfers-between-sites.md).


### <a name="configuration-manager-remote-control-users"></a><a name="configmgr_rcusers"></a> Configuration Manager fjärr styrnings användare  

Configuration Manager fjärrverktyg använder den här gruppen för att lagra de konton och grupper som du har skapat i listan över **behöriga användare** . Platsen tilldelar varje klient den här listan.  

Mer information finns i [Introduktion till fjärr styrning](../../clients/manage/remote-control/introduction-to-remote-control.md).

#### <a name="type-and-location"></a>Typ och plats
Den här gruppen är en lokal säkerhets grupp som skapas på den Configuration Manager klienten när klienten tar emot en princip som aktiverar fjärrverktyg.

När du har inaktiverat fjärrverktyg för en klient tas inte gruppen bort automatiskt. Ta bort den manuellt efter att du har inaktiverat fjärrverktyg.

#### <a name="membership"></a>Medlemskap
Det finns som standard inga medlemmar i den här gruppen. När du lägger till användare i listan över **behöriga** användare, läggs de automatiskt till i den här gruppen.

Använd listan över **tillåtna visnings program** för att hantera medlemskapet för den här gruppen i stället för att lägga till användare eller grupper direkt i gruppen.

Förutom att vara ett tillåtet visnings program måste en administrativ användare ha behörigheten **fjärr styrning** för objektet **samling** . Tilldela den här behörigheten genom att använda säkerhets rollen **ansvarig för fjärrverktyg** .  

#### <a name="permissions"></a>Behörigheter
Den här gruppen har som standard inte behörighet för några platser på datorn. Den används endast för att lagra listan över **tillåtna visnings program** .  


### <a name="sms-admins"></a>SMS-administratörer  

Configuration Manager använder den här gruppen för att bevilja åtkomst till SMS-providern via WMI. Åtkomst till SMS-providern krävs för att visa och ändra objekt i Configuration Manager-konsolen.  

> [!NOTE]  
> Den rollbaserade administrations konfigurationen för en administrativ användare bestämmer vilka objekt som de kan visa och hantera när de använder Configuration Manager-konsolen.  

Mer information finns i [Planera för SMS-providern](plan-for-the-sms-provider.md).

#### <a name="type-and-location"></a>Typ och plats
Den här gruppen är en lokal säkerhets grupp som skapas på varje dator som har en SMS-provider. 

När du avinstallerar en plats tas inte gruppen bort automatiskt. Ta bort den manuellt när du har avinstallerat en plats.

#### <a name="membership"></a>Medlemskap
Configuration Manager hanterar grupp medlemskapet automatiskt. Som standard är alla administrativa användare i en hierarki och plats serverdator kontot medlemmar i gruppen **SMS-administratörer** på varje SMS-provider på en plats.

#### <a name="permissions"></a>Behörigheter
Du kan visa rättigheter och behörigheter för gruppen SMS-administratörer i MMC-snapin-modulen **WMI-kontroll** . Som standard beviljas den här gruppen **aktivering av konto** och **fjärraktivering** i `Root\SMS` WMI-namnområdet. Autentiserade användare har behörighet att **köra metoder**, **Provider Skriv**och **Aktivera konto**.

När du använder en fjärran sluten Configuration Manager-konsol konfigurerar du DCOM-behörigheter för **fjärraktivering** på både plats SERVERDATORN och SMS-providern. Bevilja behörighet till **SMS Admins** -gruppen. Den här åtgärden fören klar administrationen i stället för att ge rättigheterna direkt till användare eller grupper. Mer information finns i [Konfigurera DCOM-behörigheter för fjärranslutna Configuration Manager-konsoler](../../servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole). 


### <a name="sms_sitesystemtositeserverconnection_mp_ltsitecode"></a><a name="bkmk_remotemp"></a> SMS_SiteSystemToSiteServerConnection_MP_ &lt; SiteCode\>  
 
Hanterings platser som är fjärranslutna från plats servern använder den här gruppen för att ansluta till plats databasen. Gruppen ger hanteringsplatsåtkomst till inkorgsmapparna på platsservern och platsdatabasen.  

#### <a name="type-and-location"></a>Typ och plats
Den här gruppen är en lokal säkerhets grupp som skapas på varje dator som har en SMS-provider.

När du avinstallerar en plats tas inte gruppen bort automatiskt. Ta bort den manuellt när du har avinstallerat en plats.

#### <a name="membership"></a>Medlemskap
Configuration Manager hanterar grupp medlemskapet automatiskt. Medlemmar är som standard datorkonton för fjärrdatorer som har en hanteringsplats för platsen.

#### <a name="permissions"></a>Behörigheter
Den här gruppen har som standard behörigheterna **läsa**, **läsa & köra**och **Visa** mappinnehåll i följande mapp på plats servern: `C:\Program Files\Microsoft Configuration Manager\inboxes` . Den här gruppen har ytterligare behörighet att **skriva** till undermappar under **inkorgar**, till vilken hanterings platsen skriver klient data.


### <a name="sms_sitesystemtositeserverconnection_smsprov_ltsitecode"></a><a name="bkmk_remoteprov"></a> SMS_SiteSystemToSiteServerConnection_SMSProv_ &lt; SiteCode\>  
 
Fjärranslutna SMS-providers använder den här gruppen för att ansluta till plats servern.  

#### <a name="type-and-location"></a>Typ och plats
Det finns en lokal säkerhetsgrupp för den här gruppen på platsservern.

När du avinstallerar en plats tas inte gruppen bort automatiskt. Ta bort den manuellt när du har avinstallerat en plats.

#### <a name="membership"></a>Medlemskap
Configuration Manager hanterar grupp medlemskapet automatiskt. Som standard inkluderar medlemskap dator kontot eller ett domän användar konto. Det här kontot används för att ansluta till plats servern från varje fjärr-SMS-provider.

#### <a name="permissions"></a>Behörigheter
Den här gruppen har som standard behörigheterna **läsa**, **läsa & köra**och **Visa** mappinnehåll i följande mapp på plats servern: `C:\Program Files\Microsoft Configuration Manager\inboxes` . Den här gruppen har ytterligare behörighet att **skriva** och **ändra** till undermappar under inkorgarna. SMS-providern kräver åtkomst till dessa mappar.

Den här gruppen har också **Läs** behörighet till undermapparna på plats servern nedan `C:\Program Files\Microsoft Configuration Manager\OSD\Bin` . 

Den har också följande behörigheter till undermapparna nedan `C:\Program Files\Microsoft Configuration Manager\OSD\boot` :
- **Läsa**  
- **Läs & kör**  
- **Visa mappinnehåll**  
- **Skriva**  
- **Modify** (Ändra)   


### <a name="sms_sitesystemtositeserverconnection_stat_ltsitecode"></a><a name="bkmk_remotestat"></a> SMS_SiteSystemToSiteServerConnection_Stat_ &lt; SiteCode\>  

Filen Dispatch Manager-komponenten på Configuration Manager fjärrplatssystem använder den här gruppen för att ansluta till plats servern.  

#### <a name="type-and-location"></a>Typ och plats
Det finns en lokal säkerhetsgrupp för den här gruppen på platsservern.

När du avinstallerar en plats tas inte gruppen bort automatiskt. Ta bort den manuellt när du har avinstallerat en plats.

#### <a name="membership"></a>Medlemskap
Configuration Manager hanterar grupp medlemskapet automatiskt. Som standard inkluderar medlemskap dator kontot eller domän användar kontot. Det här kontot används för att ansluta till plats servern från varje fjärrplatssystem som kör fil sändnings hanteraren.

#### <a name="permissions"></a>Behörigheter
Den här gruppen har som standard behörigheterna **läsa**, **läsa & köra**och **Visa** mappinnehåll till följande mapp och dess undermappar på plats servern: `C:\Program Files\Microsoft Configuration Manager\inboxes` . 

Den här gruppen har ytterligare behörighet att **skriva** och **ändra** till följande mapp på plats servern: `C:\Program Files\Microsoft Configuration Manager\inboxes\statmgr.box` .


### <a name="sms_sitetositeconnection_ltsitecode"></a><a name="bkmk_filerepl"></a> SMS_SiteToSiteConnection_ &lt; SiteCode\>  
Configuration Manager använder den här gruppen för att aktivera filbaserad replikering mellan platser i en hierarki. För varje fjärrplats som överför filer direkt till den här platsen, har den här gruppen konton som har kon figurer ATS som ett **filreplikeringsflöde**.  

#### <a name="type-and-location"></a>Typ och plats
Det finns en lokal säkerhetsgrupp för den här gruppen på platsservern.

#### <a name="membership"></a>Medlemskap
När du installerar en ny plats som underordnad till en annan plats, lägger Configuration Manager automatiskt till dator kontot för den nya plats servern i den här gruppen på den överordnade plats servern. Configuration Manager lägger också till den överordnade platsens dator konto i gruppen på den nya plats servern. Om du anger ett annat konto för filbaserade överföringar lägger du till det kontot i gruppen på mål plats servern.

När du avinstallerar en plats tas inte gruppen bort automatiskt. Ta bort den manuellt när du har avinstallerat en plats.

#### <a name="permissions"></a>Behörigheter
Den här gruppen har som standard **fullständig behörighet** till följande mapp: `C:\Program Files\Microsoft Configuration Manager\inboxes\despoolr.box\receive` .



## <a name="accounts-that-configuration-manager-uses"></a><a name="bkmk_accounts"></a> Konton som Configuration Manager använder  

Du kan konfigurera följande konton för Configuration Manager.  

> [!TIP]
> Använd inte procent andelen ( `%` ) i lösen ordet för konton som du anger i Configuration Manager-konsolen. Kontot kan inte autentiseras.<!-- SCCMDocs#1032 -->

### <a name="active-directory-group-discovery-account"></a>Konto för Active Directory grupp identifiering  

Webbplatsen använder kontot för **Active Directory grupp identifiering** för att identifiera följande objekt från de platser i Active Directory Domain Services som du anger:
- Lokala, globala och universella säkerhets grupper
- Medlemskapet i dessa grupper
- Medlemskapet i distributions grupper
  - Distributions grupper identifieras inte som grupp resurser

Det här kontot kan vara ett datorkonto för platsservern som kör identifiering, eller ett Windows-användarkonto. Den måste ha **Läs** behörighet till de Active Directory platser som du anger för identifiering.  

Mer information finns i [Active Directory Group Discovery](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).


### <a name="active-directory-system-discovery-account"></a>Active Directory konto för system identifiering  

Platsen använder **Active Directory system identifierings konto** för att identifiera datorer från de platser i Active Directory Domain Services som du anger.  

Det här kontot kan vara ett datorkonto för platsservern som kör identifiering, eller ett Windows-användarkonto. Den måste ha **Läs** behörighet till de Active Directory platser som du anger för identifiering.  

Mer information finns i [Active Directory system identifiering](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).


### <a name="active-directory-user-discovery-account"></a>Konto för Active Directory användar identifiering  
 
Platsen använder **Active Directory identifierings konto för användare** för att identifiera användar konton från de platser i Active Directory Domain Services som du anger.  

Det här kontot kan vara ett datorkonto för platsservern som kör identifiering, eller ett Windows-användarkonto. Den måste ha **Läs** behörighet till de Active Directory platser som du anger för identifiering.  

Mer information finns i [Active Directory User Discovery](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser). 


### <a name="active-directory-forest-account"></a>Active Directory skogs konto  

Platsen använder **Active Directory skogs konto** för att identifiera nätverks infrastruktur från Active Directory skogar. Centrala administrations platser och primära platser använder också den för att publicera plats data till Active Directory Domain Services för en skog.  

> [!NOTE]  
> Sekundära platser använder alltid den sekundära serverns datorkonto för att publicera till Active Directory.  

För att upptäcka och publicera till obetrodda skogar måste Active Directory skogs konto vara ett globalt konto. Om du inte använder plats serverns dator konto kan du bara välja ett globalt konto.  

Kontot måste ha **läsbehörighet** för varje Active Directory-skog vars nätverksinfrastruktur du vill identifiera.  

Kontot måste ha **fullständig** behörighet till **System Management** -behållaren och alla dess underordnade objekt i varje Active Directory skog där du vill publicera plats data. Mer information finns i [förbereda Active Directory för webbplats publicering](../network/extend-the-active-directory-schema.md).  

Mer information finns i [Active Directory skogs identifiering](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest).


### <a name="certificate-registration-point-account"></a>Konto för certifikat registrerings plats  

Certifikat registrerings platsen använder kontot för **certifikat registrerings platsen** för att ansluta till den Configuration Manager databasen. Den använder sitt dator konto som standard, men du kan konfigurera ett användar konto i stället. När certifikat registrerings platsen finns i en domän som inte är betrodd från plats servern, måste du ange ett användar konto. Det här kontot behöver bara **Läs** behörighet till plats databasen eftersom tillstånds meddelande systemet hanterar Skriv åtgärder.  

Mer information finns i [Introduktion till certifikat profiler](../../../protect/deploy-use/introduction-to-certificate-profiles.md).


### <a name="capture-os-image-account"></a>Avbilda operativ system avbildnings konto  

När du skapar en operativ system avbildning använder Configuration Manager **avbildnings kontot för avbildnings operativ system** för att få åtkomst till mappen där du lagrar insamlade avbildningar. Om du lägger till steget **avbilda operativ Systems avbildning** i en aktivitetssekvens krävs det här kontot.  

Kontot måste ha **Läs** -och **Skriv** behörighet för den nätverks resurs där du lagrar insamlade avbildningar.  

Om du ändrar lösen ordet för kontot i Windows uppdaterar du aktivitetssekvensen med det nya lösen ordet. Den Configuration Manager klienten får det nya lösen ordet nästa gång som klient principen laddas ned.  

Skapa ett domän användar konto om du behöver använda det här kontot. Ge den lägsta behörighet att komma åt de nätverks resurser som krävs och Använd dem för alla aktivitetssekvenser.  

> [!IMPORTANT]  
> Tilldela inte interaktiva inloggnings behörigheter till det här kontot.  
>   
> Använd inte kontot för nätverks åtkomst för det här kontot.  

Mer information finns i [skapa en aktivitetssekvens för att avbilda ett operativ system](../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).


### <a name="client-push-installation-account"></a>Konto för push-installation av klient  

När du distribuerar klienter med hjälp av metoden push-installation av klienter, använder platsen **kontot för push-installation** av klienter för att ansluta till datorer och installera Configuration Manager-klientprogramvaran. Om du inte anger det här kontot försöker plats servern använda sitt dator konto.  

Det här kontot måste vara medlem i den lokala **Administratörs** gruppen på mål klient datorerna. Detta konto kräver inte **domän administratörs** rättigheter.  

Du kan ange mer än ett konto för push-installation av klienter. Configuration Manager försöker var och en i tur och ett lyckas.  

> [!TIP]  
> Om du har en stor Active Directorys miljö och behöver ändra det här kontot, så kan du använda följande process för att effektivt koordinera den här konto uppdateringen: 
> 1. Skapa ett nytt konto med ett annat namn   
> 2. Lägg till det nya kontot i listan över konton för push-installation av klienter i Configuration Manager  
> 3. Tillåt tillräckligt med tid för Active Directory Domain Services att replikera det nya kontot  
> 4. Ta sedan bort det gamla kontot från Configuration Manager och Active Directory Domain Services  

> [!IMPORTANT]  
> Ge inte det här kontot rätt att logga in lokalt.  

Mer information finns i [push-installation av klienter](../../clients/deploy/plan/client-installation-methods.md#client-push-installation).


### <a name="enrollment-point-connection-account"></a>Konto för registrerings plats anslutning  

Registrerings platsen använder **kontot för registrerings plats anslutning** för att ansluta till Configuration Manager plats databasen. Den använder sitt dator konto som standard, men du kan konfigurera ett användar konto i stället. När registrerings platsen finns i en domän som inte är betrodd från plats servern måste du ange ett användar konto. Detta konto kräver **Läs** -och **Skriv** åtkomst till plats databasen.  

Mer information finns i [Installera plats system roller för lokal MDM](../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md).


### <a name="exchange-server-connection-account"></a>Anslutnings konto för Exchange Server  

Plats servern använder **anslutnings kontot för Exchange Server** för att ansluta till den angivna Exchange-servern. Den här anslutningen används för att hitta och hantera mobila enheter som ansluter till Exchange Server. Detta konto kräver Exchange PowerShell cmdlets som förser Exchange Server-datorn med de behörigheter som krävs. Mer information om cmdletarna finns i [Installera och konfigurera Exchange Connector](../../../mdm/deploy-use/install-configure-exchange-connector.md).  


### <a name="management-point-connection-account"></a>Konto för hanterings plats anslutning  

Hanterings platsen använder **hanterings platsens anslutnings konto** för att ansluta till Configuration Manager plats databasen. Den här anslutningen används för att skicka och hämta information för klienter. Hanterings platsen använder sitt dator konto som standard, men du kan konfigurera ett användar konto i stället. När hanterings platsen finns i en domän som inte är betrodd från plats servern måste du ange ett användar konto.  

Skapa kontot som ett lokalt konto med begränsade rättigheter på den dator som kör Microsoft SQL Server.  

> [!IMPORTANT]  
> Bevilja inte interaktiva inloggnings rättigheter till det här kontot.  


### <a name="multicast-connection-account"></a>Konto för multicast-anslutning  

Multicast-aktiverade distributions platser använder **multicast-anslutningens konto** för att läsa information från plats databasen. Servern använder sitt dator konto som standard, men du kan konfigurera ett användar konto i stället. När plats databasen finns i en skog som inte är betrodd måste du ange ett användar konto. Om ditt data Center exempelvis har ett perimeternätverk i en annan skog än plats servern och plats databasen kan du använda det här kontot för att läsa multicast-informationen från plats databasen.  

Om du behöver det här kontot skapar du det som ett lokalt konto med begränsade rättigheter på den dator som kör Microsoft SQL Server.  

> [!IMPORTANT]  
> Bevilja inte interaktiva inloggnings rättigheter till det här kontot.  

Mer information finns i [använda multicast för att distribuera Windows via nätverket](../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).


### <a name="network-access-account"></a>Nätverksåtkomstkonto  

Klient datorer använder **nätverks åtkomst kontot** när de inte kan använda sitt lokala dator konto för att komma åt innehåll på distributions platser. Den gäller främst för arbets grupps klienter och datorer från obetrodda domäner. Det här kontot används också vid distribution av operativ system, när datorn som installerar operativ systemet inte har ett dator konto i domänen.  

> [!Important]  
> Kontot för nätverks åtkomst används aldrig som säkerhets kontext för att köra program, installera program uppdateringar eller köra aktivitetssekvenser. Den används endast för åtkomst till resurser i nätverket.  

En Configuration Manager-klient försöker först använda sitt dator konto för att hämta innehållet. Om det Miss lyckas försöker den automatiskt med nätverks åtkomst kontot.  

Om du konfigurerar platsen för HTTPS eller [Enhanced http](enhanced-http.md)kan en arbets grupp eller Azure AD-ansluten klient på ett säkert sätt komma åt innehåll från distributions platser utan att det behövs något konto för nätverks åtkomst. Det här problemet omfattar distributions scenarier för operativ system med en aktivitetssekvens som körs från startmedia, PXE eller Software Center.<!--1358228,1358278--> Mer information finns i [klient till hanterings plats kommunikation](communications-between-endpoints.md#bkmk_client2mp).<!-- SCCMDocs#1345 -->

> [!Note]  
> Om du aktiverar **utökat http** till att inte kräva kontot för nätverks åtkomst måste distributions platsen köra Windows Server 2012 eller senare. <!--SCCMDocs-pr issue #2696-->
>  
> Uppgradera klienter till minst version 1806 innan du aktiverar den här funktionen. Om du bara tillåter **utökade HTTP-** anslutningar kan äldre klienter inte autentisera med den här metoden, så det går inte att ladda ned klient uppgraderings paketet från en distributions plats. <!--vso2841213-->   

#### <a name="permissions"></a>Behörigheter

Bevilja detta konto de lägsta lämpliga behörigheter för innehållet som klienten behöver för att få åtkomst till programvaran. Kontot måste ha **åtkomst till den här datorn från nätverket** på distributions platsen. Du kan konfigurera upp till tio konton för nätverks åtkomst per plats.  

Skapa kontot i valfri domän som ger nödvändig åtkomst till resurser. Kontot för nätverks åtkomst måste alltid innehålla ett domän namn. Direkt säkerhet stöds inte för det här kontot. Skapa kontot i en betrodd domän om du har distributionsplatser i flera domäner.  

> [!TIP]  
> Undvik konto utelåsning genom att inte ändra lösen ordet för ett befintligt konto för nätverks åtkomst. Skapa i stället ett nytt konto och konfigurera det nya kontot i Configuration Manager. När tillräckligt med tid har förflutit för att alla klienter ska ha tagit emot de nya kontodetaljerna tar du bort det gamla kontot från de delade nätverksmapparna och tar bort kontot.  

> [!IMPORTANT]  
> Bevilja inte interaktiva inloggnings rättigheter till det här kontot.  
>   
> Bevilja inte det här kontot behörighet att ansluta datorer till domänen. Om du måste ansluta datorer till domänen under en aktivitetssekvens använder du det [domän anslutnings konto](#task-sequence-domain-join-account)som används för aktivitetssekvens.  

#### <a name="configure-the-network-access-account"></a>Konfigurera kontot för nätverks åtkomst  

1.  Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** . Välj sedan platsen.  

2.  I gruppen **Inställningar** i menyfliksområdet väljer du **Konfigurera plats komponenter**och välj **program varu distribution**.  

3.  Välj fliken **nätverks åtkomst konto** . Konfigurera ett eller flera konton och välj sedan **OK**.  


### <a name="package-access-account"></a>Paket åtkomst konto  

Med ett **paket åtkomst konto** kan du ange NTFS-behörigheter för att ange de användare och användar grupper som kan komma åt paket innehåll på distributions platser. Som standard beviljar Configuration Manager endast åtkomst till de allmänna åtkomst kontona **användare** och **administratör**. Du kan kontrol lera åtkomsten för klient datorer genom att använda ytterligare Windows-konton eller grupper. Mobila enheter hämtar alltid paket innehåll anonymt, så de använder inte ett paket åtkomst konto.  

När Configuration Manager kopierar innehållsfilerna till en distributions plats beviljas som standard **Läs** behörighet till den lokala gruppen **användare** och **fullständig behörighet** till den lokala **Administratörs** gruppen. De faktiska behörigheter som krävs beror på paketet. Om du har klienter i arbets grupper eller i ej betrodda skogar använder dessa klienter nätverks åtkomst kontot för att komma åt paket innehållet. Kontrol lera att nätverks åtkomst kontot har behörighet till paketet genom att använda de definierade paket åtkomst kontona.  

Använd konton i en domän som kan komma åt distributionsplatserna. Om du skapar eller ändrar kontot när du har skapat paketet måste du distribuera om paketet. Uppdateringen av paketet ändrar inte NTFS-behörigheterna för paketet.  

Du behöver inte lägga till nätverks åtkomst kontot som ett paket åtkomst konto, eftersom medlemskapet i **användar** gruppen lägger till det automatiskt. Om du begränsar paket åtkomst kontot till endast nätverks åtkomst kontot förhindras inte klienter från att komma åt paketet.  

#### <a name="manage-package-access-accounts"></a>Hantera paket åtkomst konton  

1.  Välj **program varu bibliotek**i Configuration Manager-konsolen.  

2.  I arbets ytan **program bibliotek** bestämmer du vilken typ av innehåll som du vill hantera åtkomst konton för och följer de steg som anges:  

    - **Program**: Expandera **program hantering**, Välj **program**och välj sedan det program som du vill hantera åtkomst konton för.  

    - **Paket**: Expandera **program hantering**, Välj **paket**och välj sedan det paket som du vill hantera åtkomst konton för.  

    - **Distributions paket för program uppdatering**: Expandera **program uppdateringar**, Välj **distributions paket**och välj sedan det distributions paket som du vill hantera åtkomst konton för.  

    - **Driv rutins paket**: Expandera **operativ system**, Välj **driv rutins paket**och välj sedan det driv rutins paket som du vill hantera åtkomst konton för.  

    - **OS-avbildning**: Expandera **operativ system**, Välj **operativ Systems**avbildningar och välj sedan den operativ Systems avbildning som du vill hantera åtkomst konton för.  

    - **Uppgraderings paket**för operativ system: Expandera **operativ system**, Välj **uppgraderings paket för operativ system**och välj sedan det uppgraderings paket för operativ system som du vill hantera åtkomst konton för.  

    - **Start avbildning**: Expandera **operativ system**, Välj **Start avbildningar**och välj sedan den Start avbildning som du vill hantera åtkomst konton för.  

3.  Högerklicka på det markerade objektet och välj sedan **Hantera åtkomst konton**.  

4.  I dialog rutan **Lägg till konto** anger du den kontotyp som ska beviljas åtkomst till innehållet och anger sedan åtkomst behörigheterna som är associerade med kontot.  

    > [!NOTE]  
    > När du lägger till ett användar namn för kontot och Configuration Manager hittar både ett lokalt användar konto och ett domän användar konto med det namnet, Configuration Manager anger åtkomst rättigheter för domän användar kontot.  


### <a name="reporting-services-point-account"></a>Konto för repor ting Services-plats  
 
SQL Server Reporting Services använder **repor ting Services-platsens konto** för att hämta data för Configuration Manager-rapporter från plats databasen. Det Windows-användarkonto och -lösenord som du anger krypteras och sparas i SQL Server Reporting Services-databasen.  

> [!NOTE]  
> Kontot som du anger måste ha behörigheten **lokal inloggning** på den dator som är värd för SQL Reporting Services-databasen.

> [!NOTE]  
> Kontot beviljas automatiskt alla nödvändiga rättigheter genom att läggas till i smsschm_users SQL Database-rollen i Configuration Managers databasen.

Mer information finns i [Introduktion till rapportering](../../servers/manage/introduction-to-reporting.md).


### <a name="remote-tools-permitted-viewer-accounts"></a>Konton för tillåtna visnings program för fjärrverktyg  

De konton som du anger som **Betrodda visningsprogram** för fjärrkontroll är en lista över användare som har tillåtelse att använda fjärrverktygsfunktionerna på klienter.  

Mer information finns i [Introduktion till fjärr styrning](../../clients/manage/remote-control/introduction-to-remote-control.md).


### <a name="site-installation-account"></a>Konto för plats installation
<!--SCCMDocs issue #572-->
Använd ett domän användar konto för att logga in på den server där du kör Configuration Manager installationen och installera en ny plats.

Detta konto kräver följande rättigheter:  

- **Administratör** på följande servrar:
    - Plats servern  
    - Varje server som är värd för plats databasen  
    - Varje instans av SMS-providern för platsen  

- **Sysadmin** på den instans av SQL Server som är värd för plats databasen  

Configuration Manager-installationen lägger automatiskt till det här kontot i [SMS Admins](#sms-admins) -gruppen.

Efter installationen är det här kontot den enda användaren med behörighet till Configuration Manager-konsolen. Om du behöver ta bort det här kontot måste du först se till att lägga till dess rättigheter till en annan användare.

När du expanderar en fristående plats för att ta med en central administrations plats kräver det här kontot antingen **Fullständig administratör** eller rollbaserade administrations rättigheter **för administratörer på** den fristående primära platsen.


### <a name="site-system-installation-account"></a>Konto för installation av plats system  

Plats servern använder kontot för **installation av plats system** för att installera, installera om, avinstallera och konfigurera plats system. Om du konfigurerar plats systemet så att plats servern kräver att plats servern initierar anslutningar till det här plats systemet, använder Configuration Manager även det här kontot för att hämta data från plats systemet när plats systemet och eventuella roller har installerats. Varje plats system kan ha ett annat installations konto, men du kan bara konfigurera ett installations konto för att hantera alla roller på plats systemet.  

Detta konto kräver lokal administrativ behörighet på mål plats systemen. Dessutom måste det här kontot ha **åtkomst till den här datorn från nätverket** i säkerhets principen på mål plats systemen.  

> [!TIP]  
> Om du har många domänkontrollanter och dessa konton används över flera domäner måste du kontrol lera att Active Directory har replikerat dessa konton innan du konfigurerar plats systemet.  
>   
> När du anger ett lokalt konto på varje plats system som ska hanteras är denna konfiguration säkrare än att använda domän konton. Den begränsar skadan som angripare kan göra om kontot komprometteras. Domän konton är dock enklare att hantera. Överväg att kompromissa mellan säkerhet och effektiv administration.  


### <a name="site-system-proxy-server-account"></a>Server konto för plats systemets proxyserver
<!--SCCMDocs issue #648-->
Följande plats system roller använder **plats systemets proxy-servernamn** för att få åtkomst till Internet via en proxyserver eller brand vägg som kräver autentiserad åtkomst:

- Plats för synkronisering av tillgångsinformation
- Exchange Server-anslutning
- Tjänstanslutningspunkt
- Programuppdateringsplats

> [!IMPORTANT]  
> Ange ett konto med så få behörigheter som möjligt för den begärda proxyservern eller brandväggen.  

Mer information finns i [stöd för proxy server](../network/proxy-server-support.md).


### <a name="smtp-server-connection-account"></a>Konto för SMTP-server anslutning  

Plats servern använder **SMTP-serverns anslutnings konto** för att skicka e-postaviseringar när SMTP-servern kräver autentiserad åtkomst.  

> [!IMPORTANT]  
> Ange ett konto som har lägsta möjliga behörighet för att skicka e-post.  

Mer information finns i [använda aviseringar och status systemet](../../servers/manage/use-alerts-and-the-status-system.md).


### <a name="software-update-point-connection-account"></a>Anslutnings konto för program uppdaterings plats  

Plats servern använder **anslutnings kontot för program uppdaterings platsen** för följande två program uppdaterings tjänster:  

- Windows Server Update Services (WSUS), som konfigurerar inställningar som produkt definitioner, klassificeringar och överordnade inställningar.  

- WSUS Synchronization Manager, som begär synkronisering till en överordnad WSUS-server eller Microsoft Update.  

[Kontot för installation av plats system](#site-system-installation-account) kan installera komponenter för program uppdateringar, men kan inte utföra program uppdaterings bara funktioner på program uppdaterings platsen. Om du inte kan använda plats serverns dator konto för den här funktionen eftersom program uppdaterings platsen finns i en skog som inte är betrodd måste du ange det här kontot förutom kontot för installation av plats system.  

Kontot måste vara en lokal administratör på den dator där du installerar WSUS. Det måste också vara en del av den lokala gruppen **WSUS-administratörer** .  

Mer information finns i [Planera för program uppdateringar](../../../sum/plan-design/plan-for-software-updates.md).


### <a name="source-site-account"></a>Käll plats konto  

Vid migreringsprocessen används **käll plats kontot** för att komma åt käll PLATSens SMS-provider. Detta konto kräver **läsbehörighet** till platsobjekt på källplatsen för att samla in data för migreringsjobb.  

Om du har Configuration Manager 2007-distributions platser eller sekundära platser med samplacerade distributions platser, måste det här kontot även ha behörighet att **ta bort** om du uppgraderar dem till Configuration Manager (aktuell gren) distributions **platser.** Den här behörigheten är att ta bort distributions platsen från Configuration Manager 2007-platsen under uppgraderingen.  

> [!NOTE]  
> Både käll plats kontot och [käll plats databas kontot](#source-site-database-account) identifieras som **Migration Manager** i noden **konton** i arbets ytan **Administration** i Configuration Manager-konsolen.  

Mer information finns i [migrera data mellan hierarkier](/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="source-site-database-account"></a>Konto för käll plats databas  

Vid migreringsprocessen används **käll plats databas kontot** för att komma åt SQL Server databasen för käll platsen. Om du vill samla in data från käll platsens SQL Server databas måste käll plats databas kontot ha **Läs** -och **Kör** behörighet till käll platsens SQL Server databas.  

Om du använder dator kontot Configuration Manager (aktuell gren) ser du till att alla följande är uppfyllda för det här kontot:  
  
- Den är medlem i den **distribuerade COM-användarens** säkerhets grupp i samma domän som Configuration Manager 2007-platsen  
- Den är medlem i säkerhets gruppen **SMS-administratörer**  
- Den har **Läs** behörighet till alla Configuration Manager 2007-objekt  

> [!NOTE]  
> Både käll plats kontot och [käll plats databas kontot](#source-site-database-account) identifieras som **Migration Manager** i noden **konton** i arbets ytan **Administration** i Configuration Manager-konsolen.  

Mer information finns i [migrera data mellan hierarkier](/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="task-sequence-domain-join-account"></a>Konto för domän anslutning för aktivitetssekvens 

Installationsprogrammet för Windows använder **domän kontot** för aktivitetssekvens för att ansluta en nybildad dator till en domän. Det här kontot krävs av steget [Anslut till domän eller arbets grupp](../../../osd/understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) i aktivitetssekvensen med alternativet **Anslut till en domän** . Det här kontot kan också konfigureras med steget [tillämpa nätverks inställningar](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings) , men det är inte obligatoriskt.  

Det här kontot kräver **domän anslutning** till höger i mål domänen.  

> [!TIP]  
> Skapa ett domän användar konto med de lägsta behörigheterna för att ansluta till domänen och Använd den för alla aktivitetssekvenser.  

> [!IMPORTANT]  
> Tilldela inte interaktiva inloggnings behörigheter till det här kontot.  
>   
> Använd inte kontot för nätverks åtkomst för det här kontot.  


### <a name="task-sequence-network-folder-connection-account"></a>Anslutnings konto för nätverks katalog för aktivitetssekvens  

Motorn för aktivitetssekvenser använder **anslutnings kontot för nätverks katalogen** för att ansluta till en delad mapp i nätverket. Detta konto krävs av steget [Anslut till nätverksmapp](../../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) .  

Kontot måste ha behörighet att komma åt den angivna delade mappen. Det måste vara ett domän användar konto.  

> [!TIP]  
> Skapa ett domän användar konto med lägsta behörighet för att få åtkomst till de nödvändiga nätverks resurserna och Använd dem för alla aktivitetssekvenser.  

> [!IMPORTANT]  
> Tilldela inte interaktiva inloggnings behörigheter till det här kontot.  
>   
> Använd inte kontot för nätverks åtkomst för det här kontot.  


### <a name="task-sequence-run-as-account"></a>Kör som-konto för aktivitetssekvens  

Motorn för aktivitetssekvenser använder **Kör som-kontot för aktivitetssekvens** för att köra kommando rader eller PowerShell-skript med andra autentiseringsuppgifter än det lokala system kontot. Detta konto krävs av [kommando raden kör](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) och [kör PowerShell-skript](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript) med hjälp av instruktioner för att **köra det här steget som följande konto** .  

Konfigurera kontot så att det har de lägsta behörigheter som krävs för att köra kommando raden som du anger i aktivitetssekvensen. Kontot kräver interaktiva inloggnings rättigheter. Det kräver vanligt vis möjlighet att installera program vara och komma åt nätverks resurser. För aktiviteten kör PowerShell-skript krävs lokala administratörs behörigheter. 

> [!IMPORTANT]  
> Använd inte kontot för nätverks åtkomst för det här kontot.  
>   
> Gör aldrig kontot till en domän administratör.  
>   
> Konfigurera aldrig centrala profiler för det här kontot. När aktivitetssekvensen körs laddar den nätverks växlings profilen för kontot. Detta lämnar profilen sårbar för åtkomst på den lokala datorn.  
>   
> Begränsa kontots omfattning. Skapa exempelvis andra kör som-konton för aktivitetssekvens för varje aktivitetssekvens. Om ett konto har komprometterats komprometteras bara de klient datorer som det kontot har åtkomst till.  
>   
> Om kommando raden kräver administrativ åtkomst på datorn kan du överväga att endast skapa ett lokalt administratörs konto för det här kontot på alla datorer där aktivitetssekvensen körs. Ta bort kontot när du inte längre behöver det.  


## <a name="user-objects-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlusers"></a> Användar objekt som Configuration Manager använder i SQL 
<!--SCCMDocs issue #1160-->
Configuration Manager skapar och underhåller automatiskt följande användar objekt i SQL.  De här objekten finns i Configuration Manager-databasen under säkerhet/användare.  

> [!IMPORTANT]  
>  Att ändra eller ta bort dessa objekt kan orsaka drastiska problem inom en Configuration Managers miljö.  Vi rekommenderar att du inte gör några ändringar i dessa objekt.


### <a name="smsdbuser_readonly"></a>smsdbuser_ReadOnly

Det här objektet används för att köra frågor i den skrivskyddade kontexten.  Det här objektet utnyttjas med flera lagrade procedurer.


### <a name="smsdbuser_readwrite"></a>smsdbuser_ReadWrite

Det här objektet används för att ge behörigheter för dynamiska SQL-uttryck.


### <a name="smsdbuser_reportschema"></a>smsdbuser_ReportSchema

Det här objektet används för att köra SQL Reporting-körningar.  Följande lagrade procedur används med den här funktionen: spSRExecQuery.


## <a name="database-roles-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlroles"></a>Databas roller som Configuration Manager använder i SQL
<!--SCCMDocs issue #1160-->
Configuration Manager skapar och underhåller automatiskt följande roll objekt i SQL. De här rollerna ger åtkomst till vissa lagrade procedurer, tabeller, vyer och funktioner för att utföra de åtgärder som krävs för varje roll för att antingen hämta data eller infoga data till och från Configuration Manager databasen. De här objekten finns i Configuration Manager-databasen under säkerhet/roller/databas roller.

> [!IMPORTANT]  
> Att ändra eller ta bort dessa objekt kan orsaka drastiska problem inom en Configuration Managers miljö. Ändra inte de här objekten. Följande lista är endast avsedd som information.

### <a name="smsdbrole_aitool"></a>smsdbrole_AITool

Import av Tillgångsinformation volym licenser. Configuration Manager ger behörighet till användar konton baserat på RBA åtkomst för att kunna importera volym licenser som ska användas med Tillgångsinformation.  Det här kontot kan läggas till av en fullständig administratörs roll eller till en till gångs hanterings roll.

### <a name="smsdbrole_aius"></a>smsdbrole_AIUS

Tillgångsinformation synkronisering av uppdateringar. Configuration Manager beviljar det dator konto som är värd för Tillgångsinformations plats konto för synkronisering för att hämta Tillgångsinformation-Datadata och visa väntande AI-data för uppladdning.

### <a name="smsdbrole_amtsp"></a>smsdbrole_AMTSP

Out-of-band-hantering. Den här rollen används av Configuration Manager AMT-rollen för att hämta data på enheter som har stöd för Intel AMT.

> [!NOTE]  
> Den här rollen är föråldrad i nyare versioner av Configuration Manager.

### <a name="smsdbrole_crp"></a>smsdbrole_CRP

Certifikat registrerings plats som stöder Simple Certificate Enrollment Protocol (SCEP). Configuration Manager beviljar behörighet till dator kontot för det plats system som stöder certifikat registrerings platsen för SCEP-stöd för certifikat signering och förnyelse.

### <a name="smsdbrole_crppfx"></a>smsdbrole_CRPPfx

Certifikat registrerings plats PFX-stöd. Configuration Manager beviljar behörighet till dator kontot för plats systemet som stöder certifikat registrerings platsen som kon figurer ATS för PFX-stöd för signering och förnyelse.

### <a name="smsdbrole_dmp"></a>smsdbrole_DMP

Enhets hanterings plats. Configuration Manager ger behörighet till dator konto för en hanterings plats som har alternativet "Tillåt att mobila enheter och Mac-datorer använder den här hanterings platsen", möjlighet att tillhandahålla stöd för MDM-registrerade enheter.

### <a name="smsdbrole_dmpconnector"></a>smsdbrole_DmpConnector

Tjänst anslutnings punkt. Configuration Manager ger behörighet till det dator konto som är värd för tjänst anslutnings punkten för att hämta och tillhandahålla telemetridata, hantera moln tjänster och hämta uppdateringar av tjänsten.

### <a name="smsdbrole_dviewaccess"></a>smsdbrole_DViewAccess

Distribuerade vyer. Configuration Manager tilldelar den här behörigheten till dator kontot för de primära plats servrarna på certifikat utfärdarna när alternativet SQL Server distribuerade vyer är markerat i egenskaperna för replikeringslänken.

### <a name="smsdbrole_dwss"></a>smsdbrole_DWSS

Informations lager. Configuration Manager beviljar den här behörigheten till det dator konto som är värd för data lager rollen.

### <a name="smsdbrole_enrollsvr"></a>smsdbrole_EnrollSvr

 Registrerings plats. Configuration Manager beviljar den här behörigheten till det dator konto som är värd för registrerings platsen för att tillåta enhets registrering via MDM.

### <a name="smsdbrole_extract"></a>smsdbrole_extract

Ger åtkomst till alla utökade schema vyer.

### <a name="smsdbrole_hmsuser"></a>smsdbrole_HMSUser

Tjänsten för hierarki Manager. Configuration Manager beviljar behörighet att hantera meddelanden för redundans och SQL Server Broker-transaktioner mellan platser i en hierarki.

> [!NOTE]  
> Smdbrole_WebPortal rollen är som standard medlem i den här rollen.

### <a name="smsdbrole_mcs"></a>smsdbrole_MCS

Multicast-tjänst. Configuration Manager tilldelar den här behörigheten till dator kontot för den distributions plats som stöder multicast.

### <a name="smsdbrole_mp"></a>smsdbrole_MP

Hanterings plats. Configuration Manager ger den här behörigheten till det dator konto som är värd för hanterings plats rollen för att ge stöd för Configuration Manager-klienter.

### <a name="smsdbrole_mpmbam"></a>smsdbrole_MPMBAM

Hanterings plats Microsoft BitLocker-administration och övervakning. Configuration Manager ger den här behörigheten till det dator konto som är värd för hanterings platsen som hanterar MBAM för en miljö.

### <a name="smsdbrole_mpusersvc"></a>smsdbrole_MPUserSvc

Program förfrågan för hanterings plats. Configuration Manager ger den här behörigheten till det dator konto som är värd för hanterings platsen som stöd för användarbaserade program begär Anden.

### <a name="smsdbrole_siteprovider"></a>smsdbrole_siteprovider

SMS-provider. Configuration Manager beviljar den här behörigheten till det dator konto som är värd för en SMS-provider.  

### <a name="smsdbrole_siteserver"></a>smsdbrole_siteserver

Plats Server. Configuration Manager beviljar den här behörigheten till det dator konto som är värd för den primära platsen eller CAS-platsen.

### <a name="smsdbrole_sup"></a>smsdbrole_SUP

Program uppdaterings plats. Configuration Manager ger den här behörigheten till det dator konto som är värd för program uppdaterings platsen för att arbeta med uppdateringar från tredje part.

### <a name="smsdbrole_webportal"></a>smsdbrole_WebPortal

Programkatalog webbplats punkt. Configuration Manager beviljar behörighet till det dator konto som är värd för Programkatalog webbplats platsen för att tillhandahålla användarbaserad program distribution.

### <a name="smsschm_users"></a>smsschm_users

Åtkomst till användar rapporter. Configuration Manager beviljar åtkomst till det konto som används för repor ting Services-plats-kontot för att tillåta åtkomst till SMS-rapportvyn för att Visa Configuration Manager rapporterings data.  Data begränsas ytterligare med hjälp av RBA.

## <a name="elevated-permissions"></a>Utökade behörigheter

<!-- SCCMDocs#405 -->

Configuration Manager kräver att vissa konton har utökade behörigheter för pågående åtgärder. Se till exempel [krav för att installera en primär plats](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_PrereqPri). I följande lista sammanfattas de här behörigheterna och skälen till varför de är nödvändiga.

- Dator kontot för den primära plats servern och den centrala administrations plats servern kräver:

  - Lokal administratörs behörighet på alla plats system servrar. Den här behörigheten är att hantera, installera och ta bort system tjänster. Plats servern uppdaterar även lokala grupper på plats systemet när du lägger till eller tar bort roller.

  - Sysadmin-åtkomst till SQL-instansen för plats databasen. Den här behörigheten är att konfigurera och hantera SQL för platsen. Configuration Manager tätt integreras med SQL är det inte bara en databas.

- Användar konton i rollen fullständig administratör kräver:

  - Lokal administratörs behörighet på alla plats servrar. Den här behörigheten är att visa, redigera, ta bort och installera system tjänster, register nycklar och-värden samt WMI-objekt.

  - Sysadmin-åtkomst till SQL-instansen för plats databasen. Den här behörigheten är att installera och uppdatera databasen under installationen eller återställningen. Det krävs också för SQL-underhåll och-åtgärder. Till exempel Omindexering och uppdatering av statistik.

    > [!NOTE]
    > Vissa organisationer kan välja att ta bort sysadmin-åtkomst och bara bevilja det när det behövs. Det här beteendet kallas ibland för "just-in-Time"-åtkomst (JIT). " I det här fallet bör användare med rollen fullständig administratör fortfarande ha åtkomst till läsa, uppdatera och köra lagrade procedurer på Configuration Manager databasen. Dessa behörigheter gör att de kan felsöka de flesta problem utan fullständig sysadmin-åtkomst.