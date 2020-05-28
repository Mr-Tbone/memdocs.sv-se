---
title: Aktivera uppdateringar från tredje part
titleSuffix: Configuration Manager
description: Aktivera uppdateringar från tredje part i Configuration Manager
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 946b0f74-0794-4e8f-a6af-9737d877179b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f5461f888bfa2b749061eef4000f0d7c5f756b84
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906747"
---
# <a name="enable-third-party-updates"></a>Aktivera uppdateringar från tredje part 

*Gäller för: Configuration Manager (aktuell gren)*

Från och med version 1806 kan du med hjälp av noden **program uppdaterings kataloger från tredje part** i Configuration Manager-konsolen prenumerera på kataloger från tredje part, publicera sina uppdateringar till din program uppdaterings plats (SUP) och sedan distribuera dem till klienter.  <!--1357605, 1352101, 1358714-->

> [!Note]  
> Configuration Manager aktiverar inte den här funktionen som standard. Innan du använder den aktiverar du den valfria funktionen **Aktivera stöd för uppdateringar från tredje part på klienter**. Mer information finns i avsnittet [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).


## <a name="prerequisites"></a>Förutsättningar 
- Tillräckligt med disk utrymme på den översta program uppdaterings platsens WSUSContent-mapp för att lagra det binära innehållet för program uppdateringar från tredje part.
    - Hur mycket lagrings utrymme som krävs varierar beroende på leverantör, typer av uppdateringar och vissa uppdateringar som du publicerar för distribution.
    - Om du behöver flytta WSUSContent-mappen till en annan enhet med mer ledigt utrymme kan du läsa [om hur du ändrar platsen där WSUS lagrar uppdateringar lokalt](https://docs.microsoft.com/archive/blogs/sus/wsus-how-to-change-the-location-where-wsus-stores-updates-locally) blogg inlägg.
- Tjänsten för synkronisering av program uppdateringar från tredje part kräver Internet åtkomst.
    - Download.microsoft.com över HTTPS-port 443 krävs för partner förtecknings listan. 
    -  Internet åtkomst till eventuella kataloger från tredje part och uppdatering av innehållsfiler. Ytterligare andra portar än 443 kan behövas.
    - Uppdateringar från tredje part använder samma proxyinställningar som SUP.


## <a name="additional-requirements-when-the-sup-is-remote-from-the-top-level-site-server"></a>Ytterligare krav när SUP är fjärran sluten från plats servern på den översta nivån 

1. SSL måste vara aktiverat på SUP när den är fjärran sluten. Detta kräver ett certifikat för serverautentisering som skapats från en intern certifikat utfärdare eller via en offentlig Provider.
    - [Konfigurera SSL på WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol)
        - Observera att vissa av webb tjänsterna och de virtuella katalogerna alltid är HTTP och inte HTTPS när du konfigurerar SSL på WSUS. 
        - Configuration Manager laddar ned innehåll från tredje part för program uppdaterings paket från WSUS-innehålls katalogen via HTTP.   
    - [Konfigurera SSL på SUP](../get-started/install-a-software-update-point.md#configure-ssl-communications-to-wsus)

2. När du ställer in uppdateringar av WSUS-signeringscertifikat för uppdateringar till **Configuration Manager hanterar certifikatet** i egenskaperna för komponenten för program uppdaterings plats, krävs följande konfigurationer för att kunna skapa det självsignerade WSUS-signerings certifikatet: 
   - Fjär registret måste vara aktiverat på SUP-servern.
   -  **Anslutnings kontot för WSUS-servern** måste ha behörighet för fjärrregister på SUP/WSUS-servern. 


3. Skapa följande register nyckel på Configuration Manager plats Server: 
    - `HKLM\Software\Microsoft\Update Services\Server\Setup`skapar du ett nytt DWORD-värde med namnet **EnableSelfSignedCertificates** med värdet `1` . 

4. Så här aktiverar du installationen av det självsignerade WSUS-signeringscertifikat till betrodda utgivare och betrodda rot lager på den fjärranslutna SUP-servern:
   - **Anslutnings kontot för WSUS-servern** måste ha behörighet för fjärr administration på SUP-servern.

     Om det här objektet inte är möjligt exporterar du certifikatet från den lokala datorns WSUS-arkiv till betrodda utgivare och betrodda rot lager. 

> [!NOTE] 
>Du kan identifiera **anslutnings kontot för WSUS-servern** genom att visa fliken **Inställningar för proxy och konto** i egenskaperna för plats system rollen för SUP. Om inget konto anges används plats serverns dator konto.

## <a name="enable-third-party-updates-on-the-sup"></a>Aktivera uppdateringar från tredje part på SUP
Om du aktiverar det här alternativet kan du prenumerera på uppdaterings kataloger från tredje part i Configuration Manager-konsolen. Du kan sedan publicera dessa uppdateringar till WSUS och distribuera dem till klienter. Följande steg ska köras en gång per hierarki för att aktivera och konfigurera funktionen för användning. Du kan behöva köra stegen igen om du senare byter ut WSUS-servern på den översta nivån. 

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **plats konfiguration**och välj noden **platser** .
2. Välj platsen på den översta nivån i hierarkin. I menyfliksområdet klickar du på **Konfigurera plats komponenter**och väljer **program uppdaterings plats**.
3. Växla till fliken **uppdateringar från tredje part** . Välj alternativet **Aktivera program uppdateringar från tredje part**.

    ![Skärm bild för uppdatering av SUP från tredje part](media/third-party-sup-properties.PNG)


## <a name="configure-the-wsus-signing-certificate"></a>Konfigurera inloggnings certifikat för WSUS
Du måste bestämma om du vill att Configuration Manager automatiskt ska hantera WSUS-signeringscertifikat från tredje part med hjälp av ett självsignerat certifikat, eller om du behöver konfigurera certifikatet manuellt. 

### <a name="automatically-manage-the-wsus-signing-certificate"></a>Hantera signerings certifikatet för WSUS automatiskt
Om du inte har ett krav för att använda PKI-certifikat kan du välja att automatiskt hantera signerings certifikaten för uppdateringar från tredje part. Hantering av WSUS-certifikat görs som en del av synkroniseringsprocessen och registreras i `wsyncmgr.log` . 

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **plats konfiguration**och välj noden **platser** .
2. Välj platsen på den översta nivån i hierarkin. I menyfliksområdet klickar du på **Konfigurera plats komponenter**och väljer **program uppdaterings plats**.
3. Växla till fliken **uppdateringar från tredje part** . välj alternativet **Configuration Manager hanterar certifikatet**. 
4. Ett nytt certifikat av typen **WSUS-signering från tredje part** skapas i noden **certifikat** under **säkerhet** i arbets ytan **Administration** .  

### <a name="manually-manage-the-wsus-signing-certificate"></a>Hantera WSUS-signeringscertifikat manuellt
Om du behöver konfigurera certifikatet manuellt, till exempel för att behöva använda ett PKI-certifikat, måste du använda antingen [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server) eller något annat verktyg.  

1. Konfigurera signerings certifikatet med hjälp av [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server).
2. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **plats konfiguration**och välj noden **platser** .
3. Välj platsen på den översta nivån i hierarkin. I menyfliksområdet klickar du på **Konfigurera plats komponenter**och väljer **program uppdaterings plats**.
4. Växla till fliken **uppdateringar från tredje part** . Välj alternativet för **hantering av certifikatet manuellt**.


## <a name="enable-third-party-updates-on-the-clients"></a>Aktivera uppdateringar från tredje part på klienterna
Aktivera uppdateringar från tredje part på klienterna i klient inställningarna. Inställningen anger principen för Windows Update Agent för [Tillåt signerade uppdateringar för en Microsoft-uppdateringstjänst på intranätet](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates#allow-signed-updates-from-an-intranet-microsoft-update-service-location). Den här klient inställningen installerar även WSUS-signeringscertifikat till arkivet för betrodda utgivare på klienten. Loggningen av certifikat hanteringen visas `updatesdeployment.log` på klienterna.  Kör de här stegen för varje anpassad klient inställning som du vill använda för uppdateringar från tredje part. Mer information finns i artikeln [om klient inställningar](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates) .

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** och väljer noden **klient inställningar** .
2. Välj en befintlig anpassad klient inställning eller skapa en ny. 
3. Välj fliken **program uppdateringar** på vänster sida. Om du inte har den här fliken kontrollerar du att rutan **program uppdateringar** är aktive rad.
4. Ställ in **Aktivera program uppdateringar från tredje part** på **Ja**. 


## <a name="add-a-custom-catalog"></a>Lägg till en anpassad katalog
*Partner kataloger* är program leverantörs kataloger med information som redan har registrerats hos Microsoft. Med partner kataloger kan du prenumerera på dem utan att behöva ange ytterligare information. Kataloger som du lägger till kallas *anpassade kataloger*. Du kan lägga till en anpassad katalog från en uppdaterings leverantör från tredje part till Configuration Manager. Anpassade kataloger måste använda https och uppdateringarna måste signeras digitalt. 

1. Gå till arbets ytan **program uppdaterings bibliotek** , expandera **program uppdateringar**och välj noden **program uppdaterings kataloger från tredje part** . 
   
     ![Skärm bild för noden uppdateringar från tredje part](media/third-party-updates-node.PNG)
2. Klicka på **Lägg till anpassad katalog** i menyfliksområdet. 

     ![Uppdateringar från tredje part Lägg till anpassad katalog](media/third-party-updates-custom-catalog.png)
1. På sidan **Allmänt** anger du följande objekt: 
    - **Nedladdnings-URL**: en giltig HTTPS-adress för den anpassade katalogen.
    - **Utgivare**: namnet på den organisation som publicerar katalogen. 
    - **Namn**: namnet på den katalog som ska visas i Configuration Manager-konsolen. 
    - **Beskrivning**: en beskrivning av katalogen. 
    - **Support-URL** (valfritt): en giltig HTTPS-adress till en webbplats för att få hjälp med katalogen. 
    - **Support kontakt** (valfritt): kontakt information för att få hjälp med katalogen. 
2. Klicka på **Nästa** för att granska katalog översikten och fortsätta att slutföra **guiden program uppdateringar från tredje part**.


## <a name="subscribe-to-a-third-party-catalog-and-sync-updates"></a>Prenumerera på en katalog och synkronisera uppdateringar från tredje part
När du prenumererar på en katalog från tredje part i Configuration Manager-konsolen, synkroniseras metadata för varje uppdatering i katalogen till WSUS-servrarna för din SUP. Synkroniseringen av metadata tillåter klienterna att avgöra om någon av uppdateringarna är tillämplig. Utför följande steg för varje tredje parts katalog som du vill prenumerera på:  

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **program uppdateringar** och välj noden **program uppdaterings kataloger från tredje part** .  
2. Välj katalogen som du vill prenumerera på och klicka på **Prenumerera på katalog** i menyfliksområdet. 
    ![Uppdateringar från tredje part Lägg till anpassad katalog](media/third-party-updates-subscribe.png)
3. Granska och godkänn katalog certifikatet.  
   > [!NOTE]
   > 
   > När du prenumererar på en program uppdaterings katalog från tredje part läggs det certifikat som du granskar och godkänner i guiden till på-platsen. Det här certifikatet är av typen **program uppdaterings katalog från tredje part**. Du kan hantera den från noden **certifikat** under **säkerhet** i arbets ytan **Administration** .  
4. Slutför guiden. Efter den första prenumerationen ska katalogen börja hämtas om några minuter. 
    - Katalogen synkroniseras automatiskt var sjunde dag.
    - Klicka på **Synkronisera nu** i menyfliksområdet för att tvinga fram en synkronisering.
5. När katalogen har hämtats måste produktens metadata synkroniseras från WSUS-databasen till Configuration Manager databasen. [Starta synkroniseringen av program uppdateringar manuellt](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) för att synkronisera produkt informationen.
6. När produkt informationen har synkroniserats [konfigurerar du SUP för att synkronisera den önskade produkten](../get-started/configure-classifications-and-products.md#to-configure-classifications-and-products-to-synchronize) i Configuration Manager.  
7. [Starta synkroniseringen av program uppdateringar manuellt](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) för att synkronisera de nya produktens uppdateringar i Configuration Manager.  
8. När synkroniseringen är klar kan du se uppdateringar från tredje part i noden **alla uppdateringar** . De här uppdateringarna publiceras som **endast metadata-** uppdateringar förrän du väljer att publicera dem. 
     - Ikonen med en blå pil visar en programuppdatering med endast metadata. ![Ikon för program uppdatering med endast metadata](media/MetadataOnly.png)


## <a name="publish-and-deploy-third-party-software-updates"></a>Publicera och distribuera program uppdateringar från tredje part 
När uppdateringar från tredje part finns i noden **alla uppdateringar** kan du välja vilka uppdateringar som ska publiceras för distribution. När du publicerar en uppdatering laddas de binära filerna ned från leverantören och placeras i WSUSContent-katalogen på den översta nivån. 

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **program uppdateringar** och välj noden **alla program uppdateringar** .
2. Klicka på **Lägg till kriterier** för att filtrera listan över uppdateringar. Lägg till exempel till **leverantör** för **HP**. för att visa alla uppdateringar från HP.  
3. Välj de uppdateringar som krävs av din organisation. Klicka på **Publicera program uppdaterings innehåll från tredje part**.
    - Den här åtgärden hämtar binärfilerna för uppdateringen från leverantören och lagrar dem sedan i mappen WSUSContent på platsen för program uppdatering på den översta nivån. 
4. [Starta synkroniseringen av program uppdateringar manuellt](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) för att ändra status för publicerade uppdateringar från metadata – endast till distributions bara uppdateringar med innehåll. 
    >[!NOTE]
    >När du publicerar program uppdaterings innehåll från tredje part läggs alla certifikat som används för att signera innehållet till på-platsen. Dessa certifikat är av typen **program uppdaterings innehåll från tredje part**. Du kan hantera dem från noden **certifikat** under **säkerhet** i arbets ytan **Administration** .  

5. Granska förloppet i SMS_ISVUPDATES_SYNCAGENT. log. Loggen finns på platsen för program uppdatering på den översta nivån i mappen plats system loggar.
6. Distribuera uppdateringarna med hjälp av processen [distribuera program uppdateringar](../deploy-use/deploy-software-updates.md) . 
7. På sidan **hämtnings platser** i **guiden distribuera program uppdateringar**väljer du standard alternativet för att **Ladda ned program uppdateringar från Internet**. I det här scenariot har innehållet redan publicerats till program uppdaterings platsen, som används för att ladda ned innehållet för distributions paketet.
8. Klienterna måste köra en genomsökning och utvärdera uppdateringar innan du kan se resultatet av efterlevnaden.  Du kan aktivera den här cykeln manuellt från Configuration Manager kontroll panelen på en klient genom att köra åtgärden **genomsöknings cykel för program uppdateringar** .


## <a name="improvements-for-third-party-updates-starting-in-1910"></a><a name="bkmk_1910"></a>Förbättringar för uppdateringar från tredje part från 1910
<!--4469002-->
Nu har du fler detaljerade kontroller över synkroniseringen av uppdaterings kataloger från tredje part. Från och med Configuration Manager version 1910 kan du konfigurera synkroniseringsschemat för varje katalog oberoende av varandra. När du använder kataloger som innehåller kategoriserade uppdateringar kan du konfigurera synkroniseringen så att den endast innehåller vissa uppdaterings kategorier för att undvika synkronisering av hela katalogen. När du är säker på att du ska distribuera en kategori med kategoriserade kataloger kan du konfigurera den för automatisk nedladdning och publicering till WSUS.

### <a name="set-the-schedule-for-a-catalog-in-a-new-catalog-subscription"></a>Ange schemat för en katalog i en ny katalog prenumeration

1. Gå till arbets ytan **program varu bibliotek** , expandera **program uppdateringar**och välj noden **program uppdaterings kataloger från tredje part** .
1. Välj katalogen som du vill prenumerera på och klicka på **Prenumerera på katalog** i menyfliksområdet.
1. Välj alternativ på sidan **schema** om du vill åsidosätta standardschemat för synkronisering:
   - **Enkelt schema**: Välj tim-, dags-eller månads intervall.
   - **Anpassat schema**: Ange ett komplext schema.

### <a name="update-the-schedule-per-catalog"></a>Uppdatera schemat per katalog

1. Gå till arbets ytan **program varu bibliotek** , expandera **program uppdateringar**och välj noden **program uppdaterings kataloger från tredje part** .
1. Högerklicka på katalogen och välj **Egenskaper**.
1. Välj alternativ på fliken schema: 
   - **Enkelt schema**: Välj tim-, dags-eller månads intervall.
   - **Anpassat schema**: Ange ett komplext schema.

### <a name="new-subscription-to-a-third-party-v3-catalog"></a>Ny prenumeration på en tredje part v3-katalog

> [!IMPORTANT]
> Det här alternativet är bara tillgängligt för v3-uppdaterings kataloger från tredje part, som stöder kategorier för uppdateringar. De här alternativen är inaktiverade för kataloger som inte har publicerats i det nya v3-formatet.


1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **program uppdateringar** och välj noden **program uppdaterings kataloger från tredje part** .
1. Välj katalogen som du vill prenumerera på och klicka på **Prenumerera på katalog** i menyfliksområdet.
1. Välj alternativ på sidan **Välj kategorier** :

   - **Synkronisera alla uppdaterings kategorier** (standard)
       - Synkroniserar alla uppdateringar i uppdaterings katalogen från tredje part i Configuration Manager.
   -  **Välj kategorier för synkronisering**
       - Välj vilka kategorier och underordnade kategorier som ska synkroniseras till Configuration Manager.

      ![Välj uppdaterings kategorier som ska synkroniseras till Configuration Manager](./media/4469002-select-categories-for-sync.png)
1. Välj om du vill **mellanlagra uppdaterings innehållet** för katalogen. När du mellanlagrar innehållet hämtas alla uppdateringar i de valda kategorierna automatiskt till program uppdaterings platsen på den högsta nivån, vilket innebär att du inte behöver se till att de redan har laddats ned innan du distribuerar. Du bör bara automatiskt mellanlagra innehåll för uppdateringar som du sannolikt kommer att distribuera dem för att undvika onödigt högt bandbredds-och lagrings krav.

   - **Mellanlagra inte innehåll, synkronisera endast för genomsökning (rekommenderas)**
     - Hämta inte innehåll för uppdateringar i katalogen från tredje part
   - **Mellanlagra innehållet för de markerade kategorierna automatiskt**
     - Välj de uppdaterings kategorier som innehållet ska laddas ned automatiskt.
     - Innehållet för uppdateringar i valda kategorier laddas ned till den översta program uppdaterings platsens WSUS-innehålls katalog.
      ![Välj Uppdatera kategorier för att mellanlagra innehåll](./media/4469002-stage-content.png)
1. Ange ditt **schema** för katalog synkronisering och slutför sedan guiden.

 

### <a name="edit-an-existing-subscription"></a>Redigera en befintlig prenumeration

> [!IMPORTANT]
> Det här alternativet är bara tillgängligt för v3-uppdaterings kataloger från tredje part, som stöder kategorier för uppdateringar. De här alternativen är inaktiverade för kataloger som inte har publicerats i det nya v3-formatet.

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **program uppdateringar** och välj noden **program uppdaterings kataloger från tredje part** .
1. Högerklicka på katalogen och välj **Egenskaper**.
1. Välj alternativ på fliken **Välj kategorier** .
   - **Synkronisera alla uppdaterings kategorier** (standard)
       - Synkroniserar alla uppdateringar i uppdaterings katalogen från tredje part i Configuration Manager.
   -  **Välj kategorier för synkronisering**
       - Välj vilka kategorier och underordnade kategorier som ska synkroniseras till Configuration Manager.
1. Välj alternativ för innehålls sidan **scen uppdaterings innehåll** .
   - **Mellanlagra inte innehåll, synkronisera endast för genomsökning (rekommenderas)**
     - Hämta inte innehåll för uppdateringar i katalogen från tredje part
   - **Mellanlagra innehållet för de markerade kategorierna automatiskt**
     - Välj de uppdaterings kategorier som innehållet ska laddas ned automatiskt.
     - Innehållet för uppdateringar i valda kategorier laddas ned till den översta program uppdaterings platsens WSUS-innehålls katalog. 

## <a name="monitoring-progress-of-third-party-software-updates"></a>Övervaknings förlopp för program uppdateringar från tredje part 

Synkronisering av program uppdateringar från tredje part hanteras av SMS_ISVUPDATES_SYNCAGENT-komponenten på den översta standard program uppdaterings platsen. Du kan visa status meddelanden från den här komponenten eller Visa mer detaljerad status i SMS_ISVUPDATES_SYNCAGENT. log. Den här loggen finns på program uppdaterings platsen på den översta nivån i mappen plats system loggar. Som standard är den här sökvägen C:\Program\Microsoft Configuration Manager\Logs. Mer information om övervakning av den allmänna processen för program uppdaterings hantering finns i [övervaka program uppdateringar](../deploy-use/monitor-software-updates.md) 

## <a name="known-issues"></a>Kända problem

- Datorn där-konsolen körs används för att ladda ned uppdateringarna från WSUS och lägga till den i uppdaterings paketet. WSUS-signeringscertifikat måste vara betrott på konsol datorn. Om den inte är det kan du se problem med att kontrol lera signaturen under hämtningen av uppdateringar från tredje part. 
- Tjänsten för synkronisering av program uppdateringar från tredje part kan inte publicera innehåll till uppdateringar som har lagts till i WSUS av ett annat program, verktyg eller skript, till exempel SCUP. Åtgärden **publicera innehålls program från tredje part** kan inte utföras på dessa uppdateringar. Om du behöver distribuera uppdateringar från tredje part som den här funktionen ännu inte stöder, använder du den befintliga processen fullständigt för att distribuera uppdateringarna.  
-  Configuration Manager har en ny version för katalogens CAB-filformat. Den nya versionen innehåller certifikaten för leverantörens binära filer. Dessa certifikat läggs till i noden **certifikat** under **säkerhet** i arbets ytan **Administration** när du godkänner och litar på katalogen.  
     - Du kan fortfarande använda den äldre katalogen CAB-filversion så länge nedladdnings-URL: en är https och uppdateringarna signeras. Innehållet kan inte publiceras eftersom certifikaten för binärfilerna inte finns i CAB-filen och redan har godkänts. Du kan undvika det här problemet genom att söka efter certifikatet i noden **certifikat** , ta bort blockeringen och sedan publicera uppdateringen igen. Om du publicerar flera uppdateringar som är signerade med olika certifikat måste du avblockera varje certifikat som används.
     - Mer information finns i status meddelanden 11523 och 11524 i tabellen nedan status meddelande.
-  När program uppdaterings tjänsten från tredje part på den översta nivån för program uppdaterings platsen på den översta nivån kräver en proxyserver för Internet åtkomst, kan det hända att kontroller av digitala signaturer Miss lyckas. Du kan åtgärda det här problemet genom att konfigurera inställningarna för WinHTTP-proxyn på plats systemet. Mer information finns i [netsh-kommandon för WinHTTP](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731131(v=ws.10)).
- När du använder en CMG för innehålls lagring laddas inte innehållet för uppdateringar från tredje part ned till klienter om inställningen **Hämta delta innehåll när den tillgängliga** [klienten](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) är aktive rad. <!--6598587-->

## <a name="status-messages"></a>Statusmeddelanden

| Meddelande       | Allvarlighetsgrad           | Beskrivning | Möjlig orsak| Möjlig lösning
| ------------- |-------------| -----|----|----|
| 11516     | Fel |Det gick inte att publicera innehåll för uppdateringen av uppdaterings-ID eftersom innehållet är osignerat.  Det går bara att publicera innehåll med giltiga signaturer.  |Configuration Manager tillåter inte att osignerade uppdateringar publiceras.| Publicera uppdateringen på ett annat sätt. </br></br>Se om en signerad uppdatering är tillgänglig från leverantören.|
| 11523  | Varning |  Katalogen "X" omfattar inte innehålls signerings certifikat. försök att publicera uppdaterings innehåll för uppdateringar från den här katalogen kan Miss lyckas förrän innehålls signerings certifikaten har lagts till och godkänts. | Det här meddelandet kan inträffa när du importerar en katalog som använder en äldre version av CAB-filformat.|Kontakta katalog leverantören för att få en uppdaterad katalog som innehåller certifikat för innehålls signering. </br> </br> Certifikaten för binärfilerna ingår inte i CAB-filen så innehållet kan inte publiceras. Du kan undvika det här problemet genom att söka efter certifikatet i noden **certifikat** , ta bort blockeringen och sedan publicera uppdateringen igen. Om du publicerar flera uppdateringar som är signerade med olika certifikat måste du avblockera varje certifikat som används.|
| 11524| Fel  | Det gick inte att publicera uppdateringen "ID" på grund av saknade metadata för uppdatering. | Uppdateringen kan ha synkroniserats till WSUS utanför Configuration Manager.| Synkronisera uppdateringen med Configuration Manager innan du försöker publicera dess innehåll.  </br> </br>Om ett externt verktyg används för att publicera uppdateringen som **metadata**, använder du samma verktyg för att publicera uppdaterings innehållet.|



## <a name="working-with-third-party-updates-video"></a>Arbeta med video om uppdateringar från tredje part
<iframe width="560" height="315" src="https://www.youtube.com/embed/ai8rLCLtuTI?rel=0" frameborder="0" allowfullscreen></iframe>



## <a name="next-step"></a>Nästa steg
> [!div class="nextstepaction"]
> [Distribuera programuppdateringar](./deploy-software-updates.md)
