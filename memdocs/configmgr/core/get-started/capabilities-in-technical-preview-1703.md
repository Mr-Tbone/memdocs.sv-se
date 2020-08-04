---
title: Funktioner i Technical Preview 1703
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1703.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 98a82d118442a7ca37ff7b2df62bf4702c15ba2c
ms.sourcegitcommit: 7e34b561d43aa086fc07ab4edf2230d09c04f05b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87526023"
---
# <a name="capabilities-in-technical-preview-1703-for-configuration-manager"></a>Funktioner i Technical Preview 1703 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1703. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.    


**Följande är nya funktioner som du kan prova med den här versionen.**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Distribuera iOS-appar som köpts i volym till enhets samlingar

Nu kan du distribuera licensierade appar till enheter samt användare. Beroende på apparnas förmåga att stödja enhets licensiering kommer en lämplig licens att krävas när du distribuerar den, enligt följande:

| Configuration Manager version | App har stöd för enhets licensiering? | Distributions samlings typ | Ansökan om licens |
| ----------------------------- | ------------------------------ | -------------------------- | --------------- |
|Tidigare än 1702|Yes|Användare|Användar licens|
|Tidigare än 1702|No|Användare|Användar licens|
|Tidigare än 1702|Yes|Enhet|Användar licens|
|Tidigare än 1702|No|Enhet|Användar licens|
|1702 och senare|Yes|Användare|Användar licens|
|1702 och senare|No|Användare|Användar licens|
|1702 och senare|Yes|Enhet|Enhets licens|
|1702 och senare|No|Enhet|Användar licens|


## <a name="direct-links-to-applications-in-software-center"></a>Direkt länkar till program i Software Center

Nu kan du ge slutanvändarna en direkt länk till ett program i Software Center. Det innebär att de inte längre måste öppna Software Center och söka efter ett program innan de kan installera det. Detta är endast tillgängligt för Configuration Manager-program, inte paket och program eller aktivitetssekvenser.

### <a name="try-it-out"></a>Prova                 

Använd följande URL-format för att öppna Software Center för ett visst program:

**Softwarecenter: SoftwareId =_program-ID_**

### <a name="how-to-get-the-application-identifier-of-an-application"></a>Så här hämtar du program-ID för ett program.

1. I Configuration Manage-konsolen klickar du på **Programbibliotek**.
2. I arbetsytan Programvarubibliotek visar du **Programhantering**och klickar sedan på **Program**.
3. Högerklicka på en av kolumn rubrikerna i vyn **program** och välj sedan **unikt ID för CI**i listan. Du ser att det unika ID: t för varje program nu visas i listan.
4. Anteckna **unikt ID för CI** för det program som du vill lägga till en länk till, till exempel: **ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38** -405c-ad37-c753400b895f/2
5. Ta sedan bort all text som följer programmets GUID, i det här fallet **/2**. Detta lämnar program-ID: n.
6. Slutligen, för att slutföra konstruktion av länken, före den med **softwarecenter: SoftwareID =**. I exemplet ovan kommer den sista länken att läsa: **softwarecenter: SoftwareId = ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38**-405c-ad37-c753400b895f.

Genom att använda den här länken kan slutanvändare öppna Software Center direkt till det program som du har angett.


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>PFX-certifikat för Configuration Manager Windows-klientdatorer

Nu kan du distribuera PFX-certifikat profiler som du har importerat till Configuration Manager klient datorer som kör Windows 10.

### <a name="try-it-out"></a>Prova

Följ anvisningarna i [så här skapar du profiler för PFX-certifikat](../../mdm/deploy-use/create-pfx-certificate-profiles.md) för att importera en PFX-profil, distribuera profilen och kontrol lera sedan om certifikatet har installerats för mål användaren.



## <a name="configure-azure-services-wizard"></a>Guiden Konfigurera Azure-tjänster
Technical Preview 1703 presenterar guiden **Konfigurera Azure-tjänster** . Den här guiden innehåller en gemensam konfigurations upplevelse som ersätter de enskilda arbets flödena och konfigurerar de moln tjänster som du använder med Configuration Manager. Detta görs genom att använda en **Azure-webbapp** för att tillhandahålla prenumerations-och konfigurations information som du annars anger varje gången du konfigurerar en ny Configuration Manager komponent eller tjänst med Azure.

Med teknisk för hands version 1703 konfigureras endast Windows Store för företag (WSfB) med hjälp av den här guiden.  Andra moln tjänster konfigureras med hjälp av sina separata arbets flöden.

- Använd informationen i det här förhands gransknings avsnittet för att ersätta de konfigurations steg som finns i avsnittet [Konfigurera Windows Store för företag](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_setup) i avsnittet Current Branch [Hantera appar från Windows Store för företag med Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

- Mer information om Web Apps finns [i autentisering och auktorisering i Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview)och [Web Apps översikt](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

### <a name="prerequisites-and-planning"></a>Krav och planering
När du skapar en anslutning mellan Configuration Manager och Windows Store för företag, måste du ange en mapp där app-innehåll som synkroniseras från Store kommer att behållas. Se till att den här mappen är säker och att dess innehåll kan distribueras till enheter genom att kontrol lera att följande behörigheter är på plats:
- Datorn där du installerar tjänst anslutnings punktens plats system roll (platsen på den översta nivån i hierarkin) måste ha läs-och Skriv behörighet till den mapp som du angav när du använde **dator $** -kontot.  

- Appens författare måste ha Läs behörighet till den mapp som du har angett.  

- **Dator $** -kontot för varje dator som är värd för en instans av SMS-providern måste kunna använda den mapp som du har angett.

I Azure Active Directory registrerar du Configuration Manager som ett webb program eller hanterings verktyg för webb-API. Detta skapar det klient-ID som du kommer att behöva senare.

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>Använd guiden för att konfigurera moln tjänsten WSfB

1. I-konsolen går du till **administrations**  >  **Översikt**  >  **Cloud Services hantering**  >  **Azure**  >  **Azure-tjänster**och väljer sedan **Konfigurera Azure-tjänster** för att starta **guiden Azure-tjänster**.

2. På sidan **Azure-tjänster** väljer du den tjänst som du vill konfigurera och klickar sedan på **Nästa**. Med den här för hands versionen kan endast WSfB konfigureras.

3. På sidan **Allmänt** anger du ett eget namn för **Azure-tjänstens namn** och en valfri beskrivning och klickar sedan på **Nästa**.

4. På sidan **app** anger du din Azure-miljö och klickar sedan på **Bläddra** för att öppna fönstret Server App.

5. I fönstret **Server App** väljer du den server-app som du vill använda och klickar sedan på **OK**.
   Server appar är Azure-webbappar som innehåller konfigurationerna för ditt Azure-konto, inklusive klient-ID, klient-ID och en hemlig nyckel för klienter. Om du inte har någon tillgänglig server-app använder du något av följande:
   - **Skapa**: om du vill skapa en ny server app klickar du på **skapa**. Ange ett eget namn för appen och klienten. När du sedan har loggat in på Azure skapar Configuration Manager webbappen i Azure åt dig, inklusive klient-ID och hemlig nyckel för användning med webbappen. Senare kan du visa dessa från Azure Portal.
   - **Importera**: Klicka på **Importera**om du vill använda en webbapp som redan finns i din Azure-prenumeration. Ange ett eget namn för appen och klienten och ange sedan klient-ID, klient-ID och den hemliga nyckeln för den Azure-webbapp som du vill Configuration Manager använda. När du har **verifierat** informationen klickar du på **OK** för att fortsätta.  </br></br>

6. Granska **informations** sidan och slutför eventuella ytterligare steg och konfigurationer enligt anvisningarna. De här konfigurationerna är nödvändiga för att använda tjänsten med Configuration Manager.
   Om du till exempel vill konfigurera WSfB:

   1. I Azure måste du registrera Configuration Manager som ett webb program eller webb-API och registrera klient-ID: t. Du kan också ange en klient nyckel som ska användas av hanterings verktyget (som är Configuration Manager).

   2.    I WSfB-konsolen måste du konfigurera Configuration Manager som Store Management-verktyg, aktivera stöd för licensierade appar offline och sedan köpa minst en app.   </br>

   Klicka på **Nästa** när du är redo att fortsätta.

7. På sidan **AppData** , fyller du i program katalogen och språk konfigurationerna för tjänsten och klickar sedan på **Nästa**.
8. När guiden har slutförts visar Configuration Manager-konsolen att du har konfigurerat **Windows Store för företag** som en **moln tjänst typ**.

Du kan nu använda resten av [Current Branch innehåll](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) för att hantera appar från WSfB för att synkronisera, skapa och distribuera och övervaka Windows Store för företag-appar.

### <a name="modify-a-cloud-service-configuration"></a>Ändra en moln tjänst konfiguration
Du kan visa och redigera egenskaperna för en moln tjänst för att ändra konfigurationen.

I-konsolen går du till **administrations**  >  **Översikt**  >  **Cloud Services hantering**  >  **Azure**  >  **Azure-tjänster**och väljer sedan **Konfigurera Azure-tjänster**, väljer en moln tjänst och väljer sedan **Egenskaper**.

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Konvertera från BIOS till UEFI under en uppgradering på plats
Windows 10 Creators Update introducerar ett enkelt konverterings verktyg som automatiserar processen för att partitionera om hård disken för UEFI-aktiverad maskin vara och integrera konverterings verktyget i Windows 7 till Windows 10 uppgraderings process på plats. När du kombinerar det här verktyget med aktivitetssekvensen för uppgradering av operativ system och OEM-verktyget som konverterar den inbyggda program varan från BIOS till UEFI, kan du konvertera datorerna från BIOS till UEFI under en uppgradering på plats till Windows 10 Creators Update. Mer information finns i avsnittet [om aktivitetssekvenser för att hantera BIOS till UEFI-konvertering](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

## <a name="collapsible-task-sequence-groups"></a>Komprimerbara aktivitetssekvenser
Den här versionen ger möjlighet att expandera och minimera grupper av aktivitetssekvenser. Du kan expandera eller komprimera enskilda grupper eller expandera eller komprimera alla grupper samtidigt.


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>Klient inställningar för att konfigurera Windows Analytics för Uppgraderingsberedskap
Från och med den här versionen kan du använda enhets klient inställningar för att förenkla konfigurationen av Windows-diagnostikdata som krävs för att använda Windows Analytics-lösningar som Uppgraderingsberedskap med Configuration Manager. Configuration Manager kan hämta data från Windows Analytics som kan ge värdefull insyn i miljöns aktuella tillstånd baserat på de Windows-diagnostikdata som rapporteras av klient datorerna. Windows-diagnostikdata rapporteras av klient datorer till Windows Diagnostic-tjänsten och sedan överförs relevanta data senare till Windows Analytics-lösningar som finns i en av organisationens OMS-arbetsytor. Uppgraderingsberedskap är en Windows Analytics-lösning som kan hjälpa dig att prioritera beslut om Windows-uppgraderingar för dina hanterade enheter.

### <a name="prerequisites"></a>Förutsättningar
- Du måste ha konfigurerat platsen så att den använder Uppgraderingsberedskap moln tjänsten.

### <a name="configure-windows-analytics-client-settings"></a>Konfigurera klient inställningar för Windows Analytics
Om du vill konfigurera Windows Analytics går du till **Administration**  >  **klient inställningar**i Configuration Manager-konsolen, dubbelklickar på **skapa anpassade enhets klient inställningar** och kontrollerar sedan **Windows Analytics**.  

Konfigurera sedan följande efter att du har navigerat till fliken **Windows Analytics** -inställningar:
- **Kommersiellt ID**  
Den kommersiella ID-nyckeln mappar information från enheter som du hanterar till OMS-arbetsytan som är värd för din organisations Windows Analytics-data. Om du redan har konfigurerat en kommersiell ID-nyckel för användning med Uppgraderingsberedskap använder du detta ID. Om du ännu inte har en kommersiell ID-nyckel genererar du din kommersiella ID-nyckel.

- Ange en **diagnostisk data nivå för Windows 10-enheter**

- Välj att **delta i affärs data insamling på Windows 7-, 8-och 8,1-enheter**   

- **Konfigurera data insamling för Internet Explorer** På enheter som kör Windows 8,1 eller tidigare kan data insamling i Internet Explorer tillåta Uppgraderingsberedskap att identifiera inkompatibiliteter för webb program som kan förhindra en smidig uppgradering till Windows 10. Data insamling i Internet Explorer kan aktive ras per Internet zon.
