---
title: Hanteringsinsikter
titleSuffix: Configuration Manager
description: Lär dig mer om hanterings funktionerna i Configuration Manager-konsolen.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: de3c75982e19e6183260a2a5f99f65b9c785d27f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700522"
---
# <a name="management-insights-in-configuration-manager"></a>Hanterings insikter i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Hanterings insikter i Configuration Manager ger information om miljöns aktuella tillstånd. Informationen baseras på analys av data från plats databasen. Insights hjälper dig att bättre förstå din miljö och vidta åtgärder baserat på insikter. <!--1353967-->

## <a name="review-management-insights"></a>Granska Management Insights

Ditt konto måste ha behörigheten **läsa** för objektet **plats** för att kunna visa insikter.

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **hanterings insikter**och väljer **alla insikter**.

    > [!NOTE]
    > När du väljer noden **hanterings** information visas [instrument panelen för hanterings insikter](#bkmk_insights).

1. Öppna det namn på hanterings gruppen som du vill granska.

1. I menyfliksområdet väljer du **Visa insikter**.

Följande fyra flikar är tillgängliga för granskning:

- **Alla regler**: ger den fullständiga listan med insikter för den valda gruppen.

- **Slutförd**: visar insikter där ingen åtgärd krävs.

- **Pågår**: visar insikter där vissa, men inte alla, nödvändiga komponenter har slutförts.

- **Åtgärd krävs**: den här fliken visar insikter som kräver att du vidtar åtgärder. Välj **Mer information** för att visa vissa objekt där åtgärd krävs.

I rutan **förutsättningar** visas alla obligatoriska objekt som behövs för att köra den valda insikten.

Följande skärm bild visar till exempel ett exempel på fliken **alla regler** för gruppen **Cloud Services** :

:::image type="content" source="media/management-insights-all-cloud-rules.png" alt-text="Hanterings information: alla regler och förutsättningar för Cloud Services grupp":::

Om du vill se mer information väljer du en insikt och väljer sedan **Mer information**.

## <a name="operations"></a>Åtgärder

Platsen utvärderar om tillämpligheten för hanterings insikter på ett vecko schema. Om du vill utvärdera en insikt manuellt högerklickar du på insikten och väljer **sedan utvärdera igen**.

Logg filen för Management Insights är **SMS_DataEngine. log** på plats servern.

<!--1357930-->
Med vissa insikter kan du vidta åtgärder. Välj en insikt, Välj **Mer information**och välj sedan **utför åtgärd**om tillgänglig. Den här åtgärden har något av följande beteenden, beroende på insikter:

- Navigera automatiskt i-konsolen till noden där du kan vidta ytterligare åtgärder. Om till exempel insikter om hantering rekommenderar att du ändrar en klient inställning, navigerar du till noden **klient inställningar** . Vidta ytterligare åtgärder genom att ändra standard eller ett anpassat klient inställnings objekt.

- Navigera till en filtrerad vy baserat på en fråga. Exempelvis visar insikterna i de tomma samlingarna bara de här samlingarna i listan över samlingar. Vidta sedan ytterligare åtgärder, till exempel ta bort en samling eller ändra dess medlemskaps regler.

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a> Instrument panel för hanterings insikter

<!--1357979-->

Välj noden **Management Insights** om du vill visa en grafisk instrument panel. Den här instrument panelen visar en översikt över insikts tillstånden, vilket gör det enklare för dig att visa din förloppet.

Använd följande filter överst i instrument panelen för att förfina vyn:

- Visa slutförd
- Valfritt
- Rekommenderas
- Kritiskt

Instrument panelen innehåller följande paneler:  

- **Index för Management Insights**: spårar övergripande förloppet för hanterings insikter. Indexet är ett viktat medelvärde. Kritiska insikter är värda de flesta. Detta index ger minst vikt till valfria insikter.

- **Hanterings insikter grupper**: visar procent av insikter i varje grupp, med filter. Välj en grupp för att öka detalj nivån för de speciella insikterna i den här gruppen.

- **Prioritet för hanterings**information: visar procent av insikter efter prioritet och som följer filter.

- **10 högsta tillämpliga**insikts regler: en tabell med insikter som prioritet och tillstånd. Använd fältet **filter** överst i tabellen för att matcha strängar i någon av de tillgängliga kolumnerna. Instrument panelen sorterar tabellen i följande ordning:

  - Status: åtgärd krävs, slutförd, okänd  
  - Prioritet: kritisk, rekommenderas, valfritt  
  - Senast ändrad: äldre datum överst  

:::image type="content" source="media/1357979-management-insights-dashboard.png" alt-text="Skärm bild av instrument panelen för hanterings insikter" lightbox="media/1357979-management-insights-dashboard.png":::

## <a name="groups-and-insights"></a>Grupper och insikter

Insikter ordnas i följande grupper för hantering av insikter:

- [Program](#applications)
- [Moln tjänster](#cloud-services)
- [Samlingar](#collections)
- [Configuration Manager utvärdering](#configuration-manager-assessment)
- [Optimera för fjärran vändare](#optimize-for-remote-workers)
- [Proaktivt underhåll](#proactive-maintenance)
- [Säkerhet](#security)
- [Förenklad hantering](#simplified-management)
- [Software Center](#software-center)
- [Programuppdateringar](#software-updates)
- [Windows 10](#windows-10)

> [!NOTE]
> Platsen kanske inte visar alla följande grupper och insikter. Vissa insikter visas inte när du redan har konfigurerat webbplatsen för rekommendationen.

### <a name="applications"></a>Program

Insikter för din program hantering.

- **Program utan distributioner eller referenser**: visar en lista över de program i miljön som inte har aktiva distributioner eller referenser. Referenser inkluderar beroenden, aktivitetssekvenser och virtuella miljöer. Den här insikten hjälper dig att hitta och ta bort program som inte används för att förenkla listan över program som visas i-konsolen. Mer information finns i [distribuera program](../../../apps/deploy-use/deploy-applications.md).<!-- B585E3FF-585F-4CE9-AE2C-648A7CA2F143 -->

### <a name="cloud-services"></a>Molntjänster

Hjälper dig att integrera med många moln tjänster, vilket möjliggör modern hantering av dina enheter.

- **Utvärdera samhanterings beredskap**: hjälper dig att förstå vilka steg som behövs för att aktivera samhantering. Den här insikten har förutsättningar. Mer information finns i [Översikt över samhantering](../../../comanage/overview.md).<!-- D99F094A-A965-402F-AFE5-EE00CCAF0A12 -->

- **Enheter som inte har laddats upp till Azure AD**: från och med version 2002, visar den här insikten enheter som platsen inte har laddat upp till Azure Active Directory (Azure AD) eftersom du inte har konfigurerat den för https.<!--6268489--> Konfigurera [utökad http](../../plan-design/hierarchy/enhanced-http.md)eller aktivera minst en hanterings plats för https. Om du redan har konfigurerat platsen för HTTPS-kommunikation visas inte den här insikten.<!-- 609F03D4-D9B4-4D0D-A67F-9E365F6C0DD0 -->

- **Aktivera Cloud Management Gateway**: Cloud Management Gateway (CMG) är ett enkelt sätt att hantera Configuration Manager klienter via Internet. Genom att distribuera CMG som en moln tjänst i Microsoft Azure kan du fortsätta att hantera och hantera innehåll till klienter som är centralt på Internet. Med CMG behöver du inte någon ytterligare lokal infrastruktur som exponeras för Internet. Mer information finns i [plan for CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md).<!-- 451B9B3A-D86A-4EF1-ACC3-FE6A207886BA -->

- **Göra det möjligt för enheter att hybrid Azure Active Directory anslutna**: Azure AD-anslutna enheter gör att användarna kan logga in med sina domänautentiseringsuppgifter och se till att enheterna uppfyller organisationens standarder för säkerhet och efterlevnad. Mer information finns i [design överväganden för Azure AD hybrid Identity](/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-overview).<!-- 6DC6B149-8B48-45E9-B189-F1E12A62D994 -->

- **Platser som inte har rätt https-konfiguration**: från och med version 2002, visar den här insikten platser i hierarkin som inte är korrekt konfigurerade för https. Den här konfigurationen förhindrar att platsen [synkroniserar samlings medlemskaps resultat till Azure AD-grupper](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync). Det kan medföra att Azure AD Sync inte överför alla enheter. Hantering av dessa klienter kanske inte fungerar korrekt.<!--6268489--> Konfigurera [utökad http](../../plan-design/hierarchy/enhanced-http.md)eller aktivera minst en hanterings plats för https. Om du redan har konfigurerat platsen för HTTPS-kommunikation visas inte den här insikten.<!-- 73884047-3395-430E-B971-F853806D4349 -->

- **Uppdatera klienter till den senaste Windows 10-versionen**: Windows 10, version 1709 eller senare förbättrar och moderniserar dator upplevelsen för dina användare. Mer information finns i [viktiga artiklar om att anta Windows som en tjänst](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).<!-- FD2C7B93-E5C6-4DCB-89AF-9EFCFCD01524 -->

### <a name="collections"></a>Samlingar

Insikter som fören klar hanteringen genom att rensa och konfigurera om samlingar.

- **Tomma samlingar**: visar samlingar i din miljö som inte har några medlemmar. Mer information finns i [hantera samlingar](../../clients/manage/collections/manage-collections.md).<!-- 4266054A-695D-4BCA-8000-27BD32F7C006 -->

<!--3555752-->
- **Samlingar utan Frågeregler och inga direkta medlemmar**: för att förenkla listan över samlingar i hierarkin tar du bort dessa samlingar.<!-- 3C234964-B3F3-49EE-AA13-048CD2021924 -->

- **Samlingar med samma start tid för ny utvärdering**: dessa samlingar har samma omprövnings tid som andra samlingar. Ändra tiden för förnyad utvärdering så att de inte står i konflikt.<!-- A85B79A6-BA81-404F-8DA4-DD7C87582CCD -->

- **Samlingar med kötid över 5 minuter**: granska Frågeregler för den här samlingen. Överväg att ändra eller ta bort samlingen.<!-- 6AF42536-BDF4-4535-87C1-535AE1B813DA -->

- Följande insikter innehåller konfigurationer som kan orsaka onödig belastning på platsen. Granska samlingarna, ta bort dem eller inaktivera utvärdering av samlings regel:

  - **Samlingar utan Frågeregler och stegvisa uppdateringar är aktiverade**<!-- 6A4845AB-6D2C-4F2A-B7AB-EC77C81FD571 -->

  - **Samlingar utan Frågeregler och har Aktiver ATS för scheman**<!-- 219B9C45-BD02-4E7E-A29D-B66094366200 -->

  - **Samlingar utan Frågeregler och Schemalägg fullständig utvärdering har valts**<!-- 8A401207-5A7C-4200-A1DB-990A197458FA -->

### <a name="configuration-manager-assessment"></a>Configuration Manager utvärdering

<!--3607758-->

Från och med version 2002 är den här gruppen av Microsoft Premier Field Engineering. Dessa insikter är ett exempel på de många fler kontroller som Microsoft Premier tillhandahåller i [hubben tjänster](/services-hub/health/getting_started_with_on_demand_assessments).

- **Active Directory säkerhets grupp identifiering har kon figurer ATS för att köras för ofta**: du behöver vanligt vis inte konfigurera Active Directory identifiering av säkerhets grupper så att den inträffar oftare än var tredje timme. En frekvent konfiguration kan ha en negativ inverkan på Active Directory, nätverket och Configuration Manager. Aktivera stegvis synkronisering i stället för att använda ett fullständigt synkroniseringsschema. Mer information finns i [Active Directory Group Discovery](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).<!-- 4E739B65-AEC9-4B1D-8B36-AC6AC4A72022 -->

- **Active Directory system identifiering har kon figurer ATS för att köras för ofta**: du behöver normalt inte konfigurera Active Directory system identifiering så att det inträffar oftare än var tredje timme. En frekvent konfiguration kan ha en negativ inverkan på Active Directory, nätverket och Configuration Manager. Aktivera stegvis synkronisering i stället för att använda ett fullständigt synkroniseringsschema. Mer information finns i [Active Directory system identifiering](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).<!-- 353CAFBC-AC90-4FD3-B3CF-51D6D9FB376C -->

- **Active Directory användar identifiering har kon figurer ATS för att köras för ofta**: du behöver vanligt vis inte konfigurera Active Directory identifiering av användare som inträffar oftare än var tredje timme. En frekvent konfiguration kan ha en negativ inverkan på Active Directory, nätverket och Configuration Manager. Aktivera stegvis synkronisering i stället för att använda ett fullständigt synkroniseringsschema. Mer information finns i [Active Directory User Discovery](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).<!-- 2E742924-7319-4013-B1E1-97DE7EB16B74 -->

- **Samlingar begränsade till alla system eller alla användare**: granska alla samlingar som använder samlingarna **alla system** eller **alla användare** som den begränsande samlingen. Configuration Manager uppdaterar medlemskapet för de här standard samlingarna med data från Active Directory identifierings metoder. Dessa data kanske inte är giltiga för Configuration Manager klienter.<!-- 2382F0C9-A36D-4079-AB37-E3D8EE47E8D4 -->

- **Pulsslags identifiering har inaktiverats**: pulsslags identifiering kräver att du installerar Configuration Manager-klienten på enheter. Det är den enda identifierings metod som klienter startar. Alla andra metoder sker på plats servrar. Pulsslags identifiering är nödvändigt för att se till att klient aktivitets status är aktuell. Det säkerställer att platsen inte oavsiktligt föråldrar resurs posterna från plats databasen. Mer information finns i [pulsslags identifiering](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).<!-- A3089798-DF4E-490A-AF78-4AF474B214CF -->

- Tids krävande **samlings frågor har Aktiver ATS för stegvisa uppdateringar**: samlingar med en senaste stegvis uppdaterings tid på över 30 sekunder använder plats Server och databas resurser, vilket kan påverka övergripande Configuration Manager prestanda. Mer information finns i [metod tips för samlingar](../../clients/manage/collections/best-practices-for-collections.md).<!-- 21F14C0E-008B-47F3-B1E2-19CF79DC97B4 -->

- **Minska antalet program och paket på distributions platser**: Microsoft har officiellt stöd för en kombinerad summa på upp till 10 000 paket och program på en distributions plats. Att överskrida den här summan kan leda till drifts problem. Mer information finns i [storleks-och skalnings nummer – distributions plats](../../plan-design/configs/size-and-scale-numbers.md#distribution-point).<!-- FFE6906E-932E-4927-8EE0-BA25C37943CB -->

- **Installations problem för sekundär plats**: installations statusen för vissa sekundära platser **väntar** eller **misslyckades**. Dessa tillstånd innebär att du startade installationen men att den inte slutfördes korrekt. Klienterna kan inte kommunicera med den primära platsen förrän installationen av den sekundära platsen har slutförts. Kontrol lera arbets ytan **övervakning** och försök att installera igen. Mer information finns i [gör om installationen av en misslyckad uppdatering](install-in-console-updates.md#bkmk_retry).<!-- ED3F5BDD-2F02-44A4-87F4-BB2C1032D4DE -->

- **Uppdatera alla platser till samma version**: Använd samma version av Configuration Manager i en hierarki. Den här konfigurationen ser till att alla platser ger samma funktioner. Platser med olika versioner i samma hierarki introducerar samverkans scenarier. Senare versioner av Configuration Manager innehåller nya funktioner och löser kända problem. Mer information finns i [samverkan mellan olika versioner](../../plan-design/hierarchy/interoperability-between-different-versions.md).<!-- 88C630A5-6D6B-4DDB-95D7-78E12107970D -->

Mer information om dessa insikter finns i [reparations steg för Configuration Manager Management Insights](/services-hub/health/remediation-steps-configmgr).

> [!TIP]
> Om du redan är kund av Microsoft Unified eller Microsoft Premium loggar du in på [tjänstens hubb](https://serviceshub.microsoft.com/assessments/) för ytterligare utvärdering på begäran.
>
> För ytterligare information om Microsoft-tjänster, se [support lösningar](https://www.microsoft.com/enterprise/services/support).

### <a name="operating-system-deployment"></a>Distribution av operativsystem

<!--6982275-->

Från och med version 2006 hjälper följande hanterings insikter dig att hantera princip storleken för aktivitetssekvenser. När storleken på aktivitetssekvensen överskrider 32 MB, kan klienten inte bearbeta den stora principen. Klienten kan sedan inte köra distribution av aktivitetssekvensen.

- **Stora aktivitetssekvenser kan bidra till att överskrida den maximala princip storleken**: om du distribuerar dessa aktivitetssekvenser kanske inte klienterna kan bearbeta de stora princip objekt. Minska storleken på aktivitetssekvensen för att förhindra eventuella problem med princip bearbetningen.<!-- D9A15248-832E-4780-8151-ACD1B9E53FE1 -->

- Den **totala princip storleken för aktivitetssekvenser överskrider princip gränsen**: klienter kan inte bearbeta principen för dessa aktivitetssekvenser eftersom den är för stor. Minska storleken på aktivitetssekvensen så att distributionen kan köras på klienter.<!-- 6568F6A3-D1D8-4E63-940B-FE44F8349802 -->

Mer information finns i [minska storleken på en aktivitetssekvens](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_policysize).

I version 2006 flyttades följande insikter till den här gruppen från **proaktiva underhålls** gruppen:

- **Oanvända start avbildningar**: Start avbildningar som inte refereras till PXE-start eller aktivitetssekvens används. Mer information finns i [Hantera start avbildningar](../../../osd/get-started/manage-boot-images.md).<!-- 4C1FBA51-AD56-4CA8-8326-066F65D24F0E -->

### <a name="optimize-for-remote-workers"></a>Optimera för fjärran vändare

<!--6982226-->

Från och med version 2006 hjälper följande insikter dig att skapa bättre upplevelser för fjärran vändare och minska belastningen på din infrastruktur:

- **Konfigurera VPN-anslutna klienter för att föredra molnbaserade innehålls källor**: om du vill minska trafiken på VPN-nätverket aktiverar du alternativet för gränser grupp för att **föredra molnbaserade källor över lokala källor**. Med det här alternativet kan klienter Ladda ned innehåll från Internet i stället för distributions platser över VPN. Mer information finns i [alternativ för avgränsnings grupper](../deploy/configure/boundary-groups.md#bkmk_bgoptions4).<!-- 1BFD7A7A-077C-4E8A-9EAA-4559E41D400A -->

- **Definiera VPN-gränser grupper**: skapa en VPN-gränser och koppla den till en avgränsnings grupp. Associera VPN-plats system till gruppen och konfigurera inställningarna för din miljö. Den här insikten kontrollerar minst en avgränsnings grupp med minst en VPN-gränser. I egenskaperna för den här insikten väljer du **gransknings åtgärder** för att gå till noden **gränser grupper** . Mer information finns i [VPN-gränser](../deploy/configure/boundaries.md#vpn).<!-- E44BF0CC-0ADA-4B00-A4DF-4005256DF73E -->

- **Inaktivera delning av peer-till-peer-innehåll för VPN-anslutna klienter**: för att förhindra onödig peer-till-peer-trafik som troligen inte gynnar fjärrklienter, inaktiverar du begränsnings grupp alternativet för att **tillåta peer-nedladdningar i den här begränsnings gruppen**. Mer information finns i [alternativ för avgränsnings grupper](../deploy/configure/boundary-groups.md#bkmk_bgoptions1).<!-- 60404B23-96A9-4EE2-B8D6-1F226C2F2F5A -->

### <a name="proactive-maintenance"></a>Proaktivt underhåll

<!--1352184-->
Insikterna i den här gruppen fokuserar på potentiella konfigurations problem för att undvika att Configuration Manager objekt bevaras.

- **Gränser grupper utan tilldelade plats system**: utan tilldelade plats system kan gränser grupper bara användas för platstilldelning. Mer information finns i [Konfigurera gränser grupper](../deploy/configure/boundary-groups.md).<!-- 01E5A4BC-0E31-494E-A553-2B32C410FA5B -->

- **Gränser grupper utan medlemmar**: gränser grupper gäller inte för platstilldelning eller innehålls sökning om de inte har några medlemmar. Mer information finns i [Konfigurera gränser grupper](../deploy/configure/boundary-groups.md).<!-- 4f0d37b1-f979-4ba3-b15b-7fe3c915f239 -->

- **Distributions platser som inte betjänar innehåll till klienter**: distributions platser som inte har betjänat innehåll till klienter under de senaste 30 dagarna. Dessa data baseras på rapporter från klienter från sina nedladdnings historik. Mer information finns i [Installera och konfigurera distributions platser](../deploy/configure/install-and-configure-distribution-points.md).<!-- 9A115092-F8D4-4AB7-B846-C09143B9B9B0 -->

- **Aktivera WSUS-rensning**: verifierar att du har aktiverat alternativet att köra WSUS-rensning på egenskaperna för program uppdaterings plats komponenten. Det här alternativet hjälper till att förbättra WSUS-prestanda. Mer information finns i [underhåll av program uppdatering](../../../sum/deploy-use/software-updates-maintenance.md).<!-- D43080F1-FE98-4F24-94ED-FEB1C2DDEF50 -->

- **Oanvända konfigurations objekt**: konfigurations objekt som inte ingår i en konfigurations bas linje och som är äldre än 30 dagar. Mer information finns i [skapa konfigurations bas linjer](../../../compliance/deploy-use/create-configuration-baselines.md).<!-- 0597907B-17D4-4EA5-92E4-CCE692E1468D -->

- **Uppgradera peer-cache-källor till den senaste versionen av Configuration Manager-klienten**:<!--1358008--> Identifiera klienter som fungerar som en peer-cache-källa men som inte har uppgraderats från en klient version före 1806. Det går inte att använda pre-1806-klienter som peer-cache-källa för klienter som kör version 1806 eller senare. Välj **vidta åtgärd** för att öppna en enhets vy som visar listan över klienter.<!-- B51C6733-F9FF-46BC-8F5E-624F2CBED719 -->

> [!TIP]
> I version 2006 har insikterna för **oanvända start avbildningar** flyttats till den nya [distributions gruppen för operativ systemet](#operating-system-deployment) .

### <a name="security"></a>Säkerhet

Insikter för att förbättra säkerheten för infrastrukturen och enheterna.

- **NTLM-återställning är aktiverat**:<!--4572953--> Från och med version 1906, identifierar den här insikten om du har aktiverat återställnings metoden för den mindre säkra NTLM-autentiseringen för platsen. När klientens push-metod används för att installera Configuration Manager-klienten, kan platsen kräva ömsesidig Kerberos-autentisering. Den här förbättringen hjälper till att skydda kommunikationen mellan servern och klienten. Mer information finns i [så här installerar du klienter med klient-push](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).<!-- C16C6826-8209-47A9-BA71-14A8C83E4C35 -->

- **Klient versioner för program mot skadlig kod som inte**stöds: fler än 10% av klienterna kör versioner av System Center Endpoint Protection som inte stöds. Mer information finns i [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).<!-- ACD63321-CF15-4CDD-B1A3-69005887C633 -->

### <a name="simplified-management"></a>Förenklad hantering

Insikter som hjälper dig att förenkla den dagliga hanteringen av din miljö.

- **Anslut platsen till Microsoft Cloud för Configuration Manager uppdateringar**: den här insikten kontrollerar att din Configuration Manager tjänst anslutnings punkt har anslutits till Microsoft-molnet under de senaste sju dagarna. Den här anslutningen är att ladda ned innehåll för regelbundna uppdateringar. Granska DMPDownloader. log och hman. log. Mer information finns i [krav för Internet åtkomst](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates).<!-- AC662C91-54DF-4B43-B09A-B19D2766144B -->

- **Klient versioner som inte är CB**: visar en lista över alla klienter vars versioner inte är en aktuell gren (CB) build. Mer information finns i [Uppgradera klienter](../../clients/manage/upgrade/upgrade-clients.md).<!-- 450090EA-DF71-428C-AB49-6DEBB85A004C -->

- **Uppdatera klienter till en Windows 10-version som stöds**:<!--3897268--> Den här insikten rapporterar om klienter som kör en version av Windows 10 som inte längre stöds. Den innehåller också klienter med en Windows 10-version som är nära tjänstens slut (tre månader).<!-- 560669D6-1756-4814-9505-C54BDB4930D0 -->

### <a name="software-center"></a>Software Center

Insikter för att hantera Software Center.

- **Dirigera användare till Software Center i stället för programkatalog**: kontrol lera om användarna har installerat eller begärt program från program katalogen under de senaste 14 dagarna. De viktigaste funktionerna i program katalogen ingår nu i Software Center. Support upphör för program katalog rollerna med version 1910. Mer information finns i [föråldrade funktioner](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).<!-- DB9E65CF-C59C-4B76-B6A0-ADB95D809246 -->

- **Använd den nya versionen av Software Center**: den tidigare versionen av Software Center stöds inte längre. Konfigurera klienterna så att de använder det nya Software Center genom att aktivera klient inställningen **Använd nya Software Center** i **dator agent** gruppen. Mer information finns i [om klient inställningar](../../clients/deploy/about-client-settings.md#use-new-software-center).<!-- A9BCA10D-834F-4F39-89F5-CDCCE8F80C56 -->

### <a name="software-updates"></a>Programuppdateringar

- **Klient inställningarna har inte kon figurer ATS för att tillåta klienter att ladda ned delta innehåll**: vissa program uppdateringar som synkroniseras i din miljö innehåller delta innehåll. Aktivera klient inställningen och **Tillåt att klienter laddar ned delta innehåll när det är tillgängligt**. Om du inte aktiverar den här inställningen och distribuerar dessa uppdateringar, kommer klienten att ladda ned mer innehåll än vad som krävs. Mer information finns i [klient inställningar-program uppdateringar](../../clients/deploy/about-client-settings.md#software-updates).<!-- 3E2E9E10-1CDC-47E3-BFC9-3A46AB7FE1BD -->

- **Aktivera program uppdateringens produkt kategori "Windows 10, version 1903 och senare"**: det finns en ny produkt kategori för program uppdateringar för Windows 10, version 1903 och senare. Om du synkroniserar Windows 10-uppdateringar och har Windows 10, version 1903 eller senare klienter väljer du produkt kategorin **Windows 10, version 1903 och senare** i egenskaperna för komponenten för program uppdaterings plats. Mer information finns i[Konfigurera klassificeringar och produkter som ska synkroniseras](../../../sum/get-started/configure-classifications-and-products.md).<!-- 16B1152D-6511-4DC7-824E-539B2597F9B0 -->

### <a name="windows-10"></a>Windows 10

Insikter om distribution och underhåll av Windows 10. Windows 10 Management Insight-gruppen är bara tillgänglig när mer än hälften av klienter kör Windows 7, Windows 8 eller Windows 8,1.

- **Konfigurera Windows diagnostik-data och kommersiell ID-nyckel**: om du vill använda data från Desktop Analytics konfigurerar du enheter med en kommersiell ID-nyckel och aktiverar insamling av diagnostikdata. Ställ in Windows 10-enheter på **utökad (begränsad)** nivå eller högre. Mer information finns i [Aktivera data delning för Skriv bords analys](../../../desktop-analytics/enable-data-sharing.md).<!-- B224393F-B255-4C80-A1D1-1014BE1DC7D4 -->