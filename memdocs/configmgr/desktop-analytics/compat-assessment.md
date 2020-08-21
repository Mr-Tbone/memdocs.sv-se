---
title: Utvärdering av kompatibilitet
titleSuffix: Configuration Manager
description: Lär dig om kompatibilitetskontroll för Windows-appar och driv rutiner i Skriv bords analys.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: c9268514b43f4f728d3fff4715d4d71308a712f3
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699083"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>Kompatibilitetskontroll i Desktop Analytics

Uppgraderings utvärderingar i tidigare lösningar var generiska, till exempel: åtgärdat nödvändig eller åtgärdat tillgängligt. Den ger ingen visuell indikator för hur du prioriterar appar eller driv rutiner med problem eller uppgraderar insikter. Skriv bords analys ersätter den här funktionen med **risk för kompatibilitet**. Desktop Analytics visar bara utvärderingen för appar i vyn distribution för ett scenario före uppgradering. Den kategoriserar apparna baserat på insikter som Microsoft hämtar från de datorer som ingår i en aktuell distributions plan.

Skriv bords analys använder följande kategorier för kompatibilitetskontroll:

- **Låg**: tjänsten hittade inga signaler för att skicka den här appen till risk för en Windows-uppgradering. Det är sannolikt att du arbetar med mål operativ systemet i befintligt skick.

- **Medel**: Analytics visar att programmet kan ha nedsatt funktionalitet, även om det är troligt att reparationen är möjlig.

- **Hög**: programmet är nästan säkert att fungera under eller efter uppgraderingen. Det kan behöva åtgärdas.

- **Okänd**: appen bedömde inte. Det finns inga andra insikter som *MS-kända problem* eller *färdiga för Windows*.

I listan över appar eller driv rutins resurser i en distributions plan ser du det här värdet för varje till gång i kolumnen **Kompatibilitetsrapport** .

## <a name="app-risk-assessment"></a>Riskbedömning av appar

![Diagram över program risk utvärderings källor](media/app-risk-assessment-sources.png)

Det finns flera källor som Desktop Analytics använder för att generera utvärderings klassificeringen för program:

- [Kända problem med Microsoft](#microsoft-known-issues)
- [Redo för Windows](#ready-for-windows)
- [Avancerade insikter](#advanced-insights)

Du kan hitta utvärderingen för varje källa i appen i Skriv bords analys. I listan med app-tillgångar i en distributions plan väljer du en enskild app för att öppna dess egenskaper utfällt fönster. Du ser en övergripande rekommendations-och utvärderings nivå. Avsnittet **kompatibilitets riskfaktorer** visar Detaljer för dessa utvärderingar.

> [!TIP]
> Om fönstret programinformation inte visar kompatibilitetskontrollen kan det bero på att **information om program versioner** är av. Den är inaktive rad som standard och kombinerar alla versioner av appar med samma namn och utgivare. Tjänsten ger fortfarande kompatibilitets riskbedömningar för varje version. Aktivera program versions **information** om du vill se en riskbedömning av kompatibilitet för en speciell program version. Mer information finns i [planera till gångar](about-deployment-plans.md#plan-assets).

## <a name="microsoft-known-issues"></a>Kända problem med Microsoft

Desktop Analytics kontrollerar om det finns några kända problem i Microsoft app Compatibility-databasen. Den använder den här databasen för att fastställa eventuella befintliga kompatibilitetsinställningar för allmänt tillgängliga program från Microsoft eller andra utgivare. Den här kontrollen gäller endast för mål operativ systemet för den distributions plan som du väljer.

Följande problem visas i fönstret Egenskaper för app som **MS-kända problem**:

### <a name="asset-is-removed-during-upgrade"></a>Till gång tas bort under uppgraderingen

Windows upptäckte kompatibilitetsproblem med ett program eller en driv rutin. Till gången migreras inte till den nya versionen av operativ systemet. Ingen åtgärd krävs för att uppgraderingen ska kunna fortsätta. Installera en kompatibel version av programmet eller driv rutinen på den nya operativ system versionen.

<!-- 3594545 -->
Windows kan helt eller delvis ta bort dessa till gångar:

- Fullständig borttagning: installations programmet för Windows tar helt bort appen eller driv rutinen från enheten under uppgraderingen.
- Delvis borttagning: installations programmet för Windows tar delvis bort appen eller driv rutinen från enheten. Du måste avinstallera den manuellt när du har uppgraderat Windows.

I båda fallen kan användaren efter att du har uppgraderat Windows inte använda appen eller maskin varan som är associerad med driv rutinen.

Om du vill se den här rekommendationen i Skriv bords analys portalen:

1. I en distributions plan väljer du **Förbered pilot**.
1. Välj fliken **appar** .
1. Välj en app och Visa sedan riskfaktorer och rekommendationer för kompatibilitet i sido rutan.

[![Skärm bild av till gångs rekommendation i Desktop Analytics-portalen](media/3594545-app-removed.png)](media/3594545-app-removed.png#lightbox)

### <a name="blocking-upgrade"></a>Blockerar uppgradering

Windows har identifierat spärrnings problem och kan inte ta bort programmet under uppgraderingen. Det kanske inte fungerar på den nya versionen av operativ systemet. Ta bort programmet innan du uppgraderar. Installera om och testa det på den nya versionen av operativ systemet.

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>Blockerar uppgradering, men kan installeras om efter uppgraderingen

Programmet är kompatibelt med den nya OS-versionen, men migreras inte. Ta bort programmet innan du uppgraderar Windows. Installera om den på den nya operativ system versionen.

### <a name="blocking-upgrade-update-application-to-newest-version"></a>Blockerar uppgradering, uppdatera programmet till den senaste versionen

Den befintliga versionen av programmet är inte kompatibel med den nya OS-versionen och kommer inte att migreras. En kompatibel version av programmet är tillgänglig. Uppdatera programmet innan du uppgraderar.

### <a name="disk-encryption-blocking-upgrade"></a>Uppgradering av disk krypterings spärr

Programmets krypterings funktioner blockerar uppgraderingen. Inaktivera krypterings funktionen innan du uppgraderar Windows och aktivera den efter uppgraderingen.

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>Fungerar inte med nytt operativ system, men blockerar inte uppgradering

Programmet är inte kompatibelt med den nya OS-versionen men blockerar inte uppgraderingen. Ingen åtgärd krävs för att uppgraderingen ska kunna fortsätta. Installera en kompatibel version av programmet på den nya operativ system versionen.

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>Fungerar inte med nytt operativ system och blockerar uppgraderingen

Programmet är inte kompatibelt med den nya OS-versionen och kommer att blockera uppgraderingen. Ta bort programmet innan du uppgraderar. En kompatibel version av programmet kan vara tillgänglig.

### <a name="evaluate-application-on-new-os"></a>Utvärdera programmet på nytt operativ system

Windows kommer att migrera programmet, men det identifierade problem som kan påverka appens prestanda på den nya versionen av operativ systemet. Ingen åtgärd krävs för att uppgraderingen ska kunna fortsätta. Testa programmet på den nya operativ system versionen.

### <a name="may-block-upgrade-test-application"></a>Kan blockera uppgradering, testa program

Windows upptäckte problem som kan störa uppgraderingen, men behöver ytterligare undersökning. Testa programmets beteende under uppgraderingen. Om den blockerar uppgraderingen tar du bort den innan du uppgraderar. Installera sedan om det och testa på den nya operativ system versionen.

### <a name="multiple"></a>Flera

Flera problem påverkar programmet. Välj **fråga** för att se information om problem som upptäckts av Windows.

### <a name="reinstall-application-after-upgrading"></a>Installera om program efter uppgradering

Programmet är kompatibelt med den nya versionen av operativ systemet, men du måste installera om det när du har uppgraderat Windows. Uppgraderings processen tar bort programmet. Ingen åtgärd krävs för att uppgraderingen ska kunna fortsätta. Installera om programmet på den nya operativ system versionen.

### <a name="safeguards"></a>Skydd

<!-- 5746559 -->

Windows-kompatibilitetsproblem klassificerar vissa appar och driv rutiner med en *skydds*åtgärd, vilket kan leda till att Windows 10 Miss lyckas eller återställs. Windows kan också uppgraderas, men appen eller driv rutinen tas bort. Skriv bords analys kan nu hjälpa dig att identifiera dessa skydd i förväg, så att du kan åtgärda till gången innan du distribuerar uppdateringen.

1. Välj en distributions plan i Skriv bords analys portalen.

1. Välj **plan till gångar** på menyn och växla till fliken **appar** .

1. Filtrera kolumnen namn om du vill visa objekt med värden som innehåller ordet `Safeguard` . Välj resultatet om du vill visa mer information.

    > [!NOTE]
    > Den här posten är inte en riktig app som är installerad på dina enheter. Det är en plats hållare som hjälper dig att identifiera appar eller driv rutiner i din miljö med taggen för skydds kompatibilitet.

1. I avsnittet rekommendationer väljer du länken om du vill *veta mer*. Den här länken öppnar webbplatsen Windows med den aktuella listan över appar eller driv rutiner med skydds tag gen.

1. Jämför den aktuella publicerade listan med listan med till gångar i din miljö. Åtgärda eventuella problematiska appar eller driv rutiner genom att uppdatera till en kompatibel version.

[![Skärm bild av skydds appen i Desktop Analytics](media/5746559-safeguards.png)](media/5746559-safeguards.png#lightbox)

## <a name="ready-for-windows"></a>Redo för Windows

Tillämpnings status baseras på information från kommersiella enheter som delar data med Microsoft. Statusen är integrerad med support satser från program varu leverantörer.

Skriv bords analys ger tillämpnings status för varje version av en till gång som finns på kommersiella enheter. Den här statusen omfattar inte data från konsument enheter eller enheter som inte delar data. Statusen är kanske inte representativ för införande frekvensen på alla Windows 10-enheter.

Möjliga kategorier är:

- **Starkt infört**: minst 100 000 kommersiella Windows 10-enheter har installerat den här appen.

- **Antog**: minst 10 000 kommersiella Windows 10-enheter har installerat den här appen.

- **Otillräckliga data**: det finns för få kommersiella Windows 10-enheter som delar information för den här appen för Microsoft att kategorisera dess införande.

- **Kontakta utvecklaren**: det kan finnas kompatibilitetsproblem med den här versionen av appen. Microsoft rekommenderar att du kontaktar program leverantören och lär dig mer.

- **Okänd**: det finns ingen tillgänglig information för den här versionen av programmet. Information kan vara tillgänglig för andra versioner av programmet.

### <a name="support-statement"></a>Support instruktion

Om program varu leverantören stöder en eller flera versioner av det här programmet på Windows 10 visas den här instruktionen i fönstret Egenskaper för app. I avsnittet kompatibilitets riskfaktorer tittar du på **support instruktionen**.

## <a name="advanced-insights"></a>Avancerade insikter

Desktop Analytics kan också identifiera problem med hjälp av följande ytterligare insikter:

### <a name="adopted-version-available"></a>Antog version tillgänglig

Det finns en annan version av den här appen som är mycket antagen av andra kunder. Den här signalen använder implementerings data från Windows-eko systemet. Om det finns några uppgraderings block med din nuvarande version kan du överväga att distribuera den alternativa versionen i stället. Information om hur du hittar alternativa program versioner finns i program hälsa under "förbereda produktion".

### <a name="driver-dependency"></a>Driv rutins beroende

Appen är beroende av en driv rutin. Skriv bords analys rekommenderar appen för pilot testning att upptäcka eventuella regressioner. Om du har problem kan du kontakta utgivaren för att begära en version som är kompatibel med Windows 10.

### <a name="additional-insights"></a>Ytterligare insikter

<!-- 4021225 -->
När du uppdaterar Configuration Manager-platsen och-klienterna till version 1906, rapporterar klienter även dessa ytterligare insikter när diagnostikdata är inställd på utökad begränsad:

> [!Important]  
> För att dra full nytta av nya Configuration Manager funktioner kan du även uppdatera klienter till den senaste versionen när du har uppdaterat platsen. Det här scenariot fungerar inte förrän klient versionen också är den senaste.

#### <a name="16-bit-apps"></a>16-bitars appar

Ta bort alla 16-bitars komponenter från program och Ersätt med 32-bitars eller 64-bitars motsvarigheter. Mer information finns i [Developer-artikeln för Windows Vista och Windows Server 2008: Application Compatibility Cookbook](/previous-versions/aa480152\(v=msdn.10\)).

Det andra alternativet är att aktivera NT Virtual DOS Machine (NTVDM) för support i Windows 10.

#### <a name="requires-admin-privileges"></a>Kräver administratörs behörighet

Appen kräver att användaren har administrativ åtkomst till enheten. Använd ett app-manifest för de här apparna som kräver administratörs behörighet. Mer information finns i [skapa och bädda in ett applikations manifest](/previous-versions/bb756929\(v=msdn.10\)).

Skriv bords analys rekommenderar appen för pilot testning att upptäcka eventuella regressioner.

#### <a name="java-dependency"></a>Java-beroende

Många Java-program förlitar sig på en separat installerad Java Runtime Environment (JRE). Även om äldre JRE-versioner kan fortsätta att fungera i Windows 10, stöder Oracle bara de senaste JRE-versionerna. Om du använder en äldre JRE som inte stöds kan säkerhets problem uppstå. Kontrol lera att programmet körs på de senaste JRE-versionerna.

#### <a name="not-dpi-aware"></a>Inte DPI-medveten

Appen kan ha visnings problem med avancerade skärm lösningar i Windows 10. Använd ett app-manifest för att undvika problem med hög DPI-upplösning. Mer information finns i [program manifest](/windows/desktop/SbsCs/application-manifests).

Skriv bords analys rekommenderar appen för pilot testning att upptäcka eventuella regressioner.

#### <a name="silverlight-framework"></a>Silverlight-ramverk

Microsoft rekommenderar att icke-webbläsarbaserade appar inte använder Silverlight. Supportens slutdatum för Silverlight 5 är oktober 2021.

De flesta aktuella webbläsare stöder inte Silverlight.

| Webbläsare | Support |
|---------|---------|
| Google Chrome | Supportens slut: september 2015 |
| Firefox | Supportens slut: mars 2017 |
| Microsoft Edge | Det finns inget tillgängligt plugin-program |

Skriv bords analys rekommenderar appen för pilot testning att upptäcka eventuella regressioner.

#### <a name="net-framework-1011"></a>.NET Framework 1.0/1.1

.NET Framework version 1,0 stöds inte i Windows 10. Version 1,1 är inte kompatibel med Windows 10. Om appen kommer från en utgivare från tredje part kontaktar du leverantören för att begära en version som är kompatibel med Windows 10. Annars kan du utveckla programmet för att använda en version av .NET som stöds.

#### <a name="net-framework-2030"></a>.NET Framework 2.0/3.0

.NET 2,0-och 3,5-ramverk stöds i Windows 10. Du kan behöva aktivera Windows-funktionen. Mer information finns i [installera .NET Framework 3,5 på Windows 10](/dotnet/framework/install/dotnet-35-windows-10).

#### <a name="ui-access"></a>GRÄNSSNITTs åtkomst

Program med UI-åtkomst kan kringgå användar gränssnittets kontroll nivåer för att enhetens indata till högre privilegierade fönster på Skriv bordet. Använd endast den här inställningen för teknik program för användar gränssnitt.

Om du inte använder hjälpmedels funktionerna i appen ställer du in flaggan UI Access i app-manifestet på falskt. Mer information finns i [skapa och bädda in ett applikations manifest](/previous-versions/bb756929\(v=msdn.10\)).

Skriv bords analys rekommenderar appen för pilot testning att upptäcka eventuella regressioner.

## <a name="driver-risk-assessment"></a>Bedömning av driv rutins risk

Desktop Analytics visar också och grupper efter tillgänglighet för alla driv rutiner som inte migreras till operativ system versionen.

Du hittar utvärderingen av driv rutinen i Skriv bords analys. I listan över driv rutins resurser i en distributions plan väljer du en enskild driv rutin för att öppna dess egenskaper utfällt fönster. Du ser en övergripande rekommendations-och utvärderings nivå. Avsnittet **kompatibilitets riskfaktorer** visar Detaljer för dessa utvärderingar.

| Tillgänglighet för driv rutin | Krävs åtgärd? | Vad det innebär | Vägledning |
|---------------------|------------------|---------------|----------|
| Tillgänglig i box | Nej, endast för kännedom | Den aktuella installerade versionen av ett program eller en driv rutin migreras inte till den nya versionen av operativ systemet. En kompatibel version installeras med den nya operativ system versionen. | Ingen åtgärd krävs för att uppgraderingen ska kunna fortsätta. |
| Importera från Windows Update | Ja | Den aktuella installerade versionen av en driv rutin migreras inte till den nya versionen av operativ systemet. En kompatibel version är tillgänglig från Windows Update. | Om datorn automatiskt tar emot uppdateringar från Windows Update krävs ingen åtgärd. Annars kan du importera en ny driv rutin från Windows Update när du har uppgraderat Windows. |
| Tillgänglig i kartong och från Windows Update | Ja | Den aktuella installerade versionen av en driv rutin migreras inte till den nya versionen av operativ systemet. Även om en ny driv rutin installeras under uppgraderingen, är en nyare version tillgänglig från Windows Update. | Om datorn automatiskt tar emot uppdateringar från Windows Update krävs ingen åtgärd. Annars kan du importera en ny driv rutin från Windows Update när du har uppgraderat Windows. |
| Kontrol lera med leverantören | Ja | Driv rutinen kommer inte att migrera till den nya versionen av operativ systemet och skriv bords analys kan inte hitta en kompatibel version. | För en lösning kontrollerar du med den oberoende maskin varu leverantören (IHV) som tillverkar driv rutinen eller OEM-tillverkaren (Original Equipment Manufacturer) som tillhandahöll enheten. |

## <a name="see-also"></a>Se även

FastTrack Center-förmånen för Windows 10 ger åtkomst till **Desktop-appen**. Den här förmånen är en ny tjänst som är utformad för att åtgärda problem med Windows 10 och Microsoft 365 appar för företags kompatibilitet. Mer information finns i [Desktop app garanterar](/fasttrack/win-10-desktop-app-assure).