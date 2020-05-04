---
title: Hanteringsinsikter
titleSuffix: Configuration Manager
description: Lär dig mer om hanterings funktionerna i Configuration Manager-konsolen.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e9aae1da48deabd0cc339cd25055827caf07354b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713739"
---
# <a name="management-insights-in-configuration-manager"></a>Hanterings insikter i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Hanterings insikter i Configuration Manager ger information om miljöns aktuella tillstånd. Informationen baseras på analys av data från plats databasen. Insights hjälper dig att bättre förstå din miljö och vidta åtgärder baserat på insikter. <!--1353967-->

## <a name="review-management-insights"></a>Granska Management Insights

Om du vill visa reglerna måste ditt konto ha behörigheten **läsa** för objektet **plats** .

1. Öppna Configuration Manager-konsolen.  

2. Gå till arbets ytan **Administration** , expandera **Management Insights**och välj **alla insikter**.  

    > [!Note]  
    > När du väljer noden **hanterings** information visas [instrument panelen för hanterings insikter](#bkmk_insights).  

3. Öppna det namn på hanterings gruppen som du vill granska. Välj **Visa insikter** i menyfliksområdet.  

Följande fyra flikar är tillgängliga för granskning:

- **Alla regler**: visar en fullständig lista över regler för insikts gruppen för hantering som valts.  

- **Slutför**: visar regler där ingen åtgärd krävs.  

- **Pågår**: visar regler där vissa, men inte alla, krav har slutförts.  

- **Åtgärd krävs**: regler som kräver vidtagna åtgärder visas. Välj **Mer information** för att hämta vissa objekt där åtgärd krävs.  

I fönstret **förutsättningar** visas de nödvändiga objekt som krävs för att köra regeln.

### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>Alla regler och krav för Cloud Services-gruppen

![Hanterings insikter – alla regler och krav för Cloud Services-gruppen](./media/Management-insights-all-cloud-rules.png)

Välj en regel och välj sedan **Mer information** för att se regel informationen.

## <a name="operations"></a>Åtgärder

Reglerna för insikter för hantering utvärderar om deras användbarhet på ett vecko schema. Om du vill utvärdera om en regel på begäran högerklickar du på regeln och väljer **utvärdera igen**.

Logg filen för insikts regler för hantering är **SMS_DataEngine. log** på plats servern.

<!--1357930-->
Med vissa regler kan du vidta åtgärder. Välj en regel, Välj **Mer information**och välj sedan **vidta åtgärden**om den är tillgänglig.

Beroende på regeln har den här åtgärden något av följande beteenden:  

- Navigera automatiskt i-konsolen till noden där du kan vidta ytterligare åtgärder. Om till exempel insikter om hantering rekommenderar att du ändrar en klient inställning, navigerar du till noden klient inställningar. Vidta ytterligare åtgärder genom att ändra standard eller ett anpassat klient inställnings objekt.  

- Navigera till en filtrerad vy baserat på en fråga. Om du till exempel vidtar en åtgärd i den tomma samlings regeln visas bara dessa samlingar i listan över samlingar. Vidta sedan ytterligare åtgärder, till exempel ta bort en samling eller ändra dess medlemskaps regler.  

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a>Instrument panel för hanterings insikter

<!--1357979-->

Noden för **hanterings insikter** innehåller en grafisk instrument panel. Den här instrument panelen visar en översikt över regel tillstånden, vilket gör det enklare för dig att visa din förloppet.

Använd följande filter överst i instrument panelen för att förfina vyn:

- Visa slutförd
- Valfri
- Rekommenderas
- Kritisk

Instrument panelen innehåller följande paneler:  

- **Management Insights-index**: spårar övergripande förloppet för hanterings insikter-regler. Indexet är ett viktat medelvärde. Kritiska regler är värda de flesta. Detta index ger minst en vikt till valfria regler.  

- **Hanterings insikter grupper**: visar procent av regler i varje grupp som följer filter. Välj en grupp för att öka detalj nivån för de aktuella reglerna i den här gruppen.  

- **Prioritet för hanterings Insights**: visar procent av regler efter prioritet och som följer filter.  

- **Alla insikter**: en tabell med insikter inklusive prioritet och tillstånd. Använd fältet **filter** överst i tabellen för att matcha strängar i någon av de tillgängliga kolumnerna. Instrument panelen sorterar tabellen i följande ordning:

  - Status: åtgärd krävs, slutförd, okänd  
  - Prioritet: kritisk, rekommenderas, valfritt  
  - Senast ändrad: äldre datum överst  

![Skärm bild av instrument panelen för hanterings insikter](media/1357979-management-insights-dashboard.png)

## <a name="groups-and-rules"></a>Grupper och regler

Reglerna är indelade i följande grupper för hantering av insikter:

- [Program](#applications)
- [Moln tjänster](#cloud-services)
- [Samlingar](#collections)
- [Configuration Manager utvärdering](#configuration-manager-assessment)
- [Proaktivt underhåll](#proactive-maintenance)
- [Säkerhet](#security)
- [Förenklad hantering](#simplified-management)
- [Software Center](#software-center)
- [Windows 10](#windows-10)

### <a name="applications"></a>Program

Insikter för din program hantering.

- **Program utan distributioner**: visar en lista över de program i miljön som inte har aktiva distributioner. Med den här regeln kan du söka efter och ta bort program som inte används för att förenkla listan över program som visas i-konsolen. Mer information finns i [distribuera program](../../../apps/deploy-use/deploy-applications.md).  

### <a name="cloud-services"></a>Molntjänster

Hjälper dig att integrera med många moln tjänster, vilket möjliggör modern hantering av dina enheter.

- **Utvärdera samhanterings beredskap**: hjälper dig att förstå vilka steg som behövs för att aktivera samhantering. Den här regeln har krav. Mer information finns i [Översikt över samhantering](../../../comanage/overview.md).  

- **Enheter som inte har överförts till Azure AD**: från och med version 2002, visar den här regeln enheter som inte har laddats upp till Azure AD eftersom platsen inte är korrekt KONFIGURERAD för https.<!--6268489--> Konfigurera [utökad http](../../plan-design/hierarchy/enhanced-http.md)eller aktivera minst en hanterings plats för https. Om du redan har konfigurerat platsen för HTTPS-kommunikation visas inte den här regeln.

- **Konfigurera Azure-tjänster för användning med Configuration Manager**: den här regeln hjälper dig att publicera Configuration Manager till Azure AD, vilket gör att klienter kan autentiseras med platsen med hjälp av Azure AD. Mer information finns i [Konfigurera Azure-tjänster](../deploy/configure/azure-services-wizard.md).  

- **Göra det möjligt för enheter att hybrid Azure Active Directory anslutna**: Azure AD-anslutna enheter gör att användarna kan logga in med sina domänautentiseringsuppgifter samtidigt som de säkerställer att enheterna uppfyller organisationens standarder för säkerhet och efterlevnad. Mer information finns i [design överväganden för Azure AD hybrid Identity](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview).  

- **Platser som inte har rätt https-konfiguration**: från och med version 2002, visar den här regeln platser i hierarkin som inte är korrekt konfigurerade för https. Den här konfigurationen förhindrar att platsen [synkroniserar samlings medlemskaps resultat till Azure Active Directory (Azure AD)-grupper](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync). Det kan medföra att Azure AD Sync inte överför alla enheter. Hantering av dessa klienter kanske inte fungerar korrekt.<!--6268489--> Konfigurera [utökad http](../../plan-design/hierarchy/enhanced-http.md)eller aktivera minst en hanterings plats för https. Om du redan har konfigurerat platsen för HTTPS-kommunikation visas inte den här regeln.

- **Uppdatera klienter till den senaste Windows 10-versionen**: Windows 10, version 1709 eller senare förbättrar och moderniserar dator upplevelsen för dina användare. Mer information finns i [viktiga artiklar om att anta Windows som en tjänst](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).  

### <a name="collections"></a>Samlingar

Insikter som fören klar hanteringen genom att rensa och konfigurera om samlingar.

- **Tomma samlingar**: visar samlingar i din miljö som inte har några medlemmar. Mer information finns i [hantera samlingar](../../clients/manage/collections/manage-collections.md).  

Från och med version 1902 finns det nya regler med rekommendationer för att hantera samlingar.<!--3555752--> Använd dessa insikter för att förenkla hanteringen och förbättra prestandan:

- **Samlingar utan Frågeregler och inga direkta medlemmar**: för att förenkla listan över samlingar i hierarkin tar du bort dessa samlingar.  

- **Samlingar med samma start tid för ny utvärdering**: dessa samlingar har samma omprövnings tid som andra samlingar. Ändra tiden för förnyad utvärdering så att de inte står i konflikt.  

- **Samlingar med kötid över två sekunder**: granska Frågeregler för den här samlingen. Överväg att ändra eller ta bort samlingen.

- Följande regler innehåller konfigurationer som kan orsaka onödig belastning på platsen. Granska samlingarna, ta bort dem eller inaktivera regel utvärderingen:  

  - **Samlingar utan Frågeregler och stegvisa uppdateringar är aktiverade**  

  - **Samlingar utan Frågeregler och har Aktiver ATS för schemalagd eller stegvis utvärdering**  

  - **Samlingar utan Frågeregler och Schemalägg fullständig utvärdering har valts**  

### <a name="configuration-manager-assessment"></a>Configuration Manager utvärdering

<!--3607758-->

Från och med version 2002 är den här gruppen av Microsoft Premier Field Engineering. De här reglerna är ett exempel på de många fler kontroller som Microsoft Premier tillhandahåller i [hubben tjänster](https://docs.microsoft.com/services-hub/health/getting_started_with_on_demand_assessments).

- **Active Directory säkerhets grupp identifiering har kon figurer ATS för att köras för ofta**: du behöver vanligt vis inte konfigurera Active Directory identifiering av säkerhets grupper så att den inträffar oftare än var tredje timme. En frekvent konfiguration kan ha en negativ inverkan på Active Directory, nätverket och Configuration Manager. Aktivera stegvis synkronisering i stället för att använda ett fullständigt synkroniseringsschema. Mer information finns i [Active Directory Group Discovery](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).

- **Active Directory system identifiering har kon figurer ATS för att köras för ofta**: du behöver normalt inte konfigurera Active Directory system identifiering så att det inträffar oftare än var tredje timme. En frekvent konfiguration kan ha en negativ inverkan på Active Directory, nätverket och Configuration Manager. Aktivera stegvis synkronisering i stället för att använda ett fullständigt synkroniseringsschema. Mer information finns i [Active Directory system identifiering](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).

- **Active Directory användar identifiering har kon figurer ATS för att köras för ofta**: du behöver vanligt vis inte konfigurera Active Directory identifiering av användare som inträffar oftare än var tredje timme. En frekvent konfiguration kan ha en negativ inverkan på Active Directory, nätverket och Configuration Manager. Aktivera stegvis synkronisering i stället för att använda ett fullständigt synkroniseringsschema. Mer information finns i [Active Directory User Discovery](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

- **Samlingar begränsade till alla system eller alla användare**: granska alla samlingar som använder samlingarna **alla system** eller **alla användare** som den begränsande samlingen. Configuration Manager uppdaterar medlemskapet för de här standard samlingarna med data från Active Directory identifierings metoder. Dessa data kanske inte är giltiga för Configuration Manager klienter.

- **Pulsslags identifiering har inaktiverats**: pulsslags identifiering kräver att du installerar Configuration Manager-klienten på enheter. Det är den enda identifierings metod som klienter startar. Alla andra metoder sker på plats servrar. Pulsslags identifiering är nödvändigt för att se till att klient aktivitets status är aktuell. Det säkerställer att platsen inte oavsiktligt föråldrar resurs posterna från plats databasen. Mer information finns i [pulsslags identifiering](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).

- Tids krävande **samlings frågor har Aktiver ATS för stegvisa uppdateringar**: samlingar med en senaste stegvis uppdaterings tid på över 30 sekunder använder plats Server och databas resurser, vilket kan påverka övergripande Configuration Manager prestanda. Mer information finns i [metod tips för samlingar](../../clients/manage/collections/best-practices-for-collections.md).

- **Minska antalet program och paket på distributions platser**: Microsoft har officiellt stöd för en kombinerad summa på upp till 10 000 paket och program på en distributions plats. Att överskrida den här summan kan leda till drifts problem. Mer information finns i [storleks-och skalnings nummer – distributions plats](../../plan-design/configs/size-and-scale-numbers.md#distribution-point).

- **Installations problem för sekundär plats**: installations statusen för vissa sekundära platser **väntar** eller **misslyckades**. Dessa tillstånd innebär att du startade installationen men att den inte slutfördes korrekt. Klienterna kan inte kommunicera med den primära platsen förrän installationen av den sekundära platsen har slutförts. Kontrol lera arbets ytan **övervakning** och försök att installera igen. Mer information finns i [gör om installationen av en misslyckad uppdatering](install-in-console-updates.md#bkmk_retry).

- **Uppdatera alla platser till samma version**: Använd samma version av Configuration Manager i en hierarki. Den här konfigurationen ser till att alla platser ger samma funktioner. Platser med olika versioner i samma hierarki introducerar samverkans scenarier. Senare versioner av Configuration Manager innehåller nya funktioner och löser kända problem. Mer information finns i [samverkan mellan olika versioner](../../plan-design/hierarchy/interoperability-between-different-versions.md).

Mer information om dessa regler finns i [reparations steg för Configuration Manager Management Insights](https://docs.microsoft.com/services-hub/health/remediation-steps-configmgr).

> [!TIP]
> Om du redan är kund av Microsoft Unified eller Microsoft Premium loggar du in på [tjänstens hubb](https://serviceshub.microsoft.com/assessments/) för ytterligare utvärdering på begäran.
>
> För ytterligare information om Microsoft-tjänster, se [support lösningar](https://www.microsoft.com/enterprise/services/support).

### <a name="proactive-maintenance"></a>Proaktivt underhåll

<!--1352184-->
Reglerna i den här gruppen fokuserar på potentiella konfigurations problem för att undvika att behålla Configuration Manager objekt.

- **Gränser grupper utan tilldelade plats system**: utan tilldelade plats system kan gränser grupper bara användas för platstilldelning. Mer information finns i [Konfigurera gränser grupper](../deploy/configure/boundary-groups.md).  

- **Gränser grupper utan medlemmar**: gränser grupper gäller inte för platstilldelning eller innehålls sökning om de inte har några medlemmar. Mer information finns i [Konfigurera gränser grupper](../deploy/configure/boundary-groups.md).  

- **Distributions platser som inte betjänar innehåll till klienter**: distributions platser som inte har betjänat innehåll till klienter under de senaste 30 dagarna. Dessa data baseras på rapporter från klienter från sina nedladdnings historik. Mer information finns i [Installera och konfigurera distributions platser](../deploy/configure/install-and-configure-distribution-points.md).  

- **Aktivera WSUS-rensning**: verifierar att du har aktiverat alternativet att köra WSUS-rensning på egenskaperna för program uppdaterings plats komponenten. Det här alternativet hjälper till att förbättra WSUS-prestanda. Mer information finns i [underhåll av program uppdatering](../../../sum/deploy-use/software-updates-maintenance.md).  

- **Oanvända start avbildningar**: Start avbildningar som inte refereras till PXE-start eller aktivitetssekvens används. Mer information finns i [Hantera start avbildningar](../../../osd/get-started/manage-boot-images.md).  

- **Oanvända konfigurations objekt**: konfigurations objekt som inte ingår i en konfigurations bas linje och som är äldre än 30 dagar. Mer information finns i [skapa konfigurations bas linjer](../../../compliance/deploy-use/create-configuration-baselines.md).  

- **Uppgradera peer-cache-källor till den senaste versionen av Configuration Manager-klienten**: identifiera klienter som fungerar som en peer-cache-källa men som inte har uppgraderats från en klient version före 1806. Det går inte att använda pre-1806-klienter som peer-cache-källa för klienter som kör version 1806 eller senare. Välj **vidta åtgärd** för att öppna en enhets vy som visar listan över klienter.<!--1358008-->  

### <a name="security"></a>Säkerhet

Insikter för att förbättra säkerheten för infrastrukturen och enheterna.

- **NTLM-återställning är aktiverat**:<!--4572953--> Från och med version 1906, identifierar den här regeln om du har aktiverat återställnings metoden för den mindre säkra NTLM-autentiseringen för platsen. När klientens push-metod används för att installera Configuration Manager-klienten, kan platsen kräva ömsesidig Kerberos-autentisering. Den här förbättringen hjälper till att skydda kommunikationen mellan servern och klienten. Mer information finns i [så här installerar du klienter med klient-push](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

- **Klient versioner för program mot skadlig kod som inte**stöds: fler än 10% av klienterna kör versioner av System Center Endpoint Protection som inte stöds. Mer information finns i [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).  

### <a name="simplified-management"></a>Förenklad hantering

Insikter som hjälper dig att förenkla den dagliga hanteringen av din miljö.

- **Anslut platsen till Microsoft Cloud för Configuration Manager uppdateringar**: den här regeln kontrollerar att din Configuration Manager tjänst anslutnings punkt har anslutits till Microsoft-molnet under de senaste sju dagarna. Den här anslutningen är att ladda ned innehåll för regelbundna uppdateringar. Granska DMPDownloader. log och hman. log. Mer information finns i [krav för Internet åtkomst](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates).

- **Klient versioner som inte är CB**: visar en lista över alla klienter vars versioner inte är en aktuell gren (CB) build. Mer information finns i [Uppgradera klienter](../../clients/manage/upgrade/upgrade-clients.md).  

- **Uppdatera klienter till en Windows 10-version som stöds**: från och med version 1902 rapporteras den här regeln på klienter som kör en version av Windows 10 som inte längre stöds. Den innehåller också klienter med en Windows 10-version som är nära tjänstens slut (tre månader).<!--3897268-->  

### <a name="software-center"></a>Software Center

Insikter för att hantera Software Center.

- **Dirigera användare till Software Center i stället för programkatalog**: kontrol lera om användarna har installerat eller begärt program från program katalogen under de senaste 14 dagarna. De viktigaste funktionerna i program katalogen ingår nu i Software Center. Support upphör för program katalog rollerna med version 1910. Mer information finns i [föråldrade funktioner](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).  

- **Använd den nya versionen av Software Center**: den tidigare versionen av Software Center stöds inte längre. Konfigurera klienterna så att de använder det nya Software Center genom att aktivera klient inställningen **Använd nya Software Center** i **dator agent** gruppen. Mer information finns i [om klient inställningar](../../clients/deploy/about-client-settings.md#use-new-software-center).  

### <a name="software-updates"></a>Programuppdateringar

- **Klient inställningarna har inte kon figurer ATS för att tillåta klienter att ladda ned delta innehåll**: vissa program uppdateringar som synkroniseras i din miljö innehåller delta innehåll. Aktivera klient inställningen och **Tillåt att klienter laddar ned delta innehåll när det är tillgängligt**. Om du inte aktiverar den här inställningen och distribuerar dessa uppdateringar, kommer klienten att ladda ned mer innehåll än vad som krävs. Mer information finns i [klient inställningar-program uppdateringar](../../clients/deploy/about-client-settings.md#software-updates).

- **Aktivera program uppdateringens produkt kategori "Windows 10, version 1903 och senare"**: det finns en ny produkt kategori för program uppdateringar för Windows 10, version 1903 och senare. Om du synkroniserar Windows 10-uppdateringar och har Windows 10, version 1903 eller senare klienter väljer du produkt kategorin **Windows 10, version 1903 och senare** i egenskaperna för komponenten för program uppdaterings plats. Mer information finns i[Konfigurera klassificeringar och produkter som ska synkroniseras](../../../sum/get-started/configure-classifications-and-products.md).

### <a name="windows-10"></a>Windows 10

Insikter om distribution och underhåll av Windows 10. Windows 10 Management Insight-gruppen är bara tillgänglig när mer än hälften av klienter kör Windows 7, Windows 8 eller Windows 8,1.

- **Konfigurera Windows diagnostik-data och kommersiell ID-nyckel**: om du vill använda data från Desktop Analytics konfigurerar du enheter med en kommersiell ID-nyckel och aktiverar insamling av diagnostikdata. Ställ in Windows 10-enheter på **utökad (begränsad)** nivå eller högre. Mer information finns i [Aktivera data delning för Skriv bords analys](../../../desktop-analytics/enable-data-sharing.md).

#### <a name="windows-10-management-insights-rules"></a>Windows 10 Management Insights-regler

![Hanterings insikter – regler för Windows 10](./media/Windows-10-insights-group.png)
