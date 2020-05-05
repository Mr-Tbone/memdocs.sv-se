---
title: Platsserver hög tillgänglighet
titleSuffix: Configuration Manager
description: Konfigurera hög tillgänglighet för den Configuration Manager plats servern genom att lägga till en plats Server för passivt läge.
ms.date: 02/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 395504f5ccc3635f580bca739f1c4b7273861123
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718310"
---
# <a name="site-server-high-availability-in-configuration-manager"></a>Plats serverns hög tillgänglighet i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

<!--1128774-->

Historiskt sett kan du lägga till redundans till de flesta roller i Configuration Manager genom att ha flera instanser av dessa roller i din miljö. Förutom själva plats servern. Hög tillgänglighet för plats Server rollen är en Configuration Manager-baserad lösning för att installera ytterligare en plats server i *passivt* läge. Den centrala administrations platsen och underordnade primära platser kan ha en ytterligare plats server i passivt läge. Plats servern i passivt läge kan vara lokal eller molnbaserad i Azure.

Den här funktionen ger följande fördelar

- Redundans och hög tillgänglighet till plats Server rollen  
- Det är enklare att ändra plats serverns maskin vara eller operativ system  
- Enklare flytta plats servern till Azure IaaS  

Plats servern i passivt läge är utöver den befintliga plats servern i *aktivt* läge. En plats server i passivt läge är tillgänglig för omedelbar användning vid behov. Ta med den här ytterligare plats servern som en del av den övergripande designen för att göra tjänsten Configuration Manager [hög tillgänglig](high-availability-options.md).  

En plats server i passivt läge:

- Använder samma plats databas som plats servern i aktivt läge.
- Skriver inte data till plats databasen när den är i passivt läge.
- Använder samma innehålls bibliotek som plats servern i aktivt läge.

Om du vill att plats servern i passivt läge ska bli aktiv, *befordra* du den manuellt. Den här åtgärden växlar plats servern i aktivt läge till plats servern i passivt läge. De plats system roller som är tillgängliga på den ursprungliga aktiva läges servern förblir tillgängliga så länge datorn är tillgänglig. Endast plats Server rollen växlar mellan aktiva och passiva lägen.

Microsoft Core Services-teknik och-åtgärder använde den här funktionen för att migrera den centrala administrations platsen till Microsoft Azure. Mer information finns i [artikeln Microsoft IT Showcase](https://www.microsoft.com/itshowcase/Article/Content/1065/Migrating-System-Center-Configuration-Manager-onpremises-infrastructure-to-Microsoft-Azure).

## <a name="prerequisites"></a>Krav

- Plats innehålls biblioteket måste finnas på en fjärran sluten nätverks resurs. Både plats servrar måste ha fullständig behörighet till resursen och dess innehåll. Mer information finns i [Hantera innehålls bibliotek](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote).<!--1357525-->  

  - Plats serverns dator konto måste ha **fullständig** behörighet till nätverks Sök vägen som du flyttar innehålls biblioteket till. Den här behörigheten gäller både resursen och fil systemet. Inga komponenter är installerade på fjärrdatorn.

  - Plats servern kan inte ha distributions plats rollen. Innehålls biblioteket används också av distributions platsen, och den här rollen stöder inte ett innehålls bibliotek för fjärrnätverk. När du har flyttat innehålls biblioteket kan du inte lägga till distributions plats rollen på plats servern.  

- Plats servern i passivt läge kan vara lokal eller molnbaserad i Azure.  

    > [!NOTE]
    > En molnbaserad plats server i passivt läge använder Azure Infrastructure as a Service (IaaS). Mer information finns i följande artiklar:
    >
    >   - [Virtuella Azure-datorer (för molnbaserad infrastruktur)](../../../understand/use-cloud-services.md#azure-virtual-machines-for-cloud-based-infrastructure)
    >   - [Vanliga frågor och svar om Configuration Manager på Azure](../../../understand/configuration-manager-on-azure.md)  

- Båda plats servrarna måste vara anslutna till samma Active Directory-domän.  

- Configuration Manager stöder plats servrar i passivt läge i en hierarki. Den centrala administrations platsen och underordnade primära platser kan ha en ytterligare plats server i passivt läge.<!-- 3607755 -->  

- Båda plats servrarna måste använda samma plats databas.  

  - Databasen kan vara fjärran sluten till varje plats Server. Från och med version 1810 blockerar Configuration Manager installations processen inte längre installationen av plats Server rollen på en dator med Windows-rollen för redundanskluster. SQL Always on kräver den här rollen, så det var tidigare att du inte kunde hitta plats databasen på plats servern. Med den här ändringen kan du skapa en plats med hög tillgänglighet med färre servrar med hjälp av SQL Always on och en plats server i passivt läge.<!-- SCCMDocs issue 1074 -->  

  - SQL Server som är värd för plats databasen kan använda en standard instans, namngiven instans, [SQL Server kluster](use-a-sql-server-cluster-for-the-site-database.md)eller en [SQL Server Always on-tillgänglighetsgrupper](sql-server-alwayson-for-a-highly-available-site-database.md).  

  - Både plats servrar behöver säkerhets rollen **sysadmin** på instansen av SQL Server som är värd för plats databasen. Den ursprungliga plats servern bör redan ha dessa roller, så Lägg till dem för den nya plats servern. Följande SQL-skript lägger till exempel till dessa roller för den nya plats servern **VM2** i Contoso-domänen:  

    ```SQL
    USE [master]
    GO
    CREATE LOGIN [contoso\vm2$] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
    GO
    ALTER SERVER ROLE [sysadmin] ADD MEMBER [contoso\vm2$]
    GO
    ```

  - Båda plats servrarna måste ha åtkomst till plats databasen på instansen av SQL Server. Den ursprungliga plats servern bör redan ha den här åtkomsten, så Lägg till den för den nya plats servern. Följande SQL-skript lägger till exempel till en inloggning till **CM_ABC** databasen för den nya plats servern **VM2** i Contoso-domänen:  

    ```SQL
    USE [CM_ABC]
    GO
    CREATE USER [contoso\vm2$] FOR LOGIN [contoso\vm2$] WITH DEFAULT_SCHEMA=[dbo]
    GO
    ```

  - Plats servern i passivt läge är konfigurerad att använda samma plats databas som plats servern i aktivt läge. Plats servern i passivt läge läser endast från databasen. Den skriver inte till databasen förrän den befordras till aktivt läge.  

- Plats servern i passivt läge:  

  - Måste uppfylla kraven för att installera en primär plats. Till exempel .NET Framework, fjärrdifferentiell komprimering och Windows ADK. En fullständig lista finns i [krav för plats och plats system](../../../plan-design/configs/site-and-site-system-prerequisites.md).<!-- SCCMDocs issue 765 -->  

    > [!NOTE]
    > Se till att installera SQL Server Native Client. Om du inte installerar den, rapporterar krav kontrollen under Configuration Manager installations programmet ett fel om SQL Server behörigheter som saknas.<!-- SCCMDocs#2290 -->

  - Måste ha sitt dator konto i den lokala administratörs gruppen på plats servern i aktivt läge.<!--516036-->

  - Måste installera med källfiler som matchar versionen av plats servern i aktivt läge.  

  - Det går inte att ha en plats system roll från någon plats som är installerad innan du installerar plats servern i passivt läge.  

- Båda plats servrarna kan köra olika operativ system eller service pack-versioner, så länge båda [stöds av Configuration Manager](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).  

- Var inte värd för tjänst anslutnings punkt rollen på någon plats server som kon figurer ATS för hög tillgänglighet. Om den är på den ursprungliga plats servern tar du bort den och installerar den på en annan plats system Server. Mer information finns i [om tjänst anslutnings punkten](about-the-service-connection-point.md).  

- Behörigheter för [plats systemets installations konto](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)  

  - Som standard använder många kunder plats serverns dator konto för att installera nya plats system. Kravet är sedan att lägga till plats serverns dator konto i den lokala gruppen **Administratörer** på fjärrplatssystemet. Om din miljö använder den här konfigurationen ska du se till att lägga till dator kontot för den nya plats servern i den lokala gruppen på alla fjärranslutna plats system. Till exempel alla fjärranslutna distributions platser.  

  - Den säkrare och rekommenderade konfigurationen är att använda ett tjänst konto för att installera plats systemet. Den säkraste konfigurationen är att använda ett lokalt tjänst konto. Om din miljö använder den här konfigurationen behövs ingen ändring.  

## <a name="limitations"></a>Begränsningar

- Det finns bara stöd för en enda plats server i passivt läge på varje plats.  

- En plats server i passivt läge stöds inte på en sekundär plats.<!--SCCMDocs issue 680-->  

    > [!NOTE]  
    > Sekundära platser stöds fortfarande under en primär plats med plats servrar med hög tillgänglighet.

- Befordran av plats servern i passivt läge till aktivt läge är manuell. Det finns ingen automatisk redundans.  

- Det går inte att installera plats system roller på den nya servern innan du lägger till plats servern i passivt läge.  

    > [!NOTE]
    > När plats servern har installerats i passivt läge kan du lägga till ytterligare roller vid behov. Till exempel en hanterings plats på en primär plats.

- För roller som den rapporterings plats som använder en databas, ska du vara värd för databasen på en server som är fjärran sluten från båda plats servrarna.  

- Configuration Manager-konsolen installeras inte automatiskt på plats servern i passivt läge.  

## <a name="add-a-site-server-in-passive-mode"></a>Lägga till en plats server i passivt läge

Mer information om allmänna processer för att lägga till roller finns i [Installera plats system roller](install-site-system-roles.md).

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**, välj noden **platser** och klicka på **skapa plats system Server** i menyfliksområdet.

2. På sidan **Allmänt** i guiden skapa plats system server anger du den server som ska vara värd för plats servern i passivt läge. Den server du anger kan inte vara värd för några plats system roller innan du installerar en plats server i passivt läge.  

3. På sidan **urval för system roll** väljer du endast **plats server i passivt läge**.  

    > [!NOTE]  
    > Guiden utför följande inledande krav kontroller på den här sidan:
    >
    > - Den valda servern är inte en sekundär plats Server
    > - Den valda servern är inte redan en plats server i passivt läge
    > - Platsens innehålls bibliotek finns på en fjärran sluten plats  
    >  
    > Om dessa inledande krav kontroller Miss lyckas kan du inte fortsätta att gå förbi den här sidan i guiden.  

4. På sidan **plats server i passivt läge** anger du följande information som används för att köra installations programmet och installerar plats Server rollen på den angivna servern:

     - Välj ett av följande alternativ:  

         - **Kopiera installationskällfilerna över nätverket från plats servern i aktivt läge**: det här alternativet skapar ett komprimerat paket och skickar det till den nya plats servern.  

         - **Använd källfilerna på följande plats på plats servern i passivt läge**: till exempel en lokal sökväg som du redan har kopierat källfilerna till. Se till att det här innehållet är samma version som plats servern i aktivt läge.  

         - (*Rekommenderas*) **Använd källfilerna på följande nätverks plats**: Ange sökvägen direkt till innehållet på **CD: n. Den senaste** mappen från plats servern i aktivt läge. Till exempel, `\\Server\SMS_ABC\CD.Latest` där "*Server*" är namnet på plats servern i aktivt läge och "*ABC*" är plats koden.  

     - Ange den lokala sökväg där du vill installera Configuration Manager på den nya plats servern. Exempelvis: `C:\Program Files\Configuration Manager`  

5. Slutför guiden. Configuration Manager installerar sedan plats servern i passivt läge på den angivna servern.

Om du vill ha en detaljerad installations status går du till arbets ytan **övervakning** i-konsolen och väljer noden **plats Server status** . Status för plats servern i passivt läge visas som **installation**. Om du vill ha mer detaljerad information markerar du servern och klickar på **Visa status**. Den här åtgärden öppnar fönstret installations status för plats Server. När processen har slutförts visar statusen **OK** för båda servrarna.

Mer information om installations processen finns i [flödesschema – konfigurera en plats server i passivt läge](passive-site-server-flowchart.md).

När du har lagt till en plats server i passivt läge, se båda plats servrarna på fliken **noder** i noden **platser** i-konsolen.

Alla Configuration Manager plats Server komponenter är i vänte läge på plats servern i passivt läge. Windows-tjänsterna körs fortfarande.

## <a name="site-server-promotion"></a>Befordran av plats Server  

På samma sätt som med säkerhets kopiering och återställning, planera och öva på processen att ändra plats servrar. Tänk på följande i din kampanj plan:  

- Öva en planerad befordran där båda plats servrarna är online. Öva också på en oplanerad redundansväxling genom att tvinga bort eller stänga av plats servern i aktivt läge.  

- Fastställ drifts processerna under redundansväxling och vad som ska ske med andra Configuration Manager-administratörer.  

- Före en planerad befordran:  

  - Kontrol lera den övergripande statusen för plats-och plats komponenterna. Kontrol lera att allt är felfritt som normalt för din miljö.  

  - Kontrol lera innehålls status för alla paket som replikeras aktivt mellan platser.  

  - Kontrol lera status för sekundär plats och plats replikering.

  - Starta inga nya innehålls distributions jobb eller underhåll på underordnade eller sekundära plats servrar.

    > [!NOTE]
    > Om fil-eller databasreplikering mellan platser pågår under redundansväxlingen, kan den nya plats servern inte ta emot det replikerade innehållet. Om detta inträffar distribuerar du om program innehållet när den nya plats servern är aktiv.<!--515436--> Vid databasreplikering kan du behöva initiera om en sekundär plats efter redundansväxlingen.<!-- SCCMDocs issue 808 -->

  - Minska eller ta bort andra schemalagda aktiviteter på samma tid. Planera till exempel inte att befordra en plats Server direkt efter att platsen har uppdaterats till en ny version. Plats uppdateringen innehåller andra uppgifter som kan vara motstridiga med plats Server befordran.

    > [!TIP]
    > Här är ett exempel på hur andra aktiviteter kan vara i konflikt med plats Server befordran:
    >
    > - Måndag: uppdatera platsen till den senaste versionen. Aktivera automatisk klient uppgradering med klient pilotering.
    > - Tisdag: flytta plats servern i passivt läge till den aktiva plats servern.
    >
    > I onsdag eller torsdag kan den här åtgärden orsaka att *alla* klienter uppgraderas, inte bara pilot samlingen. Det här beteendet kan orsaka betydande nätverks användning och oväntad belastning på distributions platserna.<!-- SCCMDocs-pr#4794 -->

### <a name="process-to-promote-the-site-server-in-passive-mode-to-active-mode"></a>Process för att befordra plats servern i passivt läge till aktivt läge

I det här avsnittet beskrivs hur du ändrar plats servern i passivt läge till aktivt läge. Du måste ha åtkomst till en instans av SMS-providern för att kunna komma åt platsen och göra den här ändringen. Mer information finns i [använda flera SMS-providers](../../../plan-design/hierarchy/plan-for-the-sms-provider.md#BKMK_MultiSMSProv).  

> [!IMPORTANT]  
> Om alla instanser av SMS-providern är offline kan du inte ansluta till platsen eftersom ingen Provider är tillgänglig. När du lägger till plats servern i passivt läge installerar installations programmet en instans av SMS-providern på den här servern.<!-- SCCMDocs#1613 -->
>
> Configuration Manager-konsolen begär listan över tillgängliga SMS-providers från WMI på plats servern. När du installerar flera SMS-providrar på en plats tilldelar webbplatsen slumpmässigt varje ny anslutningsbegäran för att använda en installerad SMS-provider. Du kan inte ange platsen för SMS-providern som ska användas med en speciell session. Om konsolen inte kan ansluta till platsen eftersom den aktuella plats servern är offline, anger du den andra plats servern i fönstret plats anslutning.  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** . Välj platsen och växla sedan till fliken **noder** . Välj plats servern i passivt läge och klicka sedan på **befordra till aktiv** i menyfliksområdet. Bekräfta och Fortsätt genom att klicka på **Ja** .
  
2. Uppdatera-noden i konsolen. **Status** kolumnen för den server som du ska befordra visas på fliken **noder** som **befordran**.  

3. När befordran är slutförd visas i kolumnen **status** **OK** för både den nya plats servern i aktivt läge och för den nya plats servern i passivt läge. I kolumnen **Server namn** för platsen visas nu namnet på den nya plats servern i aktivt läge.

Om du vill ha detaljerad status går du till arbets ytan **övervakning** och väljer noden **plats Server status** . I kolumnen **mode** identifieras vilken server som är *aktiv* eller *passiv*. När du befordrar en server från passivt läge till aktivt läge väljer du den plats server som du befordrar till aktiv och väljer sedan **Visa status** från menyfliksområdet. Den här åtgärden öppnar fönstret plats Server befordran status som visar mer information om processen.

När en plats server i aktivt läge växlar över till passivt läge görs bara plats system rollen som passiv. Alla andra plats system roller som är installerade på den datorn förblir aktiva och tillgängliga för klienter.

Mer information om *planerad* befordran-processen finns i [flödesschema – befordra plats Server (planerat)](promote-site-server-flowchart.md).

### <a name="unplanned-failover"></a>Oplanerad redundans

Om den aktuella plats servern i aktivt läge är offline försöker plats servern för befordran att kontakta den aktuella plats servern i aktivt läge i 30 minuter. Om den frånkopplade servern kommer tillbaka före den här tiden, har den fått ett meddelande och ändringen fortsätter att vara korrekt. Annars tvingas plats servern för befordran att uppdatera plats konfigurationen så att den aktive ras. Om offline-servern kommer tillbaka efter den här tiden kontrollerar den först det aktuella läget i plats databasen. Den fortsätter sedan med att degradera till plats servern i passivt läge.

Under denna 30 minuters vänte tid har platsen ingen plats server i aktivt läge. Klienterna kommunicerar fortfarande med klientbaserade roller som hanterings platser, program uppdaterings platser och distributions platser. Användare kan installera program vara som redan har distribuerats. Det går inte att utföra någon plats administration under den här tids perioden. Mer information finns i [plats haveri påverkan](../../manage/site-failure-impacts.md).  

Om offline-servern är skadad så att den inte kan returnera tar du bort den här plats servern från-konsolen. Skapa sedan en ny plats server i passivt läge för att återställa en tjänst med hög tillgänglighet.

Mer information om den *oplanerade* redundansväxlingen finns i [flödesschema – befordra plats Server (oplanerad)](promote-site-server-unplanned-flowchart.md).

### <a name="additional-tasks-after-site-server-promotion"></a>Ytterligare aktiviteter efter befordran av plats Server  

När du har växlat plats servrar behöver du inte göra de flesta andra uppgifter som behövs när du [återställer en plats](../../manage/recover-sites.md#post-recovery-tasks). Du behöver till exempel inte återställa lösen ord eller återansluta Microsoft Intune prenumerationen.

Följande steg kan krävas om det behövs i din miljö:  

- Om du importerar PKI-certifikat för distributions platser importerar du om certifikatet för berörda servrar. Mer information finns i [Återskapa certifikat för distributions platser](../../manage/recover-sites.md#regenerate-the-certificates-for-distribution-points).  

- Om du integrerar Configuration Manager med Microsoft Store för företag kan du konfigurera om anslutningen. Mer information finns i [Hantera appar från Microsoft Store för företag](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).  

## <a name="daily-monitoring"></a>Daglig övervakning

När du har en plats server i passivt läge kan du övervaka den dagligen. Kontrol lera att statusen är OK och att den är klar att användas. I Configuration Manager-konsolen går du till arbets ytan **övervakning** och väljer noden **plats Server status** . Visa både plats servrar och deras aktuella status. Visa också status i arbets ytan **Administration** . Expandera **plats konfiguration**och välj noden **platser** . Välj platsen och växla sedan till fliken **noder** .

> [!NOTE]
> När du uppdaterar platsen till en ny version av Configuration Manager, uppdaterar den också plats servern i passivt läge. <!-- SCCMDocs-pr#4293 -->