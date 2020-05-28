---
title: Krav för migrering
titleSuffix: Configuration Manager
description: Förstå de versioner av Configuration Manager som stöds, stöd för käll plats språk som stöds och konfigurationer som krävs för migrering.
ms.date: 05/7/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec976930-7467-4d3c-b33c-991bf408a74a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 36e62ea5198824a6b3466853cdbcfc3057d1829e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428727"
---
# <a name="prerequisites-for-migration-in-configuration-manager"></a>Krav för migrering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Om du vill migrera från en källhierarki som stöds måste du ha åtkomst till varje tillämplig Configuration Manager käll plats och behörigheter på Configuration Manager målplats för att kunna konfigurera och köra migreringsåtgärder.  

 Använd informationen i följande avsnitt för att få hjälp att förstå de versioner av Configuration Manager som stöds för migrering och de konfigurationer som krävs.  

-   [Versioner av Configuration Manager som stöds för migrering](#BKMK_SupportedMigrationVersions)  

-   [Källplatsspråk som stöds för migrering](#BKMK_SorceSiteLanguage)  

-   [Konfigurationer som krävs för migrering](#BKMK_Required_Configurations)  

##  <a name="versions-of-configuration-manager-that-are-supported-for-migration"></a><a name="BKMK_SupportedMigrationVersions"></a>Versioner av Configuration Manager som stöds för migrering  
 Du kan migrera data från en-källhierarki som kör någon av följande versioner av Configuration Manager:  

- Configuration Manager 2007 SP2 (för migreringen är Configuration Manager 2007 R2 eller R3 på käll platsen inte några överväganden. Så länge käll platsen kör SP2 stöds platser med antingen R2-eller R3-tillägget installerat för migrering till Configuration Manager aktuella grenen).  

- System Center 2012 Configuration Manager SP2 eller System Center 2012 R2 Configuration Manager SP1.  

  > [!TIP]  
  >  Förutom migrering kan du använda en uppgradering på plats av platser som kör System Center 2012 Configuration Manager för att Configuration Manager aktuella grenen.  

- En Configuration Manager-hierarki med samma eller lägre version av Configuration Manager.  

  Om du till exempel har en målkö som kör Configuration Manager nuvarande gren 1606 kan du använda migrering för att kopiera data från en källhierarki som kör version 1606 eller 1602. Du kan dock inte migrera data från en-källhierarki som kör 1610.  


##  <a name="source-site-languages-that-are-supported-for-migration"></a><a name="BKMK_SorceSiteLanguage"></a>Käll plats språk som stöds för migrering  
 När du migrerar data mellan Configuration Manager hierarkier lagras data i målhierarkin i språkneutralt format för Configuration Manager. Eftersom Configuration Manager 2007 inte lagrar data i ett språkneutralt format måste migreringsprocessen omvandla objekt till det här formatet under migreringen från Configuration Manager 2007. Därför stöds endast Configuration Manager 2007-käll platser som är installerade med följande språk för migrering:  

-   Engelska  

-   Franska  

-   Tyska  

-   Japanska  

-   Koreanska  

-   Ryska  

-   Förenklad kinesiska  

-   Traditionell kinesiska  

När du migrerar data från ett System Center 2012 Configuration Manager eller Configuration Manager aktuell Branch-hierarki finns inga språk begränsningar för käll platsen. Objekten i källplatsens databas har redan ett språkneutralt format.  

##  <a name="required-configurations-for-migration"></a><a name="BKMK_Required_Configurations"></a>Konfigurationer som krävs för migrering  
Följande är obligatoriska konfigurationer för att använda migrering och migrering:  

- **Konfigurera, köra och övervaka migrering i Configuration Manager-konsolen:**  

   På målplatsen måste ditt konto ha tilldelats den rollbaserade administrationssäkerhetsrollen **Infrastrukturadministratör**. Den här säkerhetsrollen ger behörighet att hantera alla migreringsåtgärder,vilket innefattar att skapa, rensa och övervaka migreringsjobb samt åtgärden att dela och uppgradera distributionsplatser.  

- **Datainsamling:**  

   För att destinationsplatsen ska kunna samla in data måste du konfigurera följande två källplatskonton för användning med varje källplats:  

  -   **Källplatskonto** : Det här kontot används för att ge åtkomst till källplatsens SMS-provider.  

      -   För en Configuration Manager 2007 SP2-käll plats kräver det här kontot **Läs** behörighet till alla käll plats objekt.  

      -   För en System Center 2012 Configuration Manager eller Configuration Manager aktuella gren käll platsen måste det här kontot ha **Läs** behörighet till alla käll plats objekt. du beviljar behörigheten till kontot genom att använda rollbaserad administration. Information om hur du använder rollbaserad administration finns i [grunderna i rollbaserad administration för Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

  -   **Konto för källplatsdatabas** : Det här kontot används för att ge åtkomst till källplatsens SQL Server-databas och kräver behörigheterna **Anslutning**, **Kör**och **Välj** för källplatsens databas.  

  Du kan konfigurera de här kontona när du konfigurerar en ny källhierarki, datainsamling för en ytterligare källplats eller när du omkonfigurerar autentiseringsuppgifterna för en källplats. De här kontona kan använda ett domänanvändarkonto eller så kan du specificera datorkonot för toppnivåplatsen i källhierarkin.  

  > [!IMPORTANT]  
  >  Om du använder Configuration Manager dator konto för något av åtkomst kontona måste du se till att det här kontot är medlem i säkerhets gruppen **distribuerade COM-användare** i den domän där käll platsen finns.  

  Följande nätverksprotokoll och portar används vid datainsamling:  

  - NetBIOS/SMB-445 (TCP)  

  - RPC (WMI) – 135 (TCP & UDP)  

  - Dynamiskt RPC. Dynamiska portar använder ett intervall med port nummer som definieras av operativ Systems versionen. Dessa portar kallas även tillfälliga portar. Mer information om standardportintervallen finns i [Tjänstöversikt och krav på nätverksportar för Windows Server-systemet](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).<!-- SCCMDocs#1053 -->

  - SQL Server – TCP-portarna som används av både käll- och målplatsdatabaserna.  

- **Migrera programuppdateringar:**  

   Innan du migrerar programuppdateringar måste du konfigurera målhierarkin med en programuppdateringsplats. Mer information om hur du planerar för programuppdateringar finns i [Planera migrering av programuppdateringar](../../core/migration/planning-for-the-migration-of-objects.md#Plan_migrate_Software_updates).  

- **Dela distributionsplatser:**  

   För att det ska gå att dela distributionsplatser från en källplats måste minst en primär plats eller central administrationsplats i målhierarkin använda samma portnummer för klientbegäranden som källplatsen. Information om klient begär ande portar finns i [så här konfigurerar du klient kommunikations portar](../../core/clients/deploy/configure-client-communication-ports.md)  

   Det är endast de distributionsplatser som är installerade på platssystemservrar som är konfigurerade med ett fullständigt domännamn som delas för varje källplats.  

   För att dela en distributions plats från ett System Center 2012 Configuration Manager eller Configuration Manager aktuella gren käll platsen, måste **käll plats kontot** (som ansluter till SMS-providern för käll plats servern) ha behörighet att **ändra** **plats** objekt på käll platsen. Du tilldelar den här behörigheten till kontot genom rollbaserad administration. Information om hur du använder rollbaserad administration finns i [grunderna i rollbaserad administration för Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  


- **Uppgradera eller tilldela om distributionsplatser:**  

   Det **Åtkomstkonto för källplats** som konfigurerats att samla in data från källplatsens SMS-provider måste ha följande behörigheter:  

  - För att uppgradera en Configuration Manager 2007-distributions plats måste kontot ha behörigheterna **läsa**, **köra**och **ta bort** **för att kunna** ta bort distributions platsen från Manager2007 käll plats för konfigurations Manager2007.  

  - Om du vill omtilldela ett System Center 2012 Configuration Manager eller Configuration Manager aktuell gren distributions plats måste kontot ha behörigheten **ändra** till objektet **plats** på käll platsen. Du tilldelar den här behörigheten till kontot genom rollbaserad administration. Information om hur du använder rollbaserad administration finns i [grunderna i rollbaserad administration för Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

    För att det ska gå att uppgradera eller omtilldela en distributionsplats till en ny hierarki måste de portar som är konfigurerade för klientbegäranden på platsen som hanterar distributionsplatsen i källhierarkin matcha de portar som är konfigurerade för klientbegäranden på målplatsen som hanterar distributionsplatsen. Information om klient begär ande portar finns i [så här konfigurerar du klient kommunikations portar](../../core/clients/deploy/configure-client-communication-ports.md).  
