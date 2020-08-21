---
title: Konfigurera rapporter
titleSuffix: Configuration Manager
description: Konfigurera rapportering i Configuration Manager-hierarkin, inklusive information om SQL Server Reporting Services.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e53c61052b8ee1b217a5268e8877dc4f4415f477
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692629"
---
# <a name="configure-reporting-in-configuration-manager"></a>Konfigurera rapportering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Innan du kan skapa, ändra och köra rapporter i Configuration Manager-konsolen finns det flera konfigurations uppgifter att slutföra. Använd den här artikeln för att konfigurera rapportering i Configuration Manager hierarkin.  

Innan du installerar och konfigurerar SQL Server Reporting Services i din-hierarki kan du läsa följande Configuration Manager rapporterings artiklar:  

- [Introduktion till rapportering](introduction-to-reporting.md)  

- [Planera för rapportering](planning-for-reporting.md)  

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services är en serverbaserad rapport plattform som tillhandahåller omfattande rapporterings funktioner för olika typer av data källor. Repor ting Services-platsen i Configuration Manager kommunicerar med SQL Server Reporting Services till:

- Kopiera Configuration Manager rapporter till en angiven rapportmapp
- Konfigurera inställningar för repor ting Services
- Konfigurera säkerhets inställningar för repor ting Services

När du kör en rapport ansluter repor ting Services-komponenten till Configuration Manager plats databasen för att hämta data.  

Innan du kan installera repor ting Services-platsen på en Configuration Manager plats måste du installera och konfigurera SQL Server Reporting Services på mål plats systemet. Mer information finns i [installera SQL Server Reporting Services](/sql/reporting-services/install-windows/install-reporting-services).  

### <a name="verify-sql-server-reporting-services-installation"></a>Verifiera SQL Server Reporting Services-installationen

Kontrollera att SQL Server Reporting Services är installerat och körs korrekt på följande sätt.

1. Gå till **Start** -menyn på plats systemet och öppna **repor ting Services-Configuration Manager**. Det kan finnas i avsnittet **Konfigurationsverktyg** i **Microsoft SQL Servers** gruppen.

2. I fönstret **konfigurations anslutning för repor ting Services** anger du namnet på den server som är värd för SQL Server Reporting Services. Välj den instans av SQL Server som du installerade SQL Reporting-tjänster på. Välj sedan **Anslut** för att öppna repor ting Services-Configuration Manager.  

3. På sidan **rapport Server status** kontrollerar du att **status för rapport tjänsten** har **startats**. Om den inte är i det här läget väljer du **Starta**.  

4. På sidan **URL för webb tjänst** väljer du webb adressen i **URL: en för webb tjänst för rapport tjänst**. Den här åtgärden testar anslutningen till rapportmappen. Webbläsaren kanske uppmanas att ange autentiseringsuppgifter. Kontrollera att webbsidan visas som den ska.

5. På sidan **databas** kontrollerar du att **Report Server-läget** har angetts till **Native**.  

6. På sidan **RAPPORTHANTERAREN URL** väljer du URL: en i **Rapporthanteraren plats identifiering**. Den här åtgärden testar anslutningen till den virtuella katalogen för Rapporthanteraren. Webbläsaren kanske uppmanas att ange autentiseringsuppgifter. Kontrollera att webbsidan visas som den ska.

    > [!NOTE]  
    > Rapportering i Configuration Manager kräver inte repor ting Services-Rapporthanteraren. Du behöver bara den om du vill köra rapporter i webbläsaren eller hantera rapporter med hjälp av Rapporthanteraren.  

7. Välj **Avsluta** för att stänga repor ting Services-Configuration Manager.  

## <a name="configure-reporting-to-use-report-builder-30"></a>Konfigurera rapporter för att använda Report Builder 3,0

1. Öppna Registereditorn i Windows på den dator som kör Configuration Manager-konsolen.  

2. Gå till `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\ConfigMgr10\AdminUI\Reporting`.

3. Öppna **nyckeln ReportBuilderApplicationManifestName** -nyckeln för att redigera värde data.  

4. Ändra värdet till `ReportBuilder_3_0_0_0.application` och välj sedan **OK** för att spara.

5. Stäng Registereditorn.  

## <a name="install-a-reporting-services-point"></a>Installera en Reporting Services-plats

Installera repor ting Services-platsen om du vill hantera rapporter på platsen. Repor ting Services-platsen:

- Kopierar rapport-mappar och rapporter till SQL Server Reporting Services
- Tillämpar säkerhets principen för rapporter och mappar
- Anger konfigurations inställningar i repor ting Services

### <a name="requirements-and-limitations"></a>Krav och begränsningar

Innan du kan visa eller hantera rapporter i Configuration Manager-konsolen behöver du en repor ting Services-plats. Konfigurera den här plats system rollen på en server med Microsoft SQL Server Reporting Services. Mer information finns i [krav för rapportering](prerequisites-for-reporting.md).  

- När du väljer en plats för att installera repor ting Services-platsen måste användare som ska ha åtkomst till rapporterna vara i samma säkerhets omfång som den plats där du installerar rollen.  

- När du har installerat en repor ting Services-plats på ett plats system ska du inte ändra URL: en för rapport servern.

    Du kan till exempel skapa repor ting Services-platsen. Du ändrar sedan URL: en för rapport servern i Configuration Manager repor ting Services. Configuration Managers konsolen fortsätter att använda den gamla URL: en. Du kan inte köra, redigera eller skapa rapporter från-konsolen.

    Om du behöver ändra URL för rapport servern måste du först ta bort den befintliga repor ting Services-platsen. Ändra URL: en och installera om repor ting Services-platsen.  

- Ange ett [repor ting Services-plats-konto](../../plan-design/hierarchy/accounts.md#reporting-services-point-account)när du installerar en repor ting Services-plats. För användare från en annan domän att köra en rapport skapar du ett dubbelriktat förtroende mellan domäner. Annars går det inte att köra rapporten.

### <a name="install-the-reporting-services-point-on-a-site-system"></a><a name="bkmk_install" /> Installera repor ting Services-platsen på ett plats system  

Mer information om hur du konfigurerar plats system finns i [Installera plats system roller](../deploy/configure/install-site-system-roles.md).  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden  **servrar och plats system roller** .  

1. Lägg till repor ting Services-platsen på en ny eller befintlig plats system Server:  

    - *Nytt plats system*: Välj **skapa plats system Server**i gruppen **skapa** på fliken **Start** i menyfliksområdet. **Guiden skapa plats system Server** öppnas.  

    - *Befintligt plats system*: Välj mål servern. På fliken **Start** i menyfliksområdet väljer du **Lägg till plats system roll**i gruppen **Server** . **Guiden Lägg till plats system roller** öppnas.  

1. På sidan **Allmänt** anger du de allmänna inställningarna för platssystemservern. När du lägger till repor ting Services-platsen på en befintlig server kontrollerar du de värden som du har konfigurerat tidigare.  

1. På sidan **urval för system roll** väljer du **repor ting Services-plats** i listan över tillgängliga roller och väljer sedan **Nästa**.  

1. Konfigurera följande inställningar på sidan **repor ting Services-plats** :  

    - **Namn på plats databas server**: Ange namnet på den server som är värd för Configuration Manager plats databasen. Guiden hämtar vanligt vis det fullständigt kvalificerade domän namnet (FQDN) för servern. Om du vill ange en databas instans använder du format &lt; *Server namnet* > \& lt;* instans namn*>. Till exempel `sqlserver\named1`.

    - **Databas namn**: Ange namnet på den Configuration Manager plats databasen. Välj **Verifiera** för att bekräfta att guiden har åtkomst till plats databasen.  

        > [!IMPORTANT]  
        > Det användar konto som du använder för att skapa repor ting Services-platsen måste ha **Läs** behörighet till plats databasen. Om anslutningstestet misslyckas visas en röd varningsikon. Sammanhangsbaserad hov rings text på ikonen innehåller information om felen. Korrigera felet och välj sedan **testa** igen.  

    - **Mappnamn**: Ange namnet på mappen som ska skapas och användas för Configuration Manager rapporter i repor ting Services.  

    - **Instans för repor ting Services-server**: Välj instansen för SQL Server för repor ting Services. Om den här sidan inte listar några instanser kontrollerar du att SQL Server Reporting Services är installerat, konfigurerat och startat.  

        > [!IMPORTANT]  
        > Configuration Manager skapar en anslutning i kontexten för den aktuella användaren till WMI på det valda plats systemet. Den här anslutningen används för att hämta instansen av SQL Server för repor ting Services. Den aktuella användaren måste ha **Läs** behörighet till WMI på plats systemet, eller så kan inte guiden Hämta repor ting Services-instanserna.  

    - **Konto för repor ting Services-plats**: Välj **Ange**och välj sedan ett konto som ska användas. SQL Server Reporting Services på repor ting Services-platsen använder det här kontot för att ansluta till Configuration Managers plats databas. Den här anslutningen är att hämta data för en rapport. Välj **befintligt konto** för att ange ett Windows-användarkonto som du tidigare har konfigurerat som ett Configuration Manager konto. Välj **nytt konto** om du vill ange ett Windows-användarkonto som inte är konfigurerat för användning. Configuration Manager tilldelar automatiskt den angivna användaren åtkomst till plats databasen.  

        Kontot som kör repor ting Services måste tillhöra den domän lokala säkerhets gruppen **Windows Authorization Access Group**. Detta ger kontot behörighet **att läsa** för attributet **TokenGroupsGlobalAndUniversal** för alla användar objekt i domänen. Användare i en annan domän än kontot för repor ting Services-platsen måste ha ett dubbelriktat förtroende mellan domänerna för att kunna köra rapporter.

        Det angivna Windows-användarkontot och lösenordet krypteras och lagras i Reporting Services-databasen. Reporting Services använder kontot och lösenordet för att från platsdatabasen hämta data till rapporterna.  

        > [!IMPORTANT]  
        > Kontot som du anger måste ha behörigheten **Logga in lokalt** på den server som är värd för repor ting Services-databasen.  

1. Slutför guiden.

När guiden har slutförts skapar Configuration Manager rapportens mappar i repor ting Services. Den kopierar sedan sina rapporter till de angivna rapport mapparna.  

> [!TIP]  
> Om du bara vill lista de plats system som är värdar för plats rollen repor ting Services-plats, högerklickar du på **servrar och plats system roller**och väljer **repor ting Services-plats**.  

### <a name="languages-for-reports"></a><a name="bkmk_languages" /> Språk för rapporter

<!-- SCCMDocs#1067 -->

När Configuration Manager skapar rapport-mappar och kopierar rapporter till rapport servern, bestämmer det lämpligt språk för objekten.

- Skapa rapport-mappar, kopiera rapporter

  - Skapa objekt med hjälp av språkvarianten för plats serverns operativ system

  - Om det specifika språk paketet inte är tillgängligt, används engelska (SVE) som standard

- Visa rapporter i en webbläsare

  - Mapp-och rapport namn: samma språk som plats servern
  
  - Rapport innehåll: dynamiskt baserat på webbläsarens nationella inställningar

- Visa rapporter i Configuration Manager-konsolen

  - Mapp-och rapport namn: dynamiska baserat på konsolens språk
  
  - Rapport innehåll: dynamiskt baserat på konsolens språk

När du installerar en Reporting Services-plats på en plats utan språkpaket, installeras rapporterna på engelska. Om du installerar ett språkpaket efter det att du installerar Reporting Services-platsen, måste du avinstallera och installera om Reporting Services-platsen om rapporterna ska bli tillgängliga med det lämpliga språkpaketsspråket.  

Mer information finns i [språk paket](../deploy/install/language-packs.md).

### <a name="file-installation-and-report-folder-security-rights"></a>Filinstallation och behörigheter till rapportmappen

Configuration Manager utför följande åtgärder för att installera repor ting Services-platsen och för att konfigurera repor ting Services:  

> [!IMPORTANT]  
> Platsen utför de här åtgärderna i kontexten för det konto som har kon figurer ATS för tjänsten SMS_Executive. Detta konto är vanligt vis det lokala system kontot för plats servern.  

- Installera repor ting Services-platsens plats roll.  

- Skapa data källan i repor ting Services med de lagrade autentiseringsuppgifterna som du angav i guiden. Det här kontot är Windows-användarkontot och lösen ordet som repor ting Services använder för att ansluta till plats databasen när du kör rapporter.  

- Skapa rotmappen Configuration Manager i repor ting Services.  

- Lägg till säkerhets rollerna **ConfigMgr Report Users** och **ConfigMgr Report administrators** i repor ting Services.  

- Skapa undermappar och distribuera sedan Configuration Manager rapporter från `%ProgramFiles%\SMS_SRSRP` på plats servern till repor ting Services.  

- Lägg till rollen **ConfigMgr-rapport användare** i repor ting Services till rotmapparna för alla användar konton i Configuration Manager som har Läs behörighet för **platsen** .  

- Lägg till rollen **ConfigMgr-rapport administratörer** i repor ting Services i rotmappen för alla användar konton i Configuration Manager som har behörighet för att **ändra platsen** .  

- Hämta mappningen mellan rapportmallar och Configuration Manager skyddade objekt typer. Configuration Manager underhåller den här kartan i plats databasen.  

- Konfigurera följande rättigheter för administrativa användare i Configuration Manager till vissa rapport-mappar i repor ting Services:  

  - Lägg till användare och tilldela **användar rollen ConfigMgr-rapport** till den associerade rapportmappen för administrativa användare som har **Kör rapport** behörigheter för Configuration Manager-objektet.  

  - Lägg till användare och tilldela rollen **ConfigMgr-rapport administratörer** till den associerade rapportmappen för administrativa användare som har behörigheten **ändra rapport** för Configuration Manager-objektet.  

Configuration Manager ansluter till repor ting Services och anger behörigheter för användare i rotmapparna för Configuration Manager och repor ting Services och vissa rapportmallar. Efter den första installationen av repor ting Services-platsen Configuration Manager ansluter till repor ting Services var 10: e minut för att kontrol lera att användar rättigheterna som kon figurer ATS i rapportmappen är associerade rättigheter som är inställda för Configuration Manager användare. När användare läggs till eller användar rättigheter ändras i rapportmappen med hjälp av repor ting Services Rapporthanteraren, skriver Configuration Manager över dessa ändringar med hjälp av rollbaserade tilldelningar som lagras i plats databasen. Configuration Manager tar också bort användare som inte har rapporterings rättigheter i Configuration Manager.  

### <a name="reporting-services-security-roles"></a>Säkerhets roller för repor ting Services

När Configuration Manager installerar repor ting Services-platsen, läggs följande säkerhets roller till i repor ting Services:  

- **ConfigMgr-rapport användare**: användare som är tilldelade till den här säkerhets rollen kan bara köra Configuration Manager rapporter.  

- **ConfigMgr-rapport administratörer**: användare som är tilldelade till den här säkerhets rollen kan utföra alla uppgifter som är relaterade till rapportering i Configuration Manager.  

## <a name="verify-installation"></a><a name="bkmk_verify"></a> Verifiera installationen

Verifiera installationen av repor ting Services-platsen genom att titta på vissa status meddelanden och logg fils poster. Använd följande procedur för att verifiera att Reporting Services-platsinstallationen lyckades.  

> [!Note]  
> Om du ser rapporter i undermappen **rapporter** i noden **rapportering** på arbets ytan **övervakning** i Configuration Manager-konsolen kan du hoppa över den här proceduren.

### <a name="verify-installation-by-status-message"></a>Verifiera installation efter status meddelande

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **system status**och väljer noden **komponent status** .  

1. Välj **SMS_SRS_REPORTING_POINT** -komponenten.  

1. Välj **Visa meddelanden**i gruppen **komponent** på fliken **Start** i menyfliksområdet och välj sedan **alla**.  

1. Ange ett datum och en tid för en period innan du installerade repor ting Services-platsen. Välj sedan **OK**.  

1. Verifiera status meddelande-ID **1015**. Det här status meddelandet anger att repor ting Services-platsen har installerats.

### <a name="verify-installation-by-log-file"></a>Verifiera installationen med logg filen

Öppna filen **Srsrp. log** som finns i katalogen **loggar** i Configuration Manager installations Sök väg. Sök efter strängen `Installation was successful` .

Stega genom den här logg filen från den tidpunkt då repor ting Services-platsen har installerats. Kontrollera att rapportmapparna har skapats, att rapporterna har distribuerats och att säkerhetsprincipen för varje mapp har bekräftats. Efter den sista raden med säkerhets princip bekräftelser söker du efter strängen `Successfully checked that the SRS web service is healthy on server` .  

## <a name="configure-a-certificate-to-author-reports"></a>Konfigurera ett certifikat för att skapa rapporter

Det finns många alternativ som du kan redigera rapporter i SQL Server Reporting Services. När du skapar eller redigerar rapporter i Configuration Manager-konsolen öppnas Configuration Manager Report Builder att använda som redigerings miljö. Oavsett hur du redigerar dina Configuration Manager rapporter behöver du ett självsignerat certifikat för serverautentisering till plats databas servern.

> [!NOTE]  
> Mer information om hur du redigerar rapporter med SQL Server Reporting Services finns i [Report Builder redigerings miljö](/sql/reporting-services/tools/report-builder-authoring-environment-ssrs).  

Configuration Manager installerar certifikatet automatiskt på plats servern och eventuella SMS-provider-roller. Du kan skapa eller redigera rapporter från Configuration Manager-konsolen när du kör den från någon av dessa servrar.

När du skapar eller ändrar rapporter från en Configuration Manager-konsol på en annan dator, bör du exportera certifikatet från plats servern. Det angivna certifikatets egna namn är FQDN för plats servern i certifikat arkivet **Betrodda personer** för den lokala datorn. Lägg till det här certifikatet i certifikat arkivet **Betrodda personer** på den dator som kör Configuration Manager-konsolen.  

## <a name="modify-reporting-services-point-settings"></a>Ändra inställningar för repor ting Services-plats

När du har installerat den här rollen kan du ändra plats databas anslutningen och autentiseringsinställningarna i egenskaperna för repor ting Services-platsen.

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **servrar och plats system roller** .  

    > [!TIP]  
    > Om du bara vill lista de plats system som är värdar för repor ting Services-platsen högerklickar du på noden **servrar och plats system roller** och väljer **repor ting Services-plats**.  

1. Välj det plats system som är värd för repor ting Services-platsen. Välj sedan **rapport tjänst** platsens plats system roller i informations fönstret.

1. Välj **Egenskaper**i gruppen **Egenskaper** på fliken **plats roll** i menyfliksområdet.  

1. Du kan ändra följande inställningar i **repor ting Services-platsens egenskaper**:  

    - **Namn på plats databas server**

    - **Databasnamn**

    - **Användar konto**

1. Spara ändringarna och Stäng egenskaperna genom att klicka på **OK** .  

Mer information om de här inställningarna finns i beskrivningarna i avsnittet så här [installerar du repor ting Services-platsen på ett plats system](#bkmk_install).

## <a name="power-bi-report-server"></a>Power BI-rapportserver

Från och med version 2002 kan du integrera rapporter med Power BI-rapportserver. Mer information om hur du konfigurerar den finns i [integrera med Power BI-rapportserver](powerbi-report-server.md).

## <a name="upgrade-sql-server"></a>Uppgradera SQL Server

Om du vill uppgradera SQL Server och SQL Server Reporting Services måste du först ta bort repor ting Services-platsen från-platsen. När du har uppgraderat SQL Server måste du installera om repor ting Services-platsen i Configuration Manager.

Om du inte följer den här processen visas fel när du kör eller redigerar rapporter från Configuration Manager-konsolen. Du kan fortsätta att köra och redigera rapporter från en webbläsare.  

## <a name="configure-report-options"></a> Konfigurera rapportalternativ

Du kan välja den standard rapporterings tjänst plats som du använder för att hantera rapporter. Platsen kan ha fler än en repor ting Services-plats, men den använder bara standard servern för att hantera rapporter. Gör så här för att konfigurera rapportalternativ för platsen.  

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **rapportering**och väljer sedan noden **rapporter** .  

1. Välj **rapport alternativ**i gruppen **Inställningar** på fliken **Start** i menyfliksområdet.  

1. Välj standard rapport servern i listan och välj sedan **OK**.

Om ingen server visas kontrollerar du att du har installerat och konfigurerat en repor ting Services-plats på platsen. Mer information finns i [Verifiera installationen](#bkmk_verify).

Se till att datorn kör en version av SQL Server Report Builder som matchar den version av SQL Server som du använder för rapport servern. Annars visas ett fel meddelande om att standard rapport servern inte sparas och du inte kan skapa eller redigera rapporter.<!-- SCCMDocs#791 -->

## <a name="next-steps"></a>Nästa steg

[Åtgärder och underhåll för rapportering](operations-and-maintenance-for-reporting.md)