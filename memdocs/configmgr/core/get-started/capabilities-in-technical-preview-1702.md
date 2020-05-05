---
title: Funktioner i Technical Preview 1702
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1702.
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 73b8111cbada129997cec965ca685f1ef22b1f3a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721439"
---
# <a name="capabilities-in-technical-preview-1702-for-configuration-manager"></a>Funktioner i Technical Preview 1702 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1702. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.    


**Följande är nya funktioner som du kan prova med den här versionen.**  

##  <a name="send-feedback-from-the-configuration-manager-console"></a>Skicka feedback från Configuration Manager-konsolen

I den här för hands versionen introduceras nya alternativ för feedback i Configuration Manager-konsolen. Med feedback-alternativen kan du skicka feedback direkt till utvecklings teamet, med hjälp av webbplatsen Configuration Manager UserVoice feedback.  

> Du kan hitta **feedback** -alternativet:
> -  I menyfliksområdet längst till vänster på fliken Start på varje nod.  
>    ![Menyfliksområde](./media/feedback-home.png)

-  När du högerklickar på ett objekt i-konsolen.   
    ![Skärmdumpsverktygen – Klicka på alternativ](./media/feedback-option.png)   

Om du väljer **feedback** öppnas webbläsaren på webbplatsen för Configuration Manager UserVoice feedback på https://configurationmanager.uservoice.com/forums/300492-ideas.
##  <a name="changes-for-updates-and-servicing"></a>Ändringar för uppdateringar och underhåll
Följande introduceras i den här för hands versionen.

**Enklare uppdaterings alternativ**  
Nästa gången infrastrukturen uppfyller två eller fler uppdateringar laddas bara den senaste uppdateringen ned. Om din aktuella plats version till exempel är två eller fler äldre än den senaste versionen som är tillgänglig, hämtas bara den senaste uppdaterings versionen automatiskt.  

Du har möjlighet att ladda ned och installera andra tillgängliga uppdateringar, även om de inte är den senaste versionen. Men du får en varning om att uppdateringen har ersatts av en nyare. Om du vill hämta en uppdatering som är *tillgänglig för hämtning*väljer du uppdateringen i-konsolen och klickar sedan på **Ladda ned**.

**Förbättrad rensning av äldre uppdateringar**   
Vi har lagt till en automatisk rensning som tar bort onödiga nedladdningar från mappen "EasySetupPayload" på plats servern.  


## <a name="peer-cache-improvements"></a>Förbättringar i peer-cache
Från och med den här versionen avvisar en peer-cache käll dator en begäran om innehåll när peer-cachens käll dator uppfyller något av följande villkor:  
-  Är i läget för låg batteri nivå.
-  CPU-belastningen överskrider 80% vid den tidpunkt då innehållet begärs.
-  Disk-I/O har en *AvgDiskQueueLength* som överstiger 10.
-  Det finns inga fler tillgängliga anslutningar till datorn.   

Du kan konfigurera de här inställningarna med hjälp av klient agentens konfigurations klass för funktionen peer-källa (*SMS_WinPEPeerCacheConfig*) när du använder Configuration Manager SDK.

När datorn avvisar en begäran om innehållet fortsätter den begär ande datorn att söka efter innehålls formulär alternativa källor i sin pool med tillgängliga innehålls käll platser.   

## <a name="use-azure-active-directory-domain-services-to-manage-devices-users-and-groups"></a><a name="azurediscovery"></a>Använd Azure Active Directory Domain Services för att hantera enheter, användare och grupper

Med den här tekniska för hands versionen kan du hantera enheter som är anslutna till en Azure Active Directory (AD) Domain Services-hanterad domän. Du kan också identifiera enheter, användare och grupper i den domänen med olika Configuration Manager identifierings metoder.

Den tekniska för hands versions platsens infrastruktur, klienter och Azure AD Domain Services domän måste köras i Azure.


### <a name="set-up-configuration-manager-to-use-azure-ad"></a>Konfigurera Configuration Manager att använda Azure AD
Om du vill använda Azure AD med Configuration Manager behöver du följande:
- En Azure-prenumeration.
- Azure AD med domän tjänster (DS).
- En Configuration Manager plats som körs på en virtuell Azure-dator som är ansluten till Azure AD.
- Configuration Manager klienter som körs i samma Azure AD-miljö.

Information om hur du konfigurerar Azure AD Domain Service finns i [Kom igång med Azure AD Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/create-instance).

### <a name="discover-resources"></a>Identifiera resurser
När du har konfigurerat Configuration Manager att köras i Azure AD kan du använda följande Active Directory identifierings metoder för att söka efter resurser i Azure AD:  
- Identifiering av Active Directory-system
- Identifiering av Active Directory-användare
- Identifiering av Active Directory-grupper  

För varje metod som du använder redigerar du LDAP-frågan för att söka i Azure AD OU-strukturer i stället för de behållare som är typiska för lokala Active Directory. Detta kräver att du dirigerar frågan för att söka i din Active Directory i din Azure-prenumeration.  

I följande exempel används en Azure AD- *contoso.onmicrosoft.com*:
- **System identifiering**   
  Azure AD lagrar enheter i ou för **AADDC-datorer** .  Konfigurera följande:  
  - *LDAP://OU = AADDC Computers, DC = contoso, DC = onmicrosoft, DC = com*  


- **Användar identifiering** AAD lagrar användare under **AADDC-användarens** organisationsenhet.  Konfigurera följande:
  - *LDAP://OU = AADDC Users, DC = contoso, DC = onmicrosoft, DC = com*


- **Grupp identifiering**  
Azure AD har ingen ORGANISATIONSENHET som lagrar grupper. Använd i stället samma allmänna struktur som system-eller användar frågorna och konfigurera LDAP-frågan så att den pekar på den ORGANISATIONSENHET som innehåller de grupper som du vill identifiera.

Se följande om du vill ha mer information om Azure AD:  
- [Azure Active Directory Domain Services](https://azure.microsoft.com/services/active-directory-ds) på Azure.Microsoft.com.
- [Active Directory Domain Services dokumentation](https://docs.microsoft.com/azure/active-directory-domain-services) på docs.Microsoft.com.

## <a name="conditional-access-device-compliance-policy-improvements"></a>Förbättringar av efterlevnadsprinciper för villkorlig åtkomst

En ny regel för efterlevnadsprinciper är tillgänglig för att hjälpa dig att blockera åtkomst till företags resurser som har stöd för villkorlig åtkomst, när användare använder appar som ingår i en icke-kompatibel lista över appar. Den icke-kompatibla listan över appar kan definieras av administratören när de nya kompatibla regel **appar som inte kan installeras**läggs till. Den här regeln kräver att administratören anger **appens namn**, **app-ID**och **app utgivare** (valfritt) när de lägger till en app i listan över inkompatibla. Den här inställningen gäller endast iOS-och Android-enheter.

Dessutom hjälper organisationerna att undvika data läckage via oskyddade appar och förhindra onödig data förbrukning via vissa appar.

### <a name="try-it-out"></a>Prova nu

**Scenario:** Identifiera appar som kan orsaka data läckage genom att skicka företags data utanför företaget eller som orsakar överdriven data förbrukning, och sedan [skapa en efterlevnadsprincip för villkorlig åtkomst](../../mdm/understand/what-happened-to-hybrid.md) som lägger till dessa appar i listan över appar som inte är kompatibla. Detta kommer att blockera åtkomst till företags resurser som har stöd för villkorlig åtkomst tills användaren kan ta bort den blockerade appen.

## <a name="antimalware-client-version-alert"></a>Klient versions avisering för program mot skadlig kod
Från och med den här för hands versionen ger Configuration Manager Endpoint Protection en avisering om mer än 20% (standard) av hanterade klienter använder en utgången version av klienten för program mot skadlig kod (t. ex. Windows Defender eller Endpoint Protection klient).

### <a name="try-it-out"></a>Prova nu
Se till att Endpoint Protection är aktiverat på alla Skriv bords-och Server klienter med hjälp av klient inställnings principen. Nu kan du Visa **klient versionen av program mot skadlig kod** och **Endpoint Protection distributions status** genom att gå **till till gångar och efterlevnad** > **Översikt** > **enheter** > **alla datorer och betjäna klienter**. Om du vill söka efter en avisering kan du Visa **aviseringar** i arbets ytan **övervakning** . Om fler än 20% av de hanterade klienterna kör en inaktuell version av program mot skadlig kod, visas en inaktuell varning i klient versionen av program mot skadlig kod. Den här aviseringen visas inte på fliken **övervakning** > **Översikt** . Aktivera program uppdateringar för klienter för program mot skadlig kod för att uppdatera utgångna klienter för program mot skadlig kod.

Om du vill konfigurera den procent andel som aviseringen genereras vid expanderar du **övervaknings** > **aviseringar** > **alla aviseringar**, dubbelklickar på **klienter för program mot skadlig kod** och ändrar **varningen om procent andelen hanterade klienter med en inaktuell klient version av program mot skadlig kod är mer än** alternativet.

## <a name="compliance-assessment-for-windows-update-for-business-updates"></a>Kompatibilitetskontroll för Windows Update för affärs uppdateringar
Nu kan du konfigurera en uppdaterings regel för efterlevnadsprinciper för att inkludera ett Windows Update för företags utvärderings resultat som en del av utvärderingen av villkorlig åtkomst.
> [!IMPORTANT]
> Du måste ha Windows 10 Insider Preview version 15019 eller senare för att kunna använda kompatibilitetskontroll för Windows Update för affärs uppdateringar.

### <a name="allow-windows-update-for-business-to-manage-windows-10-updates"></a>Tillåt Windows Update för företag att hantera Windows 10-uppdateringar
Om du vill samla in information om bedömning av efterlevnad för Windows Update för affärs uppdateringar använder du följande procedur för att konfigurera klient agent inställningen för att uttryckligen tillåta Windows Update för företag att hantera Windows 10-uppdateringar.
1. I Configuration Manager-konsolen går du till **Administration** > **klient inställningar**.
2. I egenskaperna för klient inställningarna går du till **program uppdateringar**och väljer **Ja** för inställningen **hantera Windows 10-uppdateringar med Windows Update för företag** .

### <a name="create-a-compliance-policy-for-windows-update-for-business-assessment"></a>Skapa en policy för efterlevnad för Windows Update för företags utvärdering
1. I Configuration Manager-konsolen går du till **till gångar och** > **Compliance Settings** > **Compliance policies**efterlevnadsprinciper kompatibilitetsinställningar.
2. Klicka på **skapa policy för efterlevnad** eller Välj en befintlig efterlevnadsprincip som ska ändras.
3. På sidan Allmänt anger du ett namn och en beskrivning. Välj **regler för efterlevnad för enheter som hanteras med Configuration Manager-klienten**, ange allvarlighets grad för inkompatibilitet för rapportering och klicka på **Nästa**.
4. På sidan plattformar som stöds väljer du **Windows 10**och klickar sedan på **Nästa**.
5. Klicka på nytt på sidan regler **....** och välj sedan **Kräv Windows Update för företags efterlevnad**för **villkoret** . Inställningen **Value** anges automatiskt till **True**.

Den nya principen visas i noden **Efterlevnadsprinciper** på arbetsytan **Tillgångar och efterlevnad**.

### <a name="deploy-a-compliance-policy"></a>Distribuera en efterlevnadsprincip
1. I Configuration Manager-konsolen går du till **till gångar och efterlevnad** > **kompatibilitetsinställningar och**klickar sedan på **efterlevnadsprinciper**.
2. På fliken **Start** går du till gruppen **Distribution** och klickar på **Distribuera**.
3. I dialogrutan **Distribuera efterlevnadsprincip** klickar du på **Bläddra** för att välja användarsamlingen som principen ska distribueras i.
   Du kan också välja alternativ för att generera aviseringar när principen inte är kompatibel samt konfigurera schemat som den här efterlevnadsprincipen ska utvärderas efter.
4. När du är klar klickar du på **OK**.

### <a name="monitor-the-compliance-policy"></a>Övervaka efterlevnadsprincipen
När du har skapat en efterlevnadsprincip kan du övervaka resultatet av efterlevnaden i Configuration Manager-konsolen. Mer information finns i [övervaka policyn för efterlevnad](../../mdm/understand/what-happened-to-hybrid.md).


## <a name="improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences"></a>Förbättringar av Software Center-inställningar och aviserings meddelanden för aktivitetssekvenser med hög effekt
Den här versionen innehåller följande förbättringar av Software Center-inställningar och aviserings meddelanden för aktivitetssekvenser med hög effekt:

- I egenskaperna för aktivitetssekvensen kan du nu konfigurera en aktivitetssekvens, inklusive aktivitetssekvenser som inte är operativ system, som en distribution med hög risk. En aktivitetssekvens som uppfyller vissa villkor definieras automatiskt som hög påverkan. Mer information finns i [Hantera distributioner med hög risk](../servers/manage/settings-to-manage-high-risk-deployments.md).
- I egenskaperna för aktivitetssekvensen kan du välja att använda standard meddelandet eller skapa ett eget anpassat aviserings meddelande för distributioner med hög effekt.
- I egenskaperna för aktivitetssekvensen kan du konfigurera Software Center-egenskaper, bland annat göra en omstart nödvändig, hämtnings storlek för aktivitetssekvensen och den beräknade körnings tiden.
- Standard distributions meddelandet med hög effekt för uppgraderingar på plats anger nu att dina appar, data och inställningar migreras automatiskt. Tidigare var standard meddelandet för alla installations program för operativ systemet, vilket indikerade att alla appar, data och inställningar skulle gå förlorade, vilket inte var sant för en uppgradering på plats.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Ange en aktivitetssekvens som en aktivitet med hög effekt
Använd följande procedur för att ange en aktivitetssekvens som hög påverkan.
> [!NOTE]
> En aktivitetssekvens som uppfyller vissa villkor definieras automatiskt som hög påverkan. Mer information finns i [Hantera distributioner med hög risk](../servers/manage/settings-to-manage-high-risk-deployments.md).

1. I Configuration Manager-konsolen går du till**aktivitetssekvenser**för **program biblioteks** > **operativ system** > .
2. Välj den aktivitetssekvens som du vill redigera och klicka på **Egenskaper**.
3. På fliken **användar meddelande** väljer du **det här är en aktivitetssekvens med hög effekt**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Skapa ett anpassat meddelande för distributioner med hög risk
1. I Configuration Manager-konsolen går du till**aktivitetssekvenser**för **program biblioteks** > **operativ system** > .
2. Välj den aktivitetssekvens som du vill redigera och klicka på **Egenskaper**.
3. På fliken **användar meddelande** väljer du **Använd anpassad text**.
   > [!NOTE]
   >  Du kan bara ange meddelande text när det **här är en vald aktivitetssekvens** .

4. Konfigurera följande inställningar (högst 255 tecken för varje text ruta):

   **Rubrik text för användar meddelande**: anger den blå text som visas i användar meddelandet för Software Center. I standard användar meddelandet innehåller det här avsnittet exempelvis något som "bekräfta att du vill uppgradera operativ systemet på den här datorn".

   **Meddelande text för användar meddelande**: det finns tre text rutor som innehåller bröd texten i det anpassade meddelandet.
   - första text rutan: anger huvud texten i texten, vanligt vis med instruktioner för användaren. I standard användar meddelandet innehåller det här avsnittet t. ex. att uppgradera operativ systemet tar tid och datorn kan starta om flera gånger. "
   - andra text rutan: anger den fetstilta texten under textens huvuddel. I det här avsnittet innehåller till exempel det här avsnittet något liknande "den här uppgraderings funktionen installerar det nya operativ systemet och migrerar automatiskt dina appar, data och inställningar."
   - tredje text rutan: anger den sista text raden under fet text. I standard meddelandet innehåller det här avsnittet exempelvis något som "Klicka på installera för att börja. Annars klickar du på Avbryt. "   

   Anta att du konfigurerar följande anpassade meddelande i egenskaper.

   ![Anpassat meddelande för en aktivitetssekvens](./media/user-notification.png)

   Följande meddelande visas när slutanvändaren öppnar installationen från Software Center.

   ![Anpassat meddelande för en aktivitetssekvens](./media/user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>Konfigurera Software Center-egenskaper
Använd följande procedur för att konfigurera information om aktivitetssekvensen som visas i Software Center. Informationen är endast för information.  
1. I Configuration Manager-konsolen går du till**aktivitetssekvenser**för **program biblioteks** > **operativ system** > .
2. Välj den aktivitetssekvens som du vill redigera och klicka på **Egenskaper**.
3. På fliken **Allmänt** finns följande inställningar för Software Center:
   - **Omstart krävs**: låter användaren veta om en omstart krävs under installationen.
   - **Hämtnings storlek (MB)**: anger hur många megabyte som visas i Software Center för aktivitetssekvensen.  
   - **Beräknad körnings tid (minuter)**: anger den uppskattade körnings tiden i minuter som visas i Software Center för aktivitetssekvensen.


## <a name="check-for-running-executable-files-before-installing-an-application"></a>Sök efter körning av körbara filer innan du installerar ett program

I dialog rutan * \<namn på distributions typ>* **Egenskaper** för en distributions typ, på fliken installations beteende, kan du nu ange en eller flera körbara filer som, om den körs, blockerar installationen av distributions typen. Användaren måste stänga den körbara filen som körs (eller så kan den stängas automatiskt för distributioner med syftet obligatorisk) innan distributions typen kan installeras.

### <a name="try-it-out"></a>Prova.

1. I egenskaperna för en Configuration Manager distributions typ väljer du fliken **installations beteende** .
2. Välj **Lägg** till för att lägga till en eller flera körbara fil namn som du vill söka efter. Du kan också lägga till ett visnings namn för att göra det enklare för användarna att identifiera program i listan.
3. Om distributionen måste vara obligatoriskt i guiden distribuera program vara kan du välja att **automatiskt stänga alla körbara filer som körs och som du har angett på fliken installations beteende i dialog rutan Egenskaper för distributions typ**.

Om programmet har distribuerats som **tillgängligt**och en användare försöker installera ett program uppmanas de att stänga alla körbara körbara filer som du har angett innan de kan fortsätta med installationen.

Om programmet har distribuerats vid **behov**, och alternativet **automatiskt stänger alla körbara filer som du har angett på fliken installations beteende i dialog rutan Egenskaper för distributions typ** , visas en dialog ruta som informerar dem om att körbara filer som du har angett ska stängas automatiskt när tids gränsen för programinstallationen har uppnåtts. Du kan schemalägga dessa dialog rutor i **klient inställningar** > **dator agent**. Om du inte vill att slutanvändaren ska se dessa meddelanden väljer du **Dölj i Software Center och alla meddelanden** på fliken **användar upplevelse** i distributionens egenskaper.

Om programmet har distribuerats vid **behov** och alternativet **stängde automatiskt körning av körbara filer som du har angett på fliken installations beteende i dialog rutan Egenskaper för distributions typ** inte är markerat, kommer installationen av appen att Miss sen Miss sen om ett eller flera av de angivna programmen körs.

## <a name="create-pfx-certificates-with-s-mime-support"></a>Skapa PFX-certifikat med S MIME-support

Nu kan du skapa en PFX-certifikat profil som stöder S/MIME och distribuera den till användarna.  Certifikatet kan sedan användas för S/MIME-kryptering och dekryptering mellan enheter som användaren har registrerat.

Dessutom kan du nu ange flera certifikat utfärdare (ca) på flera plats system roller för certifikat registrering och sedan tilldela vilka certifikat utfärdare som ska bearbeta begär Anden som en del av certifikat profilen.

För iOS-enheter kan du koppla en PFX-certifikat profil till en e-postprofil och aktivera S/MIME-kryptering.  Detta aktiverar sedan S/MIME i den interna e-postklienten på iOS och kopplar rätt S/MIME-krypteringsnyckel till den.

Mer information om certifikat i Configuration Manager finns i [Introduktion till certifikat profiler]( https://docs.microsoft.com/sccm/protect/deploy-use/introduction-to-certificate-profiles).


## <a name="new-compliance-settings-for-ios-devices"></a>Nya kompatibilitetsinställningar för iOS-enheter

Vi har lagt till nya inställningar som du kan använda i konfigurations objekt för iOS-enheter. Detta är inställningar som tidigare fanns i Microsoft Intune i en fristående konfiguration och som nu är tillgängliga när du använder Intune med Configuration Manager. Om du behöver hjälp med någon av dessa inställningar går du till [princip inställningar för iOS i Microsoft Intune](/mem/intune/configuration/device-restrictions-ios).

- **Synkronisera data från hanterade appar till iCloud**
- **Leverans för att fortsätta aktiviteter på en annan enhet**
- **iCloud-bilddelning**
- **iCloud-bildbibliotek**
- **Lita på nya företags program författare**
- **Tillåt att användaren laddar ned innehåll från iBook-butiken flaggat som "erotik"** (endast övervakat läge)
- **Tvinga parkopplade Apple Watches att använda handledsavkänningen**
- **Lösen ord för utgående AirPlay-begäranden**
- **Ändra konto inställningar** (endast övervakat läge)
- **Ändringar av inställningar för mobil data användning i appar** (endast övervakat läge)
- **Radera allt innehåll och alla inställningar** (endast övervakat läge)
- **Konfigurera begränsningar för enheten** (endast övervakat läge)
- **Använd värd koppling för att styra vilka enheter en iOS-enhet kan kopplas** till (endast övervakat läge)
- **Installera konfigurations profiler och certifikat** (endast övervakat läge)
- **Ändring av enhets namn** (endast övervakat läge)
- **Ändring av lösen ord** (endast övervakat läge)
- **Apple Watch-par** (endast övervakat läge)
- **Ändring av meddelande inställningar** (endast övervakat läge)
- **Ändra tapet** (endast övervakat läge)
- **Ändring av inställningar för att skicka diagnostik** (endast övervakat läge)
- **Bluetooth-ändring** (endast övervakat läge)
- **Ta bort** (endast övervakat läge)
- **Använd Siri för att söka efter innehåll som skapats av användare från Internet** (endast övervakat läge)
- **Siri-svordomar filter** (endast övervakat läge)
- **Returnera resultat från Internet i Spotlight-sökning** (endast övervakat läge)
- **Ord definitions sökning** (endast övervakat läge)
- **Förutsägande tangent bord** (endast övervakat läge)
- **Automatisk korrigering** (endast övervakat läge)
- **Tangent bord med stavnings kontroll** (endast övervakat läge)
- **Kortkommandon (endast** övervakat läge)
  <!--- - **Enterprise app trust settings modification** --->
- **Installera endast appar med Apple Configurator och iTunes** (endast övervakat läge)
- **Automatisk nedladdning av appar** (endast övervakat läge)
- **Ändra inställningarna för appen Hitta mina vänner** (endast övervakat läge)
- **Åtkomst till iBooks Store** (endast övervakat läge)
- **Meddelanden-app** (endast övervakat läge)
- **Poddsändningar** (endast övervakat läge)
- **Apple Music** (endast övervakat läge)
- **iTunes Radio** (endast övervakat läge)
- **Apple News** (endast övervakat läge)
- **Game Center** (endast övervakat läge)
- **Hantera luftsläpp som ett ohanterat mål**

## <a name="android-for-work-support"></a>Stöd för Android for Work

Från och med Technical Preview version 1702 kan du binda ett Google-konto till din hybrid MDM-klient. På så sätt kan du göra följande:

- Registrera [Android-enheter som stöds](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) som Android for Work och skapa arbets profiler på de registrerade enheterna
- Godkänn appar i Play for Work-butiken, synkronisera dem med Configuration Manager-konsolen och distribuera dem sedan till enhets arbets profiler
- Skapa och distribuera konfigurations objekt för att konfigurera arbets profil och lösen ords inställningar för enheterna
- Skapa och distribuera objekt för efterlevnadsprinciper och resurs åtkomst profiler för Android for Work-enheter eftersom du redan har Android-enheter
- Utför selektiv rensning på Android for Work-enheter

När du registrerar en enhet som Android for Work skapar en arbets profil på enheten som Intune kan hantera. Den här arbets profilen finns sida vid sida med den personliga profilen på Android-enheten. Användare kan enkelt växla mellan appar för arbets profiler och personliga profiler. Du kan inte hantera objekt i den personliga profilen. Personliga appar och data förblir ohanterade. Configuration Manager har fullständig kontroll över arbets profilen och dess innehåll och kan ta bort den från enheten.

Android for Work är en separat plattform från Android och du måste bestämma vilken typ av hantering som ska användas för Android-enheter som har stöd för arbets profiler.

### <a name="try-it-out"></a>prova!
I följande avsnitt beskrivs Android for Work-hantering.

#### <a name="enable-android-for-work-management"></a>Aktivera hantering av Android for Work
1. Skapa ett Google-konto https://accounts.google.com/SignUp som ska användas som administratörs konto för Android for Work som ska associeras med alla hanterings uppgifter för Android for Work för den här Intune-klienten. Detta kan vara ett Google-konto som delas mellan administratörer som hanterar Android-enheter. Det här är det Google-konto som används i din organisation för att hantera och publicera appar i Play for Work-konsolen. Du kommer att använda det här kontot för att godkänna appar i Play for Work-butiken, så håll koll på kontots namn och lösen ord.
2. Aktivera Android-registrering genom att binda Google-kontot till Intune-klienten som hanteras i Configuration Manager:
   1. Gå till **administrations** > **Översikt** > **Cloud Services** > **Microsoft Intune prenumerationer** och välj din Intune-prenumeration.
   2. I menyfliksområdet klickar du på **Konfigurera plattformar** > **Android** och kontrollerar att **Aktivera Android-registrering** är markerat.
   3. I menyfliksområdet klickar du på **Konfigurera plattformar** > **Android for Work**.
   4. I dialog rutan klickar du på **Konfigurera Android for Work i Intune-konsolen**. Intune-konsolen öppnas i webbläsaren.
   5. Använd dina autentiseringsuppgifter för Intune-administratören för att logga in på Intune-portalen.
   6. Klicka på **Konfigurera** för att öppna Google Plays Android for Work-webbplats.
   7. På Googles inloggnings sida anger du autentiseringsuppgifterna för Google-kontot från steg 1 och anger sedan företagets information.
3. När du återgår till Intune-portalen är Android for Work aktiverat och du har tre registrerings alternativ för Android for Work-enheter:
   - **Hantera alla enheter som Android** -(inaktive rad) alla Android-enheter, inklusive enheter som stöder Android for Work, registreras som konventionella Android-enheter
   - **Manage all devices as Android for Work** (Hantera alla enheter som Android for Work) – (Aktiverat) Alla enheter som stöder Android for Work registreras som Android for Work-enheter. Alla Android-enheter som inte stöder Android for Work registreras som konventionella Android-enheter.
   - **Hantera enheter som stöds för användare endast i de här grupperna som Android for Work** – (testning) gör att du kan rikta in dig på Android for Work-hantering till en begränsad uppsättning användare. Endast medlemmar i de valda grupperna som registrerar en enhet som har stöd för Android for Work registreras som Android for Work-enheter. Alla andra registreras som Android-enheter.
  
> [!NOTE]
> Ett känt problem förhindrar att **hanterade enheter som stöds för användare endast i de här grupperna som Android for Work** -alternativ fungerar som förväntat. Användarnas enheter i de angivna Azure AD-grupperna registreras som Android i stället för Android for Work. För att testa Android for Work måste du använda funktionen **hantera alla enheter som stöds som Android for Work**.


  Om du vill aktivera Android for Work-registrering måste du välja ett av de två nedre alternativen. Alternativet **Hantera enheter som stöds för användare endast i de här grupperna som Android for Work** kräver att du har Azure Active Directory säkerhets grupper konfigurerat först.

Du ser konto namnet och organisations namnet i Intune-portalen när bindningen är klar. i det här läget kan du stänga båda webbläsarna.

#### <a name="approve-and-deploy-android-for-work-apps"></a>Godkänn och distribuera Android for Work-appar
Följ de här stegen för att godkänna appar i Play for Work-butiken, synkronisera dem till Configuration Manager-konsolen och distribuera dem till hanterade Android for Work-enheter. Om du vill distribuera appar till användarnas arbets profiler måste du godkänna apparna i Play for Work och sedan synkronisera apparna med Configuration Manager-konsolen.

1. Öppna en webbläsare och gå till: https://play.google.com/work.
2. Logga in med det Google admin-konto som du har kopplat till din Intune-klient.
3. Bläddra efter appar som du vill distribuera i din miljö och klicka på **Godkänn** för var och en av dem.
4. Gå till **Administratörs** > **Översikt** > **Cloud Services** > **Android for Work** i Configuration Manager-konsolen och klicka på **Synkronisera**.
5. Vänta i upp till 10 minuter för appar att synkronisera och gå sedan till översikt över **program bibliotek** > **Översikt över** > **program hantering** > **licens information för Store-appar**.
6. Klicka på en app som har synkroniserats från spela upp för arbete och klicka sedan på **skapa program**.
7. Slutför guiden och klicka på **Stäng**.
8. Gå till **program bibliotek** > **Översikt** > program**hantering** > **program**, Välj en Android for Work-app och distribuera som vanligt.

Om du vill synkronisera Play for Work-appar med Configuration Manager måste du godkänna minst en app på webbplatsen Play for Work.

#### <a name="enroll-an-android-for-work-device"></a>Registrera en Android for Work-enhet
Hur du registrerar Android for Work-enheter liknar registrering för Android. Hämta och kör Företagsportal-appen för Android på din mobila enhet. Du uppmanas att skapa en arbets profil som en del av registrerings processen.  När arbets profilen har skapats måste du växla till den hanterade versionen av Företagsportal. Den hanterade Företagsportal är Taggad med en liten orange portfölj i det nedre högra hörnet.

#### <a name="create-and-deploy-a-configuration-item"></a>Skapa och distribuera ett konfigurations objekt
Android for Work har två inställnings grupper för konfigurations objekt:
- lösenordsinställning
- Arbetsprofil

Du kan konfigurera innehålls delning mellan arbets profiler, samt följande konfigurations objekt på enheter som kör Android 6 eller senare:
- Beteendet för appar som efterfrågar vissa behörigheter
- Om meddelanden för program i arbets profilen visas på Lås skärmen

Du kan prova detta genom att skapa ett konfigurations objekt via standard arbets flödet, välja **Android for Work** på sidan **Allmänt** och konfigurera inställningar för varje inställnings grupp, lägga till konfigurationsobjektet i en bas linje och distribuera som vanligt. De här inställningarna gäller endast för enheter som har registrerats som Android for Work och inte de som är registrerade som Android.

#### <a name="perform-selective-wipe"></a>Utför selektiv rensning
Enheter som har registrerats som Android for Work kan bara rensas selektivt eftersom du bara hanterar arbets profilen. Detta skyddar den personliga profilen från att rensas. Att utföra en selektiv rensning på en Android for Work-enhet tar bort arbets profilen, inklusive alla appar och data, och avregistrerar enheten.

Om du vill rensa en Android for Work-enhet selektivt, använder du den normala [selektiva rensnings processen](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe) i Configuration Manager-konsolen.

#### <a name="known-issues-for-android-for-work"></a>Kända problem för Android for Work
Om **du konfigurerar synkroniseringsschemat i Android for Work-e-postprofiler kan de inte distribueras** Ett av alternativen i ConfigMgr-gränssnittet för e-postprofiler för Android for Work är "schema". På andra plattformar gör det möjligt för administratören att konfigurera ett schema för synkronisering av e-post och andra e-postkonton till de mobila enheter som den distribueras till. Det fungerar dock inte för Android for Work-e-postprofiler och om du väljer andra alternativ än "inte konfigurerad" kommer profilen inte att distribueras till några enheter.
