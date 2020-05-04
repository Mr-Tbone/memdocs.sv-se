---
title: Diagnostikdata för 1610
titleSuffix: Configuration Manager
description: Lär dig mer om de nivåer av diagnostik-och användnings data som Configuration Manager version 1610 samlar in.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: eb20eb90-bcc0-41de-bfea-638ea470c0dd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 87049bb9799ba5764a3cdd5a14fbf622e7056f3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81716322"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1610-of-configuration-manager"></a>Nivåer av diagnostik användnings data insamling för version 1610 av Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager version 1610 samlar in tre nivåer av diagnostik-och användnings data: **Basic**, **Enhanced**och **full**. Standardnivån för den här funktionen är Utökad. Följande avsnitt innehåller ytterligare information om data som samlas in på varje nivå.

Ändringar från tidigare versioner anges med ***[ny]***, ***[uppdaterat]***, ***[borttaget]*** eller ***[flyttat]***.


> [!IMPORTANT]
>  Configuration Manager samlar inte in plats koder, plats namn, IP-adresser, användar namn, dator namn, fysiska adresser eller e-postadresser på nivåerna Basic eller Enhanced. En samling av den här informationen på nivån fullständig är inte ändamålsenlig, det vill säga eventuellt inkluderad i avancerad diagnostikinformation, t. ex. loggfiler eller minnes ögonblicks bilder. Microsoft kommer inte att använda den här informationen för att identifiera dig, kontakta dig eller utveckla annonser.

##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Ändra nivån
 Administratörer som har en rollbaserad administrativ omfattning som inkluderar **ändrings** behörigheter för objekt klassen **plats** kan ändra nivån på data som samlas in i inställningarna för diagnostik-och användnings data i Configuration Manager-konsolen.

Från och med version 1610 kan du ändra data insamlings nivå i-konsolen genom att gå till **Administration** > **Översikt** > **plats konfiguration** > **platser**. Öppna **Inställningar för hierarki**och välj sedan den data nivå som du vill använda.  

##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Nivå 1 – Grundläggande
 Nivån Basic innehåller data om hierarkin, data som krävs för att förbättra installations-eller uppgraderings upplevelsen och data som hjälper dig att fastställa de Configuration Manager uppdateringar som är tillämpliga för hierarkin.

 för Configuration Manager version 1610 omfattar den här nivån följande:


- Installations information:
  - Build, Installations typ, språk paket, funktioner som du har aktiverat  

  - Distributions status och fel för uppdaterings paket, hämtnings förlopp och nödvändiga fel    

  - Version av skript efter uppgradering

  - Användning av snabb ring för uppdatering

  - ***[Ny]*** För hands versions användning, installations medie typ, förgrenings typ

  - ***[Ny]*** Utgångs datum för Software Assurance

- Prestandamått för databas (information om replikeringsbearbetning, de viktigaste SQL-lagrade procedurer efter processor- och diskanvändning)

- Grundläggande databas konfiguration (processorer, kluster konfiguration och konfiguration av distribuerade vyer)

- Configuration Manager-databasschemat (hash för alla objekt definitioner)

- Antal Configuration Manager-klient versioner och operativ system versioner

- Antal operativ system för hanterade enheter och principer som angetts av Exchange Connector

- Antal klient språk och nationella inställningar

- Antal Windows 10-enheter per gren och version

- Grundläggande Configuration Manager platshierarki (plats lista, typ, version, status, antal klienter och tidszon)

- Grundläggande Server information för plats system (plats system roller som används, status för Internet och SSL, operativ system, processorer och fysisk eller virtuell dator)

- Grundläggande identifierings statistik för användare (antal användar identifieringar och minsta/högsta/genomsnittlig grupp storlek)

- Grundläggande Endpoint Protection information (klient versioner av program mot skadlig kod)

- Grundläggande program-och distributions typer (totalt antal appar, totalt antal appar med flera distributions typer, totalt antal appar med beroenden, totalt ersatta appar och antal distributions tekniker som används)

- OSD-antal (Basic Opera ting System Deployment) (bilder)

- Distributions plats-och hanterings plats typer och grundläggande konfigurations information (skyddad, förinstallerad, PXE, multicast, SSL-tillstånd, pull-/peer-distributions platser, MDM-aktiverad, SSL-aktiverad osv.)

- Telemetristatistik (när de körs, runtime, fel)

- Konfigurerat telemetri-nivå, läge (online eller offline) och snabb uppdaterings konfiguration

- Användning av nätverks identifiering (aktive rad eller inaktive rad)
- Administratörs konsol:

  - Statistik om konsol anslutningar (operativ system version, språk, SKU och arkitektur, system minne, antal logiska processorer, Anslut plats-ID, installerade .NET-versioner och konsol språk paket)    

- SQL-version, service pack nivå, utgåva, sorterings-ID och teckenuppsättning


##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Nivå 2 – Utökad
Den förbättrade nivån är standard när installationen är klar. Den här nivån omfattar data som samlas in på Basic-nivå och funktions specifika data (frekvens och användnings tid), Configuration Manager klient inställningar (komponent namn, tillstånd och vissa inställningar som avsöknings intervall) och grundläggande information om program uppdateringar.

Den här nivån rekommenderas eftersom den förser Microsoft med den minsta mängd data som krävs för att göra användbara förbättringar i framtida versioner av produkter och tjänster. Den här nivån samlar inte in objekt namn (platser, användare, dator eller objekt), information om säkerhetsrelaterade objekt eller säkerhets risker som antalet system som kräver program uppdateringar.

För Configuration Manager version 1610 omfattar den här nivån följande:

-   **Program hantering:**  

    -    Grundläggande användning/mål information för distributions typer som används inom organisationen (användare jämfört med enhetens mål, krävs respektive är tillgänglig och Universal Apps)  

    -   Information om program distribution (installera/avinstallera, kräver godkännande, användar interaktion aktiverat/inaktiverat, beroende och ersättande)  

    -   Statistik över förfrågningar om programtillgänglighet  

    -   Antal paket efter typ  

    -   Antal tillämpliga program efter operativsystem  

    -   Antal paket-/programdistributioner  

    -   Antal App-V-miljöer och distributionsegenskaper  

    -   Antal Windows 10-licensierade programlicenser  

    -   Minsta/högsta/Genomsnittligt antal program distributioner per användare/enhet per tids period

    -   Underhållsperiodstyp och varaktighet  

    -  Storlek och komplexitets statistik för program princip

    - ***[Uppdaterat]*** Antal Windows Store för företag-appar och synkronisering av statistik (inklusive sammanfattande typer av appar, status för licensierad app och antal online-och offline-licensierade appar)  

    - Statistik över gränserna (hur många snabba, hur många långsamma och antalet per grupp)

    - Konfigurations alternativ och antal för MSI

    - Krav för appar (antal inbyggda villkor refereras till av distributions teknik)

    - App-ersättning, maximalt kedje djup

    - UDA-användning (Universal Data Access), hur skapas

    - ***[Ny]*** Statistik för program godkännande och användnings frekvens



-   **Klientsession**  

    -   Lista/antal aktiverade klientagenter  

    -   Antal klientinstallationer från varje typ av källplats  

    -   Antal klientinstallationsfel  

    -  ***[Uppdaterat]*** Automatisk klient uppgradering: distributions konfiguration, inklusive klient pilotering och undantags användning (utökad klient för interoperabilitet)

    -  Statistik över klient hälsa och topp ärende Sammanfattning

    - BIOS-ålder i år

    - Operativ systemets ålder i månader

    - Antal Software Center-åtgärder

    - Active Management Technology (AMT) klient version

    - Hämtnings fel för klient distribution

    - Åtgärds status för klient meddelande åtgärd (hur många gånger varje körs, högsta antal mål klienter och genomsnittlig frekvens för lyckade)

    - Distributions metoder som används för klienten och antalet klienter per distributions metod

    - Konfiguration av cachestorlek för klient

    - ***[Ny]***  Antal maskin varu lager klasser, program inventerings regler och fil insamlings regler




- **Cloud Services:**

  - Antal samlingar som har synkroniserats med Operations Management Suite

  -  Om Operations Management Suite Cloud Connector är aktiverat

  - ***[Ny]*** Konfiguration och användnings statistik för Cloud Management Gateway

  - ***[Ny]*** Antal Upgrade Analytics kopplingar




- **Samlingar**

    -  Statistik för samlings utvärdering (fråge tid, tilldelad till antal otilldelade, antal efter typ, ID-förnyelse och regel användning)

    - Samlingar utan distribution

    - Användning av samlings-ID (börjar inte med ID: n)



-   **Kompatibilitetsinställningar:**  

    -   Antal konfigurationsobjekt efter typ  

    -   Grundläggande information om konfigurationsbaslinjer (antal, antal distributioner och antal referenser)  

    -   Antal distributioner som refererar till inbyggda inställningar (nu ska du fånga in en reparations inställning)  

    -   Antal regler och distributioner som har skapats för anpassade inställningar (nu ska du fånga inställningen)  
    -   Antal distribuerade Simple Certificate Enrollment Protocol (SCEP), VPN, Wi-Fi, Certificate (. pfx) och mallar för efterlevnadsprinciper

    -  Antal SCEP-certifikat, VPN, Wi-Fi, certifikat (. pfx) och distributioner av efterlevnadsprinciper efter plattform

    - Passport for Work-princip (skapad, distribuerad)



-   **Innehåll**  

    -   Antal gränser efter typ  

    -   Information om gräns grupper (antal gränser och plats system som har tilldelats varje gräns grupp)  

    - ***[Ny]*** Relationer mellan gränser och återställnings konfiguration

    -   Information om distributions plats grupper (antal paket och distributions platser som har tilldelats varje distributions plats grupp)  

    -   Konfigurations information för distributions platser (användning av Branch cache och övervakning av distributions platser)  

    -   Konfigurations information för distributions hanteraren (trådar, fördröjning för omförsök, antal återförsök och inställningar för mottagar distributions plats)  

    - ***[Ny]*** Antal peer-cache-klienter och användnings statistik

    - ***[Ny]*** Statistik för nedladdning av klient innehåll


-   **Endpoint Protection:**  

    -   Användning av Endpoint Protection principer för program mot skadlig kod och Windows-brandväggen (antal unika principer som tilldelats gruppen)<br /><br /> Detta omfattar inte information om inställningarna som ingår i principen.  

    -   Endpoint Protection distributions fel (antal Endpoint Protection princip distributions fel koder)  

    -   Antal samlingar som har marker ATS för att visas i Endpoint Protection-instrumentpanelen  

    -   Antal aviseringar som kon figurer ATS för Endpoint Protection funktion  

    -   Principer för avancerat skydd (ATP) (antal principer och om principer har distribuerats)


- **Migreringsarkivet**

  -   Antal migrerade objekt (användning av migreringsguiden)



-   **Hantering av mobila enheter (MDM):**  

    -   ***[Uppdaterat]*** Antal utfärdade åtgärder för mobila enheter: lås, fäst rest, rensa, dra tillbaka och synkronisera nu-kommandon  

    -   Antal mobila enheter som hanteras av Configuration Manager och Microsoft Intune och hur de registrerades (bulk, User-based)  

    -   Schema för avsökning av mobila enheter och statistik för mobila enheters inchecknings tid  

    -   Antal principer för mobila enheter  

    -   Antal användare som har flera registrerade mobila enheter  

-   **Microsoft Intune fel sökning:**

    -   Antal och storlek på tillstånd, status, inventering, RDR, DDR, UDX, klient organisationens tillstånd, POL, LOG, cert, CRP, resync, CFD, RDO, BEX, ISM och Compliance-meddelanden som hämtas från Microsoft Intune

    -   Antal och storlek på enhets åtgärder (rensa, dra tillbaka, låsa), telemetri och data meddelanden som replikeras till Microsoft Intune

    -   Statistik över fullständig och delta-synkronisering av användare för Microsoft Intune


-   **Lokal hantering av mobila enheter (MDM)**  

    -   Statistik över distributionsresultat (lyckade/misslyckade) för lokala distributioner av MDM-program  

    -   Antal massregistrerade Windows 10-paket och Windows 10-profiler  



-   **Distribution av operativ system:**  

    -   Antal startavbildningar, drivrutiner, drivrutinspaket, multicast-aktiverade distributionsplatser, PXE-aktiverade distributionsplatser och aktivitetssekvenser  

    -   Antal användnings steg i en aktivitetssekvens

    - ***[Ny]*** Antal uppgraderings principer för utgåva



-   **Plats uppdateringar:**

    - Versioner av installerade Configuration Manager snabb korrigeringar




-   **Program uppdateringar:**  

    -   Totalt/genomsnittligt antal samlingar som har program uppdaterings distributioner och det högsta/genomsnittliga antalet distribuerade uppdateringar  

    -   Antal regler för automatisk distribution som är knutna till synkronisering  

    -   Antal regler för automatisk distribution som skapar nya uppdateringar eller som lägger till uppdateringar i en befintlig grupp  

    -   Tillgängliga och tids gräns delta som används i regler för automatisk distribution  

    -   Genomsnittligt och högsta antal tilldelningar per uppdatering  

    -   Antal uppdateringar som skapas och distribueras med System Center Update Publisher  

    -   Antal uppdateringsgrupper och tilldelningar  

    -   Antal uppdaterings paket och högsta/minsta/genomsnittliga antal distributions platser som är riktade till paket  

    -   Antalet uppdateringsgrupper och minsta/högsta/genomsnittligt antal uppdateringar per grupp  

    -   Antal uppdateringar och procent andelen uppdateringar som har distribuerats, förfallit, ersatts, laddats ned och innehåller licens avtal  

    -   Felkoder för uppdateringssökning och antal datorer  

    -   Utvärderingen av klientuppdateringar och avsökningsscheman  

    -   Synkroniseringsschema för programuppdateringsplats  

    -   Antal regler för automatisk distribution som har flera distributioner  

    -   Konfigurationer som används för aktiva Service planer för Windows 10  

    -   Innehållsversioner för Windows 10-instrumentpanelen  

    -   Antal Windows 10-klienter som använder Windows Update för företag  

    -   Klusterkorrigeringsstatistik  

    -   Antal distribuerade Office 365-uppdateringar  

    -   Klassificeringar som synkroniseras av program uppdaterings platsen

    -   Statistik över belastnings utjämning för program uppdaterings plats

    -  ***[Ny]*** Konfiguration av Windows 10 Express-uppdateringar




-   **SQL-/prestandadata:**  

    -   Antal största databastabeller  

    -   ***[Uppdaterat]***  SQL AlwaysOn-replikerad information, användning och hälso status

    -  Kvarhållningsperioden för ändrings spårning i SQL

    - Identifierings typer, aktiverade och schema (fullständig, stegvis)

    - Identifierings drifts statistik (antal objekt som hittades)

    - Prestanda problem i SQL Change tracking, kvarhållningsperiod och status för automatisk rensning



- **Övrigt**

    - Antal platser med Wake-on-LAN (WOL)

    - ***[Ny]*** Rapportering av användnings-och prestanda statistik  



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Nivå 3 – Fullständig
Den fullständiga nivån omfattar alla data i nivåerna Basic och Enhanced. Den innehåller också ytterligare information om Endpoint Protection, procentandel uppdateringskompatibilitet och information om programvaruuppdateringar.  Den här nivån kan även innehålla avancerad diagnostikinformation, t. ex. systemfiler och ögonblicks bilder av minnet, som kan innehålla personlig information som fanns i minnet eller loggfilerna vid hämtnings tillfället.

För Configuration Manager version 1610 omfattar den här nivån följande:

-   Samlingsutvärdering och uppdateringsstatistik

-   Endpoint Protection-hälsoöversikt (inklusive antal skyddade klienter, klienter i fara, okända klienter och klienter som inte stöds)

-   Konfiguration av Endpoint Protection-principer

-   Information om distribution av program uppdatering (procent andel distributioner som är riktade till klienten jämfört med UTC-tid, krävs jämfört med valfria kontra tyst och omstart av under tryckning)

-   Övergripande kompatibilitet för distributioner av programuppdateringar

-   Schemainformation för utvärdering av regler för automatisk distribution

-   Felkoder och antal för distributioner av programvaruuppdateringar

-   Minsta/högsta/genomsnittligt antal inaktiva klienter i samlingar med distributioner av programvaruuppdateringar

-   Antal grupper som har upphört att gälla program uppdateringar

-   Minsta/högsta/genomsnittligt antal programvaruuppdateringar per paket

-   Procentuellt antal lyckade sökningar efter programvaruuppdateringar

-   Minsta/högsta/genomsnittligt antal timmar sedan den senaste sökningen efter programvaruuppdateringar

-    Program uppdaterings produkter som har synkroniserats med program uppdaterings platsen
-    Kompatibilitetsinställningar: SCEP, VPN, Wi-Fi och mall för efterlevnadsprincip konfigurations information

-    Typ av EAS-principer för villkorlig åtkomst (block eller karantän) för enheter som hanteras av Intune

-   De främsta 50 processorerna i miljön

-   DCM-konfigurations paket för Configuration Manager användning

-   MSI produkt kod (vanliga appar som kunder distribuerar)

-   Översikt över ATP-hälsa

-   Detaljerade installations fel för klient distribution

- ***[Ny]*** Program information för Windows Store för företag (icke-aggregerad lista över synkroniserade program, inklusive AppID, online-tillstånd eller offline-tillstånd och totalt antal köpta licenser)
