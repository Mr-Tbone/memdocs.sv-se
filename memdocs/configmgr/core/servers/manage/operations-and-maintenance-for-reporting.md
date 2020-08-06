---
title: Åtgärder och underhåll för rapportering
titleSuffix: Configuration Manager
description: Lär dig mer om att hantera rapporter och rapport prenumerationer i Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 414d1138a7682d6b9acbc7731035fff1842a1fe7
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87815420"
---
# <a name="operations-and-maintenance-for-reporting-in-configuration-manager"></a>Åtgärder och underhåll för rapportering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När infrastrukturen är på plats för rapportering i Configuration Manager finns det ett antal åtgärder som du vanligt vis utför för att hantera rapporter och rapport prenumerationer.

> [!NOTE]
> Den här artikeln fokuserar på rapporter i SQL Server Reporting Services. Från och med version 2002 kan du integrera rapporter med Power BI-rapportserver. Mer information finns i [integrera med Power BI-rapportserver](powerbi-report-server.md).

## <a name="run-a-report-from-reporting-services"></a>Köra en rapport från repor ting Services

Configuration Manager lagrar sina rapporter i SQL Server Reporting Services. Rapporten hämtar data från Configuration Manager plats databasen. Du kan komma åt rapporter i Configuration Manager-konsolen eller genom att använda Rapporthanteraren via en webbläsare. Öppna rapporter från en webbläsare på en dator som har åtkomst till repor ting Services-platsen och användaren har tillräcklig behörighet för att visa rapporterna. Om du vill köra rapporter måste du ha **Läs** behörighet för **plats** behörigheten och behörigheten **Kör rapport** för vissa objekt.

När du kör en rapport visas rapportens rubrik, beskrivning och kategori på det lokala operativ systemets språk. Mer information finns i [språk för-rapporter](configuring-reporting.md#-languages-for-reports).

> [!NOTE]  
> Rapporthanteraren är ett webbaserat verktyg för åtkomst och hantering av rapporter. Du kan använda den för att administrera en enskild rapport Server instans via en HTTPS-anslutning. Använd Rapporthanteraren för operativa uppgifter: Visa rapporter, ändra rapport egenskaper och hantera associerade rapport prenumerationer. Den här artikeln innehåller anvisningar för att visa en rapport och ändra rapport egenskaper i Rapporthanteraren. Mer information om andra alternativ i Rapporthanteraren finns [Rapporthanteraren?](https://docs.microsoft.com/sql/reporting-services/report-server/manage-a-reporting-services-native-mode-report-server)

Använd följande procedurer för att köra en Configuration Manager-rapport.

### <a name="run-a-report-in-the-configuration-manager-console"></a>Köra en rapport i Configuration Manager-konsolen

1. Gå till arbets ytan **övervakning** i Configuration Manager-konsolen. Expandera **rapportering**och välj sedan **rapporter**. Den här noden listar tillgängliga rapporter.

    > [!TIP]
    > Om den här noden inte listar några rapporter kontrollerar du att repor ting Services-platsen har installerats och kon figurer ATS. Mer information finns i [Konfigurera rapportering](configuring-reporting.md).

1. Välj den rapport som du vill köra. På fliken **Start** i menyfliksområdet i avsnittet **rapport grupp** väljer du **Kör** för att öppna rapporten.

1. Om det finns nödvändiga parametrar anger du dem och väljer sedan **Visa rapport**.

### <a name="run-a-report-in-a-web-browser"></a>Köra en rapport i en webbläsare

1. I webbläsaren går du till Rapporthanteraren URL, till exempel `https://Server1/Reports` . Hitta den här adressen på sidan **RAPPORTHANTERAREN URL** i repor ting Services-Configuration Manager.

1. I Rapporthanteraren väljer du rapportmappen för Configuration Manager, till exempel **ConfigMgr_CAS**.

    > [!TIP]
    > Om Rapporthanteraren inte listar några rapporter kontrollerar du att repor ting Services-platsen har installerats och kon figurer ATS. Mer information finns i [Konfigurera rapportering](configuring-reporting.md).

1. Välj rapport kategori för den rapport som du vill köra och välj sedan den aktuella rapporten. Rapporten öppnas i Rapporthanteraren.

1. Om det finns nödvändiga parametrar anger du dem och väljer sedan **Visa rapport**.

## <a name="modify-the-properties-of-a-report"></a>Ändra egenskaperna för en rapport

Rapport egenskaperna inkluderar rapportens namn och beskrivning. Du kan visa egenskaperna för en rapport n Configuration Manager-konsolen.

Om du vill ändra egenskaperna använder Rapporthanteraren:

1. I webbläsaren går du till Rapporthanteraren URL, till exempel `https://Server1/Reports` .

1. I Rapporthanteraren väljer du rapportmappen för Configuration Manager, till exempel **ConfigMgr_CAS**.

1. Välj rapport kategori och välj sedan den aktuella rapporten. Rapporten öppnas i Rapporthanteraren.

1. Välj fliken **Egenskaper** . ändra rapportens namn och beskrivning och välj sedan **Använd**.

Rapporthanteraren sparar rapport egenskaperna på rapport servern. I Configuration Manager-konsolen visas uppdaterade rapport egenskaper för rapporten.

## <a name="edit-a-report"></a><a name="bkmk_edit"></a>Redigera en rapport

När en befintlig Configuration Manager rapport inte hämtar den information som du vill ha, redigerar du den i Report Builder. Du kan också använda Report Builder för att ändra layouten eller designen för rapporten. Även om du kan redigera en standard rapport direkt är det bäst att klona den. Öppna rapporten för att redigera och välj sedan **Spara som**.

Om du vill redigera en rapport måste du ha behörigheten **plats ändring** och **Ändra rapport** behörigheter för de enskilda objekten i rapporten.

> [!IMPORTANT]
> Plats uppdateringar Behåll inbyggda rapporter. Om du ändrar en standard rapport och platsen uppdateras, byter den namn på rapporten med ett under streck ( `_` ). Det här beteendet ser till att plats uppdateringen inte skriver över den ändrade rapporten i standard rapporten.
>
> Om du ändrar fördefinierade rapporter måste du säkerhetskopiera dina anpassade rapporter innan du installerar en plats uppdatering. Efter uppdateringen återställer du rapporten i repor ting Services. Om du gör betydande ändringar i en fördefinierad rapport ska du skapa en ny rapport i stället. Nya rapporter som du skapar innan du uppgraderar en plats skrivs inte över.

Använd följande procedur för att redigera egenskaperna för en Configuration Manager rapport.

1. Gå till arbets ytan **övervakning** i Configuration Manager-konsolen. Expandera **rapportering**och välj sedan noden **rapporter** .

1. Välj den rapport som du vill ändra. På fliken **Start** i menyfliksområdet i avsnittet **rapport grupp** väljer du **Redigera**. Du kan bli ombedd att ange autentiseringsuppgifter. Om Report Builder inte är installerat på datorn, måste du Configuration Manager att installera det. Report Builder krävs för att ändra och skapa rapporter.

1. I Report Builder ändrar du lämpliga rapport inställningar. Välj **Spara** för att spara rapporten på rapport servern.

## <a name="create-reports"></a>Skapa rapporter

Det finns två typer av rapporter som du kan skapa:

- Med en **modell baserad rapport** kan du interaktivt välja de objekt som du vill ta med i rapporten. Mer information om hur du skapar anpassade rapport modeller finns [i skapa anpassade rapport modeller för Configuration Manager i SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).

- Med en **SQL-baserad rapport** kan du hämta data som baseras på rapportens SQL-uttryck.

> [!IMPORTANT]
> Ditt konto måste ha behörighet att **ändra plats** för att kunna skapa en ny rapport. Du kan bara skapa en rapport i mappar som du har **ändrat rapport** behörigheter för.

### <a name="create-a-model-based-report"></a>Skapa en modell baserad rapport

Använd följande procedur för att skapa en modellbaserade Configuration Manager-rapport.

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **rapportering**och väljer noden **rapporter** .

1. På fliken **Start** i menyfliksområdet i avsnittet **skapa** väljer du **Skapa rapport**. Den här åtgärden öppnar **guiden Skapa rapport**.

1. Konfigurera följande inställningar på sidan **information** :

    - **Typ**: Välj **modell-baserad rapport**.

    - **Namn**: Ange ett namn för rapporten.

    - **Beskrivning**: Ange en beskrivning av rapporten.

    - **Server**: visar namnet på rapport servern där du skapar den här rapporten.

    - **Sökväg**: Välj **Bläddra** för att ange en mapp där du vill lagra rapporten.

1. På sidan **modell val** väljer du en tillgänglig modell i listan för att skapa den här rapporten. I **förhands gransknings** avsnittet visas SQL Server vyer och entiteter som är tillgängliga i den här rapport modellen.

1. Slutför guiden Skapa rapport.

1. Öppna Report Builder för att konfigurera rapport inställningarna. Mer information finns i [Redigera en Configuration Manager rapport](#bkmk_edit).

1. I Report Builder skapar du rapportlayout, väljer data i vyerna tillgängliga SQL Server och lägger till parametrar i rapporten.

1. Välj **Kör** för att köra rapporten. Kontrol lera att rapporten innehåller den information som du förväntar dig. Om det behövs väljer du **design** för att ändra rapporten ytterligare.

1. Välj **Spara** för att spara rapporten på rapport servern.

### <a name="create-a-sql-based-report"></a>Skapa en SQL-baserad rapport

När du skapar ett SQL-uttryck för en anpassad rapport ska du inte direkt referera till SQL Server tabeller. Referens som stöds SQL Server vyer från plats databasen alltid. Dessa vyer har namn som börjar med `v_` . Mer information finns i [skapa anpassade rapporter med hjälp av SQL Server vyer i Configuration Manager](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

Du kan också referera till offentliga lagrade procedurer från plats databasen. Dessa lagrade procedurer har namn som börjar med `sp_` .

Använd följande procedur för att skapa en SQL-baserad Configuration Manager-rapport.

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **rapportering**och väljer noden **rapporter** .

1. På fliken **Start** i menyfliksområdet i avsnittet **skapa** väljer du **Skapa rapport**. Den här åtgärden öppnar **guiden Skapa rapport**.

1. Konfigurera följande inställningar på sidan **information** :

    - **Typ**: Välj **SQL-baserad rapport**.

    - **Namn**: Ange ett namn för rapporten.

    - **Beskrivning**: Ange en beskrivning av rapporten.

    - **Server**: visar namnet på rapport servern där du skapar den här rapporten.

    - **Sökväg**: Välj **Bläddra** för att ange en mapp där du vill lagra rapporten.

1. Slutför guiden Skapa rapport.

1. Öppna Report Builder för att konfigurera rapport inställningarna. Mer information finns i [Redigera en Configuration Manager rapport](#bkmk_edit).

1. I Report Builder anger du rapportens SQL-uttryck. Du kan också bygga SQL-instruktionen genom att använda kolumner i tillgängliga vyer. Om det behövs kan du lägga till parametrar i rapporten.

1. Välj **Kör** för att köra rapporten. Kontrol lera att rapporten innehåller den information som du förväntar dig. Om det behövs väljer du **design** för att ändra rapporten ytterligare.

1. Välj **Spara** för att spara rapporten på rapport servern.

## <a name="manage-report-subscriptions"></a><a name="bkmk_subscription"></a>Hantera rapport prenumerationer

Med rapport prenumerationer i SQL Server Reporting Services kan du konfigurera automatisk leverans av angivna rapporter via e-post eller till en fil resurs med schemalagda intervall. Om du vill konfigurera rapport prenumerationer använder du **guiden Skapa prenumeration** i Configuration Manager.

### <a name="create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>Skapa en rapport prenumeration för att leverera en rapport till en fil resurs

När du skapar en rapport prenumeration för att leverera en rapport till en fil resurs, kopierar repor ting Services rapporten i angivet format till den fil resurs som du anger. Du kan prenumerera på och begära leverans för endast en rapport i taget.

När du skapar en prenumeration som använder en fil resurs måste du ange en befintlig delad mapp som mål. Rapport servern skapar inte mappen eller nätverks resursen. När du anger målmappen i en prenumeration ska du använda en UNC-sökväg och ta inte med avslutande omvänt snedstreck ( `\` ) i mappsökvägen. Följande exempel är en giltig UNC-sökväg för målmappen: `\\server\reportfiles\operations\2001` .

> [!NOTE]
> När du skapar prenumerationen anger du ett användar namn och lösen ord. Kontot måste ha åtkomst till den här resursen med **Skriv** behörighet till målmappen.

Repor ting Services kan återge rapporter i olika fil format. Till exempel MHTML eller Excel. Du väljer formatet när du skapar prenumerationen. Även om du kan välja ett åter givnings format som stöds, fungerar vissa format bättre än andra vid åter givning till en fil.

### <a name="limitations-for-report-subscriptions-to-a-file-share"></a>Begränsningar för rapport prenumerationer till en fil resurs

Följande lista innehåller begränsningar för rapport prenumerationer till en fil resurs:

- Till skillnad från rapporter som du är värd för och hanterar på en rapport Server levererar repor ting Services rapporter till en delad mapp som statiska filer.

- Interaktiva funktioner i rapporten fungerar inte för rapporter som lagras som filer. Rapporten representerar alla interaktiva funktioner som statiska element.

- Om rapporten innehåller diagram används standard presentationen.

- Om rapporten länkar till en annan rapport, återges länken som statisk text.

Om du vill behålla interaktiva funktioner i en levererad rapport använder du e-postleverans. Mer information finns i [skapa en rapport prenumeration för att leverera en rapport via e-post](#bkmk_subscription-email).

### <a name="process-to-create-a-report-subscription-for-a-file-share"></a>Process för att skapa en rapport prenumeration för en fil resurs

Använd följande procedur för att skapa en rapport prenumeration för att leverera en rapport till en fil resurs.  

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **rapportering**och väljer noden **rapporter** .

1. Välj en rapportmapp och välj sedan den rapport som du vill prenumerera på. På fliken **Start** i menyfliksområdet väljer du **Skapa prenumeration**i avsnittet **rapport grupp** . Den här åtgärden öppnar **guiden Skapa prenumeration**.

1. Konfigurera följande inställningar på sidan **prenumerations leverans** :  

    - **Rapport levererad av**: Välj **Windows-filresurs**.

    - **Fil namn**: Ange fil namnet för rapporten. Som standard innehåller rapport filen inte något fil namns tillägg. Välj **Lägg till fil namns tillägg när det skapas** för att automatiskt lägga till ett fil namns tillägg baserat på formatet.

    - **Sökväg**: Ange en UNC-sökväg till en befintlig mapp dit du vill leverera rapporten. Till exempel `\\server\reportfiles\operations`.

    - **Åter givnings format**: Välj något av följande format för rapport filen:

      - **XML-fil med rapport data**
      - **CSV (kommaavgränsad)**
      - **TIFF-fil**
      - **Acrobat-fil (PDF)**
      - **HTML 4,0**
        > [!NOTE]
        > Om rapporten innehåller bilder, ingår inte HTML 4,0-formatet.
      - **MHTML (webb Arkiv)**
      - **RPL-återgivning** (rapportens sidlayout)
      - **Excel**
      - **Word**

    - **Användar namn**: Ange ett Windows-användarkonto med *Skriv* behörighet till den angivna **sökvägen**.

    - **Lösen ord**: Ange lösen ordet för Windows-användarkontot ovan.

    - **Överskrivnings alternativ**: Välj något av följande alternativ för att konfigurera beteendet när en fil med samma namn finns i målmappen:

      - **Skriv över en befintlig fil med en senare version**
      - **Skriv inte över en befintlig fil**
      - **Öka fil namn när nya versioner läggs till**: med det här alternativet läggs ett tal till i den nya rapportens fil namn för att skilja det från tidigare versioner.

    - **Beskrivning**: om du vill kan du ange ytterligare information om den här rapport prenumerationen.

1. På sidan **prenumerations schema** väljer du något av följande alternativ för leverans schema för rapport prenumerationen:

    - **Använd delat schema**: ett delat schema är ett tidigare definierat schema som kan användas av andra rapport prenumerationer. När du väljer det här alternativet väljer du också ett delat schema. Om det inte finns några delade scheman väljer du alternativet för att skapa ett nytt schema.

    - **Skapa nytt schema**: konfigurera det schema som rapporten körs på. Schemat innehåller intervall, start tid och-datum samt slutdatum för den här prenumerationen. Som standard skapar en ny prenumeration ett nytt schema som ska köras varje timme med början vid aktuellt datum och aktuell tid.

1. På sidan **prenumerations parametrar** anger du alla parametrar som den här rapporten behöver för att köra obevakad. Om rapporten inte har några parametrar visas inte den här sidan i guiden.

1. Slutför guiden.

1. Kontrol lera att Configuration Manager har skapat rapport prenumerationen. Välj noden **prenumerationer** om du vill visa och ändra rapport prenumerationer.

### <a name="create-a-report-subscription-to-deliver-a-report-by-email"></a><a name="bkmk_subscription-email"></a>Skapa en rapport prenumeration för att leverera en rapport via e-post

När du skapar en rapport prenumeration för att leverera en rapport via e-post skickar repor ting Services ett e-postmeddelande till de mottagare som du konfigurerar. E-postmeddelandet innehåller rapporten som en bifogad fil. Rapport servern validerar inte e-postadresser eller hämtar dem från en e-postserver. Du kan skicka rapporter till alla giltiga e-postkonton i eller utanför organisationen.

> [!NOTE]
> Om du vill aktivera alternativet för **e-** postprenumeration måste du konfigurera e-postinställningarna i repor ting Services. Mer information finns i [e-postleverans i repor ting Services](https://docs.microsoft.com/sql/reporting-services/subscriptions/e-mail-delivery-in-reporting-services).

Du kan välja ett eller båda av följande alternativ för e-postleverans:

- Skicka ett meddelande med en länk till den genererade rapporten.

- Skicka en inbäddad eller bifogad rapport. Åter givnings formatet och webbläsaren avgör om den bäddar in eller bifogar rapporten.

  - Om din webbläsare har stöd för HTML 4,0 och MHTML, och du väljer formatet **MHTML (webb Arkiv)** , bäddar e-postmeddelandet in rapporten i meddelandet.
  - Alla andra format levererar rapporter som bifogade filer.
  - Repor ting Services kontrollerar inte storleken på bilagan eller meddelandet innan rapporten skickas. Om bilagan eller meddelandet överskrider max gränsen som tillåts av e-postservern levereras inte rapporten.

Använd följande procedur för att skapa en rapport prenumeration för att leverera en rapport med hjälp av e-post.  

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **rapportering**och väljer noden **rapporter** .

1. Välj en rapportmapp och välj sedan den rapport som du vill prenumerera på. På fliken **Start** i menyfliksområdet väljer du **Skapa prenumeration**i avsnittet **rapport grupp** . Den här åtgärden öppnar **guiden Skapa prenumeration**.

1. Konfigurera följande inställningar på sidan **prenumerations leverans** :  

    - **Rapport levererad av**: Välj **e-post**.

    - **Till**: Ange en giltig e-postadress som mottagare.

        > [!NOTE]
        > Ange flera mottagare genom att avgränsa varje e-postadress med semikolon ( `;` ).

    - **CC**: Alternativt kan du ange en e-postadress för att få en kopia av den här rapporten.

    - **Hemlig kopia**: Alternativt kan du ange en e-postadress för att ta emot en hemlig kopia av den här rapporten.

    - **Svara till**: Ange svars adress. Om mottagaren svarar på e-postmeddelandet skickas svaret till den här adressen.

    - **Subject**: Ange en ämnesrad för prenumerationens e-postmeddelande.

    - **Prioritet**: Välj prioritets flagga för det här e-postmeddelandet: **låg**, **Normal**eller **hög**. Microsoft Exchange använder den här flaggan för att ange e-postmeddelandets prioritet.

    - **Kommentar**: ange text för bröd texten i prenumerationens e-postmeddelande.

    - **Beskrivning**: om du vill kan du ange ytterligare information om den här rapport prenumerationen.

    - **Inkludera länk**: ta med URL: en för rapporten i bröd texten i e-postmeddelandet.

    - **Inkludera rapport**: bifoga rapporten i e-postmeddelandet. Använd alternativet **åter givnings format** för att ange rapport formatet som ska bifogas.

    - **Åter givnings format**: Välj något av följande format för den bifogade rapport filen:

      - **XML-fil med rapport data**
      - **CSV (kommaavgränsad)**
      - **TIFF-fil**
      - **Acrobat-fil (PDF)**
      - **MHTML (webb Arkiv)**
      - **Excel**
      - **Word**

1. På sidan **prenumerations schema** väljer du något av följande alternativ för leverans schema för rapport prenumerationen:

    - **Använd delat schema**: ett delat schema är ett tidigare definierat schema som kan användas av andra rapport prenumerationer. När du väljer det här alternativet väljer du också ett delat schema. Om det inte finns några delade scheman väljer du alternativet för att skapa ett nytt schema.

    - **Skapa nytt schema**: konfigurera det schema som rapporten körs på. Schemat innehåller intervall, start tid och-datum samt slutdatum för den här prenumerationen. Som standard skapar en ny prenumeration ett nytt schema som ska köras varje timme med början vid aktuellt datum och aktuell tid.

1. På sidan **prenumerations parametrar** anger du alla parametrar som den här rapporten behöver för att köra obevakad. Om rapporten inte har några parametrar visas inte den här sidan i guiden.

1. Slutför guiden.

1. Kontrol lera att Configuration Manager har skapat rapport prenumerationen. Välj noden **prenumerationer** om du vill visa och ändra rapport prenumerationer.
