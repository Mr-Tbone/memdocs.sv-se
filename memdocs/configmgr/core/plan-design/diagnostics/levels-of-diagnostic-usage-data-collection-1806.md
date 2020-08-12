---
title: Diagnostik-och användnings data för 1806
titleSuffix: Configuration Manager
description: Läs mer om vilka data som Configuration Manager samlar in på varje nivå i version 1806.
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: a0287beb-70a9-4b57-a627-e7bfba27fd3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e1f10f291619ecf6ff3d5b997046f035c02bf7e7
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128669"
---
# <a name="diagnostic-and-usage-data-for-1806"></a>Diagnostik-och användnings data för 1806

*Gäller för: Configuration Manager (aktuell gren)*

Följande avsnitt innehåller ytterligare information om data som samlas in på varje nivå. Mer information om nivåerna och hur du ändrar dem finns i [nivåer av diagnostikens användnings data](levels-overview.md).

Ändringar från tidigare versioner anges med ***[ny]***, ***[uppdaterat]***, ***[borttaget]*** eller ***[flyttat]***.

> [!IMPORTANT]
> Configuration Manager samlar inte in plats koder, plats namn, IP-adresser, användar namn, dator namn, fysiska adresser eller e-postadresser på nivåerna Basic eller Enhanced. En samling av den här informationen på nivån fullständig är inte ändamålsenlig. Den kan inkluderas i avancerad diagnostisk information som loggfiler eller minnes ögonblicks bilder. Microsoft använder inte den här informationen för att identifiera dig, kontakta dig eller utveckla annonser.

## <a name="level-1---basic"></a><a name="bkmk_level1"></a> Nivå 1 – Grundläggande

För Configuration Manager version 1806 omfattar den här nivån följande data:

- Statistik om Configuration Manager konsol anslutningar: OS-version, språk, SKU och arkitektur, system minne, antal logiska processorer, Anslut plats-ID, installerade .NET-versioner och konsol språk paket

- Grundläggande program-och distributions typer antal: totalt antal appar, totalt antal appar med flera distributions typer, totalt antal appar med beroenden, totalt antal ersatta appar och antal distributions tekniker som används

- Grundläggande Configuration Manager webbplatsens hierarki data: plats lista, typ, version, status, antal klienter och tidszon

- ***[Uppdaterat]*** Grundläggande databas konfiguration: processorer, minnes storlek, minnes inställningar, Configuration Manager databas konfiguration, Configuration Manager databas storlek, kluster konfiguration och konfiguration av distribuerade vyer

- Grundläggande identifierings statistik: antal identifieringar, minsta/högsta/genomsnittlig grupp storlek och när platsen körs helt med Azure Active Directory Services

- Grundläggande Endpoint Protection information om klient versioner av program mot skadlig kod

- Antal avbildningar av Basic OS-distribution

- Grundläggande plats system Server information: plats system roller som används, status för Internet och SSL, operativ system, processorer, fysisk eller virtuell dator och användning av plats Server hög tillgänglighet

- Configuration Manager-databasschemat (hash för alla objekt definitioner)

- Konfigurerad nivå för diagnostik-och användnings data, online-eller offline-läge och snabb uppdaterings konfiguration

- Antal klient språk och nationella inställningar

- Antal Configuration Manager-klient versioner, OS-versioner och Office-versioner

- Antal operativ system för hanterade enheter och principer som angetts av Exchange Connector

- Antal Windows 10-enheter per gren och version

- Antal Windows 10-klienter som använder Windows Update för företag  

- Prestanda mått för databasen: bearbetnings information för replikering, SQL Server lagrade procedurer per processor och disk användning

- Distributions plats-och hanterings plats typer och grundläggande konfigurations information: skyddad, förinstallerad, PXE, multicast, SSL-tillstånd, pull-/peer-distributions platser, MDM-aktiverad och SSL-aktiverad

- Hash-lista med tillägg för administratörs konsolens egenskaps sidor och guider

- Installations information:
     - Build, Installations typ, språk paket, funktioner som du har aktiverat   

     - För hands versions användning, installations medie typ, förgrenings typ

     - Utgångs datum för Software Assurance      

     - Distributions status och fel för uppdaterings paket, hämtnings förlopp och nödvändiga fel 

     - Användning av snabb ring för uppdatering

     - Version av skript efter uppgradering

- SQL-version, service pack nivå, utgåva, sorterings-ID och teckenuppsättning     

- Statistik för diagnostik-och användnings data: vid körning, körning, fel

- Om nätverks identifiering är aktiverat eller inaktiverat

- Antal klienter som är anslutna till Azure Active Directory

- Antal tidfasade distributioner som skapats av typ

- Antal utökade klienter för samverkan

- En hashad lista över maskin varu inventerings egenskaper som är längre än 255 tecken

- ***[Flyttad]*** Antal klienter efter samhanterings registrerings metod  

- ***[Flyttad]*** Fel statistik för samhanterings registrering  

- ***[Ny]*** Antal klienter efter Windows OS-ålder, till närmaste tre månaders period  

- ***[Ny]*** De 10 viktigaste processor namnen som används på klienter  

- ***[Ny]*** Antal och bearbetnings takt för nyckel Configuration Manager objekt: data identifierings poster (DDR), tillstånds meddelanden, status meddelanden, maskin varu inventering, program varu inventering och totalt antal filer i inkorgar  

- ***[Ny]*** Information om plats serverns disk-och processor prestanda  

- ***[Ny]*** Information om drift tid och minnes användning för Configuration Manager plats Server processer  

- ***[Ny]*** Antal krascher för Configuration Manager plats Server processer och Watson-signatur-ID, om tillgängligt  



## <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Nivå 2 – Utökad

För Configuration Manager version 1806 omfattar den här nivån följande data:

### <a name="application-management"></a>Programhantering  

- Krav för appar: antal inbyggda villkor som en distributions teknik refererar till

- App-ersättning, maximalt kedje djup

- Statistik för program godkännande och användnings frekvens

- Statistik för program innehålls storlek

- Information om program distribution: användning av installation och avinstallation kräver godkännande, användar interaktion aktiverat/inaktiverat, beroende, ersättnings-och användnings antal för funktionen installera beteende  

- Storlek och komplexitets statistik för program princip

- Statistik över förfrågningar om programtillgänglighet

- Grundläggande konfigurations information för paket och program: distributions alternativ och program flaggor

- Grundläggande användning/mål information för distributions typer: användare mot enhet, krävs respektive tillgänglig och Universal Apps

- Antal App-V-miljöer och distributionsegenskaper

- Antal program tillämplighets per operativ system  

- Antal program som refereras till av en aktivitetssekvens

- Antal olika anpassningar för program katalogen

- Antal Office 365-program som skapats med instrument panelen

- Antal paket efter typ  

- Antal paket-/programdistributioner  

- Antal Windows 10-licensierade programlicenser  

- Antal Windows Installer distributions typer genom avinstallation av innehålls inställningar

- Antal Microsoft Store för företags-och synkroniserings statistik: sammanfattade typer av appar, status för licensierad app och antalet online-och offline-licensierade appar  

- Underhållsperiodstyp och varaktighet  

- Minsta/högsta/Genomsnittligt antal program distributioner per användare/enhet per tids period

- De vanligaste fel koderna för programinstallationer per distributions teknik

- Konfigurations alternativ och antal för MSI

- Statistik för slut användar interaktion med meddelanden om nödvändiga program distributioner   

- Användning av universell data åtkomst, hur skapas

- Statistik över sammanställd mappning mellan användare och enhet 

- Högsta och genomsnittliga primära användare per enhet  

- ***[Ny]*** Användning av globala villkor för program efter typ  

- ***[Ny]*** Anpassnings konfiguration för Software Center  

- ***[Ny]*** Paket konverterings hanterarens beredskap och antal  

- ***[Ny]*** Antal program identifierings metoder per typ  

- ***[Ny]*** Antal fel för tvingande program  

- ***[Ny]*** Egenskaper för MSI-installationsprogrammet 

- ***[Ny]*** Statistik för användar installations begär Anden



### <a name="client"></a>Klient  

- Active Management Technology (AMT) klient version

- BIOS-ålder i år

- Antal enheter med säker start aktiverat

- Antal enheter efter TPM-tillstånd

- Automatisk klient uppgradering: distributions konfiguration, inklusive klient pilotering och undantags användning (utökad klient för interoperabilitet)

- Konfiguration av cachestorlek för klient

- Hämtnings fel för klient distribution

- ***[Uppdaterat]*** Statistik för klient hälsa och topp ärende sammanfattning efter klient version

- Åtgärds status för klient meddelande åtgärd: hur många gånger varje körs, högsta antal mål klienter och genomsnittlig frekvens för lyckade

- Antal klientinstallationer från varje typ av källplats  

- Antal klientinstallationsfel  

- Antal enheter som virtualiserats av Hyper-V eller Azure  

- Antal Software Center-åtgärder   

- Antal UEFI-aktiverade enheter

- Distributions metoder som används för klienten och antalet klienter per distributions metod

- Lista/antal aktiverade klientagenter  

- OS-ålder i månader

- Antal maskin varu lager klasser, program inventerings regler och fil insamlings regler

- Statistik för hälsoattestering av enhet: de vanligaste fel koderna, antalet lokala servrar och antalet enheter i olika tillstånd

- Antal enheter som standard webbläsare  

- ***[Ny]*** Antal certifikat för serverautentisering som skapats av Configuration Manager  

- ***[Ny]*** Antal Microsoft-Surface-enheter efter modell  


### <a name="cloud-services"></a>Cloud Services  

- Azure Active Directory identifierings statistik

- Konfiguration och användnings statistik för Cloud Management Gateway: antal regioner och miljöer samt statistik över autentisering/auktorisering

- Antal Azure Active Directory program och tjänster som är anslutna till Configuration Manager

- Antal samlingar som har synkroniserats till Azure Log Analytics

- Antal Upgrade Analytics kopplingar

- Om Azure Log Analytics Cloud Connector har Aktiver ATS  

- ***[Ny]*** Antal mottagar distributions platser med en moln distributions plats som käll plats  


### <a name="co-management"></a>Samhantering  
- Sammanställd användnings statistik för samhantering: antalet registrerade klienter, klienter som tar emot principer, arbets belastnings tillstånd, samlings storlekar för pilot/undantag och registrerings fel  

- Registrerings schema och historisk statistik  

- Antal klienter som är kvalificerade för samhantering  

- Associerad Microsoft Intune-klient


### <a name="collections"></a>Samlingar  

- Användning av samlings-ID (börjar inte med ID: n)

- Statistik för samlings utvärdering: fråge tid, tilldelad till antal otilldelade, antal efter typ, ID-förnyelse och regel användning

- Samlingar utan distribution


### <a name="compliance-settings"></a>Kompatibilitetsinställningar  

- Grundläggande konfigurations bas linje information: antal, antal distributioner och antal referenser

- Fel statistik för policy för efterlevnad

- Antal konfigurationsobjekt efter typ  

- Antal distributioner som refererar till inbyggda inställningar, inklusive åtgärds inställning  

- Antal regler och distributioner som skapats för anpassade inställningar, inklusive åtgärds inställning  

- Antal distribuerade Simple Certificate Enrollment Protocol (SCEP), VPN, Wi-Fi, Certificate (. pfx) och mallar för efterlevnadsprinciper

- Antal SCEP-certifikat, VPN, Wi-Fi, certifikat (. pfx) och distributioner av efterlevnadsprinciper efter plattform

- Windows Hello för företag-princip (skapad, distribuerad)  

- ***[Ny]*** Antal distribuerade äldre webb läsar principer i Microsoft Edge  


### <a name="content"></a>Innehåll  

- Statistik över gränserna grupp: hur många snabba, antalet långsamma, antal per grupp och återställnings relationer

- Information om gräns grupper: antal gränser och plats system som har tilldelats varje gräns grupp  

- Relationer mellan gränser och återställnings konfiguration

- Statistik för nedladdning av klient innehåll

- Antal gränser efter typ  

- Antal klienter för peer-cache, användnings statistik och delvis nedladdnings statistik

- Konfigurations information för distributions hanteraren: trådar, fördröjning av återförsök, antal återförsök och inställningar för mottagar distributions plats  

- Konfigurations information för distributions plats: användning av Branch cache och distributions plats övervakning

- Information om distributions plats grupper: antal paket och distributions platser som har tilldelats varje distributions plats grupp  

- ***[Ny]*** Innehålls biblioteks typ, antingen lokal eller fjärran sluten  


### <a name="endpoint-protection"></a>Slutpunktsskydd  

- Principer för Microsoft Defender Avancerat skydd (ATP) (tidigare Windows Defender ATP): antal principer och om principer har distribuerats.

- Antal aviseringar som kon figurer ATS för Endpoint Protection funktion  

- Antal samlingar som har marker ATS för att visas i Endpoint Protection-instrumentpanelen  

- Antal Windows Defender sårbarhet Guard-principer, distributioner och mål klienter

- Endpoint Protection distributions fel, antal fel koder för distribution av Endpoint Protection princip  

- Användning av Endpoint Protection principer för program mot skadlig kod och Windows-brandväggen (antal unika principer som tilldelats gruppen)<br /><br /> Dessa data innehåller inte information om inställningarna som ingår i principen.  


### <a name="migration"></a>Migrering  

- Antal migrerade objekt (användning av migreringsguiden)


### <a name="mobile-device-management-mdm"></a>Hantering av mobilenheter (MDM)  

- Antal utfärdade åtgärder för mobila enheter: lås, fäst rest, rensa, dra tillbaka och synkronisera nu-kommandon

- Antal principer för mobila enheter  

- Antal mobila enheter som hanteras av Configuration Manager och Microsoft Intune och hur de registrerades (bulk, User-based)  

- Antal användare som har flera registrerade mobila enheter  

- Schema för avsökning av mobila enheter och statistik för mobila enheters inchecknings tid  


### <a name="microsoft-intune-troubleshooting"></a>Microsoft Intune fel sökning  

- Antal och storlek på enhets åtgärder (rensa, dra tillbaka, låsa), användnings data och data meddelanden som replikeras till Microsoft Intune

- Antal och storlek på tillstånd, status, inventering, RDR, DDR, UDX, klient organisationens tillstånd, POL, LOG, cert, CRP, resync, CFD, RDO, BEX, ISM och Compliance-meddelanden som hämtas från Microsoft Intune

- Statistik över fullständig och delta-synkronisering av användare för Microsoft Intune


### <a name="on-premises-mobile-device-management-mdm"></a>Lokal hantering av mobila enheter (MDM):  

- Antal massregistrerade Windows 10-paket och Windows 10-profiler  

- Statistik över distributionsresultat (lyckade/misslyckade) för lokala distributioner av MDM-program  


### <a name="os-deployment"></a>Distribution av operativsystem  

- Antal startavbildningar, drivrutiner, drivrutinspaket, multicast-aktiverade distributionsplatser, PXE-aktiverade distributionsplatser och aktivitetssekvenser  

- Antal start avbildningar per Configuration Manager klient version

- Antal start avbildningar från Windows PE-version

- Antal uppgraderings principer för utgåva

- Antal maskinvaru-ID: n som undantas från PXE

- Antal operativ system distributioner per operativ system version

- Antal operativ system uppgraderingar över tid

- Antal aktivitetssekvensdistributioner som använder alternativ för att hämta innehåll i förväg

- Antal användnings steg i en aktivitetssekvens

- Version av Windows ADK installerad  

- ***[Ny]*** Antal avbildnings underhålls uppgifter  


### <a name="site-updates"></a>Plats uppdateringar  

- Versioner av installerade Configuration Manager snabb korrigeringar


### <a name="software-updates"></a>Programuppdateringar  

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

- Antal Windows Update för affärs principer som skapats och distribuerats

- Sammanställd statistik för Windows Update för företags konfiguration

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

- ***[Ny]*** Antal prenumerationer och användning av program uppdaterings kataloger från tredje part  

- ***[Ny]*** Antal program uppdateringar som har distribuerats med och utan innehåll  


### <a name="sqlperformance-data"></a>SQL/Performance-data  

- Konfiguration och varaktighet för sammanfattning av webbplats

- Antal största databastabeller  

- Identifierings drifts statistik (antal objekt som hittades)

- Identifierings typer, aktiverade och schema (fullständig, stegvis)

- SQL AlwaysOn-replikerad information, användning och hälso status

- Prestanda problem i SQL Change tracking, kvarhållningsperiod och status för automatisk rensning

- Kvarhållningsperioden för ändrings spårning i SQL

- Prestanda statistik för tillstånd och status meddelanden, inklusive de vanligaste och mest dyra meddelande typerna


### <a name="miscellaneous"></a>Övriga farliga ämnen  

- Konfiguration av informations lager service punkt, inklusive synkroniseringsschema och genomsnittlig tid

- Antal skript och körnings statistik

- Antal platser med Wake On LAN (WOL)

- Rapportering av användnings-och prestanda statistik

- Användnings statistik för stegvis distribution  

- ***[Ny]*** Användnings statistik för CMPivot  

- ***[Ny]*** Antal insikter för hanterings objekt och förlopp  

- ***[Ny]*** Antal krascher för unika icke-Configuration Manager processer på plats servern och Watson-signatur-ID, om tillgängligt



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Nivå 3 – Fullständig

För Configuration Manager version 1806 omfattar den här nivån följande data:

- Schemainformation för utvärdering av regler för automatisk distribution

- Översikt över ATP-hälsa

- Samlingsutvärdering och uppdateringsstatistik

- Statistik om efterlevnad och fel i policyn för efterlevnad

- Kompatibilitetsinställningar: konfigurations information för SCEP, VPN, Wi-Fi och efterlevnadsprincip

- DCM-konfigurations paket för Configuration Manager användning

- Detaljerade installations fel för klient distribution

- Endpoint Protection hälso översikt: inklusive antal skyddade, på risk-, okända klienter och klienter som inte stöds

- Konfiguration av Endpoint Protection-principer

- Lista över processer som kon figurer ATS med installations beteende för program

- Minsta/högsta/genomsnittligt antal timmar sedan den senaste sökningen efter programvaruuppdateringar

- Minsta/högsta/genomsnittligt antal inaktiva klienter i samlingar med distributioner av programvaruuppdateringar

- Minsta/högsta/genomsnittligt antal programvaruuppdateringar per paket

- Distributions statistik för MSI produkt kod 

- Övergripande kompatibilitet för distributioner av programuppdateringar

- Antal grupper som har upphört att gälla program uppdateringar

- Felkoder och antal för distributioner av programvaruuppdateringar

- Information om distribution av program uppdatering: procent andel distributioner som är riktade till klienten jämfört med UTC-tid, krävs jämfört med valfria kontra tyst och omstart av under tryckning

- Program uppdaterings produkter som har synkroniserats med program uppdaterings platsen

- Procentuellt antal lyckade sökningar efter programvaruuppdateringar

- De främsta 50 processorerna i miljön

- Typ av Exchange Active Sync (EAS) villkorliga åtkomst principer (block eller karantän) för enheter som Microsoft Intune hanterar

- Microsoft Store information om företags program: icke-aggregerad lista över synkroniserade program, inklusive AppID, online-tillstånd eller offline-tillstånd, och totalt antal köpta licenser
