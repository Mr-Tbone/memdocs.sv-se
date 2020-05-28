---
title: Optimera leverans för Windows 10-uppdatering
titleSuffix: Configuration Manager
description: Lär dig hur du använder Configuration Manager för att hantera uppdaterings innehåll för att hålla dig uppdaterad med Windows 10.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: b670cfaf-96a4-4fcb-9caa-0f2e8c2c6198
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 835dcd0c86244c1731cb6c6e040d577160759614
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83267798"
---
# <a name="optimize-windows-10-update-delivery-with-configuration-manager"></a>Optimera Windows 10-uppdaterings leverans med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

För många kunder börjar en lyckad väg att få och hålla sig uppdaterad med Windows 10 månads uppdateringar med en bra innehålls distributions strategi med hjälp av Configuration Manager. Storleken på de månatliga kvalitets uppdateringarna kan vara en risk för stora organisationer. Det finns några tillgängliga tekniker som hjälper till att minska bandbredden och nätverks belastningen för att optimera uppdaterings leveransen. Den här artikeln förklarar dessa tekniker, jämför dem och ger rekommendationer för att hjälpa dig att fatta beslut om vilka en som ska användas.  
 
Windows 10 tillhandahåller flera olika typer av uppdateringar. Mer information finns i [uppdaterings typer i Windows Update för företag](/windows/deployment/update/waas-manage-updates-wufb#types-of-updates-managed-by-windows-update-for-business). Den här artikeln fokuserar på Windows 10- *kvalitets* uppdateringar med Configuration Manager. 


## <a name="express-update-delivery"></a>Leverans av Express uppdatering

Hämtnings bara filer för Windows 10-kvalitet kan vara stora. Alla paket innehåller alla tidigare utgivna korrigeringar för att säkerställa konsekvens och enkelhet. Microsoft har kunnat minska storleken på det uppdaterings innehåll i Windows 10 som varje klient laddar ned med en funktion som heter Express. Express används idag av miljon tals enheter som hämtar uppdateringar direkt från den Windows Update tjänsten och minskar storleks nedladdningen avsevärt. Den här förmånen är också tillgänglig för kunder vars klienter inte direkt laddas ned från tjänsten Windows Update. 

Configuration Manager lagt till stöd för [Express installationsfiler](manage-express-installation-files-for-windows-10-updates.md) för Windows 10 kvalitets uppdateringar i version 1702. För den bästa upplevelsen rekommenderar vi dock att du använder Configuration Manager version 1802 eller senare. För bästa prestanda vid nedladdnings hastigheten rekommenderar vi också att du använder Windows 10, version 1703 eller senare. 

> [!NOTE]  
> Innehållet i Express-versionen är betydligt större än den fullständiga fil versionen. En snabb installations fil innehåller alla möjliga variationer för varje fil som den är avsedd att uppdateras. Därför ökar den mängd disk utrymme som krävs för uppdateringar i uppdaterings paketets källa och på distributions platser när du aktiverar Express support i Configuration Manager. Även om kravet på disk utrymme på distributions platserna ökar, minskar innehålls storleken som klienterna laddar ned från dessa distributions platser. Klienterna laddar bara ned de bitar de behöver (delta), men inte hela uppdateringen.


## <a name="peer-to-peer-content-distribution"></a>Distribution av peer-to-peer-innehåll

Även om klienterna bara laddar ned de delar av innehållet som de behöver, så kan du påskynda Windows-uppdateringar i din miljö genom att använda peer-to-peer-innehåll distribution. Att använda peer-datorer som en nedladdnings källa för kvalitets uppdateringar kan vara fördelaktiga för miljöer där lokala distributions platser inte finns på fjärranslutna kontor. Det här beteendet förhindrar att alla klienter laddar ned innehåll från en fjärrdistributions plats via en långsam WAN-länk. Att använda peer-datorer kan också vara fördelaktigt när klienterna återgår till tjänsten Windows Update. Endast en peer krävs för att ladda ned uppdaterings innehåll från molnet innan det blir tillgängligt för andra enheter.

Configuration Manager stöder många peer-to-peer-tekniker, inklusive följande:
- Leverans optimering för Windows
- Configuration Manager peer-cache
- Windows BranchCache  

Följande avsnitt innehåller ytterligare information om dessa tekniker.

### <a name="windows-delivery-optimization"></a>Leverans optimering för Windows

[Leverans optimering](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) är den viktigaste nedladdnings tekniken och peer-to-peer-distribution som är inbyggd i Windows 10. Windows 10-klienter kan hämta innehåll från andra enheter i det lokala nätverket som laddar ned samma uppdateringar. Med de [Windows-alternativ som är tillgängliga för leverans optimering](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#delivery-optimization-options)kan du konfigurera klienter i grupper. Den här grupperingen gör det möjligt för din organisation att identifiera enheter som eventuellt är de bästa kandidaterna för att uppfylla peer-to-peer-begäranden. Leverans optimering minskar avsevärt den totala bandbredd som används för att hålla enheterna uppdaterade samtidigt som hämtnings tiden går snabbare.

> [!NOTE]  
> Leverans optimering är en moln-hanterad lösning. Internet åtkomst till moln tjänsten för leverans optimering är ett krav för att använda peer-to-peer-funktioner. Information om vilka Internet-slutpunkter som behövs finns i [vanliga frågor och svar om leverans optimering](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions). 

För bästa resultat kan du behöva ange [hämtnings läget](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#download-mode) för leverans optimering till **grupp (2)** och definiera grupp- *ID: n*. I grupp läge kan peering korsa interna undernät mellan enheter som tillhör samma grupp, inklusive enheter på fjärranslutna kontor. Använd [alternativet grupp-ID](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#select-the-source-of-group-ids) för att skapa en egen anpassad grupp oberoende av domäner och AD DS-platser. Grupp hämtnings läge är det rekommenderade alternativet för de flesta organisationer som vill uppnå bästa möjliga bandbredds optimering med leverans optimering.

Det är svårt att konfigurera dessa grupp-ID: n manuellt när klienterna växlar över olika nätverk. Configuration Manager version 1802 lade till en ny funktion för att förenkla hanteringen av den här processen genom att [integrera gränser grupper med leverans optimering](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization). När en klient aktive ras, kommunicerar den med hanterings platsen för att hämta principer och ger dess nätverks-och gränser grupp information. Configuration Manager skapar ett unikt ID för varje avgränsnings grupp. Platsen använder klientens plats information för att automatiskt konfigurera klientens ID för leverans optimerings grupp med Configuration Manager gränser-ID. När klienten växlar till en annan avgränsnings grupp pratar den med sin hanterings plats och konfigureras automatiskt på nytt med ett nytt avgränsnings grupps-ID. Med den här integrationen kan leverans optimering använda Configuration Manager gränser för att hitta en peer som uppdateringar ska hämtas från.

### <a name="delivery-optimization-starting-in-version-1910"></a><a name="bkmk_DO-1910"></a>Leverans optimering från och med version 1910
<!--4699118-->
Från och med Configuration Manager version 1910 kan du använda leverans optimering för distribution av allt Windows Update-innehåll för klienter som kör Windows 10 version 1709 eller senare, inte bara Express-installationsfiler.

Om du vill använda leverans optimering för alla installationsfiler för Windows Update aktiverar du följande [klient inställningar för program uppdateringar](../../core/clients/deploy/about-client-settings.md#software-updates):

- **Tillåt att klienter laddar ned delta innehåll när det är tillgängligt** på **Ja**.
- **Port som klienter använder för att ta emot begär Anden om delta-innehåll** som är inställt på 8005 (standard) eller ett anpassat port nummer.

> [!IMPORTANT]
> - Leverans optimering måste vara aktive rad (standard) och inte kringgås. Mer information finns i [referens för Windows Delivery Optimization](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference).
> - Verifiera [inställningarna för leverans optimerings klient](../../core/clients/deploy/about-client-settings.md#delivery-optimization) när du ändrar [klient inställningarna för program uppdateringar](../../core/clients/deploy/about-client-settings.md#software-updates) för delta innehåll.
> - Det går inte att använda leverans optimering för Office 365-klient uppdateringar om Office COM är aktiverat. Office COM används av Configuration Manager för att hantera uppdateringar för Office 365-klienter. Du kan avregistrera Office COM för att tillåta användning av leverans optimering för Office 365-uppdateringar. När Office COM är inaktiverat hanteras program uppdateringar för Office 365 av den schemalagda uppgiften standard Office automatiska uppdateringar 2,0. Det innebär att Configuration Manager inte dikterar eller övervakar installations processen för Office 365-uppdateringar. Configuration Manager fortsätter att samla in information från maskin varu inventeringen för att fylla i instrument panelen för Office 365-klient hantering i-konsolen. Information om hur du avregistrerar Office COM finns i [Aktivera office 365-klienter för att ta emot uppdateringar från Office CDN i stället för Configuration Manager](https://docs.microsoft.com/deployoffice/manage-office-365-proplus-updates-with-configuration-manager#enable-office-365-clients-to-receive-updates-from-the-office-cdn-instead-of-configuration-manager).
> - När du använder en CMG för innehålls lagring laddas inte innehållet för uppdateringar från tredje part ned till klienter om inställningen **Hämta delta innehåll när den tillgängliga** [klienten](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) är aktive rad. <!--6598587-->


### <a name="configuration-manager-peer-cache"></a>Configuration Manager peer-cache

[Peer-cache](../../core/plan-design/hierarchy/client-peer-cache.md) är en funktion i Configuration Manager som gör att klienter kan dela med andra klient innehåll direkt från deras lokala Configuration Manager cache. Peer-cache ersätter inte användningen av andra peer caching-lösningar som Windows BranchCache. Det fungerar tillsammans med dem för att ge fler alternativ för att utöka traditionella lösningar för innehålls distribution, till exempel distributions platser. Peer-cache förlitar sig inte på BranchCache. Om du inte aktiverar eller använder BranchCache fungerar peer-cache fortfarande.

> [!NOTE]  
> Klienter kan bara ladda ned innehåll från peer-cache-klienter som finns i den aktuella gränser-gruppen.  


### <a name="windows-branchcache"></a>Windows BranchCache
[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) är en teknik för optimering av bandbredd i Windows. Varje klient har en cache och fungerar som en alternativ källa för innehåll. Enheter i samma nätverk kan begära det här innehållet. [Configuration Manager kan använda BranchCache](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache) för att tillåta att peer-datorer från varandra och alltid måste kontakta en distributions plats. Med BranchCache cachelagras filer på varje enskild klient och andra klienter kan hämta dem efter behov. Den här metoden distribuerar cacheminnet i stället för att ha en enda hämtnings punkt. Det här beteendet sparar en stor mängd bandbredd och minskar tiden för klienter att ta emot det begärda innehållet.



## <a name="selecting-the-right-peer-caching-technology"></a>Välja rätt teknik för peer-cachelagring

Att välja rätt peer caching-teknik för Express-installationsfiler beror på din miljö och dina krav. Även om Configuration Manager stöder alla ovanstående peer-to-peer-tekniker bör du använda de som passar bäst för din miljö. För de flesta kunder är det nödvändigt att anta att klienterna uppfyller Internet kraven för leverans optimering. den inbyggda peer-cachelagringen i Windows 10 med leverans optimering bör vara tillräcklig. Om klienterna inte uppfyller dessa Internet krav kan du överväga att använda funktionen Configuration Manager peer-cache. Om du för närvarande använder BranchCache med Configuration Manager och det uppfyller alla dina behov, kan Express-filer med BranchCache vara av rätt alternativ. 

### <a name="peer-cache-comparison-chart"></a>Jämförelse diagram över peer-cache


| Funktioner  | Leveransoptimering  | Peer-cache  | BranchCache  |
|---------|---------|---------|---------|
| Stöds över undernät | Ja | Ja | Nej |
| Bandbredds begränsning | Ja (inbyggt) | Ja (via BITS) | Ja (via BITS) |
| Stöd för delar av innehåll | Ja, för alla innehålls typer som stöds visas i nästa rad i den här kolumnen. | Endast för Office 365 och Express-uppdateringar | Ja, för alla innehålls typer som stöds visas i nästa rad i den här kolumnen. |
| Innehålls typer som stöds | **Via ConfigMgr:** </br> -Express uppdateringar </br> – Alla Windows-uppdateringar (från och med version 1910). Detta omfattar inte Office-uppdateringar.</br> </br> **Via Microsoft Cloud:**</br> – Windows-och säkerhets uppdateringar</br> – Driv rutiner</br> – Windows Store-appar</br> – Windows Store för företag-appar | Alla innehålls typer för ConfigMgr, inklusive bilder som hämtats i [Windows PE](../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) | Alla innehålls typer i ConfigMgr, förutom bilder |
| Cachestorlek på disk kontroll | Ja | Ja | Ja |
| Identifiering av en peer-källa | Automatiskt | Manuell (klient agent inställning) | Automatiskt |
| Peer-identifiering | Via moln tjänsten för leverans optimering (kräver Internet åtkomst) | Via hanterings plats (baserat på klient gränser grupper) | Multicast |
| Rapportering | Ja (med hjälp av Skriv bords analys) | ConfigMgr-klient data källor instrument panel | ConfigMgr-klient data källor instrument panel |
| WAN-användnings kontroll | Ja (ursprunglig, kan styras via grup princip inställningar) | Gränsgrupper | Endast undernät stöder |
| Hantering via ConfigMgr | Delvis (klient agent inställning) | Ja (klient agent inställning) | Ja (klient agent inställning) |



## <a name="conclusion"></a>Slutsats

Microsoft rekommenderar att du optimerar leverans kvaliteten i Windows 10 med hjälp av Configuration Manager med Express installationsfiler och en teknik för peer-cachelagring, efter behov. Den här metoden bör minska de utmaningar som är kopplade till Windows 10-enheter för att ladda ned stora mängder innehåll för att installera kvalitets uppdateringar. Att hålla Windows 10-enheter aktuella genom att distribuera kvalitets uppdateringar varje månad rekommenderas också. Den här metoden minskar den delta i kvalitets uppdaterings innehåll som krävs av enheterna varje månad. Genom att minska den här innehålls förändringen får du mindre storleks nedladdning från distributions platser eller peer-källor. 

På grund av typen av Express installationsfiler är deras innehålls storlek betydligt större än traditionella självständiga filer. Den här storleken resulterar i längre uppdatering av hämtnings tider från tjänsten Windows Update till Configuration Manager plats Server. Mängden disk utrymme som krävs för både plats servern och distributions platserna ökar också. Den totala tiden som krävs för att ladda ned och distribuera kvalitets uppdateringar kan vara längre. Däremot bör fördelarna på enhets sidan märkas under nedladdning och installation av kvalitets uppdateringar av Windows 10-enheter. Mer information finns i [använda snabb installationsfiler](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc708456(v=ws.10)?#using-express-installation-files).

Om Server sidans kompromisser med större storleks uppdateringar är block för att anta Express support, men fördelarna på enhets sidan är avgörande för ditt företag och din miljö, rekommenderar Microsoft att du använder [Windows Update för företag](integrate-windows-update-for-business-windows-10.md) med Configuration Manager. Windows Update för företag ger alla fördelar med Express utan att behöva ladda ned, lagra och distribuera Express installationsfiler i din miljö. Klienter laddar ned innehåll direkt från Windows Updates tjänsten, men kan fortfarande använda leverans optimering.



## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a>Vanliga frågor och svar

#### <a name="how-do-windows-express-downloads-work-with-configuration-manager"></a>Hur fungerar Windows Express-hämtningar med Configuration Manager?

Windows Update Agent (WUA) begär innehåll först. Om det inte går att installera Express uppdateringen kan den återgå till den fullständiga fil uppdateringen.  

1. Den Configuration Manager klienten instruerar WUA att ladda ned uppdaterings innehållet. När WUA initierar en Express nedladdning laddar den först ned en stub (till exempel `Windows10.0-KB1234567-<platform>-express.cab` ), som ingår i Express paketet.  

2. WUA skickar denna stub till installations programmet för Windows Update, Component-Based Servicing (CBS). CBS använder stub-funktionen för att göra en lokal inventering, och jämför de delta i filen på enheten med vad som behövs för att komma till den senaste versionen av filen som erbjuds.  

3. CBS ber sedan WUA att ladda ned de nödvändiga intervallen från en eller flera Express. polyesterstapelfibrer-filer.  

4. Om leverans optimering är aktive rad och peer-datorer identifieras för att ha de intervall som krävs, kommer klienten att ladda ned från peer-datorer oberoende av ConfigMgr-klienten. Om leverans optimeringen är inaktive rad eller om inga peer-datorer har de intervall som behövs laddar ConfigMgr-klienten dessa intervall från en lokal distributions plats (eller en peer-eller Microsoft Update). Intervallen skickas till Windows Update Agent som gör dem tillgängliga för CBS för att tillämpa intervallen.


#### <a name="why-are-the-express-files-psf-so-large-when-stored-on-configuration-manager-peer-sources-in-the-ccmcache-folder"></a>Varför är Express-filerna (. polyesterstapelfibrer) så stora när de lagras på Configuration Manager peer-källor i ccmcache-mappen?

Express-filerna (. polyesterstapelfibrer) är sparse-filer. Om du vill fastställa det faktiska utrymmet som används på disken av filen kontrollerar du **storleken på** filens disk egenskap. Storleken på disk egenskapen bör vara betydligt mindre än värdet för storlek.  


#### <a name="does-configuration-manager-support-express-installation-files-with-windows-10-feature-updates"></a>Stöder Configuration Manager Express-installationsfiler med funktions uppdateringar för Windows 10?

Nej, Configuration Manager för närvarande endast stöder Express-installationsfiler med kvalitets uppdateringar av Windows 10.  


#### <a name="how-much-disk-space-is-needed-per-quality-update-on-the-site-server-and-distribution-points"></a>Hur mycket disk utrymme behövs per kvalitets uppdatering på plats servern och distributions platserna?

Det beror på. För varje kvalitets uppdatering lagras både fullständig fil-och Express versionen av uppdateringen på-servrar. Kvalitets uppdateringar för Windows 10 är kumulativa, så storleken på dessa filer ökar varje månad. Planera minst 5 GB per uppdatering per språk. 


#### <a name="do-configuration-manager-clients-still-benefit-from-express-installation-files-when-falling-back-to-the-windows-update-service"></a>Kommer Configuration Manager-klienter fortfarande att ha nytta av Express installationsfiler när de återgår till tjänsten Windows Update?

Ja. Om du använder följande alternativ för program uppdaterings distribution använder klienterna Express uppdateringar och leverans optimering när de återgår till moln tjänsten:  

**Om program uppdateringar inte är tillgängliga på distributions platsen i aktuella, intilliggande eller plats grupper laddar du ned innehåll från Microsoft Updates**


#### <a name="why-is-express-file-content-not-downloaded-for-existing-updates-after-i-enable-express-file-support"></a>Varför laddas inte Express File-innehåll ned för befintliga uppdateringar när jag har aktiverat stöd för Express-filen? 

Ändringarna börjar gälla för alla nya uppdateringar som synkroniseras och distribueras efter att stödet har Aktiver ATS.


#### <a name="is-there-any-way-to-see-how-much-content-is-downloaded-from-peers-using-delivery-optimization"></a>Finns det något sätt att se hur mycket innehåll som hämtas från peer-datorer med hjälp av leverans optimering?
Windows 10, version 1703 (och senare) innehåller två nya PowerShell-cmdletar, **Get-DeliveryOptimizationPerfSnap** och **Get-DeliveryOptimizationStatus**. Dessa cmdletar ger mer insikter om leverans optimering och cache-användning. Mer information finns i avsnittet [om leverans optimering för Windows 10-uppdateringar](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#the-cloud-service-doesnt-see-other-peers-on-the-network)


#### <a name="how-do-clients-communicate-with-delivery-optimization-over-the-network"></a>Hur kommunicerar klienter med leverans optimering i nätverket?
Mer information om nätverks portar, proxy-krav och värdnamn för brand väggar finns i [vanliga frågor och svar om leverans optimering](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).

## <a name="log-files"></a>Loggfiler

Använd följande loggfiler för att övervaka delta hämtningar:

- WUAHandler.log
- DeltaDownload. log

## <a name="next-steps"></a>Nästa steg

- [Distribuera programuppdateringar](deploy-software-updates.md)
- [Distribuera programuppdateringar automatiskt](automatically-deploy-software-updates.md)
