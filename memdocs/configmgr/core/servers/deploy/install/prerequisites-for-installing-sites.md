---
title: Krav för platser
titleSuffix: Configuration Manager
description: Läs om förutsättningar för att installera de olika typerna av Configuration Manager-platser.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a7f7853b006d4ac8b11a30217d1b05b1eedd69dc
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268988"
---
# <a name="prerequisites-for-installing-configuration-manager-sites"></a>Krav för att installera Configuration Manager-platser

*Gäller för: Configuration Manager (aktuell gren)*

Innan du påbörjar en plats installation bör du läsa om förutsättningarna för att installera de olika typerna av Configuration Manager-platser.


## <a name="primary-sites-and-the-central-administration-site"></a>Primära platser och den centrala administrations platsen

Följande krav gäller för att installera någon av följande typer:

- En central administrations plats som den första platsen i en hierarki
- En fristående primär plats
- En underordnad primär plats

Om du installerar en central administrations plats som en del av en hierarki för en hierarki, se [expandera en fristående primär plats](#bkmk_expand).

### <a name="prerequisites-for-installing-a-primary-site-or-a-central-administration-site"></a><a name="bkmk_PrereqPri"></a>Krav för att installera en primär plats eller en central administrations plats  

- De nödvändiga Windows Server-rollerna, funktionerna och Windows-komponenterna måste vara installerade. Mer information finns i [krav för plats system](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012sspreq)  

- Det användar konto som installerar webbplatsen måste ha följande rättigheter:  

    - **Administratör** på följande servrar:  
        - Plats servern  
        - Varje server som är värd för **plats databasen**  
        - Varje instans av **SMS-providern** för platsen  

    - **Sysadmin** på den instans av SQL Server som är värd för plats databasen  

        > [!IMPORTANT]  
        > När Configuration Manager installationen är klar måste plats serverns dator konto behålla sysadmin-behörighet att SQL Server. Ta inte bort SQL sysadmin-rättigheterna från det här kontot.  

    > [!NOTE]
    > Mer information om behovet av de här behörigheterna när installationen är klar finns i [förhöjd behörighet](../../../plan-design/hierarchy/accounts.md#elevated-permissions).

- Om du installerar en primär plats behöver du följande ytterligare rättigheter:  

    - **Administratör** på ytterligare servrar där du installerar den första hanterings platsen och distributions platsen, om inte på plats servern  

- Om du installerar en ny underordnad primär plats under en central administrations plats behöver du följande ytterligare rättigheter:  

    - **Administratör** på den server som är värd för den centrala administrations platsen  

    - Rollbaserade administrations rättigheter inom Configuration Manager som motsvarar säkerhets rollen **infrastruktur administratör** eller **Fullständig administratör**  

- Använd rätt källfiler för installationen och kör installations programmet från den platsen. Information om rätt källfiler som ska användas för att installera olika typer av platser finns i [alternativ för att installera olika typer av platser](prepare-to-install-sites.md#bkmk_options).  

- Plats servern måste ha till gång till uppdaterade installationsfiler från Microsoft på något av följande sätt:  

    - Innan du påbörjar installationen hämtar och lagrar du en kopia av dessa filer i det lokala nätverket. Mer information finns i [installations hämtaren](setup-downloader.md).  

    - Om en lokal kopia av filen inte är tillgänglig måste plats servern ha Internet åtkomst. Filerna hämtas från Microsoft under installationen.  

- Plats servern och plats databas servern måste uppfylla alla nödvändiga konfigurationer. [Kör krav kontrollen manuellt](prerequisite-checker.md) för att identifiera och åtgärda problem innan du påbörjar installationen av Configuration Manager.  

### <a name="prerequisites-to-expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a>Krav för att expandera en fristående primär plats

En fristående primär plats måste uppfylla följande krav innan du kan expandera den till en hierarki med en central administrations plats:

#### <a name="source-file-version-matches-site-version"></a>Käll fil version matchar plats version

Installera den nya centrala administrations platsen med hjälp av media från en CD. Den senaste mappen som matchar versionen av den fristående primära platsen. Om du vill kontrol lera att versionerna stämmer använder du källfilerna som finns på [CD-skivan. Senaste mappen](../../manage/the-cd.latest-folder.md) på den fristående primära platsen.

Mer information om rätt källfiler som ska användas för att installera olika platser finns i [alternativ för att installera olika typer av platser](prepare-to-install-sites.md#bkmk_options).  

#### <a name="stop-active-migration-from-another-hierarchy"></a>Stoppa aktiv migrering från en annan hierarki

Du kan inte konfigurera den fristående primära platsen för att migrera data från en annan Configuration Manager-hierarki. Stoppa aktiv migrering till den fristående primära platsen från andra Configuration Manager hierarkier och ta bort alla konfigurationer för migrering. De här konfigurationerna är:

- Migreringsjobb som inte har slutförts  
- Datainsamling  
- Konfigurationen av den aktiva källhierarkin  

Den här konfigurationen är nödvändig eftersom Configuration Manager migrerar data från platsen på den översta nivån i hierarkin. När du expanderar en fristående primär plats överförs inte konfigurationerna för migrering till den centrala administrations platsen.  

När du har expanderat den fristående primära platsen, utför den centrala administrations platsen migreringen om du konfigurerar om migreringen på den primära platsen.

Mer information om hur du konfigurerar migrering finns i [Konfigurera käll-hierarkier och käll platser för migrering](../../../migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

#### <a name="computer-account-as-administrator"></a>Dator konto som administratör

Dator kontot för den server som är värd för den nya centrala administrations platsen måste vara medlem i gruppen **Administratörer** på den fristående primära plats servern.

För att den fristående primära platsen ska kunna expanderas måste dator kontot för den nya centrala administrations platsen ha **Administratörs** behörighet på den fristående primära platsen. Detta krävs endast under plats expansion. När plats expansionen är klar kan du ta bort kontot från användar gruppen på den primära platsen.  

#### <a name="installation-account-permissions"></a>Installations kontots behörigheter

Det användar konto som kör Configuration Manager installations programmet för att installera den nya centrala administrations platsen måste ha rollbaserade administrations rättigheter på den fristående primära platsen.

Om du vill installera en central administrations plats som en del av en plats expansion måste det användar konto som kör installations programmet för att installera den centrala administrations platsen definieras i rollbaserad administration på den fristående primära platsen som antingen en **Fullständig administratör** eller **infrastruktur administratör**.

Mer information, inklusive den fullständiga listan över nödvändiga behörigheter, finns i [plats installations konto](../../../plan-design/hierarchy/accounts.md#site-installation-account).

#### <a name="top-level-site-roles"></a>Plats roller på den högsta nivån

Innan du expanderar platsen avinstallerar du följande plats system roller från den fristående primära platsen:

- Tillgångsinformation plats för synkronisering  
- Plats för slutpunktsskydd  
- Tjänstanslutningspunkt  

Configuration Manager stöder bara de här rollerna på platsen på den översta nivån i hierarkin. Avinstallera dessa plats system roller innan du expanderar den fristående primära platsen. När du har expanderat platsen installerar du om dessa plats system roller på den centrala administrations platsen.  

Alla andra plats system roller kan vara installerade på den primära platsen.  

#### <a name="open-the-sql-server-service-broker-port"></a>Öppna SQL Server Service Broker port

Nätverks porten måste vara öppen för SQL Server Service Broker (SSB) mellan den fristående primära platsen och servern för den centrala administrations platsen.  

För att kunna replikera data mellan en central administrations plats och en primär plats, kräver Configuration Manager en öppen port mellan de två platserna för att SSB ska kunna användas. När du installerar en central administrations plats och expanderar en fristående primär plats, verifierar inte krav kontrollen att den port som du anger för SSB är öppen på den primära platsen.  

#### <a name="known-issues-with-azure-services"></a>Kända problem med Azure-tjänster

När du har expanderat platsen måste du konfigurera om följande Azure-tjänster med Configuration Manager:

- [Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  
- [Microsoft Store för företag](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  
- [Gateway för molnhantering](../../../clients/manage/cmg/plan-cloud-management-gateway.md)

Det enklaste sättet är att förnya Azure Active Directory-klientens hemliga nyckel. Mer information finns i [förnya hemlig nyckel](../configure/azure-services-wizard.md#bkmk_renew).

Du kan också ta bort och återskapa anslutningen till tjänsten:

1. Ta bort Azure-tjänsten från noden **Azure-tjänster** i Configuration Manager-konsolen.  

2. I Azure Portal tar du bort klienten som är associerad med tjänsten från noden Azure Active Directory klienter. Den här åtgärden tar också bort Azure AD-webbappen som är associerad med tjänsten.  

3. Konfigurera om anslutningen till Azure-tjänsten för användning med Configuration Manager.  


## <a name="secondary-sites"></a><a name="bkmk_secondary"></a>Sekundära platser

Följande är förutsättningar för att installera sekundära platser:  

- De nödvändiga Windows Server-rollerna, funktionerna och Windows-komponenterna måste vara installerade. Mer information finns i [krav för plats system](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012secpreq)  

- Administratören som konfigurerar installationen av den sekundära platsen i Configuration Manager-konsolen måste ha rollbaserade administrations rättigheter som motsvarar säkerhets rollen **infrastruktur administratör** eller **Fullständig administratör**.  

- Dator kontot för den överordnade primära platsen måste vara en **administratör** på den sekundära plats servern.  

- När den sekundära platsen använder en tidigare installerad instans av SQL Server som värd för den sekundära plats databasen:  

    - Dator kontot för den överordnade primära platsen måste ha **sysadmin** -behörighet på instansen av SQL Server på den sekundära plats servern.  

    - Det **lokala system** kontot för den sekundära plats serverdatorn måste ha **sysadmin** -behörighet på instansen av SQL Server på den sekundära plats servern.  

        > [!IMPORTANT]  
        > När Configuration Manager installationen är klar måste båda kontona behålla sysadmin-behörighet att SQL Server. Ta inte bort sysadmin-rättigheterna från dessa konton.  

- Den sekundära plats servern måste uppfylla alla nödvändiga konfigurationer. Dessa konfigurationer omfattar SQL Server och standard plats system roller för hanterings platsen och distributions platsen.  


## <a name="next-steps"></a>Nästa steg

När du har bekräftat kraven är du redo att köra installations programmet. Mer information finns i [använda installations guiden för att installera Configuration Manager-platser](use-the-setup-wizard-to-install-sites.md).
