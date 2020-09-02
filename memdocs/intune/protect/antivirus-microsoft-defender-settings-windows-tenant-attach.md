---
title: Windows 10 Antivirus principinställningar för Microsoft Defender Antivirus för Intune för klientanslutna enheter | Microsoft Docs
description: Se en lista över inställningarna i Microsoft Defender Antivirus-profilen för Windows 10-enheter som hanteras av Configuration Manager. Du kan konfigurera dessa inställningar som en del av antivirusprinciperna för slutpunktssäkerhet i Microsoft Intune när du har konfigurerat klientanslutning för Configuration Manager.
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
ms.openlocfilehash: 3bb1d4806271ab40c60f0ad419e4e708d36bbc97
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194131"
---
# <a name="settings-for-microsoft-defender-antivirus-policy-for-tenant-attached-devices-in-microsoft-intune"></a>Inställningar för Microsoft Defender Antivirus för Intune för klientanslutna enheter i Microsoft Intune

Visa inställningarna för Microsoft Defender Antivirus som du kan hantera med profilen **Microsoft Defender Antivirus-princip (ConfigMgr)** från Intune. Profilen är tillgänglig när du konfigurerar Intune [Endpoint Security Antivirus-principen](../protect/endpoint-security-antivirus-policy.md) och principen distribueras till enheter som du hanterar med Configuration Manager när du har konfigurerat scenariot [klientkoppling](../protect/tenant-attach-intune.md).

## <a name="cloud-protection"></a>Molnskydd

- **Aktivera molnlevererat skydd**  
  CSP: [AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Som standard skickar Defender på Windows 10 Desktop-enheter information till Microsoft om eventuella problem som identifieras. Microsoft analyserar informationen för att lära sig mer om problem som påverkar dig och andra kunder och erbjuda bättre lösningar.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Inte tillåtet.** Inaktiverar Microsoft Active Protection Service.
  - **Tillåts.**  Inaktiverar Microsoft Active Protection Service.

- **Nivå för molnlevererat skydd**  
  CSP: [CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Konfigurera hur aggressivt Defender Antivirus ska blockera och genomsöka misstänkta filer.
  - **Inte konfigurerad** (*standard*) – Standardnivå för blockering i Defender.
  - **Hög** – Aggressiv blockering av okända filer och optimering av klientprestanda, med större risk för falskt positiva resultat.
  - **Hög plus** – Aggressiv blockering av okända filer och tillämpning av ytterligare skyddsåtgärder som kan påverka klientprestandan.
  - **Nolltolerans** – Blockerar alla okända körbara filer.

- **Defender: utökad tidsgräns för moln i sekunder**  
  CSP: [CloudExtendedTimeout](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender Antivirus blockerar automatiskt misstänkta filer i 10 sekunder så att det kan genomsöka filerna i molnet för att kontrollera att de är säkra. Med den här inställningen kan du lägga till upp till 50 ytterligare sekunder till tidsgränsen.

## <a name="microsoft-defender-antivirus-exclusions"></a>Microsoft Defender antivirusundantag

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

- **Starta realtidsskydd**  
  CSP: [AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  Kräv att Defender på Windows 10 Desktop-enheter ska använda funktionen för övervakning i realtid.
  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard
  - **Inte tillåtet.** Inaktiverar tjänsten för övervakning i realtid.
  - **Tillåts.** Aktiverar och kör tjänsten för övervakning i realtid.

- **Tillåt kontinuerligt skydd**  
  CSP: [AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935)

  Konfigurera virusskydd som hela tiden är aktivt, i stället för på begäran.

  - **Inte konfigurerad** (*standard*) – Den här principen ändrar inte statusen för den här inställningen på en enhet. Det befintliga statusen  på enheten är oförändrad.
  - **Inte tillåtet.** Inaktiverar tjänsten för övervakning i realtid.
  - **Tillåts.**

- **Övervaka inkommande och utgående filer**  
  CSP: [Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  Konfigurera den här inställningen för att ange vilken NTFS-fil och programaktivitet som ska övervakas.
  - **Övervaka alla filer (dubbelriktat).** (*standard*)
  - **Övervaka inkommande filer.**
  - **Övervaka utgående filer.**

- **Aktivera beteendeövervakning**  
  CSP: [AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  Som standard använder Defender på Windows 10 Desktop-enheter funktionen för beteendeövervakning.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Inte tillåtet.** Inaktiverar beteendeövervakning.
  - **Tillåts.** Aktiverar beteendeövervakning i realtid.

- **Tillåt intrångsskyddssystem**  
  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Inte tillåtet.**
  - **Tillåts.**

- **Genomsök alla nedladdade filer och bifogade filer**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  Konfigurera Defender för att söka igenom alla nedladdade filer och bifogade filer.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Inte tillåtet.**
  - **Tillåts.**

- **Genomsök skript som används i Microsoft-webbläsare**  
  CSP: [AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  Konfigurera Defender för att söka igenom skript.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Inte tillåtet.**
  - **Tillåts.**

- **Genomsök nätverksfiler**  
  CSP: [AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  Konfigurera Defender för att söka igenom nätverksfiler.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Inte tillåtet.** Inaktiverar genomsökning av nätverksfiler.
  - **Tillåts.** Genomsöker nätverksfiler.

- **Genomsök e-post**  
  CSP: [AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Konfigurera Defender för att söka igenom inkommande e-post.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Inte tillåtet.** Stänger av genomsökning av e-post.
  - **Tillåts.** Aktiverar genomsökning av e-post.

## <a name="remediation"></a>Åtgärder

- **Antal dagar (0–90) som skadlig kod ska bevaras i karantän**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  Ange ett antal dagar från noll till 90 som systemet ska hålla kvar objekt i karantän innan de tas bort automatiskt. Värdet noll håller kvar objekten i karantän och tar inte bort dem automatiskt.

- **Medgivande till att skicka stickprov**  

  - **Ej konfigurerat** (*standard*)
  - **Fråga alltid.**
  - **Skicka säkra exempel automatiskt.**
  - **Skicka aldrig.**
  - **Skicka alla exempel automatiskt.**

- **Åtgärd som ska vidtas vid potentiellt oönskade appar**  
  CSP: [PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  Ange identifieringsnivå för potentiellt oönskade appar (PUA). Defender varnar användare när potentiellt oönskad programvara laddas ned eller försöker installeras på en enhet.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard, där PUA-skydd är AV.
  - **Skydd mot potentiellt oönskade program av.** Windows Defender skyddar inte mot oönskade program.
  - **Skydd mot potentiellt oönskade program på.** Identifierade objekt blockeras. Dessa objekt visas i historiken tillsammans med andra hot.
  - **Granskningsläge.** Defender identifierar potentiellt oönskade program men vidtar inga åtgärder. Du kan läsa information om vilka program som Windows Defender skulle ha vidtagit åtgärder mot genom att söka efter händelser som har skapats av Defender i Loggboken.

- **Skapa en systemåterställningspunkt innan datorerna rensas**  
  - **Ja** (*standard*)
  - **Nej**
  - **Inte konfigurerat**

- **Åtgärder för identifierade hot**  
  CSP: [ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

  Ange den åtgärd som Defender ska vidta för identifierad skadlig kod baserat på hotnivån på den skadliga koden.
  
  Defender klassificerar skadlig kod som identifieras som en av följande allvarlighetsgrader:
  - **Lågt hot**
  - **Måttligt hot**
  - **Högt hot**
  - **Allvarligt hot**

  Ange den åtgärd som ska vidtas för varje nivå. Standardvärdet för varje allvarlighetsgrad är *Inte konfigurerat*.

  - **Ej konfigurerat** (*standard*)
  - **Rensa** – Tjänsten försöker återställa filer och rensa dem.
  - **Karantän** – Flyttar filer till karantän.
  - **Ta bort** – Tar bort filer från enheten.
  - **Tillåt** – Tillåter filen och utför inte några andra åtgärder.
  - **Användardefinierad** – Enhetsanvändaren fattar beslutet om vilken åtgärd som ska vidtas.
  - **Blockera** – Blockerar filen från att köras.

## <a name="scan"></a>Genomsökning

- **Sök igenom arkivfiler**  
  CSP: [AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)

  Konfigurera Defender för att söka igenom arkivfiler, t. ex. ZIP-eller CAB-filer.

  - **Inte konfigurerad** (*standard*) – Inställningen återgår till klientens standardvärde, som är att söka igenom arkiverade filer, men användaren kan inaktivera genomsökningen.
Läs mer
  - **Tillåts inte** Inaktiverar genomsökning av arkiverade filer.
  - **Tillåts.** Söker igenom arkivfiler.

- **Använd låg CPU-prioritet för schemalagda genomsökningar**  
  CSP: [EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  Konfigurera CPU-prioritet för schemalagda genomsökningar.
  - **Inte konfigurerad** (*standard*) – Inställningen återgår till systemstandard, där inga ändringar av processorprioriteten görs.
  - **Disabled** (Inaktiverat)
  - **Aktiverad**

- **Inaktivera fullständig komma ifatt-sökning**  
  CSP: [DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  Konfigurera komma ifatt-sökningar för schemalagda fullständiga genomsökningar. En komma ifatt-sökning är en genomsökning som initieras eftersom en regelbundet schemalagd genomsökning missades. Dessa schemalagda genomsökningar missas vanligtvis eftersom datorn stängdes av vid den schemalagda tiden.

  - **Inte konfigurerad** (*standard*) – Inställningen returneras till klientens standardvärde, vilket är att aktivera komma ifatt-sökningar för fullständiga genomsökningar, men användaren kan inaktivera dem.
  - **Disabled** (Inaktiverat)
  - **Aktiverad**

- **Inaktivera komma ifatt-snabbsökning**  
  CSP: [DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  Konfigurera komma ifatt-sökningar för schemalagda snabbgenomsökningar. En komma ifatt-sökning är en genomsökning som initieras eftersom en regelbundet schemalagd genomsökning missades. Dessa schemalagda genomsökningar missas vanligtvis eftersom datorn stängdes av vid den schemalagda tiden.

  - **Inte konfigurerad** (*standard*) – Inställningen returneras till klientens standardvärde, vilket är att aktivera komma ifatt-sökningar för snabbsökningar, men användaren kan inaktivera dem.
  - **Disabled** (Inaktiverat)
  - **Aktiverad**

- **CPU-användningsgräns (0–100 procent) per sökning**  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Ange som en procentandel från noll till 100 den genomsnittliga processorbelastningsfaktorn för Defender-genomsökningen.

- **Låt mappade nätverksdrivrutiner genomsökas vid fullständig genomsökning**  
  CSP: [AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  Konfigurera Defender för att söka igenom mappade nätverksenheter.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard, som inaktiverar genomsökning av mappade nätverksenheter.
  - **Inte tillåtet.** Inaktiverar genomsökning på mappade nätverksenheter.
  - **Tillåts.** Söker igenom mappade nätverksenheter.

- **Kör daglig snabbsökning**  
  CSP: [ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Välj tidpunkt på dagen då Defender-snabbskanningen ska köras.
  Som standard är detta alternativ **Inte konfigurerat**

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
  - **Disabled** (Inaktiverat)
  - **Aktiverad**

- **Slumpgenerera starttiderna för schemalagd genomsökning och säkerhetsinsiktsuppdatering**  
  -**Inte konfigurerat** (*standard*) -**Ja**
  -**Nej**

- **Genomsök flyttbara enheter vid fullständig genomsökning**
  - **Inte konfigurerat** (*standard*)
  - **Inte tillåtet.** Inaktiverar sökning på flyttbara enheter.
  - **Tillåts.** Sök igenom flyttbara enheter.

## <a name="updates"></a>Uppdateringar

- **Ange hur ofta (0–24 timmar) sökning ska ske efter säkerhetsinsiktsuppdateringar**  
  CSP: [SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  Ange intervallet från noll till 24 (i timmar) som ska användas för att söka efter signaturer. Värdet noll resulterar innebär ingen kontroll för nya signaturer. Värdet 2 kommer att kontrollera varannan timme och så vidare.

- **Återställningsordning för signaturuppdatering (enhet)**

- **Signaturuppdatering för filresurskällor (enhet)**

- **Plats för säkerhetsinsikter (enhet)**  

## <a name="user-experience"></a>Användarupplevelse

- **Blockera användaråtkomst till Microsoft Defender-app**  
  - **Inte konfigurerat** (*standard*)
  - **Inte tillåtet.** Förhindrar användare från att få åtkomst till användargränssnittet.
  - **Tillåts.** Låter användare få åtkomst till användargränssnittet.

- **Visa meddelanden på klientdatorn när användaren behöver göra en fullständig genomsökning, uppdatera säkerhetsinsikter eller köra Windows Defender Offline**  
  - **Inte konfigurerat** (*standard*)
  - **Ja**
  - **Nej**

- **Inaktivera användargränssnittet på klientdatorn**  
  - **Inte konfigurerat** (*standard*)
  - **Ja**
  - **Nej**

- **Låt användare visa fullständiga historikresultat**
  - **Inte konfigurerat** (*standard*)
  - **Ja**
  - **Nej**