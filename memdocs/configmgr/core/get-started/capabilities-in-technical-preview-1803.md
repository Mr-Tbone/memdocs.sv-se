---
title: Teknisk för hands version 1803
titleSuffix: Configuration Manager
description: Lär dig mer om nya funktioner som är tillgängliga i Configuration Manager Technical Preview version 1803.
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 56dc4b07-5aa4-43e2-9be8-d26ae5ff5613
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: bb8224df3ccbb086ca0c83d08f29522cf3289c32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719045"
---
# <a name="capabilities-in-technical-preview-1803-for-configuration-manager"></a>Funktioner i Technical Preview 1803 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1803. Du kan installera den här versionen om du vill uppdatera och lägga till nya funktioner på din tekniska för hands versions webbplats. 

Läs artikeln om [teknisk för hands version](technical-preview.md) innan du installerar den här uppdateringen. Den artikeln är bekant med de allmänna kraven och begränsningarna för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**Följande är nya funktioner som du kan prova med den här versionen.**  



 
## <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Mottagar distributions platser har stöd för moln distributions platser som källa  
<!--1321554-->
Många kunder använder [mottagar distributions platser](../plan-design/hierarchy/use-a-pull-distribution-point.md) på fjärr-eller avdelnings kontor som laddar ned innehåll från en käll distributions plats via WAN. Om dina fjärranslutna kontor har en bättre anslutning till Internet, eller om du vill minska belastningen på dina WAN-länkar, kan du nu använda en [moln distributions plats](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) i Microsoft Azure som källa. När du lägger till en källa på fliken **mottagar distributions plats** i egenskaperna för distributions platsen, visas nu alla moln distributions platser på platsen som en tillgänglig distributions plats. Beteendet för båda plats system rollerna förblir i övrigt. 

### <a name="prerequisites"></a>Krav
- Mottagar distributions platsen måste ha Internet åtkomst för att kunna kommunicera med Microsoft Azure.
- Innehållet måste distribueras till käll moln distributions platsen.

> [!Note]  
> Den här funktionen debiterar din Azure-prenumeration för data lagring och utgående nätverk. Mer information finns i [kostnaden för att använda molnbaserad distribution](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost).



## <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Stöd för delvis hämtning i klient-peer-cache för att minska WAN-användningen
<!--1357346-->
Klientens peer-cache-källor kan nu dela upp innehåll i delar. Dessa delar minimerar nätverks överföringen för att minska WAN-användningen. Hanterings platsen ger en mer detaljerad spårning av innehålls delarna. Det försöker eliminera mer än en hämtning av samma innehåll per gränser grupp. 

### <a name="example-scenario"></a>Exempelscenario
Contoso har en enda primär plats med två gränser grupper: huvud kontor (HQ) och avdelnings kontor. Det finns en 30-minuters återställnings relation mellan gränser grupperna. Hanterings platsen och distributions platsen för platsen finns bara i HQ-gränser. Avdelnings kontorets plats har ingen lokal distributions plats. Två av de fyra klienterna på avdelnings kontoret är konfigurerade som peer-cache-källor. 

![Diagram över nätverks konfiguration enligt beskrivningen i exempel scenariot](media/1357346-peer-cache-source-parts.png)

1. Du riktar en distribution till innehåll till alla fyra klienter på avdelnings kontoret. Du distribuerar bara innehållet till distributions platsen.
2. Client3 och Client4 har ingen lokal källa för distributionen. Hanterings platsen instruerar klienterna att vänta 30 minuter innan de återgår till den fjärranslutna avgränsnings gruppen.
3. KLIENT1 (PCS1) är den första peer-cache-källan för att uppdatera principen med hanterings platsen. Eftersom den här klienten är aktive rad som en peer cache-källa instruerar hanterings platsen att den omedelbart börjar hämta del A från distributions platsen.  
4. När KLIENT2 (PCS2) kontaktar hanterings platsen, som del A redan pågår men inte har slutförts, instruerar hanterings platsen att den omedelbart börjar ladda ned del B från distributions platsen.
5. PCS1 har slutfört hämtningen av del A, och meddelar genast hanterings platsen. Eftersom del B redan pågår men inte har slutförts instruerar hanterings platsen att den börjar ladda ned del C från distributions platsen.
6. PCS2 har slutfört nedladdning av del B och meddelar genast hanterings platsen. Hanterings platsen instruerar den att börja ladda ned del D från distributions platsen. 
7. PCS1 har slutfört nedladdning av del C och meddelar genast hanterings platsen. Hanterings platsen informerar om att det inte finns några fler tillgängliga delar från den fjärranslutna distributions platsen. Hanterings platsen instruerar den att ladda ned del B från dess lokala peer, PCS2.
8. Den här processen fortsätter tills både klientens peer-cache-källor har alla delar från varandra. Hanterings platsen prioriterar delar från den fjärranslutna distributions platsen innan de instruerar peer-cachens källor för att ladda ned delar från lokala peer-datorer. 
9. Client3 är den första att uppdatera principen när återställnings perioden på 30 minuter upphör att gälla. Nu kontrol leras den igen med hanterings platsen, vilket informerar klienten om nya lokala källor. I stället för att ladda ned innehållet fullständigt från distributions platsen i WAN-nätverket laddar den ned innehållet från en av klientens peer-cache-källor. Klienter prioriterar lokala peer-källor. 

> [!Note]  
> Om antalet klient-peer cache-källor är större än antalet innehålls delar, instruerar hanterings platsen ytterligare peer cache-källor för att vänta på återställning som en normal klient. 


### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Sedan skickar du **feedback** från fliken **Start** i menyfliksområdet och låter oss se hur det fungerade.

1. Konfigurera [gränser grupper](../servers/deploy/configure/boundary-groups.md) och peer- [cache-källor](../plan-design/hierarchy/client-peer-cache.md) per normal.
2. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj **platser**. Klicka på **Inställningar för hierarki** i menyfliksområdet. 
3. På fliken **Allmänt** aktiverar du alternativet för att **Konfigurera klientens peer-cache-källor för att dela upp innehåll i delar**. 
4. Skapa en nödvändig distribution med innehåll.  

   > [!Note]  
   > Den här funktionen fungerar bara när klienten laddar ned innehåll i bakgrunden, till exempel med en nödvändig distribution. Hämtningar på begäran, till exempel när användaren installerar en tillgänglig distribution i Software Center, fungerar som vanligt.  

1. Om du vill se vilka som hanterar nedladdningen av innehåll i delar, granskar du **ContentTransferManager. log** på klientens peer-cache-källa och **MP_Location. log** på hanterings platsen.  
 



## <a name="maintenance-windows-in-software-center"></a>Underhålls fönster i Software Center
<!--1358131-->
I Software Center visas nu nästa schemalagda underhålls period. På fliken installations status växlar du vyn från alla till kommande. Det visar tidsintervallet och listan över distributioner som är schemalagda. Listan är tom om det inte finns några framtida underhålls fönster. 

![Software Center som visar listan över kommande distributioner på fliken installations status](media/1358131-software-center-maintenance-windows.png)


## <a name="custom-tab-for-webpage-in-software-center"></a>Anpassad flik för webb sida i Software Center
<!--1358132-->
Nu kan du skapa en anpassad flik för att öppna en webb sida i Software Center. Med den här funktionen kan du Visa innehåll till dina slutanvändare på ett konsekvent och tillförlitligt sätt. Följande lista innehåller några exempel:
- Kontakta IT-avdelningen: information om hur du kontaktar din organisations IT-avdelning
- Support Center: IT-självbetjänings åtgärder som att söka i en kunskaps bas eller öppna ett support ärende.
- Dokumentation om slutanvändare: artiklar om användare i din organisation på olika IT-ämnen, till exempel att använda program eller uppgradera till Windows 10.


### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Sedan skickar du **feedback** från fliken **Start** i menyfliksområdet och låter oss se hur det fungerade.

1. I noden Configuration Manager konsol, **Administration** , **klient inställningar** , öppnar du principen **standard klient inställningar** .
2. Välj **Software Center** -gruppen.
3. Klicka på **Anpassa**för **Software Center-inställningar**.
4. Växla till fliken **flikar** .
5. Aktivera alternativet för att **Ange en anpassad flik för Software Center**.
    1. Ange ett namn i text fältet **fliknamn** . Det här namnet är det som visas för användaren i Software Center.
    2. Ange en giltig URL i text fältet **innehålls-URL** . Den här URL: en är det innehåll som Software Center visar när användarna klickar på den här fliken.

> [!Tip]  
> Software Center använder Internet Explorer-komponenter för att återge webb sidan.

## <a name="enable-third-party-software-update-support-on-clients"></a>Aktivera stöd för program uppdateringar från tredje part på klienter

Nu kan du aktivera konfiguration av Configuration Manager-klienter för program uppdateringar från tredje part. När du **aktiverar program uppdateringar från tredje part** för komponent egenskaperna för SUP hämtar SUP det signerings certifikat som används av WSUS för uppdateringar från tredje part. <!--1357605-->

Om du väljer **Aktivera program uppdateringar från tredje part** i klient inställningar sker följande: 
- På klienten anger den principen för "Tillåt signerade uppdateringar för en Microsoft-uppdateringstjänst på intranätet" 
- Installerar signerings certifikatet i arkivet för betrodda utgivare på klienten. 

### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Sedan skickar du **feedback** från fliken **Start** i menyfliksområdet och låter oss se hur det fungerade.

1. På den översta platsen i Configuration Manager hierarkin går du till noden **Administration** , expanderar **plats konfiguration**och sedan **platser**.
2. Högerklicka på den översta plats servern och välj **Konfigurera plats komponenter** sedan **program uppdaterings plats**.
3. Klicka på fliken **uppdateringar från tredje part** och markera **Aktivera program uppdateringar från tredje part**.
4. Öppna **klient inställningar** och gå till inställningarna för **program uppdateringar**.
5. Se till att **Aktivera program uppdateringar från tredje part** är inställt på **Ja**.

## <a name="enable-copypaste-of-asset-details-from-monitoring-views"></a>Aktivera kopiera/klistra in till gångs information från övervaknings vyer
Som ett resultat av din [röst feedback för användare](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20234866-allow-us-to-copy-information-out-of-the-asset-det) kan du nu aktivera funktionen för att kopiera och klistra in i fönstret till gångs information i vyerna för att övervaka distribution och distributions status.  <!--1357552-->

## <a name="scap-extensions"></a>SCAP-tillägg
För hands versionen av SCAP-tillägg är tillgängligt i CD. senaste-mappen under SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi. Den här för hands versionen av SCAP-tilläggen kan installeras på alla versioner som stöds för närvarande Configuration Manager aktuella grenen och LTSB 1606.



## <a name="next-steps"></a>Nästa steg
Information om hur du installerar eller uppdaterar den tekniska för hands versionen finns i [teknisk för hands version för Configuration Manager](technical-preview.md).    
