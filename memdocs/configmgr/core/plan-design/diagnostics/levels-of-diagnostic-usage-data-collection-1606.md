---
title: Diagnostikdata för 1606
titleSuffix: Configuration Manager
description: Lär dig mer om de nivåer av diagnostik-och användnings data som Configuration Manager version 1606 samlar in.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7350d03-f440-4744-82d4-75f8c6c25028
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: a8cc58a11c1cce86bb5964ef4ad55958619a4529
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994879"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1606-of-configuration-manager"></a>Nivåer av diagnostik användnings data insamling för version 1606 av Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager version 1606 samlar in tre nivåer av diagnostik-och användnings data: **Basic**, **Enhanced**och **full**. Standardnivån för den här funktionen är Utökad. Följande avsnitt innehåller ytterligare information om data som samlas in på varje nivå.

Ändringar från tidigare versioner anges med ***[ny]***, ***[uppdaterat]***, ***[borttaget]*** eller ***[flyttat]***.


> [!IMPORTANT]
>  Configuration Manager samlar inte in plats koder, plats namn, IP-adresser, användar namn, dator namn, fysiska adresser eller e-postadresser på nivåerna Basic eller Enhanced. En samling av den här informationen på nivån fullständig är inte ändamålsenlig, det vill säga eventuellt inkluderad i avancerad diagnostikinformation, t. ex. loggfiler eller minnes ögonblicks bilder. Microsoft kommer inte att använda den här informationen för att identifiera dig, kontakta dig eller utveckla annonser.

##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Ändra nivån
 Administratörer som har en rollbaserad administrativ omfattning som inkluderar **ändrings** behörigheter för objekt klassen **plats** kan ändra nivån på data som samlas in i inställningarna för diagnostik-och användnings data i Configuration Manager-konsolen.

   Det gör du genom att gå till fliken backstage (den övre vänstra fliken med den nedrullningsbara pilen) i-konsolen, välja **användnings data**och sedan välja den data nivå som du vill använda.  

##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Nivå 1 – Grundläggande
 Nivån Basic innehåller data om hierarkin, data som krävs för att förbättra installations-eller uppgraderings upplevelsen och data som hjälper dig att fastställa de Configuration Manager uppdateringar som är tillämpliga för hierarkin.

 Från och med Configuration Manager version 1606 omfattar den här nivån följande:


-   Installations information:
      - Build, Installations typ, språk paket, funktioner som du har aktiverat  

      -   Distributions status och fel för uppdaterings paket, hämtnings förlopp och nödvändiga fel 

      -  Version av skript efter uppgradering

      -  Användning av snabb ring för uppdatering

-   Databas prestanda mått (information om bearbetning av replikering, SQL Server lagrade procedurer per processor och disk användning)

-   Grundläggande databas konfiguration (processorer, kluster konfiguration och konfiguration av distribuerade vyer)

-   Configuration Manager-databasschemat (hash för alla objekt definitioner)

-   Antal Configuration Manager-klient versioner och operativ system versioner

-   Antal operativ system för hanterade enheter och principer som angetts av Exchange Connector

-   Antal klient språk och nationella inställningar

-   Antal Windows 10-enheter per gren och version

-   Grundläggande Configuration Manager platshierarki (plats lista, typ, version, status, antal klienter och tidszon)

-   Grundläggande Server information för plats system (plats system roller som används, status för Internet och SSL, operativ system, processorer och fysisk eller virtuell dator)

-   Grundläggande identifierings statistik för användare (antal användar identifieringar och minsta/högsta/genomsnittlig grupp storlek)

-   Grundläggande Endpoint Protection information (klient versioner av program mot skadlig kod)

-   Grundläggande program-och distributions typer (totalt antal appar, totalt antal appar med flera distributions typer, totalt antal appar med beroenden, totalt ersatta appar och antal distributions tekniker som används)

-   OSD-antal (Basic Opera ting System Deployment) (bilder)

-   Distributions plats-och hanterings plats typer och grundläggande konfigurations information (skyddad, förinstallerad, PXE, multicast, SSL-tillstånd, pull-/peer-distributions platser, MDM-aktiverad, SSL-aktiverad osv.)

-   Telemetri statistik (vid körning, körning och fel)

-  Konfigurerat telemetri-nivå, läge (online eller offline) och snabb uppdaterings konfiguration

-  Användning av nätverks identifiering (aktive rad eller inaktive rad)
-  Administratörs konsol:

    -  Statistik om konsol anslutningar (operativ system version, språk, SKU och arkitektur, system minne, antal logiska processorer, Anslut plats-ID, installerade .NET-versioner och konsol språk paket)    


- ***[Ny]*** SQL-version, service pack nivå, utgåva, sorterings-ID och teckenuppsättning


##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Nivå 2 – Utökad
Den förbättrade nivån är standard när installationen är klar. Den här nivån omfattar data som samlas in på Basic-nivå, funktions specifika data (frekvens och användnings tid), Configuration Manager klient inställningar (komponent namn, tillstånd och vissa inställningar som avsöknings intervall) och grundläggande information om program uppdateringar.

Den här nivån rekommenderas eftersom den förser Microsoft med den minsta mängd data som krävs för att göra användbara förbättringar i framtida versioner av produkter och tjänster. Den här nivån samlar inte in objekt namn (platser, användare, dator eller objekt), information om säkerhetsrelaterade objekt eller säkerhets risker som antalet system som kräver program uppdateringar.

Från och med Configuration Manager version 1606 omfattar den här nivån följande:

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

    - ***[Ny]*** Antal Windows Store för företag-appar och synkronisering av statistik (inklusive sammanfattande typer av appar)  

    - ***[Ny]*** Statistik över gränserna (hur många snabba, hur många långsamma och antalet per grupp)

    - ***[Ny]*** Konfigurations alternativ och antal för MSI

    - ***[Ny]*** Krav för appar (antal inbyggda villkor refereras till av distributions teknik)

    - ***[Ny]*** App-ersättning, maximalt kedje djup

    - ***[Ny]*** UDA-användning (Universal Data Access) och hur skapas



-   **Klientsession**  

    -   Lista/antal aktiverade klientagenter  

    -   Antal klientinstallationer från varje typ av källplats  

    -   Antal klientinstallationsfel  

    -  ***[Ny]*** Automatisk distributions konfiguration för klient uppgradering, inklusive klient pilotering

    -  ***[Ny]*** Statistik över klient hälsa och topp ärende Sammanfattning

    - ***[Ny]*** BIOS-ålder i år

    - ***[Ny]*** Operativ systemets ålder i månader

    - ***[Ny]*** Antal Software Center-åtgärder

    - ***[Ny]*** Active Management Technology (AMT) klient version

    - ***[Ny]*** Hämtnings fel för klient distribution

    - ***[Ny]*** Åtgärds status för klient meddelande åtgärd (hur många gånger varje körs, högsta antal mål klienter och genomsnittlig frekvens för lyckade)

    - ***[Ny]*** Distributions metoder som används för klienten och antalet klienter per distributions metod

    - ***[Ny]*** Konfiguration av cachestorlek för klient



- ***[Ny]*** **Cloud Services:**

  - ***[Ny]*** Antal samlingar som har synkroniserats med Operations Management Suite

  - ***[Ny]***  Om Operations Management Suite Cloud Connector är aktiverat



- ***Nyårs Samlingar***

    -  ***[Flyttad]*** Statistik för samlings utvärdering (fråge tid, tilldelad till antal otilldelade, antal efter typ, ID-förnyelse och regel användning)

    - ***[Ny]*** Samlingar utan distribution

    - ***[Ny]*** Användning av samlings-ID (börjar inte med ID: n)



-   **Kompatibilitetsinställningar:**  

    -   Antal konfigurationsobjekt efter typ  

    -   Grundläggande information om konfigurationsbaslinjer (antal, antal distributioner och antal referenser)  

    -   ***[Uppdaterat]*** Antal distributioner som refererar till inbyggda inställningar (nu ska du fånga in en reparations inställning)  

    -   ***[Uppdaterat]*** Antal regler och distributioner som har skapats för anpassade inställningar (nu ska du fånga inställningen)  
    -   Antal distribuerade Simple Certificate Enrollment Protocol (SCEP), VPN, Wi-Fi, Certificate (. pfx) och mallar för efterlevnadsprinciper

    -  Antal SCEP-certifikat, VPN, Wi-Fi, certifikat (. pfx) och distributioner av efterlevnadsprinciper efter plattform

    - ***[Ny]*** Passport for Work-princip (skapad, distribuerad)



-   **Innehåll**  

    -   Antal gränser efter typ  

    -   Information om gräns grupper (antal gränser och plats system som har tilldelats varje gräns grupp)  

    -   Information om distributions plats grupper (antal paket och distributions platser som har tilldelats varje distributions plats grupp)  

    -   Konfigurations information för distributions platser (användning av Branch cache och övervakning av distributions platser)  

    -   Konfigurations information för distributions hanteraren (trådar, fördröjning för omförsök, antal återförsök och inställningar för mottagar distributions plats)  


-   **Endpoint Protection:**  

    -   Användning av Endpoint Protection principer för program mot skadlig kod och Windows-brandväggen (antal unika principer som tilldelats gruppen)<br /><br /> Detta omfattar inte information om inställningar som ingår i principen.  

    -   Endpoint Protection distributions fel (antal Endpoint Protection princip distributions fel koder)  

    -   Antal samlingar som har marker ATS för att visas i Endpoint Protection-instrumentpanelen  

    -   Antal aviseringar som har kon figurer ATS för Endpoint Protection funktionen  

    - ***[Ny]*** Principer för avancerat skydd (ATP) (antal principer och om principer har distribuerats)


-   ***[Borttaget]*** **hantering av mobil program (MAM):**  

    -   ***[Borttaget]*** Antal MAM-aktiverade Office-program, branschspecifika program och principer efter operativ system  

    -   ***[Borttaget]*** Antal distributioner av MAM-program/-principer  

    -   ***[Borttaget]*** Antal regler som skapas per MAM-inställning  


- ***[Ny]*** **migrering:**

  -  ***[Ny]***  Antal migrerade objekt (användning av migreringsguiden)



-   **Hantering av mobila enheter (MDM):**  

    -   Antal utfärdade åtgärder för mobila enheter: lås, fäst rest, rensa och dra tillbaka kommandon  

    -   Antal mobila enheter som hanteras av Configuration Manager och Microsoft Intune och hur de registrerades (bulk eller användarbaserade)  

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

    -   ***[Ny]*** Antal användnings steg i en aktivitetssekvens



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

    -   Antal distribuerade Microsoft 365 uppdateringar  

    -   Klassificeringar som synkroniseras av program uppdaterings platsen

    -   ***[Ny]*** Statistik över belastnings utjämning för program uppdaterings plats



-   **SQL-/prestandadata:**  

    -   Antal största databastabeller  

    -   SQL Always-On-replikinformation  

    -  Kvarhållningsperioden för ändrings spårning i SQL

    - ***[Ny]*** Identifierings typer, aktiverade och schema (fullständig, stegvis)

    - ***[Ny]*** Identifierings drifts statistik (antal objekt som hittades)

    - ***[Ny]*** Prestanda problem i SQL Change tracking, kvarhållningsperiod och status för automatisk rensning



- ***[Ny]*** **Diverse**

    - ***[Ny]*** Antal platser med Wake-on-LAN (WOL)



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Nivå 3 – Fullständig
Den fullständiga nivån omfattar alla data i nivåerna Basic och Enhanced. Den innehåller också ytterligare information om Endpoint Protection, procentandel uppdateringskompatibilitet och information om programvaruuppdateringar. Den här nivån kan även innehålla avancerad diagnostikinformation, t. ex. systemfiler och ögonblicks bilder av minnet, som kan innehålla personlig information som fanns i minnet eller loggfilerna vid hämtnings tillfället.

Från och med Configuration Manager version 1606 omfattar den här nivån följande:

-   Samlingsutvärdering och uppdateringsstatistik

-   Endpoint Protection-hälsoöversikt (inklusive antal skyddade klienter, klienter i fara, okända klienter och klienter som inte stöds)

-   Konfiguration av Endpoint Protection-principer

-   Information om distribution av program uppdatering (procent andel distributioner som är riktade till klienten jämfört med UTC-tid, krävs jämfört med valfria kontra tyst och omstart av under tryckning)

-   Övergripande kompatibilitet för distributioner av programuppdateringar

-   Schemainformation för utvärdering av regler för automatisk distribution

-   ***[Borttaget]*** Antal klienter som har NAP-principer (Network Access Protection)

-   Felkoder och antal för distributioner av programvaruuppdateringar

-   Minsta/högsta/genomsnittligt antal inaktiva klienter i samlingar med distributioner av programvaruuppdateringar

-   Antal grupper som har upphört att gälla program uppdateringar

-   Minsta/högsta/genomsnittligt antal programvaruuppdateringar per paket

-   Procentuellt antal lyckade sökningar efter programvaruuppdateringar

-   Minsta/högsta/genomsnittligt antal timmar sedan den senaste sökningen efter programvaruuppdateringar

-    Program uppdaterings produkter som har synkroniserats med program uppdaterings platsen
-    Kompatibilitetsinställningar: konfigurations information för SCEP, VPN, Wi-Fi och efterlevnadsprincip

-    Typ av EAS-principer för villkorlig åtkomst (block eller karantän) för enheter som hanteras av Intune

-   ***[Ny]*** De främsta 50 processorerna i miljön

-   ***[Ny]*** DCM-konfigurations paket för Configuration Manager användning

-   ***[Ny]*** MSI produkt kod (vanliga appar som kunder distribuerar)

-   ***[Ny]*** Översikt över ATP-hälsa

-   ***[Ny]*** Detaljerade installations fel för klient distribution
