---
title: Hantera inställningar för programuppdateringar
titleSuffix: Configuration Manager
description: Läs om de klient inställningar som är lämpliga för program uppdateringar på din webbplats när du har installerat program uppdaterings platsen.
ms.date: 03/30/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 0d484c1a-e903-4bff-9e9b-e452c62e38a8
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 0a2a45ff866ea02aacc83c42109c8cba4020ed4e
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906805"
---
#  <a name="manage-settings-for-software-updates"></a><a name="BKMK_ManageSUSettings"></a>Hantera inställningar för program uppdateringar  

*Gäller för: Configuration Manager (aktuell gren)*

När du har synkroniserat program uppdateringar i Configuration Manager konfigurerar och kontrollerar du inställningarna i följande avsnitt.

##  <a name="client-settings-for-software-updates"></a><a name="BKMK_ClientSettings"></a> Klientinställningar för programuppdateringar  
När du installerar platsen för programuppdatering aktiveras programuppdateringar som standard på klienterna, och inställningarna på sidan **Programuppdateringar** i klientinställningarna har standardvärden. Klient inställningarna används hela platsen och påverkas när program uppdateringar genomsöks efter kompatibilitet och hur och när program uppdateringar installeras på klient datorer. Innan du distribuerar program uppdateringar kontrollerar du att klient inställningarna är lämpliga för program uppdateringar på din plats.  

> [!IMPORTANT]  
>  Inställningen **Aktivera programvaruuppdateringar på klienter** aktiveras som standard. Om du avmarkerar den här inställningen tar Configuration Manager bort befintliga distributions principer från klienten.  

Information om hur du konfigurerar klient inställningar finns i [Konfigurera klient inställningar](../../core/clients/deploy/configure-client-settings.md).  

Mer information om klient inställningarna finns i [om klient inställningar](../../core/clients/deploy/about-client-settings.md).  

##  <a name="group-policy-settings-for-software-updates"></a><a name="BKMK_GroupPolicy"></a> Grupprincipinställningar för programuppdateringar  
Det finns specifika grupprincipinställningar som används av Windows Update Agent (WUA) på klientdatorer för att ansluta till WSUS som körs på platsen för programuppdatering. Dessa grupprincipinställningar används också för att söka igenom programuppdateringarnas efterlevnad och för att uppdatera programuppdateringarna och WUA automatiskt.

### <a name="specify-intranet-microsoft-update-service-location-local-policy"></a>Den lokala principen Ange sökväg till tjänsten Microsoft Update på intranätet  
När programuppdateringsplatsen har skapats för en plats tar klienterna emot en datorprincip som förser dem med programuppdateringsplatsens servernamn och konfigurerar den lokala principen **Ange sökväg till tjänsten Microsoft Update på intranätet** på datorn. WUA hämtar servernamnet som anges i inställningen **Ange intranätserver för identifiering av uppdateringar**, och sedan ansluter WUA till denna server när den söker igenom programuppdateringarnas kompatibiliteter. När en domänprincip skapas för inställningen **Ange sökväg till tjänsten Microsoft Update på intranätet** åsidosätts den lokala principen så att WUA kan ansluta till en annan server än platsen för programuppdatering. Om detta inträffar kan det hända att klienten söker efter programuppdateringarnas kompatibilitet med utgångspunkt i olika produkter, klassificeringar och språk. Därför bör du inte konfigurera Active Directory-principen för klientdatorerna.  

### <a name="allow-signed-content-from-intranet-microsoft-update-service-location-group-policy"></a>Grupprincipen Tillåt signerat innehåll från tjänsten Microsoft Update på intranätet  
Du måste aktivera grupprincipinställningen **Tillåt signerat innehåll från Microsoft-uppdateringstjänst på intranätet** innan WUA (på datorerna) söker efter programuppdateringar som har skapats och publicerats med System Center Updates Publisher. När principinställningen har aktiverats godtar WUA programuppdateringar som tas emot via en plats i intranätet, om programuppdateringarna har signerats i certifikatarkivet **Betrodda utgivare** på den lokala datorn. Mer information om vilka grupprincipinställningar som krävs för Updates Publisher finns i [dokumentationsbiblioteket för Updates Publisher 2011](https://docs.microsoft.com/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10)).  

### <a name="automatic-updates-configuration"></a>Konfiguration av automatiska uppdateringar  
Automatiska uppdateringar gör att säkerhetsuppdateringar och andra viktiga uppdateringar kan hämtas till klientdatorerna. Automatiska uppdateringar konfigureras i grupprincipinställningen **Konfigurera automatiska uppdateringar** eller på kontrollpanelen på den lokala datorn. När Automatiska uppdateringar har aktiverats kan klientdatorerna ta emot uppdateringsaviseringar, och om inställningarna har konfigurerats rätt kan klientdatorerna hämta och installera nödvändiga uppdateringar. När Automatiska uppdateringar används samtidigt som programuppdateringar kan varje klientdator visa både aviseringsikoner och meddelandefönster om samma uppdatering. När klientdatorn måste startas om kan varje klientdator dessutom visa en dialogruta om omstarten för samma uppdatering.  

### <a name="self-update"></a>Självuppdatering  
När Automatiska uppdateringar har aktiverats på klientdatorerna utför WUA automatiskt en självuppdatering när en nyare version blir tillgänglig eller om det uppstår problem med en WUA-komponent. När Automatiska uppdateringar inte har konfigurerats eller om de är inaktiverade och klientdatorerna har en äldre version av WUA, måste klientdatorerna köra WUA-installationsfilen.  

## <a name="software-updates-properties"></a>Egenskaper för program uppdateringar
Egenskaperna för programuppdatering ger information om programuppdateringar och associerat innehåll. Du kan också använda dessa egenskaper för att konfigurera inställningar för programuppdateringar. När du öppnar egenskaper för flera programuppdateringar visas endast flikarna **Maximal körtid** och **Anpassad allvarlighetsgrad** .   

Använd följande procedur för att öppna egenskaper för programuppdatering.  

#### <a name="to-open-software-update-properties"></a>Öppna egenskaper för programuppdatering  

1. I Configuration Manage-konsolen klickar du på **Programbibliotek**.  
2. Expandera **Programuppdateringar** på arbetsytan Programbibliotek och klicka sedan på **Alla programuppdateringar**.  
3. Välj en eller flera programuppdateringar och klicka sedan på **Egenskaper** på fliken **Start** i gruppen **Egenskaper** .  

   > [!NOTE]  
   >  I noden **alla program uppdateringar** visar Configuration Manager endast de program uppdateringar som har klassificeringen **kritisk** och **säkerhet** och som har släppts under de senaste 30 dagarna.  

###  <a name="review-software-updates-information"></a><a name="BKMK_SoftwareUpdatesInformation"></a>Granska information om program uppdateringar  
I egenskaperna för programuppdatering kan du granska detaljerad information om en programuppdatering. Den detaljerade informationen visas inte när du väljer fler än en programuppdatering. I följande avsnitt beskrivs informationen som är tillgänglig för en vald programuppdatering.  

####  <a name="software-update-details"></a><a name="BKMK_SoftwareUpdateDetails"></a> Programuppdateringsinformation  
På fliken **Uppdateringsinformation** kan du se följande översiktsinformation om den valda programuppdateringen:  

- **Anslags-ID**: Anger det anslags-ID som är associerat med säkerhetsprogramuppdateringar. Du hittar information om säkerhetsbulletiner genom att söka efter Bulletin-ID: t på webb sidan [Microsoft Security Response Center](https://portal.msrc.microsoft.com/) .  

> [!NOTE]
> Hur säkerhets uppdateringar av Microsoft-dokument ändras. Föregående webb sidor för modell användning av säkerhets bulletiner och innehöll ID-nummer för säkerhetsbulletiner (t. ex. MS16-XXX) som en pivot-punkt. Den här typen av dokumentation om säkerhets uppdatering, inklusive Bulletin-ID-nummer, dras tillbaka och ersätts med säkerhets uppdaterings guiden. I stället för Bulletin-ID: n, pivoterar den nya guiden om sårbarhets-ID-nummer och KB-artikel-ID-nummer Mer information finns i [vanliga frågor och svar om säkerhets uppdaterings guide](https://www.microsoft.com/msrc/faqs-security-update-guide).


- **Artikel-ID**: Anger artikel-ID:t för programuppdateringen. Den artikel som refereras innehåller mer detaljerad information om programuppdateringen och det problem som åtgärdas eller förbättras.  

- **Reviderad**: Anger det datum då programuppdateringen senast ändrades.  

- **Maximal allvarlighetsgrad**:Anger den leverantörsdefinierade allvarlighetsgraden för programuppdateringen.  

- **Beskrivning**: Ger en översikt över vilket tillstånd som programuppdateringen åtgärdar eller förbättrar.  

- **Tillämpliga språk**: Listar de språk som programuppdateringen gäller.  

- **Påverkade produkter**: Listar de produkter som programuppdateringen gäller.  

####  <a name="content-information"></a><a name="BKMK_ContentInformation"></a> Innehållsinformation  
På fliken **Innehållsinformation** granskar du följande information om det innehåll som är associerat med den valda programuppdateringen:  

-   **Innehålls-ID**: Anger innehålls-ID:t för programuppdateringen.  

-   **Hämtad**: anger om Configuration Manager har hämtat program uppdaterings filerna.  

-   **Språk**: Anger språk-ID:t för programuppdateringen.  

-   **Källsökväg**: Anger sökvägen för källfilerna för programuppdatering.  

-   **Storlek (MB)**: Anger storleken på källfilerna för programuppdatering.  

####  <a name="custom-bundle-information"></a><a name="BKMK_CustomBundleInformation"></a> Anpassad paketinformation  
På fliken **Anpassad paketinformation** granskar du den anpassade paketinformationen för programuppdateringen. När den valda programuppdateringen innehåller anpassade programuppdateringar som ingår i programuppdateringsfilen visas de i avsnittet **Paketinformation** . Under den här fliken visas inte paketerade programuppdateringar som visas på fliken **Innehållsinformation**, till exempel uppdateringsfiler för olika språk.  

####  <a name="supersedence-information"></a><a name="BKMK_SupersedenceInformation"></a> Ersättningsinformation  
På fliken **Ersättningsinformation** kan du se följande information om ersättningen av programuppdateringen:  

- **Den här uppdateringen har ersatts av följande uppdateringar**: Anger programuppdateringar som ersätter den här uppdateringen, vilket innebär att de uppdateringar som listas är nyare. I de flesta fall distribuerar du en av dessa programuppdateringar som ersätter programuppdateringen. Programuppdateringarna som visas i listan innehåller hyperlänkar till webbsidor som innehåller mer information om programuppdateringarna. När den här uppdateringen inte ersätts visas **Ingen** .  

- **Den här uppdateringen ersätter följande uppdateringar**: Anger de programuppdateringar som ersätts av den här programuppdateringen, vilket innebär att programuppdateringen är nyare. I de flesta fall distribuerar du den här programuppdateringen för att byta ut de ersatta programuppdateringarna. Programuppdateringarna som visas i listan innehåller hyperlänkar till webbsidor som innehåller mer information om programuppdateringarna. När den här uppdateringen inte ersätter någon annan uppdateringen visas **Inget**.  

###  <a name="configure-software-updates-settings"></a><a name="BKMK_SoftwareUpdatesSettings"></a> Konfigurera inställningar för programuppdateringar  
I egenskaper kan du konfigurera inställningar för programuppdateringar för en eller flera programuppdateringar. Du kan konfigurera de flesta inställningar för programuppdatering på den centrala administrationsplatsen eller den fristående primära platsen. Följande avsnitt innehåller hjälp om hur du konfigurerar inställningar för programuppdateringar.  

####  <a name="set-maximum-run-time"></a><a name="BKMK_SetMaxRunTime"></a> Ange maximal körtid  
På fliken **Maximal körningstid** anger du den maximala tidsperiod som en programuppdatering tilldelas för att slutföras på klientdatorer. Om uppdateringen tar längre tid än det maximala körnings tids värdet skapar Configuration Manager ett status meddelande och slutar övervaka distributionen för program uppdaterings installationen. Du kan bara konfigurera den här inställningen på den centrala administrationsplatsen eller på en fristående primär plats.  

Configuration Manager använder också den här inställningen för att avgöra om installationen av program uppdateringen ska initieras inom ett konfigurerat underhålls fönster. Om det maximala körningstidsvärdet är större än den tillgängliga återstående tiden i underhållsfönstret skjuts installationen av programuppdateringarna upp till starten av nästa underhållsfönster. När det finns flera programuppdateringar att installera på en klientdator med ett konfigurerat underhållsfönster (tidsram) installeras programuppdateringen med den lägsta maximala körningstiden först, sedan programuppdateringen med den näst lägsta maximala körningstiden och så vidare. Innan varje programuppdatering installeras verifierar klienten att det tillgängliga underhållsfönstret erbjuder tillräckligt lång tid för att installera programuppdateringen. När installationen av en programuppdatering har påbörjats fortsätter den att installeras även om installationen fortsätter när underhållsfönstret är slut. Mer information om underhålls perioder finns i [använda underhålls fönster](../../core/clients/manage/collections/use-maintenance-windows.md).  

På fliken **Maximal körningstid** kan du visa och konfigurera följande inställningar:  

- **Maximal kör tid**: anger det maximala antalet minuter som har tilldelats för att en program uppdaterings installation ska slutföras innan installationen inte längre övervakas av Configuration Manager. Den här inställningen används också för att bestämma om det finns tillräckligt med tid kvar för att installera uppdateringen innan underhållsfönstret tar slut. Standardvärdet är 60 minuter för Service Pack. För andra program uppdaterings typer är standardvärdet 10 minuter om du gjorde en ny installation av Configuration Manager version 1511 eller senare och 5 minuter när du har uppgraderat från en tidigare version. Värdena kan ligga mellan 5 till 9999 minuter.  

> [!IMPORTANT]  
>  Se till att ange det maximala kör tids värde som är mindre än den konfigurerade underhålls perioden eller öka tiden för underhålls perioden till ett värde som är större än den maximala körnings tiden. Annars initieras aldrig installationen av programuppdateringen.  

####  <a name="set-custom-severity"></a><a name="BKMK_SetCustomSeverity"></a>Ange anpassad allvarlighets grad  
I egenskaperna för en programuppdatering kan du använda fliken **Anpassad allvarlighetsnivå** om du vill konfigurera anpassade allvarlighetsgrader för programuppdateringarna. Detta kan vara nödvändigt om de fördefinierade allvarlighetsgraderna inte motsvarar dina behov. De anpassade värdena visas i kolumnen **anpassad allvarlighets grad** i Configuration Manager-konsolen. Du kan sortera programuppdateringarna efter de anpassade allvarlighetsgraderna och kan även skapa frågor och rapporter som kan filtrera enligt dessa värden. Du kan konfigurera den här inställningen enbart för den centrala administrationsplatsen eller för en fristående primär plats.  

Du kan konfigurera följande inställningar på fliken **Anpassad allvarlighetsnivå** .  

- **Anpassad allvarlighetsgrad**: Anger en anpassad allvarlighetsgrad för programuppdateringarna. Välj **Kritisk**, **Viktig**, **Måttlig**eller **Låg** från listan. Som standard är den anpassade allvarlighetsgraden tom.

## <a name="crl-checking-for-software-updates"></a>CRL-kontroll för program uppdateringar
Som standard kontrol leras inte CRL-listan (Certificate Revocation List) när signaturen på Configuration Manager program uppdateringar verifieras. Att kontrollera CRL-listan vid varje certifikatanvändning ger högre säkerhet än att använda ett certifikat som har återkallats, men ger även upphov till att anslutningen blir långsammare och att belastningen ökar på den dator där CRL-kontrollen utförs.  

Om CRL-kontrollen används måste den vara aktive rad på de Configuration Manager-konsoler som bearbetar program uppdateringar.  

#### <a name="to-enable-crl-checking"></a>Aktivera CRL-kontroll  
På den dator som utför CRL-kontrollen går du till produkt-DVD: n och kör följande från en kommando tolk: **\SMSSETUP\BIN\X64 \\ ** < *language* > **\UpdDwnldCfg.exe/checkrevocation**.  

Till exempel för engelska (US) kör **\SMSSETUP\BIN\X64\00000409\UpdDwnldCfg.exe/checkrevocation**  
