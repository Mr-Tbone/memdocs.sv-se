---
title: Nyheter i version 2002
titleSuffix: Configuration Manager
description: Få information om ändringar och nya funktioner som introducerats i version 2002 av Configuration Manager aktuella grenen.
ms.date: 05/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: de718cdc-d0a9-47e2-9c99-8fa2cb25b5f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: afdcc608133d306042c9c6dc817396bb2fc3f387
ms.sourcegitcommit: b0ae4a9972bac3518d0d4f33e033ac492eefe3c1
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/28/2020
ms.locfileid: "84126489"
---
# <a name="whats-new-in-version-2002-of-configuration-manager-current-branch"></a>Vad är nytt i version 2002 av Configuration Manager aktuella grenen

*Gäller för: Configuration Manager (aktuell gren)*

Uppdatering 2002 för Configuration Manager aktuella grenen är tillgänglig som en uppdatering i konsolen. Använd den här uppdateringen på webbplatser som kör version 1810 eller senare. <!-- baseline only statement:-->När du installerar en ny plats är den också tillgänglig som en bas linje version. I den här artikeln sammanfattas ändringar och nya funktioner i Configuration Manager version 2002.

Läs alltid den senaste check listan för att installera den här uppdateringen. Mer information finns i [Check lista för att installera uppdatering 2002](../../servers/manage/checklist-for-installing-update-2002.md). När du har uppdaterat en plats granskar du även [Check listan efter uppdatering](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist).

För att dra full nytta av nya Configuration Manager funktioner kan du även uppdatera klienter till den senaste versionen när du har uppdaterat platsen. När nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen, fungerar inte det fullständiga scenariot förrän klient versionen också är den senaste.

> [!TIP]
> Om du vill få ett meddelande när den här sidan uppdateras kopierar du och klistrar in följande URL i din RSS-feed läsare:`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2002+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a>Microsoft Endpoint Manager-klient anslutning

### <a name="device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Enhets synkronisering och enhets åtgärder
<!--3555758-->
Microsoft Endpoint Manager är en integrerad lösning för att hantera alla dina enheter. Microsoft sammanför Configuration Manager och Intune i en enda konsol som kallas **administrations Center för Microsoft Endpoint Manager**. Från och med den här versionen kan du ladda upp dina Configuration Manager-enheter till moln tjänsten och vidta åtgärder från bladet **enheter** i administrations centret.

Mer information finns i [Microsoft Endpoint Manager-klient anslutning](../../../tenant-attach/device-sync-actions.md).

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a>Plats infrastruktur

### <a name="remove-a-central-administration-site"></a>Ta bort en central administrations plats
<!-- 3607277 -->

Om hierarkin består av en central administrations plats (ca) och en enda underordnad primär plats kan du nu ta bort certifikat utfärdarna. Den här åtgärden fören klar din Configuration Manager-infrastruktur till en enda fristående primär plats. Den tar bort de komplexa funktionerna för plats-till-plats-replikering och fokuserar dina hanterings uppgifter på den primära platsen.

Mer information finns i [ta bort CAS](../../servers/deploy/install/remove-central-administration-site.md).

### <a name="new-management-insight-rules"></a>Nya regler för hantering av insikter

I den här versionen ingår följande regler för hantering av insikter:

- Nio regler i **Configuration Manager utvärderings** grupp av Microsoft Premier Field Engineering. De här reglerna är ett exempel på de många fler kontroller som Microsoft Premier tillhandahåller i hubben tjänster.<!-- 3607758 -->

  - Active Directory säkerhets grupps identifiering har kon figurer ATS för att köras för ofta
  - Active Directory system identifiering har kon figurer ATS för att köras för ofta
  - Active Directory användar identifiering har kon figurer ATS för att köras för ofta
  - Samlingar begränsade till alla system eller alla användare
  - Pulsslags identifiering har inaktiverats
  - Tids krävande samlings frågor har Aktiver ATS för stegvisa uppdateringar
  - Minska antalet program och paket på distributions platser
  - Installations problem för sekundär plats
  - Uppdatera alla platser till samma version

- Två ytterligare regler i **Cloud Servicess** gruppen som hjälper dig att konfigurera platsen för att lägga till säker HTTPS-kommunikation:<!-- 6268489 -->

  - Platser som inte har rätt HTTPS-konfiguration
  - Enheter som inte laddats upp till Azure AD

Mer information finns i [hanterings insikter](../../servers/manage/management-insights.md).

### <a name="improvements-to-administration-service"></a>Förbättringar av administrations tjänsten

<!-- 5728365 -->

Administrations tjänsten är en REST API för SMS-providern. Tidigare var du tvungen att implementera något av följande beroenden:

- Aktivera utökad HTTP för hela webbplatsen
- Bind ett PKI-baserat certifikat manuellt till IIS på den server som är värd för SMS-providerns roll

Från och med den här versionen använder administrations tjänsten automatiskt platsens självsignerade certifikat. Den här ändringen bidrar till att minska friktionen för enklare användning av administrations tjänsten. Platsen genererar alltid det här certifikatet. Inställningen för utökad HTTP-plats för att **använda Configuration Manager-genererade certifikat för HTTP-plats system** styr bara om plats systemen använder den eller inte. Nu ignorerar administrations tjänsten den här plats inställningen eftersom den alltid använder platsens certifikat även om inga andra plats system använder utökad HTTP. Du kan fortfarande använda ett PKI-baserat certifikat för serverautentisering.

Mer information finns i följande nya artiklar:

- [Vad är administrationstjänsten?](../../../develop/adminservice/overview.md)
- [Konfigurera administrations tjänsten](../../../develop/adminservice/set-up.md)

### <a name="proxy-support-for-azure-active-directory-discovery-and-group-sync"></a>Proxy-stöd för Azure Active Directory identifiering och gruppsynkronisering

<!-- 5913817 -->

Plats systemets proxyinställningar, inklusive autentisering, används nu av:

- Azure Active Directory (Azure AD) identifiering av användare
- Identifiering av Azure AD-användargrupp
- Synkroniserar samlings medlemskaps resultat till Azure Active Directory grupper

Mer information finns i [stöd för proxy server](../network/proxy-server-support.md#bkmk_other).

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a>Molnbaserad hantering

### <a name="critical-status-message-shows-server-connection-errors-to-required-endpoints"></a>Meddelande om kritisk status visar Server anslutnings fel till obligatoriska slut punkter

<!-- 5566763 -->

Om Configuration Manager plats servern inte kan ansluta till obligatoriska slut punkter för en moln tjänst, genererar den en kritisk status meddelande-ID 11488. När plats servern inte kan ansluta till tjänsten ändras SMS_SERVICE_CONNECTOR komponent status till kritisk. Visa detaljerad status i noden komponent status i Configuration Manager-konsolen.

### <a name="token-based-authentication-for-cloud-management-gateway"></a>Tokenbaserad autentisering för Cloud Management Gateway

<!-- 5686290 -->

CMG (Cloud Management Gateway) stöder många typer av klienter, men även med utökad HTTP kräver dessa klienter ett certifikat för klientautentisering. Detta certifikat krav kan vara svårt att etablera på Internetbaserade klienter som inte ofta ansluter till det interna nätverket, inte kan ansluta Azure Active Directory (Azure AD) och inte har någon metod för att installera ett PKI-utfärdat certifikat.

Configuration Manager utökar sin enhets support med följande metoder:

- Registrera i det interna nätverket för en unik token
- Skapa en token för Mass registrering för Internetbaserade enheter

Mer information finns i [tokenbaserad autentisering för CMG](../../clients/deploy/deploy-clients-cmg-token.md).

### <a name="microsoft-endpoint-configuration-manager-cloud-features"></a>Microsoft Endpoint Configuration Manager moln funktioner

<!--5834830-->

När nya molnbaserade funktioner är tillgängliga i administrations centret för Microsoft Endpoint Manager, eller andra anslutna moln tjänster för din lokala Configuration Manager-installation, kan du nu välja dessa nya funktioner i Configuration Manager-konsolen. Mer information om hur du aktiverar funktioner i Configuration Manager-konsolen finns i [Aktivera valfria funktioner från uppdateringar](../../servers/manage/install-in-console-updates.md#bkmk_options).

## <a name="desktop-analytics"></a><a name="bkmk_da"></a>Skriv bords analys

Mer information om de månatliga ändringarna i moln tjänsten för Station ära datorer finns i [Nyheter i Skriv bords analys](../../../desktop-analytics/whats-new.md).

### <a name="connection-health-dashboard-shows-client-connection-issues"></a>Anslutnings hälso instrument panel visar problem med klient anslutning

Använd instrument panelen för anslutnings hälsa för Skriv bords analys i Configuration Manager för att övervaka klienternas anslutnings hälsa. Nu kan du enklare identifiera konfigurations problem för klientens proxyserver på två områden:

- **Kontroll av slut punkts anslutning**: om klienterna inte kan komma åt en obligatorisk slut punkt visas en konfigurations avisering på instrument panelen. Öka detalj nivån för att se slut punkterna som klienterna inte kan ansluta till på grund av konfigurations problem.<!-- 4963230 -->

- **Anslutnings status**: om klienterna använder en proxyserver för att få åtkomst till moln tjänsten för Skriv bords analys visar Configuration Manager nu problem med proxyautentisering från klienter. Öka detalj nivån för att se klienter som inte kan registreras på grund av proxyautentisering.<!-- 4963383 -->

Mer information finns i [övervaka anslutnings hälsa](../../../desktop-analytics/monitor-connection-health.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a>Real tids hantering

### <a name="improvements-to-cmpivot"></a>Förbättringar av CMPivot

<!-- 5870934 -->

Vi har gjort det enklare att navigera i CMPivot-entiteter. Nu kan du söka efter CMPivot-entiteter. Nya ikoner har också lagts till för att enkelt särskilja entiteter och objekt typer för entiteten.

Mer information finns i [CMPivot](../../servers/manage/cmpivot.md#bkmk_2002).

## <a name="content-management"></a><a name="bkmk_content"></a>Innehålls hantering

### <a name="exclude-certain-subnets-for-peer-content-download"></a>Undanta vissa undernät för nedladdning av peer-innehåll

<!-- 3555777 -->

I gränser grupper ingår följande alternativ för peer-nedladdningar: **vid peer-nedladdningar använder du endast peer-datorer i samma undernät**. Om du aktiverar det här alternativet innehåller innehålls plats listan från hanterings platsen endast peer-källor som finns i samma undernät och gränser som klienten. Beroende på nätverkets konfiguration kan du nu undanta vissa undernät för matchning. Du vill till exempel ta med en kant linje men undanta ett speciellt VPN-undernät.

Mer information finns i [alternativ för avgränsnings grupper](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

### <a name="proxy-support-for-microsoft-connected-cache"></a>Stöd för proxy för Microsoft Connected cache

<!-- 5856396 -->

Om din miljö använder en oautentiserad proxyserver för Internet åtkomst, nu när du aktiverar en Configuration Manager distributions plats för Microsoft Connected cache, kan den kommunicera via proxyservern. Mer information finns i [Microsoft Connected cache](../hierarchy/microsoft-connected-cache.md).

## <a name="client-management"></a><a name="bkmk_client"></a>Klient hantering

### <a name="client-log-collection"></a>Klient logg samling

<!-- 4226618 -->

Du kan nu utlösa en klient enhet för att överföra klient loggarna till plats servern genom att skicka en klient meddelande åtgärd från Configuration Manager-konsolen.

Mer information finns i [klient meddelande](../../clients/manage/client-notification.md#client-diagnostics).

### <a name="wake-up-a-device-from-the-central-administration-site"></a>Aktivera en enhet från den centrala administrations platsen

<!-- 6030715 -->

På den centrala administrations platsen (CAS) i noden enheter eller enhets samlingar kan du nu använda åtgärden klient meddelande för att aktivera enheter. Den här åtgärden var tidigare endast tillgänglig från en primär plats.

Mer information finns i [så här konfigurerar du Wake on LAN](../../clients/deploy/configure-wake-on-lan.md#bkmk_wol-1810).

### <a name="improvements-to-support-for-arm64-devices"></a>Förbättringar av stöd för ARM64-enheter

<!--5954175-->

**Alla Windows 10-plattformar (arm64)** finns i listan över operativ system versioner som stöds på objekt med krav regler eller tillämplighets listor.

> [!NOTE]
> Om du tidigare har valt **Windows 10** -plattformen på den översta nivån, markeras den här åtgärden automatiskt både **alla windows 10 (64-bitars)** och **alla Windows 10 (32-bitars)**. Den här nya plattformen väljs inte automatiskt. Om du vill lägga till **alla Windows 10 (arm64)** väljer du det manuellt i listan.

Mer information om Configuration Manager Support för ARM64-enheter finns i [Windows 10 på arm64](../configs/support-for-windows-10.md#bkmk_arm64).

### <a name="track-configuration-item-remediations"></a>Spåra reparationer av konfigurations objekt
<!--4261411-->
Nu kan du **spåra reparations historiken när den stöds** i dina efterlevnadsprinciper för konfigurations objekt. När det här alternativet är aktiverat genererar alla åtgärder som sker på klienten för konfigurationsobjektet ett tillstånds meddelande. Historiken lagras i Configuration Manager databasen.

Mer information om den här inställningen finns i [skapa anpassade konfigurations objekt för Windows-datorer och serverdatorer som hanteras med Configuration Manager-klienten](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md#bkmk_track).

<!-- ## <a name="bkmk_comgmt"></a> Co-management -->

## <a name="application-management"></a><a name="bkmk_app"></a>Program hantering

### <a name="microsoft-edge-management-dashboard"></a>Instrument panel för Microsoft Edge-hantering

<!-- 3871913 -->

Instrument panelen för Microsoft Edge Management ger dig insikter om användningen av Microsoft Edge och andra webbläsare. I den här instrument panelen kan du:

- Se hur många av dina enheter som har Microsoft Edge installerat
- Se hur många klienter som har olika versioner av Microsoft Edge installerade
- Visa de installerade webbläsarna på olika enheter
- Visa önskad webbläsare efter enhet

I arbets ytan program bibliotek klickar du på Microsoft Edge Management för att se instrument panelen. Ändra samlingen för diagrammets data genom att klicka på Bläddra och välja en annan samling. Som standard är de fem största samlingarna i list rutan. När du väljer en samling som inte finns i listan, visas den nyligen valda samlingen längst ned i list rutan.

Mer information finns i [Microsoft Edge Management](../../../apps/deploy-use/deploy-edge.md#bkmk_edge-dash).

### <a name="improvements-to-microsoft-edge-management"></a>Förbättringar av Microsoft Edge Management

<!-- 4561024 -->

Nu kan du skapa ett Microsoft Edge-program som har kon figurer ATS för att ta emot automatiska uppdateringar i stället för att automatiska uppdateringar har inaktiverats. Med den här ändringen kan du välja att hantera uppdateringar för Microsoft Edge med Configuration Manager eller tillåta att Microsoft Edge uppdateras automatiskt. När du skapar programmet väljer du Tillåt att Microsoft Edge automatiskt uppdaterar versionen av klienten på slutanvändarens enhet på sidan med inställningar för Microsoft Edge.

Mer information finns i [Microsoft Edge Management](../../../apps/deploy-use/deploy-edge.md#bkmk_autoupdate).

### <a name="task-sequence-as-an-app-model-deployment-type"></a>Aktivitetssekvens som distributions typ för program modell

<!-- 3555953 -->

Nu kan du installera komplexa program med hjälp av aktivitetssekvenser via program modellen. Lägg till en distributions typ till en app som är en aktivitetssekvens, antingen för att installera eller avinstallera appen. Den här funktionen ger följande beteenden:

- Visa aktivitetssekvensen för appar med en ikon i Software Center. En ikon gör det enklare för användarna att hitta och identifiera programaktivitetssekvens.

- Definiera ytterligare metadata för aktivitetssekvensen, inklusive lokaliserad information

Mer information finns i [skapa Windows-program](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).

## <a name="os-deployment"></a><a name="bkmk_osd"></a>OS-distribution

### <a name="bootstrap-a-task-sequence-immediately-after-client-registration"></a>Starta en aktivitetssekvens omedelbart efter klient registrering

<!-- 5526972 -->

När du installerar och registrerar en ny Configuration Manager-klient och även distribuerar en aktivitetssekvens till den, är det svårt att fastställa hur lång tid efter registreringen som kommer att köra aktivitetssekvensen. Den här versionen innehåller en ny klient konfigurations egenskap som du kan använda för att starta en aktivitetssekvens på en klient när den har registrerats på platsen.

Mer information finns i [om klient installations egenskaper – etableringar](../../clients/deploy/about-client-installation-properties.md#provisionts).

### <a name="improvements-to-check-readiness-task-sequence-step"></a>Förbättringar för att kontrol lera beredskap för aktivitetssekvenser

<!-- 6005561 -->

Nu kan du kontrol lera fler enhets egenskaper i steget **kontrol lera readiness** -åtgärd. Använd det här steget i en aktivitetssekvens för att kontrol lera att mål datorn uppfyller dina krav.

- Arkitektur för aktuellt operativ system
- Minsta operativsystemversion
- Högsta version av operativsystemet
- Lägsta klient version
- Språk för aktuellt operativ system
- Nätström är nätansluten
- Nätverkskortet är anslutet och inte trådlöst

Mer information finns i avsnittet om [aktivitetssekvenser – kontrol lera beredskap](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness).

### <a name="improvements-to-task-sequence-progress"></a>Förbättringar av förlopp för aktivitetssekvens

<!-- 5932692 -->

I fönstret förlopp för aktivitetssekvens ingår nu följande förbättringar:

- Du kan aktivera det för att visa det aktuella steg numret, det totala antalet steg och procent färdigt
- Ökat fönstrets bredd så att du får mer utrymme för att bättre Visa organisationens namn på en enda rad

Mer information finns i [användar upplevelser för distribution av operativ system](../../../osd/understand/user-experience.md#task-sequence-progress).

### <a name="improvements-to-os-deployment"></a>Förbättringar av OS-distribution

Den här versionen innehåller följande förbättringar av OS-distributionen:

- Miljön i aktivitetssekvensen innehåller en ny skrivskyddad variabel `_TSSecureBoot` .<!--5842295--> Använd den här variabeln för att fastställa statusen för säker start på en UEFI-aktiverad enhet. Mer information finns i [_TSSecureBoot](../../../osd/understand/task-sequence-variables.md#TSSecureBoot).

- Ange variabler för aktivitetssekvens för att konfigurera användar kontexten för **körnings kommando raden** och **köra PowerShell-skript** steg.<!-- 5573175 --> Mer information finns i [SMSTSRunCommandLineAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunCommandLineAsUser) och [SMSTSRunPowerShellAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunPowerShellAsUser).

- I steget **kör PowerShell-skript** kan du nu ange **parameter** egenskapen till en variabel.<!-- 5690481 --> Mer information finns i [kör PowerShell-skript](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).

- Configuration Manager PXE-svarare skickar nu status meddelanden till plats servern. Den här ändringen gör det enklare att felsöka OS-distributioner som använder den här tjänsten.<!-- 5568051 -->

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a>Program uppdateringar

### <a name="orchestration-groups"></a>Orkestreringsgrupper

<!-- 3098816 -->

Skapa en Orchestration-grupp för att få bättre kontroll över distributionen av program uppdateringar till enheter. Många Server administratörer måste noggrant hantera uppdateringar för vissa arbets belastningar och automatisera beteenden mellan.

En Orchestration-grupp ger dig flexibiliteten att uppdatera enheter baserat på en procents ATS, ett bestämt nummer eller en explicit ordning. Du kan också köra ett PowerShell-skript före och efter att enheterna har kört uppdaterings distributionen.

Medlemmar i en Orchestration-grupp kan vara alla Configuration Manager-klienter, inte bara servrar. Reglerna för Dirigerings grupper gäller för enheterna för alla program uppdaterings distributioner till en samling som innehåller en medlem i en Orchestration-grupp. Andra distributions beteenden gäller fortfarande. Du kan till exempel underhålla Windows-och distributions scheman.

Mer information finns i [Orchestration-grupper](../../../sum/deploy-use/orchestration-groups.md).

### <a name="evaluate-software-updates-after-a-servicing-stack-update"></a>Utvärdera program uppdateringar efter en underhålls stack uppdatering

<!-- 4639943 -->

Configuration Manager upptäcker nu om en uppdatering av underhålls stacken (SJÄLVBETJÄNINGS) ingår i en installation för flera uppdateringar. När en SJÄLVBETJÄNINGS identifieras installeras den först. Efter installationen av SJÄLVBETJÄNINGS körs en utvärderings cykel för program uppdateringar för att installera de återstående uppdateringarna. Den här ändringen gör att en beroende ackumulerad uppdatering installeras efter uppdateringen av underhålls stacken. Enheten behöver inte startas om mellan installationer, och du behöver inte skapa ytterligare en underhålls period. SSUs installeras först endast för icke-användarinitierade installationer. Om en användare till exempel initierar en installation för flera uppdateringar från Software Center, kanske SJÄLVBETJÄNINGS inte installeras först.

Mer information finns i [Planera för program uppdateringar](../../../sum/plan-design/plan-for-software-updates.md#bkmk_ssu).

### <a name="office-365-updates-for-disconnected-software-update-points"></a>Office 365-uppdateringar för frånkopplade program uppdaterings platser

<!-- 4065163 -->

Du kan använda ett nytt verktyg för att importera Office 365-uppdateringar från en Internet-ansluten WSUS-server till en frånkopplad Configuration Managers miljö. Tidigare när du exporterade och importerade metadata för program som har uppdaterats i frånkopplade miljöer kunde du inte distribuera Office 365-uppdateringar. Office 365-uppdateringar kräver ytterligare metadata som hämtats från ett Office API och Office CDN, vilket inte är möjligt för frånkopplade miljöer.

Mer information finns i [synkronisera Office 365-uppdateringar från en frånkopplad program uppdaterings plats](../../../sum/get-started/synchronize-office-updates-disconnected.md).

<!-- ## <a name="bkmk_o365"></a> Office management -->

## <a name="protection"></a><a name="bkmk_protect"></a>Skyddas

### <a name="expand-microsoft-defender-advanced-threat-protection-atp-onboarding"></a>Expandera Microsoft Defender Advanced Threat Protection (ATP) onboarding

<!-- 5229962 -->
Configuration Manager har utökat sitt stöd för onboarding-enheter till Microsoft Defender ATP. Mer information finns i [Microsoft Defender Avancerat skydd](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md#onboard-devices).

## <a name="onboard-configuration-manager-clients-to-microsoft-defender-atp-via-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_atp"></a>Publicera Configuration Manager klienter till Microsoft Defender ATP via administrations Center för Microsoft Endpoint Manager
<!--5691658-->
Nu kan du distribuera hanterings principer för Microsoft Defender ATP-EDR för att Configuration Manager hanterade klienter. Dessa klienter kräver inte Azure AD eller MDM-registrering och principen riktas mot ConfigMgr-samlingar i stället för Azure AD-grupper.

Med den här funktionen kan kunder hantera både Intune MDM och Configuration Manager EDR/ATP-onboarding från en enda hanterings upplevelse – administrations Center för Microsoft Endpoint Manager. Mer information finns i [princip för slut punkts identifiering och-svar för slut punkts säkerhet i Intune](../../../../intune/protect/endpoint-security-edr-policy.md).

> [!Important]
> Du behöver samla in snabb korrigering, [KB4563473](https://support.microsoft.com/help/4563473), installerad i din miljö för den här funktionen.

### <a name="improvements-to-bitlocker-management"></a>Förbättringar av BitLocker-hantering

- Hanterings principen för BitLocker innehåller nu ytterligare inställningar, inklusive principer för fasta och flyttbara enheter.<!-- 5925683 --> Mer information finns i [referens för BitLocker-inställningar](../../../protect/tech-ref/bitlocker/settings.md).

- I Configuration Manager nuvarande gren version 1910, för att integrera BitLocker-återställningsnyckeln som du var tvungen att aktivera för en hanterings plats. HTTPS-anslutningen är nödvändig för att kryptera återställnings nycklarna över nätverket från Configuration Manager-klienten till hanterings platsen. Det kan vara svårt för många kunder att konfigurera hanterings platsen och alla klienter för HTTPS.

    Från och med den här versionen är HTTPS-kravet för IIS-webbplatsen som är värd för återställnings tjänsten, inte hela hanterings plats rollen. Den här ändringen sänker certifikat kraven och krypterar fortfarande återställnings nycklarna vid överföring.<!-- 5925660 --> Mer information finns i [kryptera återställnings data](../../../protect/deploy-use/bitlocker/encrypt-recovery-data.md).

## <a name="reporting"></a><a name="bkmk_report"></a>Uppgiftslämn

### <a name="integrate-with-power-bi-report-server"></a>Integrera med Power BI-rapportserver

<!-- 3721603 -->

Nu kan du integrera Power BI-rapportserver med Configuration Manager repor ting. Den här integrationen ger modern visualisering och bättre prestanda. Det lägger till konsol stöd för Power BI rapporter på liknande sätt som redan finns med SQL Server Reporting Services.

Mer information finns i [integrera med Power BI-rapportserver](../../servers/manage/powerbi-report-server.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a>Configuration Manager-konsol

### <a name="show-boundary-groups-for-devices"></a>Visa gränser grupper för enheter

<!--6521835-->

För att hjälpa dig att bättre felsöka enhets beteenden med gränser grupper kan du nu Visa gränserna för vissa enheter. I noden **enheter** eller när du visar medlemmar i en **enhets samling**lägger du till kolumnen ny **gränser grupp (er)** i listvyn.

Mer information finns i [gränser grupper](../../servers/deploy/configure/boundary-groups.md#bkmk_show-boundary).

### <a name="send-a-smile-improvements"></a>Skicka ett leende förbättringar

<!-- 5891852 -->

När du skickar ett leende eller skickar en bister min, skapas ett status meddelande när feedback skickas. Den här förbättringen innehåller en post med:

- När din feedback skickades
- Som skickade feedbacken
- Feedback-ID
- Om feedback-överföringen lyckades eller inte

Ett status meddelande med ID 53900 är en lyckad överföring och 53901 är ett misslyckat överförings försök.

Mer information finns i [produkt feedback](../../understand/find-help.md#BKMK_1806Feedback).

### <a name="search-all-subfolders-for-configuration-items-and-configuration-baselines"></a>Sök i alla undermappar efter konfigurations objekt och konfigurations bas linjer

<!--5891241-->

Precis som förbättringar i tidigare versioner kan du nu använda sökalternativet **alla undermappar** från noden **konfigurations objekt** och **konfigurations bas linjer** .

## <a name="tools"></a><a name="bkmk_tools"></a>Formateringsverktyg

### <a name="onetrace-log-groups"></a>OneTrace logg grupper

<!-- 5559993 -->

OneTrace stöder nu anpassningsbara logg grupper som liknar funktionen i Support Center. Med logg grupper kan du öppna alla loggfiler för ett enda scenario. OneTrace innehåller för närvarande grupper för följande scenarier:

- Programhantering
- Kompatibilitetsinställningar (kallas även för önskad konfigurations hantering)
- Programuppdateringar

Mer information finns i [Support Center OneTrace](../../support/support-center-onetrace.md).

### <a name="improvements-to-extend-and-migrate-on-premises-site-to-microsoft-azure"></a><a name="bkmk_extend"></a>Förbättringar för att utöka och migrera lokal plats till Microsoft Azure
<!--5665775, 6307931-->
Verktyget för att utöka och migrera den lokala platsen till Microsoft Azure nu har stöd för etablering av flera plats system roller på en enda virtuell Azure-dator. Du kan lägga till plats system roller när den första distributionen av virtuella Azure-datorer har slutförts.

Mer information finns i [utöka och migrera en lokal plats till Microsoft Azure](../../support/azure-migration-tool.md#bkmk_add_role).

## <a name="other-updates"></a>Övriga uppdateringar

Från och med den här versionen är följande funktioner inte längre [för hands version](../../servers/manage/pre-release-features.md):

- [Azure Active Directory användar grupp identifiering](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956-->
- [Synkronisera samlings medlemskaps resultat till Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)<!--3607475-->
- [Fristående CMPivot](../../servers/manage/cmpivot.md#bkmk_standalone)<!--3555890/4692885-->
- [Klient program för samhanterade enheter](../../../comanage/workloads.md#client-apps) (kallades tidigare *mobilappar för samhanterade enheter*)<!-- 1357892/3600959 -->

Mer information om ändringar i Windows PowerShell-cmdlets för Configuration Manager finns i [versions anteckningar för PowerShell version 2002](https://docs.microsoft.com/powershell/sccm/2002-release-notes?view=sccm-ps).

Mer information om ändringar i administrations tjänsten REST API finns i viktig information om [administrations tjänsten](../../../develop/adminservice/release-notes.md#bkmk_2002).

Förutom nya funktioner innehåller den här versionen även ytterligare ändringar som fel korrigeringar. Mer information finns i [Sammanfattning av ändringar i Configuration Manager aktuella grenen, version 2002](https://support.microsoft.com/help/4556203).

<!--
The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Nästa steg

<!-- At this time, version 2002 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2002.md#early-update-ring). -->

Från och med den 11 maj 2020 är version 2002 globalt tillgängligt för alla kunder att installera.

När du är redo att installera den här versionen, se [Installera uppdateringar för Configuration Manager](../../servers/manage/updates.md) och [Check lista för att installera uppdatering 2002](../../servers/manage/checklist-for-installing-update-2002.md).

> [!TIP]
> Om du vill installera en ny plats använder du en bas linje version av Configuration Manager.
>
> Läs mer om:
>
> - [Nya platser installeras](../../servers/deploy/install/installing-sites.md)
> - [Bas linje-och uppdaterings versioner](../../servers/manage/updates.md#bkmk_Baselines)

Information om kända viktiga problem finns i [versions anteckningarna](../../servers/deploy/install/release-notes.md).

När du har uppdaterat en plats granskar du även [Check listan efter uppdatering](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist).
