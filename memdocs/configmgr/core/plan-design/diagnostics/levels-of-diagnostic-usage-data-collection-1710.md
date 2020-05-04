---
title: Diagnostikdata för 1710 | Configuration Manager
titleSuffix: Configuration Manager
description: Lär dig mer om de nivåer av diagnostik-och användnings data som Configuration Manager version 1710 samlar in.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8fce5391-8e75-4f99-813a-76f8842be5bc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: fcc3d2e34c9387e158b3b35cd104c9fc43136ace
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715552"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1710-of-configuration-manager"></a>Nivåer av diagnostik användnings data insamling för version 1710 av Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager version 1710 samlar in tre nivåer av diagnostik-och användnings data: **Basic**, **Enhanced**och **full**. Standardnivån för den här funktionen är Utökad. Följande avsnitt innehåller ytterligare information om data som samlas in på varje nivå.

Ändringar från tidigare versioner anges med ***[ny]***, ***[uppdaterat]***, ***[borttaget]*** eller ***[flyttat]***.


> [!IMPORTANT]
>  Configuration Manager samlar inte in plats koder, plats namn, IP-adresser, användar namn, dator namn, fysiska adresser eller e-postadresser på nivåerna Basic eller Enhanced. En samling av den här informationen på nivån fullständig är inte ändamålsenlig, det vill säga eventuellt inkluderad i avancerad diagnostikinformation, t. ex. loggfiler eller minnes ögonblicks bilder. Microsoft kommer inte att använda den här informationen för att identifiera dig, kontakta dig eller utveckla annonser.



##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Ändra nivån
 Administratörer som har en rollbaserad administrativ omfattning som inkluderar **ändrings** behörigheter för objekt klassen **plats** kan ändra nivån på data som samlas in i inställningarna för diagnostik-och användnings data i Configuration Manager-konsolen.

Du ändrar data insamlings nivån från-konsolen genom att gå till **Administration** > **Översikt** > **plats konfiguration** > **platser**. Öppna **Inställningar för hierarki**och välj sedan den data nivå som du vill använda.  



##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Nivå 1 – Grundläggande
Nivån Basic innehåller data om hierarkin, data som krävs för att förbättra installations-eller uppgraderings upplevelsen och data som hjälper dig att fastställa de Configuration Manager uppdateringar som är tillämpliga för hierarkin.

För Configuration Manager version 1710 omfattar den här nivån följande:

- Administratörs konsol:
   - Statistik om konsol anslutningar (operativ system version, språk, SKU och arkitektur, system minne, antal logiska processorer, Anslut plats-ID, installerade .NET-versioner och konsol språk paket)

- Grundläggande program-och distributions typer (totalt antal appar, totalt antal appar med flera distributions typer, totalt antal appar med beroenden, totalt ersatta appar och antal distributions tekniker som används)

- Grundläggande Configuration Manager platshierarki (plats lista, typ, version, status, antal klienter och tidszon)

- Grundläggande databas konfiguration (processorer, kluster konfiguration och konfiguration av distribuerade vyer)

- Grundläggande identifierings statistik (antal identifiering och minsta/högsta/genomsnittlig grupp storlek), inklusive när platsen körs helt med Azure Active Directory Services.

- Grundläggande Endpoint Protection information (klient versioner av program mot skadlig kod)

- OSD-antal (Basic Opera ting System Deployment) (bilder)

- Grundläggande Server information för plats system (plats system roller som används, status för Internet och SSL, operativ system, processorer, fysisk eller virtuell dator och användning av plats Server hög tillgänglighet)

- Configuration Manager-databasschemat (hash för alla objekt definitioner)

- Konfigurerat telemetri-nivå, läge (online eller offline) och snabb uppdaterings konfiguration

- Antal klient språk och nationella inställningar

- ***[Uppdaterat]*** Antal Configuration Manager-klient versioner, operativ system versioner och Office-versioner

- Antal operativ system för hanterade enheter och principer som angetts av Exchange Connector

- Antal Windows 10-enheter per gren och version

- Prestandamått för databas (information om replikeringsbearbetning, de viktigaste SQL-lagrade procedurer efter processor- och diskanvändning)

- Distributions plats-och hanterings plats typer och grundläggande konfigurations information (skyddad, förinstallerad, PXE, multicast, SSL-tillstånd, pull-/peer-distributions platser, MDM-aktiverad, SSL-aktiverad osv.)

- Hash-lista med tillägg för administratörs konsolens egenskaps sidor och guider

- Installations information:
     - Build, Installations typ, språk paket, funktioner som du har aktiverat   

     - För hands versions användning, installations medie typ, förgrenings typ

     - Utgångs datum för Software Assurance      

     - Distributions status och fel för uppdaterings paket, hämtnings förlopp och nödvändiga fel 

     - Användning av snabb ring för uppdatering

     - Version av skript efter uppgradering

- SQL-version, service pack nivå, utgåva, sorterings-ID och teckenuppsättning     
- Telemetristatistik (när de körs, runtime, fel)

- Användning av nätverks identifiering (aktive rad eller inaktive rad)




##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Nivå 2 – Utökad
Den förbättrade nivån är standard när installationen är klar. Den här nivån omfattar data som samlas in på Basic-nivå och funktions specifika data (frekvens och användnings tid), Configuration Manager klient inställningar (komponent namn, tillstånd och vissa inställningar som avsöknings intervall) och grundläggande information om program uppdateringar.

Den här nivån rekommenderas eftersom den förser Microsoft med den minsta mängd data som krävs för att göra användbara förbättringar i framtida versioner av produkter och tjänster. Den här nivån samlar inte in objekt namn (platser, användare, dator eller objekt), information om säkerhetsrelaterade objekt eller säkerhets risker som antalet system som kräver program uppdateringar.

För Configuration Manager version 1710 omfattar den här nivån följande:

- **Program hantering:**  

   - Krav för appar (antal inbyggda villkor refereras till av distributions teknik)

   - App-ersättning, maximalt kedje djup

   - Statistik för program godkännande och användnings frekvens

   - Statistik för program innehålls storlek

   - Information om program distribution (användning av installation och avinstallation kräver godkännande, användar interaktion aktiverat/inaktiverat, beroende, ersättnings-och användnings antal för installations beteende funktionen)  

   - Storlek och komplexitets statistik för program princip

   - Statistik över förfrågningar om programtillgänglighet

   - Grundläggande konfigurations information för paket och program (distributions alternativ och program flaggor)

   - Grundläggande användning/mål information för distributions typer som används inom organisationen (användare jämfört med enhetens mål, krävs respektive är tillgänglig och Universal Apps)

   - Statistik över gränserna (hur många snabba, hur många långsamma och antalet per grupp)

   - Antal App-V-miljöer och distributionsegenskaper

   - Antal tillämpliga program efter operativsystem  

   - Antal program som refereras till av en aktivitetssekvens

   - Antal olika anpassningar för program katalogen

   - Antal Office 365-program som skapats med instrument panelen

   - Antal paket efter typ  

   - Antal paket-/programdistributioner  

   - Antal Windows 10-licensierade programlicenser  

   - Antal Windows Installer distributions typer genom avinstallation av innehålls inställningar

   - Antal Microsoft Store för affärsappar och synkronisering av statistik (inklusive sammanställda typer av appar, status för licensierad app och antal online-och offline-licensierade appar)  

   - Underhållsperiodstyp och varaktighet  

   - Minsta/högsta/Genomsnittligt antal program distributioner per användare/enhet per tids period

   - De vanligaste fel koderna för programinstallationer per distributions teknik

   - Konfigurations alternativ och antal för MSI

   - Statistik för slut användar interaktion med meddelanden om nödvändiga program distributioner   

   - UDA-användning (Universal Data Access), hur skapas




- **Klientsession**  

   - Active Management Technology (AMT) klient version

   - BIOS-ålder i år

   - Antal enheter med säker start aktiverat

   - Antal enheter efter TPM-tillstånd

   - Automatisk klient uppgradering: distributions konfiguration, inklusive klient pilotering och undantags användning (utökad klient för interoperabilitet)

   - Konfiguration av cachestorlek för klient

   - Hämtnings fel för klient distribution

   - Statistik över klient hälsa och topp ärende Sammanfattning

   - Åtgärds status för klient meddelande åtgärd (hur många gånger varje körs, högsta antal mål klienter och genomsnittlig frekvens för lyckade)
   - Antal klientinstallationer från varje typ av källplats  

   - Antal klientinstallationsfel  

   - Antal enheter som virtualiserats av Hyper-V eller Azure  

   - Antal Software Center-åtgärder   

   - Antal UEFI-aktiverade enheter

   - Distributions metoder som används för klienten och antalet klienter per distributions metod

   - Lista/antal aktiverade klientagenter  

   - Operativ systemets ålder i månader

   - Antal maskin varu lager klasser, program inventerings regler och fil insamlings regler

   - Statistik för hälsoattestering av enheter, inklusive de vanligaste fel koderna, antalet lokala servrar och antalet enheter i olika tillstånd.



- **Cloud Services:**

  - Azure Active Directory identifierings statistik

  - Konfigurations-och användnings statistik för Cloud Management Gateway, inklusive antal regioner och miljöer samt statistik för autentisering och auktorisering

  - Antal Azure Active Directory program och tjänster som är anslutna till Configuration Manager

  - Antal klienter som är anslutna till Azure Active Directory Services

  - Antal samlingar som har synkroniserats till Azure Log Analytics

  - Antal Upgrade Analytics kopplingar

  - Om Azure Log Analytics Cloud Connector har Aktiver ATS


- ***[Ny]*** Samhantering
  - ***[Ny]*** Sammanställd användnings statistik för samhantering, inklusive antal registrerade klienter, klienter som tar emot principer, arbets belastnings tillstånd, pilot/exkludering samlings storlekar, registrerings fel
  - ***[Ny]*** Antal klienter efter samhanterings registrerings metod
  - ***[Ny]*** Fel statistik för samhanterings registrering
  - ***[Ny]*** Registrerings schema och historisk statistik
  - ***[Ny]*** Antal klienter som är kvalificerade för samhantering
  - ***[Ny]*** Associerad Intune-klient


- **Samlingar**

    - Användning av samlings-ID (börjar inte med ID: n)

    - Statistik för samlings utvärdering (fråge tid, tilldelad till antal otilldelade, antal efter typ, ID-förnyelse och regel användning)

    - Samlingar utan distribution




- **Kompatibilitetsinställningar:**  

    - Grundläggande information om konfigurationsbaslinjer (antal, antal distributioner och antal referenser)

    - Fel statistik för policy för efterlevnad

    - Antal konfigurationsobjekt efter typ  

    - Antal distributioner som refererar till inbyggda inställningar (nu ska du fånga in en reparations inställning)  

    - Antal regler och distributioner som har skapats för anpassade inställningar (nu ska du fånga inställningen)  

    - Antal distribuerade Simple Certificate Enrollment Protocol (SCEP), VPN, Wi-Fi, Certificate (. pfx) och mallar för efterlevnadsprinciper

    - Antal SCEP-certifikat, VPN, Wi-Fi, certifikat (. pfx) och distributioner av efterlevnadsprinciper efter plattform

    - Passport for Work-princip (skapad, distribuerad)



- **Innehåll**  

    - Information om gräns grupper (antal gränser och plats system som har tilldelats varje gräns grupp)  

    - Relationer mellan gränser och återställnings konfiguration

    - Statistik för nedladdning av klient innehåll

    - Antal gränser efter typ  

    - Antal klienter för peer-cache, användnings statistik och delvis nedladdnings statistik

    - Konfigurations information för distributions hanteraren (trådar, fördröjning för omförsök, antal återförsök och inställningar för mottagar distributions plats)  

    - Konfigurations information för distributions platser (användning av Branch cache och övervakning av distributions platser)

    - Information om distributions plats grupper (antal paket och distributions platser som har tilldelats varje distributions plats grupp)  



- **Endpoint Protection:**  

   - Principer för avancerat skydd (ATP) (antal principer och om principer har distribuerats)

   - Antal aviseringar som kon figurer ATS för Endpoint Protection funktion  

   - Antal samlingar som har marker ATS för att visas i Endpoint Protection-instrumentpanelen  

   - ***[Ny]*** Antal Windows Defender sårbarhet Guard-principer, distributioner och riktade klienter

   - Endpoint Protection distributions fel (antal Endpoint Protection princip distributions fel koder)  

   - Användning av Endpoint Protection principer för program mot skadlig kod och Windows-brandväggen (antal unika principer som tilldelats gruppen)<br /><br /> Detta omfattar inte information om inställningarna som ingår i principen.  



- **Migreringsarkivet**

  - Antal migrerade objekt (användning av migreringsguiden)



- **Hantering av mobila enheter (MDM):**  

    - Antal utfärdade åtgärder för mobila enheter: lås, fäst rest, rensa, dra tillbaka och synkronisera nu-kommandon

    - Antal principer för mobila enheter  

    - Antal mobila enheter som hanteras av Configuration Manager och Microsoft Intune och hur de registrerades (bulk, User-based)  

    - Antal användare som har flera registrerade mobila enheter  

    - Schema för avsökning av mobila enheter och statistik för mobila enheters inchecknings tid  




- **Microsoft Intune fel sökning:**

    - Antal och storlek på enhets åtgärder (rensa, dra tillbaka, låsa), telemetri och data meddelanden som replikeras till Microsoft Intune

    - Antal och storlek på tillstånd, status, inventering, RDR, DDR, UDX, klient organisationens tillstånd, POL, LOG, cert, CRP, resync, CFD, RDO, BEX, ISM och Compliance-meddelanden som hämtas från Microsoft Intune

    - Statistik över fullständig och delta-synkronisering av användare för Microsoft Intune



- **Lokal hantering av mobila enheter (MDM)**  

    - Antal massregistrerade Windows 10-paket och Windows 10-profiler  

    - Statistik över distributionsresultat (lyckade/misslyckade) för lokala distributioner av MDM-program  




- **Distribution av operativ system:**  

    - Antal startavbildningar, drivrutiner, drivrutinspaket, multicast-aktiverade distributionsplatser, PXE-aktiverade distributionsplatser och aktivitetssekvenser  

    - Antal start avbildningar per Configuration Manager klient version

    - Antal start avbildningar från Windows PE-version

    - Antal uppgraderings principer för utgåva

    - Antal maskinvaru-ID: n som undantas från PXE

    - ***[Ny]*** Antal operativ system distributioner per operativ system version

    - ***[Ny]*** Antal operativ system uppgraderingar över tid

    - Antal aktivitetssekvensdistributioner som använder alternativ för att hämta innehåll i förväg

    - Antal användnings steg i en aktivitetssekvens

    - Version av Windows ADK installerad


- **Plats uppdateringar:**

    - Versioner av installerade Configuration Manager snabb korrigeringar



- **Program uppdateringar:**  

    - Tillgängliga och tids gräns delta som används i regler för automatisk distribution  

    - Genomsnittligt och högsta antal tilldelningar per uppdatering  

    - Utvärderingen av klientuppdateringar och avsökningsscheman  

    - Klassificeringar som synkroniseras av program uppdaterings platsen

    - Klusterkorrigeringsstatistik  

    - Konfiguration av Windows 10 Express-uppdateringar

    - Konfigurationer som används för aktiva Service planer för Windows 10  

    - Antal distribuerade Office 365-uppdateringar  

    - Antal synkroniserade Microsoft-ytaktiva driv rutiner

    - Antal uppdateringsgrupper och tilldelningar  

    - Antal uppdaterings paket och högsta/minsta/genomsnittliga antal distributions platser som är riktade till paket  

    - Antal uppdateringar som skapas och distribueras med System Center Update Publisher  

    - Antal Windows 10-klienter som använder Windows Update för företag  

    - Antal Windows Update för affärs principer som skapats och distribuerats

    - Antal regler för automatisk distribution som är knutna till synkronisering  

    - Antal regler för automatisk distribution som skapar nya uppdateringar eller som lägger till uppdateringar i en befintlig grupp  

    - Antal regler för automatisk distribution som har flera distributioner  

    - Antalet uppdateringsgrupper och minsta/högsta/genomsnittligt antal uppdateringar per grupp  

    - Antal uppdateringar och procent andelen uppdateringar som har distribuerats, förfallit, ersatts, laddats ned och innehåller licens avtal  

    - Statistik över belastnings utjämning för program uppdaterings plats

    - Synkroniseringsschema för programuppdateringsplats  

    - Totalt/genomsnittligt antal samlingar som har program uppdaterings distributioner och det högsta/genomsnittliga antalet distribuerade uppdateringar  

    - Felkoder för uppdateringssökning och antal datorer  

    - Innehållsversioner för Windows 10-instrumentpanelen  



- **SQL-/prestandadata:**  

    - Konfiguration och varaktighet för sammanfattning av webbplats

    - Antal största databastabeller  

    - Identifierings drifts statistik (antal objekt som hittades)

    - Identifierings typer, aktiverade och schema (fullständig, stegvis)

    - SQL AlwaysOn-replikerad information, användning och hälso status

    - Prestanda problem i SQL Change tracking, kvarhållningsperiod och status för automatisk rensning

    - Kvarhållningsperioden för ändrings spårning i SQL

    - Prestanda statistik för tillstånd och status meddelanden, inklusive de vanligaste och mest dyra meddelande typerna



- **Övrigt**

    - Konfiguration av informations lager service punkt, inklusive synkroniseringsschema och genomsnittlig tid

    - Antal skript och körnings statistik

    - Antal platser med Wake-on-LAN (WOL)

    - Rapportering av användnings-och prestanda statistik  



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Nivå 3 – Fullständig
Den fullständiga nivån omfattar alla data i nivåerna Basic och Enhanced. Den innehåller också ytterligare information om Endpoint Protection, procentandel uppdateringskompatibilitet och information om programvaruuppdateringar.  Den här nivån kan även innehålla avancerad diagnostikinformation, t. ex. systemfiler och ögonblicks bilder av minnet, som kan innehålla personlig information som fanns i minnet eller loggfilerna vid hämtnings tillfället.

För Configuration Manager version 1710 omfattar den här nivån följande:

- Schemainformation för utvärdering av regler för automatisk distribution

- Översikt över ATP-hälsa

- Samlingsutvärdering och uppdateringsstatistik

- Statistik om efterlevnad och fel i policyn för efterlevnad

- Kompatibilitetsinställningar: SCEP, VPN, Wi-Fi och mall för efterlevnadsprinciper konfiguration information antal grupper som har upphört att gälla program uppdateringar

- DCM-konfigurations paket för Configuration Manager användning

- Detaljerade installations fel för klient distribution

- Endpoint Protection-hälsoöversikt (inklusive antal skyddade klienter, klienter i fara, okända klienter och klienter som inte stöds)

- Konfiguration av Endpoint Protection-principer

- Lista över processer som kon figurer ATS med installations beteende för program

- Minsta/högsta/genomsnittligt antal timmar sedan den senaste sökningen efter programvaruuppdateringar

- Minsta/högsta/genomsnittligt antal inaktiva klienter i samlingar med distributioner av programvaruuppdateringar

- Minsta/högsta/genomsnittligt antal programvaruuppdateringar per paket

- MSI produkt kod (vanliga appar som kunder distribuerar)

- Övergripande kompatibilitet för distributioner av programuppdateringar

- Felkoder och antal för distributioner av programvaruuppdateringar

- Information om distribution av program uppdatering (procent andel distributioner som är riktade till klienten jämfört med UTC-tid, krävs jämfört med valfria kontra tyst och omstart av under tryckning)

- Program uppdaterings produkter som har synkroniserats med program uppdaterings platsen

- Procentuellt antal lyckade sökningar efter programvaruuppdateringar

- De främsta 50 processorerna i miljön

- Typ av EAS-principer för villkorlig åtkomst (block eller karantän) för enheter som hanteras av Intune

- Microsoft Store information om företags program (icke-aggregerad lista över synkroniserade program, inklusive AppID, online-tillstånd eller offline-tillstånd och totalt antal köpta licenser)
