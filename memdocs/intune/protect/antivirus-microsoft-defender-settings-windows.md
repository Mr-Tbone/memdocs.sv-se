---
title: Windows 10 Antivirus principinställningar för Microsoft Defender Antivirus för Intune | Microsoft Docs
description: Se en lista över inställningarna i Microsoft Defender Antivirus-profilen för Windows 10. Du kan konfigurera dessa inställningar som en del av antivirusprinciperna för slutpunktssäkerhet i Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: ff5c8208cb1ee9357c501a3c457bc346879b241d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88906709"
---
# <a name="settings-for-windows-10-microsoft-defender-antivirus-policy-in-microsoft-intune"></a>Inställningar för Windows 10 Microsoft Defender antivirusprinciper i Microsoft Intune

Visa inställningarna för antiviruspolicyn i Slutpunktssäkerhet som du kan konfigurera för profilen Microsoft Defender Antivirus för Windows 10 i Microsoft Intune som en del av [Endpoint Security-policyn](../protect/endpoint-security-policy.md).

## <a name="cloud-protection"></a>Molnskydd

Följande inställningar är tillgängliga för följande profiler:

- Microsoft Defender Antivirus

**Inställningar**:

- **Aktivera molnlevererat skydd**  
  CSP: [AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Som standard skickar Defender på Windows 10 Desktop-enheter information till Microsoft om eventuella problem som identifieras. Microsoft analyserar informationen för att lära sig mer om problem som påverkar dig och andra kunder och erbjuda bättre lösningar.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Nej** – Inställningen är inaktiverad. Enhetsanvändare kan inte ändra den här inställningen.
  - **Ja** – Molnlevererat skydd är aktiverat.  Enhetsanvändare kan inte ändra den här inställningen.

- **Nivå för molnlevererat skydd**  
  CSP: [CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Konfigurera hur aggressivt Defender Antivirus ska blockera och genomsöka misstänkta filer.
  - **Inte konfigurerad** (*standard*) – Standardnivå för blockering i Defender.
  - **Hög** – Aggressiv blockering av okända filer och optimering av klientprestanda, med större risk för falskt positiva resultat.
  - **Hög plus** – Aggressiv blockering av okända filer och tillämpning av ytterligare skyddsåtgärder som kan påverka klientprestandan.
  - **Nolltolerans** – Blockerar alla okända körbara filer.

- **Defender: utökad tidsgräns för moln i sekunder**  
  CSP: [CloudExtendedTimeout](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender Antivirus blockerar automatiskt misstänkta filer i 10 sekunder så att det kan genomsöka filerna i molnet för att kontrollera att de är säkra. Du kan lägga till upp till 50 ytterligare sekunder till tidsgränsen.

## <a name="microsoft-defender-antivirus-exclusions"></a>Microsoft Defender antivirusundantag

Följande inställningar är tillgängliga för följande profiler:

- Microsoft Defender Antivirus
- Microsoft Defender antivirusundantag

**Inställningar**:

För varje inställning i den här gruppen kan du expandera inställningen, välja **Lägg till**och sedan ange ett värde för undantaget.

- **Defender-processer som ska uteslutas**  
  CSP: [ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  Ange en lista över filer som har öppnats av processer som ska ignoreras vid en genomsökning. Själva processen undantas inte från sökningen.

- **Filnamnstillägg som ska undantas från genomsökningar och realtidsskydd**  
  CSP: [ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  Ange en lista över filnamnstillägg som ska ignoreras vid en genomsökning.

- **Defender-filer och mappar som ska uteslutas**  
  CSP: [ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  Ange en lista över filer och katalogvägar som ska ignoreras vid en genomsökning.

## <a name="real-time-protection"></a>Realtidsskydd

Följande inställningar är tillgängliga för följande profiler:

- Microsoft Defender Antivirus

**Inställningar**:

- **Starta realtidsskydd**  
  CSP: [AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  Kräv att Defender på Windows 10 Desktop-enheter ska använda funktionen för övervakning i realtid.
  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard
  - **Nej** – Inställningen är inaktiverad. Enhetsanvändare kan inte ändra den här inställningen.
  - **Ja** – Framtvinga användning av övervakning i realtid. Enhetsanvändare kan inte ändra den här inställningen.

- **Tillåt kontinuerligt skydd**  
  CSP: [AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935)

  Konfigurera virusskydd som hela tiden är aktivt, i stället för på begäran.

  - **Inte konfigurerad** (*standard*) – Den här principen ändrar inte statusen för den här inställningen på en enhet. Det befintliga statusen  på enheten är oförändrad.
  - **Nej** – Blockera åtkomstskydd på enheter. Enhetsanvändare kan inte ändra den här inställningen.
  - **Ja** – Åtkomstskydd är aktivt på enheterna.

- **Övervaka inkommande och utgående filer**  
  CSP: [Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  Konfigurera den här inställningen för att ange vilken NTFS-fil och programaktivitet som ska övervakas.
  - **Övervaka alla filer** (*standard*)
  - **Övervaka enbart inkommande filer**
  - **Övervaka enbart utgående filer**

- **Aktivera beteendeövervakning**  
  CSP: [AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  Som standard använder Defender på Windows 10 Desktop-enheter funktionen för beteendeövervakning.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Nej** – Inställningen är inaktiverad. Enhetsanvändare kan inte ändra den här inställningen.
  - **Ja** – Framtvinga användning av beteendeövervakning i realtid. Enhetsanvändare kan inte ändra den här inställningen.

- **Aktivera nätverksskydd**  
  CSP: [EnableNetworkProtection](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  Skydda enhetsanvändare som använder appar mot nätfiske, trojaner och skadligt innehåll från internet. Skyddet omfattar att webbläsare från tredje part hindras från att ansluta till farliga platser.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Nej** – Inställningen är inaktiverad. Enhetsanvändare kan inte ändra den här inställningen.
  - **Ja** – Nätverksskydd är aktiverat. Enhetsanvändare kan inte ändra den här inställningen.

- **Genomsök alla nedladdade filer och bifogade filer**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  Konfigurera Defender för att söka igenom alla nedladdade filer och bifogade filer.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Nej** – Inställningen är inaktiverad. Enhetsanvändare kan inte ändra den här inställningen.
  - **Ja** – Defender söker igenom alla nedladdade filer och bifogade filer. Enhetsanvändare kan inte ändra den här inställningen.

- **Genomsök skript som används i Microsoft-webbläsare**  
  CSP: [AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  Konfigurera Defender för att söka igenom skript.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Nej** – Inställningen är inaktiverad. Enhetsanvändare kan inte ändra den här inställningen.
  - **Ja** – Defender söker igenom skript. Enhetsanvändare kan inte ändra den här inställningen.

- **Genomsök nätverksfiler**  
  CSP: [AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  Konfigurera Defender för att söka igenom nätverksfiler.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Nej** – Inställningen är inaktiverad. Enhetsanvändare kan inte ändra den här inställningen.
  - **Ja** – Aktivera genomsökning av nätverksfiler. Enhetsanvändare kan inte ändra den här inställningen.

- **Genomsök e-post**  
  CSP: [AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Konfigurera Defender för att söka igenom inkommande e-post.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Nej** – Inställningen är inaktiverad. Enhetsanvändare kan inte ändra den här inställningen.
  - **Ja** – Aktivera genomsökning av e-post. Enhetsanvändare kan inte ändra den här inställningen.

## <a name="remediation"></a>Åtgärder

Följande inställningar är tillgängliga för följande profiler:

- Microsoft Defender Antivirus

**Inställningar**:

- **Antal dagar (0–90) som skadlig kod ska bevaras i karantän**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  Ange ett antal dagar från noll till 90 som systemet ska hålla kvar objekt i karantän innan de tas bort automatiskt. Värdet noll håller kvar objekten i karantän och tar inte bort dem automatiskt.

- **Medgivande till att skicka stickprov**  

  - **Ej konfigurerat** (*standard*)
  - **Skicka säkra exempel automatiskt**
  - **Fråga alltid**
  - **Skicka aldrig**
  - **Skicka alla exempel automatiskt**

- **Åtgärd som ska vidtas vid potentiellt oönskade appar**  
  CSP: [PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  Ange identifieringsnivå för potentiellt oönskade appar (PUA). Defender varnar användare när potentiellt oönskad programvara laddas ned eller försöker installeras på en enhet.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard, där PUA-skydd är AV.
  - **Inaktivera**
  - **Aktivera** – Identifierade objekt blockeras och visas i historiken tillsammans med andra hot.
  - **Granskningsläge** – Defender identifierar potentiellt oönskade program, men vidtar inga åtgärder. Du kan läsa information om vilka program som Windows Defender skulle ha vidtagit åtgärder mot genom att söka efter händelser som har skapats av Defender i Loggboken.

- **Åtgärder för identifierade hot**  
  CSP: [ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

  Ange den åtgärd som Defender ska vidta för identifierad skadlig kod baserat på hotnivån på den skadliga koden.
  
  Defender klassificerar skadlig kod som identifieras som en av följande allvarlighetsgrader:
  - **Låg allvarlighetsgrad**
  - **Måttligt hög allvarlighetsgrad**
  - **Hög allvarlighetsgrad**
  - **Mycket hög allvarlighetsgrad**

  Ange den åtgärd som ska vidtas för varje nivå. Standardvärdet för varje allvarlighetsgrad är *Inte konfigurerat*.

  - **Inte konfigurerat**
  - **Rensa** – Tjänsten försöker återställa filer och rensa dem.
  - **Karantän** – Flyttar filer till karantän.
  - **Ta bort** – Tar bort filer från enheten.
  - **Tillåt** – Tillåter filen och utför inte några andra åtgärder.
  - **Användardefinierad** – Enhetsanvändaren fattar beslutet om vilken åtgärd som ska vidtas.
  - **Blockera** – Blockerar filen från att köras.

## <a name="scan"></a>Genomsökning

Följande inställningar är tillgängliga för följande profiler:

- Microsoft Defender Antivirus

**Inställningar**:

- **Sök igenom arkivfiler**  
  CSP: [AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)

  Konfigurera Defender för att söka igenom arkivfiler, t. ex. ZIP-eller CAB-filer.

  - **Inte konfigurerad** (*standard*) – Inställningen återgår till klientens standardvärde, som är att söka igenom arkiverade filer, men användaren kan inaktivera den här inställningen.
Läs mer
  - **Nej** – Filarkiven genomsöks inte. Enhetsanvändare kan inte ändra den här inställningen.
  - **Ja** – Aktivera genomsökning av arkivfiler. Enhetsanvändare kan inte ändra den här inställningen.

- **Använd låg CPU-prioritet för schemalagda genomsökningar**  
  CSP: [EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  Konfigurera CPU-prioritet för schemalagda genomsökningar.
  - **Inte konfigurerad** (*standard*) – Inställningen återgår till systemstandard, där inga ändringar av processorprioriteten görs.
  - **Nej** – Inställningen är inaktiverad. Enhetsanvändare kan inte ändra den här inställningen.
  - **Ja** – Låg processorprioritet kommer att användas under schemalagda genomsökningar. Enhetsanvändare kan inte ändra den här inställningen.

- **Inaktivera fullständig komma ifatt-sökning**  
  CSP: [DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  Konfigurera komma ifatt-sökningar för schemalagda fullständiga genomsökningar. En komma ifatt-sökning är en genomsökning som initieras eftersom en regelbundet schemalagd genomsökning missades. Dessa schemalagda genomsökningar missas vanligtvis eftersom datorn stängdes av vid den schemalagda tiden.

  - **Inte konfigurerad** (*standard*) – Inställningen returneras till klientens standardvärde, vilket är att aktivera komma ifatt-sökningar för fullständiga genomsökningar, men användaren kan inaktivera dem.
  - **Nej** – Inställningen är inaktiverad. Enhetsanvändare kan inte ändra den här inställningen.
  - **Ja** – Komma ifatt-sökningar för schemalagda fullständiga genomsökningar verkställs och användaren kan inte inaktivera dem. Om en dator är offline under två på varandra följande schemalagda genomsökningar startas en komma ifatt-sökning nästa gång någon loggar in på datorn. Om ingen schemalagd genomsökning har konfigurerats kommer det inte att bli någon komma ifatt-sökning. Enhetsanvändare kan inte ändra den här inställningen.

- **Inaktivera komma ifatt-snabbsökning**  
  CSP: [DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  Konfigurera komma ifatt-sökningar för schemalagda snabbgenomsökningar. En komma ifatt-sökning är en genomsökning som initieras eftersom en regelbundet schemalagd genomsökning missades. Dessa schemalagda genomsökningar missas vanligtvis eftersom datorn stängdes av vid den schemalagda tiden.

  - **Inte konfigurerad** (*standard*) – Inställningen returneras till klientens standardvärde, vilket är att aktivera komma ifatt-sökningar för snabbsökningar, men användaren kan inaktivera dem.
  - **Nej** – Inställningen är inaktiverad. Enhetsanvändare kan inte ändra den här inställningen.
  - **Ja** – Komma ifatt-sökningar för schemalagda snabbgenomsökningar verkställs och användaren kan inte inaktivera dem. Om en dator är offline under två på varandra följande schemalagda genomsökningar startas en komma ifatt-sökning nästa gång någon loggar in på datorn. Om ingen schemalagd genomsökning har konfigurerats kommer det inte att bli någon komma ifatt-sökning. Enhetsanvändare kan inte ändra den här inställningen.

- **Gräns för processoranvändning under genomsökning**  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Ange som en procentandel från noll till 100 den genomsnittliga processorbelastningsfaktorn för Defender-genomsökningen.

- **Sök igenom anslutna nätverksenheter vid fullständig** genomsökning  
  CSP: [AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  Konfigurera Defender för att söka igenom mappade nätverksenheter.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard, som inaktiverar genomsökning av mappade nätverksenheter.
  - **Nej** – Inställningen är inaktiverad. Enhetsanvändare kan inte ändra den här inställningen.
  - **Ja** – Aktivera genomsökning av mappade nätverksenheter. Enhetsanvändare kan inte ändra den här inställningen.

- **Kör daglig snabbsökning**  
  CSP: [ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Välj tidpunkt på dagen då Defender-snabbskanningen ska köras.
  Denna inställning är **inte konfigurerad** som standard

- **Skanningstyp**  
  CSP: [ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045)

  Välj den typ av genomsökning som Defender ska köra.

  - **Inte konfigurerat** (*standard*)
  - **Snabbsökning**
  - **Fullständig genomsökning**

- **Veckodag schemalagd sökning ska köras**  
  - **Inte konfigurerat** (*standard*)

- **Tidpunkt på dagen då schemalagd sökning ska köras**  
  - **Inte konfigurerat** (*standard*)

- **Sök efter signaturuppdateringar innan du kör en genomsökning**  
  - **Inte konfigurerat** (*standard*)
  - **Nej**
  - **Ja**

## <a name="updates"></a>Uppdateringar

Följande inställningar är tillgängliga för följande profiler:

- Microsoft Defender Antivirus

**Inställningar**:

- **Ange hur ofta (0–24 timmar) sökning ska ske efter säkerhetsinsiktsuppdateringar**  
  CSP: [SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  Ange intervallet från noll till 24 (i timmar) som ska användas för att söka efter signaturer. Värdet noll resulterar innebär ingen kontroll för nya signaturer. Värdet 2 kommer att kontrollera varannan timme och så vidare.

- **Ange filresurser för nedladdning av definitionsuppdateringar**  
  CSP: [SignatureUpdateFallbackOrder](/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder)

  Hantera platser, t. ex. en UNC-filresurs, som en plats för källplatsen för nedladdningen för att hämta definitionsuppdateringar. När definitionsuppdateringarna har laddats ned från en angiven källa kommer de återstående källorna i listan inte att kontaktas.

  Du kan **lägga till** enskilda platser eller **importera** en lista över platser som en .csv-fil.

- **Ange källordning för nedladdning av definitionsuppdateringar**  
  CSP: [SignatureUpdateFileSharesSources](/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources)

  Ange i vilken ordning du vill kontakta källplatser som du har angett för att hämta definitionsuppdateringar. När definitionsuppdateringarna har laddats ned från en angiven källa kommer de återstående källorna i listan inte att kontaktas.

## <a name="user-experience"></a>Användarupplevelse

Följande inställningar är tillgängliga för följande profiler:

- Microsoft Defender Antivirus

**Inställningar**:

- **Tillåt användaråtkomst till Microsoft Defender-app**  
  CSP: [AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043)  

  - **Inte konfigurerad** (*standard*) – Inställningen återgår till klientens standardvärde där gränssnitt och aviseringar tillåts.
  - **Nej** – Användargränssnittet för Defender är inte tillgängligt och aviseringar visas inte.
  - **Ja**