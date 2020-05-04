---
title: Introduktion till till gångs information
titleSuffix: Configuration Manager
description: Använd till gångs information i Configuration Manager för att inventera och hantera användningen av program varu licenser i hela företaget.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25deb098f6e1f4ce275a0c0a0817249cd36558f7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714187"
---
# <a name="introduction-to-asset-intelligence-in-configuration-manager"></a>Introduktion till till gångs information i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Inventera och hantera användningen av program licenser i hela företaget med hjälp av till gångs informations katalogen. Till gångs information lägger till maskin varu lager klasser för att förbättra den informations bredd som Configuration Manager samlar in. Den här informationen inkluderar maskinvaru-och program varu titlar som används i din miljö. Över 60-rapporter presenterar den här informationen i ett lättanvänt format. Många av de här rapporterna länkar till mer detaljerade rapporter. Fråga efter allmän information och öka detalj nivån till mer detaljerad information. 

Lägg till anpassad information i till gångs informations katalogen. Till exempel anpassade program varu kategorier, program varu familjer, program varu etiketter och maskin varu krav. Om du vill uppdatera till gångs informations katalogen dynamiskt med den senaste tillgängliga informationen ansluter du den till Microsoft Cloud. 

Använd till gångs information för att få hjälp med att stämma av användningen av din företags program vara. Importera information om program varu licenser till Configuration Manager plats databasen för att visa den mot vilken program vara som används.  



## <a name="asset-intelligence-catalog"></a><a name="BKMK_AssetIntelligenceCatalog"></a>Till gångs informations katalog  

Till gångs informations katalogen är en uppsättning databas tabeller som lagras i plats databasen. Tabellerna innehåller kategoriserings-och identifierings information för över 300 000 program varu titlar och versioner. De hjälper också till att hantera maskin varu krav för särskilda program varu titlar.  

Till gångs information innehåller information om program varu licenser för program varu titlar som används, både Microsoft och andra program som inte kommer från Microsoft. En fördefinierad uppsättning maskin varu krav för program varu titlar finns i till gångs informations katalogen och du kan skapa ny användardefinierad information om maskin varu krav för att uppfylla anpassade krav. Du kan också anpassa informationen i till gångs informations katalogen och du kan ladda upp information om program varu titlar till Microsoft-molnet för kategorisering.  

Uppdateringar av till gångs informations katalogen som innehåller nyligen utgiven program vara finns tillgängliga för nedladdning regelbundet för att utföra Mass katalogs uppdateringar. Den kan också uppdateras dynamiskt med hjälp av platsen för synkronisering av till gångs information.  


### <a name="software-categories"></a><a name="BKMK_SoftwareCategories"></a>Program varu kategorier  

Program varu kategorier i till gångs information används för att gruppera inventerade program varu titlar och som övergripande grupperingar av mer detaljerade program varu familjer. En programvarukategori kan till exempel vara elbolag, och en programvarufamilj i den programvarukategorin kan vara olja och gas eller hydroelektrisk. Många program varu kategorier är fördefinierade i till gångs informations katalogen. Du kan skapa användardefinierade kategorier om du vill definiera inventerad program vara. Validerings statusen för alla fördefinierade program varu kategorier är alltid **verifierad**. Anpassad information om program varu kategorier som läggs till i till gångs informations katalogen är **användardefinierad**. 

Mer information om hur du hanterar program varu kategorier finns i [Konfigurera till gångs information](configuring-asset-intelligence.md).  

> [!NOTE]  
> Fördefinierad information om program varu kategorier som lagras i till gångs informations katalogen är skrivskyddad. Du kan inte ändra eller ta bort den. Administratörer kan lägga till, ändra eller ta bort användardefinierade programvarukategorier.  


### <a name="software-families"></a><a name="BKMK_SoftwareFamilies"></a>Program varu familjer  

Program varu familjer för till gångs information används för att definiera inventerade program varu titlar i program varu kategorier. Många program varu familjer är fördefinierade i till gångs informations katalogen. Du kan skapa användardefinierade kategorier om du vill definiera inventerad program vara. Validerings statusen för alla fördefinierade program varu familjer är alltid **verifierad**. Anpassad information om program varu familjer som läggs till i till gångs informations katalogen är **användardefinierad**. 

Mer information om hur du hanterar program varu familjer finns i [Konfigurera till gångs information](configuring-asset-intelligence.md).  

> [!NOTE]  
> Fördefinierad information om program varu familjer är skrivskyddad och kan inte ändras. Administratörer kan lägga till, ändra eller ta bort användardefinierade programvarufamiljer.  


### <a name="software-labels"></a><a name="BKMK_CustomLabels"></a>Program varu etiketter  

Med anpassade program varu etiketter i till gångs information kan du skapa filter för att gruppera program varu titlar och visa dem i till gångs informations rapporter. Använd program varu etiketter för att skapa användardefinierade grupper av program varu titlar som delar ett gemensamt attribut. Du kan till exempel skapa en program varu etikett som heter shareware, associera den med inventerade shareware-titlar och köra en rapport för att visa alla program titlar med den etiketten. Det finns inga fördefinierade etiketter. Valideringstillståndet för programvaruetiketter är alltid **användardefinierat**. 

Mer information om hur du hanterar program varu etiketter finns i [Konfigurera till gångs information](configuring-asset-intelligence.md).  


### <a name="hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a>Maskin varu krav  

Använd informationen om maskin varu krav för att kontrol lera att datorerna uppfyller maskin varu kraven för program varu titlar innan de är avsedda för program distributioner. Hantera maskin varu krav för program varu titlar i arbets ytan **till gångar och efterlevnad** på noden **maskin varu krav** under noden **tillgångsinformation** . 

Många maskin varu krav är fördefinierade i till gångs informations katalogen. Skapa ny användardefinierad information om maskin varu krav för att uppfylla anpassade krav. Validerings statusen för alla fördefinierade maskin varu krav är alltid **verifierad**. Användardefinierad information om maskin varu krav som läggs till i till gångs informations katalogen är **användardefinierad**. 

Mer information om hur du hanterar maskin varu krav finns i [Konfigurera till gångs information](configuring-asset-intelligence.md).  

> [!NOTE]  
> Maskin varu kraven som visas i Configuration Manager-konsolen hämtas från till gångs informations katalogen. De baseras inte på information om inventerade program varu titlar från klienter. 
> 
> Information om maskin varu krav uppdateras inte som en del av synkroniseringsprocessen med Microsoft. 
> 
> Du kan skapa användardefinierade maskin varu krav för Inventerad program vara som inte har några associerade maskin varu krav.  

Som standard visas följande information för varje maskinvarukrav som visas:  

- **Program varu titel**: program varu titeln som är associerad med maskin varu kravet  

- **Lägsta CPU (megahertz)**: den lägsta processor hastigheten i megahertz (MHz) som krävs av program varu titeln  

- **Minsta RAM (KB)**: minsta ram i KILOBYTE (KB) som krävs av program varu titeln  

- **Minsta disk utrymme (KB)**: minsta lediga hårddisk utrymme i KB som program varu titeln kräver  

- **Minsta disk storlek (KB)**: minsta hård disk storlek i KB som program varu titeln kräver  

- **Validerings tillstånd**: validerings tillstånd för maskin varu krav  

Fördefinierade maskin varu krav som lagras i till gångs informations katalogen är skrivskyddade och kan inte tas bort. Administrativa användare kan lägga till, ändra eller ta bort användardefinierade maskin varu krav för program varu titlar som inte lagras i till gångs informations katalogen.  



## <a name="inventoried-software-titles"></a><a name="BKMK_InventoriedSoftwareTitles"></a>Inventerade program varu titlar  

Om du vill visa information om inventerade program varu titlar i Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** , expanderar noden **tillgångsinformation** och väljer noden **Inventerad program vara** . Maskin varu inventerings agenten samlar in Inventerad program varu information från Configuration Manager-klienter baserat på program varu titlar som lagras i till gångs informations katalogen.  

> [!Note]  
> Maskin varu inventerings agenten samlar in inventering baserat på de rapport klasser för maskin varu inventering för till gångs information som du aktiverar. Mer information om hur du aktiverar rapporterings klasser finns i [Konfigurera till gångs information](configuring-asset-intelligence.md).  

Som standard visas följande information för varje inventerad programvarutitel:  

- **Namn**: namnet på den inventerade program varu titeln  

- **Leverantör**: namnet på leverantören som utvecklade den inventerade program varu titeln  

- **Version**: produkt versionen av den inventerade program varu titeln  

- **Kategori**: den program varu kategori som för närvarande är kopplad till den inventerade program varu titeln  

- **Familj**: den program varu familj som för närvarande är kopplad till den inventerade program varu titeln  

- **Etikett** [**1**, **2**och **3**]: de anpassade etiketter som är associerade med program varu titeln. Inventerade programvarutitlar kan ha upp till tre anpassade etiketter.  

- **Antal**: antalet Configuration Manager-klienter som har inventerat program varu titeln  

- **Tillstånd**: validerings tillstånd för den inventerade program varu titeln  

> [!NOTE]  
> Du kan bara ändra kategoriserings informationen för Inventerad program vara på platsen på den översta nivån i hierarkin. Den här informationen omfattar produkt namn, leverantör, program varu kategori och program varu familj. När du har ändrat kategoriseringsinformationen för fördefinierad programvara ändras valideringstillståndet för programvaran från **Verifierad** till **Användardefinierad**.  



## <a name="asset-intelligence-synchronization-point"></a><a name="AssetIntelligenceSycnronizationPoint"></a>Plats för synkronisering av till gångs information  

Platsen för synkronisering av till gångs information är en Configuration Manager plats system roll. Den används för att ansluta till Microsoft-molnet på TCP-port 443 för att hantera uppdateringar av dynamisk katalog information. Installera endast den här plats rollen på den översta nivån i hierarkin. Konfigurera all anpassning av till gångs informations katalogen med hjälp av en Configuration Manager-konsol som är ansluten till platsen på den översta nivån. 

När du konfigurerar alla uppdateringar på platsen på den översta nivån replikeras katalog information till andra platser i hierarkin. Med plats rollen kan du begära katalog synkronisering på begäran med Microsoft eller schemalägga automatisk katalog synkronisering. Förutom att hämta ny katalog information kan platsen för synkronisering av till gångs information överföra anpassad information om program varu titlar till Microsoft för kategorisering. Microsoft behandlar alla överförda program varu titlar som offentlig information. Se till att dina anpassade program varu titlar inte innehåller konfidentiell eller patentskyddad information.  

När du har skickat in en Okategoriserade program varu titel, granskar inte Microsoft den förrän det finns minst fyra kategoriserings förfrågningar från kunder för samma program varu titel. Sedan kan Microsoft-forskare identifiera, kategorisera och göra kategoriserings informationen för program varu titeln tillgänglig för alla kunder som använder online tjänsten. Programvarutitlar med flest kategoriseringsförfrågningar prioriteras högst. Anpassade program-och branschspecifika program är osannolika för att få en kategori. Skicka inte dessa program titlar till Microsoft för kategorisering.  

En plats för synkronisering av till gångs information krävs för att ansluta till Microsoft-molnet. Information om hur du installerar rollen finns i [Konfigurera till gångs information](configuring-asset-intelligence.md).  



## <a name="asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a>Start sida för till gångs information  

Noden **tillgångsinformation** på arbets ytan **till gångar och efterlevnad** är start sidan för till gångs information i Configuration Manager. Den här start sidan visar en översikt över en instrument panel för till gångs informations katalogen.  

> [!NOTE]  
> Start sidan för **tillgångsinformation** uppdateras inte automatiskt när du visar den.  

På Start sidan för **tillgångsinformation** ingår följande avsnitt:  

- **Katalog-synkronisering**: information om huruvida till gångs information är aktive rad och aktuell status för platsen för synkronisering av till gångs information.  

    > [!NOTE]  
    > Start sidan visar bara det här avsnittet när du installerar en plats för synkronisering av till gångs information.  

    Avsnittet innehåller också följande information:  

    - Synkroniseringsschema  

    - Om du har importerat en kund licens översikt   

    - Senaste status uppdatering  

    - Tiden för nästa schemalagda uppdatering  

    - Antalet ändringar efter att du har installerat platsen för synkronisering av till gångs information   

- **Inventerad program varu status**: antal och procent av Inventerad program vara, program varu kategorier och program varu familjer som identifieras av Microsoft, som identifieras av en administratör, väntar på online-identifiering eller oidentifierade och inte väntande. Informationen som visas i tabellformat anger antalet för var och en, och informationen i diagrammet visar procentandelen.  



## <a name="asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a>Till gångs informations rapporter  

Till gångs informations rapporterna finns i Configuration Manager-konsolen i arbets ytan **övervakning** i mappen **till gångs information** under noden **rapportering** . Rapporterna innehåller information om maskinvara, licenshantering och programvara. Mer information om rapporter i Configuration Manager finns i [Introduktion till rapportering](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
> Antalet installerade program varu titlar och licens information som visas i till gångs informations rapporterna kan skilja sig från det faktiska antalet program varu titlar som är installerade eller licenser som används i miljön. Detta beror på komplexa beroenden och begränsningar i inventeringen av programvarulicenser för program som är installerade i företagsmiljöer. Använd inte till gångs informations rapporter som den enda källan för att fastställa kompatibilitet för köpt program varu licenser.  


### <a name="hardware-reports"></a><a name="BKMK_HardwareReports"></a>Maskin varu rapporter  

Maskin varu rapporter för till gångs information innehåller information om maskin varu till gångar i organisationen. Genom att använda maskin varu inventerings information som hastighet, minne och kring utrustning kan maskin varu rapporter i till gångs information visa information om USB-enheter, om maskin vara som måste uppgraderas och även om datorer som inte är redo för en speciell program uppgradering.  

> [!NOTE]  
> Vissa användar data i maskin varu rapporterna i till gångs information samlas in från säkerhets händelse loggen i Windows. För bättre rapport noggrannhet rensar du den här loggen när du omtilldelar en dator till en ny användare.  


### <a name="license-management-reports"></a><a name="BKMK_LicenseManagementReports"></a>Licens hanterings rapporter  

Licens hanterings rapporter i till gångs information innehåller information om licenser som används. I rapporten **licens** rapport listas installerade Microsoft-program i ett format som är kompatibelt med Microsoft License statement (MLS). Det här formatet är en praktisk metod för att matcha hämtade licenser med använda licenser. Andra licens hanterings rapporter innehåller information om datorer som fungerar som servrar som kör nyckel hanterings tjänsten (KMS) för Windows aktiverings statistik.  

> [!IMPORTANT]  
> Flera av licens hanterings rapporterna för till gångs information visar information om KMS-funktionen, en metod för att administrera volym licensiering. Om du inte har implementerat en KMS-server kanske vissa rapporter inte returnerar några data.  


### <a name="software-reports"></a><a name="BKMK_SoftwareReports"></a>Program varu rapporter  

Program varu rapporter till till gångs information innehåller information om program varu familjer, kategorier och vissa program varu titlar som är installerade på datorerna i organisationen. Program varu rapporterna visar information som webb läsar hjälp objekt och program vara som startar automatiskt. Dessa rapporter kan användas för att identifiera annons program, spionprogram och annan skadlig kod. Du kan också använda dem för att identifiera programredundans för att effektivisera program varu förvärv och-support.  


### <a name="software-identification-tag-reports"></a><a name="BKMK_SoftwareIdTagReports"></a>Tagga rapporter för program varu identifiering  

Taggar för till gångs informationens program varu identifiering innehåller information om program vara som innehåller en tagg för program varu identifiering som är kompatibel med ISO/IEC 19770-2. Taggar för program varu identifiering tillhandahåller auktoritativ information som används för att identifiera installerad program vara. När du aktiverar rapport klassen **SMS_SoftwareTag** maskin varu inventering samlar Configuration Manager in information om program vara med taggar för program varu identifiering. 

Följande rapporter innehåller information om programvaran:  

- **Program vara 14a-sökning efter program med aktiverade taggar för program varu identifiering**: antalet installerade program med en tagg för program varu identifiering aktive rad  

- **Program vara 14b – datorer med ett visst program med aktiverade taggar för program varu identifiering installerade**: alla datorer som har installerat program vara med en angiven tagg för program varu identifiering aktive rad  

- **Program vara 14c-installerad program vara med aktiverade taggar för program varu identifiering på en angiven dator**: all installerad program vara med en angiven tagg för program varu identifiering aktive rad på en angiven dator  


### <a name="reporting-limitations"></a><a name="BKMK_ReportingLImitations"></a>Rapporterings begränsningar  

Till gångs informations rapporter kan ge stora mängder information om installerade program varu titlar och köpta program varu licenser som används. Använd inte den här informationen som den enda källan för att fastställa kompatibilitet för program varu licenser.  

#### <a name="example-dependencies"></a><a name="BKMK_ExampleDependencies"></a> Exempelberoenden  
Precisionen för den kvantitet som visas i till gångs informations rapporterna för installerade program varu titlar och licens information kan skilja sig från de faktiska mängder som för närvarande används. Detta beror på komplexa beroenden i inventeringen av programvarulicenser för program som används i företagsmiljöer. Följande exempel visar de beroenden som ingår i inventeringen av installerad program vara i företaget med hjälp av till gångs information som kan påverka noggrannheten i till gångs informations rapporter:  

- **Klient maskin varu inventerings beroenden**: till gångs information installerade program varu rapporter baseras på data som samlas in från Configuration Manager-klienter genom att utöka maskin varu inventeringen för att aktivera till gång På grund av det här beroendet av maskin varu inventerings rapporter återspeglar till gångs informations rapporterna endast data från klienter som har slutfört maskin varu inventerings processer med nödvändiga WMI-rapporterings klasser för till gångs information. Eftersom Configuration Manager klienter utför maskin varu inventerings processer enligt ett schema som definierats av den administrativa användaren kan en fördröjning uppstå i data rapportering som påverkar noggrannheten hos till gångs informations rapporter. 

    Till exempel kan en inventerad licensierad programvarutitel avinstalleras när klienten har slutfört en lyckad maskinvaruinventeringscykel. I till gångs informations rapporter visas program varu titeln som installerad tills klientens nästa schemalagda maskin varu inventerings cykel.  

- **Program varu paket beroenden**: till gångs informations rapporter baseras på installerade program varu titlar som samlas in med standard Configuration Manager klient maskin varu inventerings processer. Vissa program titlars data kanske inte samlas in korrekt. Exempel som kan orsaka felaktig rapportering av till gångs information:  

    - Program varu installationer som inte är kompatibla med standard installations processer  

    - Program varu installationer som har ändrats före installationen   

#### <a name="legal-limitations"></a><a name="BKMK_LegalLimitations"></a> Juridiska begränsningar  
Informationen som visas i till gångs informations rapporter är beroende av många begränsningar. Den information som visas i dem representerar inte juridisk, redovisning eller annan professionell rådgivning. Informationen som tillhandahålls av till gångs informations rapporter är endast avsedd för information. Använd inte den som den enda informations källan för att fastställa kompatibilitet för program varu licenser.  

Följande begränsningar är exempel på hur du använder till gångs information som kan påverka noggrannheten i rapporterna:  

- **Begränsningar för antalet Microsoft-licens användning**:  

    - Antalet köpta program licenser från Microsoft baseras på den information som administratörerna tillhandahåller. Se noga till att du har rätt antal program varu licenser.  

    - Det rapporterade antalet licenser för program vara från Microsoft innehåller endast information om licenser för Microsoft-programvara som köpts via volym licensierings program. Det visar inte information om program varu licenser som har köpts via återförsäljar-, OEM-eller annan program varu licens försäljnings kanaler.  

    - Programvarulicenser köpta under de senaste 45 dagarna kan inte tas med i antalet rapporterade Microsoft-programvarulicenser på grund av programvaruåterförsäljarnas rapporteringskrav och scheman.  

    - Överföringar av programvarulicenser genom företagssammanslagningar eller företagsförvärv kanske inte återspeglas i antalet Microsoft-programvarulicenser.  

    - Avvikande villkor i ett MVLS-avtal (Microsoft Volume Licensing) kan påverka antalet rapporterade program varu licenser. De kan kräva ytterligare granskning av en Microsoft-representant.  

- **Begränsningar för installerad program varu titel**: Configuration Manager klienter måste ha slutfört rapporterings cykler för maskin varu inventering för till gångs informations rapporterna för att korrekt rapportera antalet installerade program varu titlar. Det kan uppstå en fördröjning mellan installationen eller avinstallationen av en licensierad program varu titel efter en lyckad rapporterings cykel för maskin varu inventering. Den här åtgärden kanske inte återspeglas i till gångs informations rapporter innan klienten rapporterar nästa schemalagda maskin varu inventering.  

- **Begränsningar i licens avstämningen**: avstämningen av antalet installerade program varu titlar till mängden köpta program varu licenser beräknas med hjälp av en jämförelse av den licens mängd som anges av administratören och mängden installerade program som samlas in från Configuration Manager klient maskin varu inventering baserat på det schema som angetts av administratören. Den här jämförelsen representerar inte en slutgiltig Microsoft-slutsats om licens befattningarna. Den faktiska licenssituationen beror på den specifika programvarulicensen och användarrättigheterna som beviljas i licensvillkoren.  



## <a name="asset-intelligence-validation-states"></a><a name="BKMK_ValidationStates"></a>Validerings tillstånd för till gångs information  

Validerings tillstånd för till gångs information representerar källan och den aktuella validerings statusen för information om till gångs informations katalogen. I följande tabell visas möjliga validerings tillstånd för till gångs information och administratörs åtgärder som kan orsaka dem.  

| Status | Definition | Åtgärd av administratören | Kommentar |  
|---------------|--------------------|------------------------------|-----------------|  
|**Verifierad**|Microsoft-forskare definierade katalog objekt|Inga|Bästa tillstånd|  
|**Användardefinierad**|Microsoft-forskare har inte definierat katalog posten|Anpassa den lokala katalog informationen|Det här läget visas i till gångs informations rapporter|  
|**Väntar**|Microsoft-forskare har inte definierat katalog posten, men du skickade objektet till Microsoft för kategorisering|Ingen ytterligare åtgärd efter förfrågan om kategorisering|Katalogobjekten förblir i det här läget tills Microsoft-forskare kategoriserar objektet och du synkroniserar till gångs informations katalogen|  
|**Uppdaterbar**|Ett användardefinierat katalog objekt har kategoriserats annorlunda av Microsoft under katalog synkroniseringen.|Använd åtgärden **Lös konflikt** för att bestämma om den nya kategoriserings informationen eller det tidigare användardefinierade värdet ska användas. Mer information om hur du löser konflikter finns i [åtgärder för till gångs information](operations-for-asset-intelligence.md).|När du har löst en kategoriserings konflikt verifieras inte objektet som ett objekt i konflikt igen om inte senare kategoriserings uppdateringar tillför ny information om objektet.|  
|**Ej kategoriserade**|Katalogobjektet har inte definierats av Microsoft-forskare, objektet har inte skickats till Microsoft för kategorisering och administratören har inte tilldelat ett användardefinierat kategoriserings värde.|Begär kategorisering eller anpassa den lokala katalog informationen. Mer information finns i [åtgärder för till gångs information](operations-for-asset-intelligence.md).|Inga|  

> [!NOTE]  
> Katalog objekt som du skickar till Microsoft för kategorisering har validerings statusen **väntar** på en central administrations plats, men fortsätter att visas med validerings tillstånd för **Okategoriserade** på underordnade primära platser.  

Exempel på när ett validerings tillstånd kan övergå från ett tillstånd till ett annat finns i [exempel på validerings tillstånds över gångar för till gångs information](example-validation-state-transitions-for-asset-intelligence.md).  
