---
title: Inställningar för minskning av attackytan i slutpunktssäkerheten i Intune | Microsoft Docs
description: Inställningar för policyn Minskning av attackytan i slutpunktssäkerheten i Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/06/2020
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
ms.openlocfilehash: ac5b4685249ffa46be63e9ad55ca6067edec1b03
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022406"
---
# <a name="attack-surface-reduction-policy-settings-for-endpoint-security-in-intune"></a>Inställningar för policyn Minskning av attackytan i slutpunktssäkerheten i Microsoft Intune

Visa de inställningar du kan konfigurera i profiler för policyn *Minskning av attackytan* i noden Endpoint Security i Intune inom ramen för en [Endpoint Security-policy](../protect/endpoint-security-policy.md).

Plattformar och profiler som stöds:

- **Windows 10 och senare**:
  - Profil: **App- och webbläsarisolering**
  - Profil: **Webbskydd**
  - Profil: **Programregleringstyp**
  - Profil: **Regler för att minska attackytan**
  - Profil: **Enhetskontroll**
  - Profil: **Sårbarhetsskydd**

## <a name="app-and-browser-isolation-profile"></a>Profilen App- och webbläsarisolering

### <a name="app-and-browser-isolation"></a>App- och webbläsarisolering

- **Aktivera Application Guard för Edge (alternativ)**  
  CSP: [AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)

  - **Ej konfigurerat** (*standard*)
  - **Aktiverat för Microsoft Edge** – Application Guard öppnar icke-godkända webbplatser i en Hyper-V-virtualiserad webbläsarcontainer.

  Följande inställningar är tillgängliga när du anger *Aktiverat för Microsoft Edge*:
  
  - **Funktionssätt för Urklipp**  
    CSP: [ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    Välj vilka kopierings- och inklistringsåtgärder som ska tillåtas från den lokala datorn och en virtuell Application Guard-webbläsare.
    - **Ej konfigurerat** (*standard*)
    - **Blockera kopiera och klistra in mellan dator och webbläsare**
    - **Tillåt endast kopiera och klistra in från webbläsare till dator**
    - **Tillåt endast kopiera och klistra in från dator till webbläsare**
    - **Tillåt kopiera och klistra in mellan dator och webbläsare**

  - **Blockera externt innehåll från webbplatser som inte godkänts av företaget**  
    CSP: [BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Ej konfigurerat** (*standard*)
    - **Ja** – Blockera inläsning av innehåll från webbplatser som inte är godkända.

  - **Samla in loggar för händelser som inträffar i en Application Guard-webbläsarsession**  
    CSP: [AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)

    - **Ej konfigurerat** (*standard*)
    - **Ja** – Samla in loggar för händelser som inträffar under en virtuell Application Guard-webbläsarsession.

  - **Tillåt att användargenererade webbläsardata sparas**  
    CSP: [AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)

    - **Ej konfigurerat** (*standard*)
    - **Ja** – Tillåt att användardata som skapas under en virtuell Application Guard-webbläsarsession sparas. Exempel på användardata är lösenord, favoriter och cookies.

  - **Aktivera maskinvarubaserad grafikacceleration**  
    CSP: [AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)

    - **Ej konfigurerat** (*standard*)
    - **Ja** – Använd en virtuell grafikprocessor till att läsa in grafikintensiva webbplatser snabbare i den virtuella Application Guard-webbläsarsessionen.

  - **Tillåt att användare laddar ned filer till värden**  
    CSP: [SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)

    - **Ej konfigurerat** (*standard*)
    - **Ja** – Låt användare ladda ned filer från den virtuella webbläsaren till värdoperativsystemet.

- **Application Guard: tillåt utskrift på lokala skrivare**  

  - **Ej konfigurerat** (*standard*)
  - **Ja** – Tillåt utskrift på lokala skrivare.

- **Application Guard: tillåt utskrift på nätverksskrivare**  

  - **Ej konfigurerat** (*standard*)
  - **Ja** – Tillåt utskrift på nätverksskrivare.

- **Application Guard: tillåt utskrift i PDF**  

  - **Ej konfigurerat** (*standard*)
  - **Ja** – Tillåt utskrift i PDF-format.

- **Application Guard: tillåt utskrift i XPS**  

  - **Ej konfigurerat** (*standard*)
  - **Ja** – Tillåt utskrift i XPS-format.

- **Princip för nätverksisolering i Windows**  
  
  - **Ej konfigurerat** (*standard*)
  - **Ja** – Konfigurera policy för nätverksisolering i Windows.  
  
  När värdet är *Ja* kan du konfigurera följande inställningar.

  - **IP-intervall**  
    Expandera listrutan, välj **Lägg till** och ange sedan en *undre adress* och en *övre adress*.

  - **Molnresurser**  
    Expandera listrutan, välj **Lägg till** och ange sedan en *IP-adress eller FQDN* och en *Proxy*.

  - **Nätverksdomäner**  
   Expandera listrutan, välj **Lägg till** och ange sedan *Nätverksdomäner*.

  - **Proxyservrar**  
    Expandera listrutan, välj **Lägg till** och ange sedan *Proxyservrar*.

  - **Interna proxyservrar**  
    Expandera listrutan, välj **Lägg till** och ange sedan *Interna proxyservrar*.

  - **Neutrala resurser**  
    Expandera listrutan, välj **Lägg till** och ange sedan *Neutrala resurser*.

  - **Avaktivera automatisk identifiering av andra företags proxyservrar**  
    - **Ej konfigurerat** (*standard*)
    - **Ja** – Avaktivera automatisk identifiering av andra företags proxyservrar.

  - **Avaktivera automatisk identifiering av andra företags IP-intervall**  
    - **Ej konfigurerat** (*standard*)
    - **Ja** – Avaktivera automatisk identifiering av andra företags IP-intervall.

## <a name="web-protection-profile"></a>Profilen Webbskydd

### <a name="web-protection"></a>Webbskydd

- **Aktivera nätverksskydd**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Inte konfigurerat** (*standard*) – Inställningen återgår till Windows standardvärde, som är inaktiverad.
  - **Användardefinierad**
  - **Aktivera** – Nätverksskydd är aktiverat för alla användare i systemet.
  - **Gransknings läge** – Användare blockeras inte från farliga domäner och Windows-händelser höjs i stället.

- **Require SmartScreen for Microsoft Edge** (Kräv SmartScreen för Microsoft Edge)  
  CSP: [Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Ja** – Använd SmartScreen till att skydda användarna mot potentiella nätfiskeförsök och skadlig programvara.
  - **Ej konfigurerat** (*standard*)

- **Block malicious site access** (Blockera åtkomst till skadliga webbplatser)  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Ja** – Förhindra att användare ignorerar varningar från Microsoft Defender SmartScreen Filter och att de går till webbplatsen.
  - **Ej konfigurerat** (*standard*)

- **Block unverified file download** (Blockera nedladdning av overifierade filer)  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Ja** – Förhindra att användare ignorerar varningar från Microsoft Defender SmartScreen Filter och att de laddar ned okontrollerade filer.
  - **Ej konfigurerat** (*standard*)

## <a name="application-control-profile"></a>Profilen Programreglering

### <a name="microsoft-defender-application-control"></a>Microsoft Defender Application Control

- **Programreglering med applåsning**  
  - **Ej konfigurerat** (*standard*)
  - **Tvinga komponenter och Store-appar**
  - **Granska komponenter och Store-appar**
  - **Tvinga komponenter, Store-appar och Smartlocker**
  - **Granska komponenter, Store-appar och Smartlocker**

- **Blockera användare från att ignorera SmartScreen-varningar**  
  [PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  - **Inte konfigurerat** (*standard*) – Användare kan ignorera SmartScreen-varningar för filer och skadliga appar.
  - **Ja** – SmartScreen är aktiverat och användare kan inte kringgå varningar för filer eller skadliga appar.


- **Aktivera Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Inte konfigurerat** (*standard*) – Inställningen återgår till Windows standardvärde som är att aktivera SmartScreen, men användare kan ändra inställningen. Om du vill inaktivera SmartScreen använder du en anpassad URI.
  - **Ja** – Framtvinga användning av SmartScreen för alla användare.

## <a name="attack-surface-reduction-rules-profile"></a>Profilen Regler för att minska attackytan

### <a name="attack-surface-reduction-rules"></a>Regler för att minska attackytan

- **Blockera stöld av autentiseringsuppgifter från det lokala säkerhetsundersystemet i Windows (lsass.exe)**  
  <!-- Defender ATP security baseline, Device configuration Endpoint protection profile -->
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=874499)

  Den här regeln för att minska attackytan styrs via följande GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Inte konfigurerat** (*standard*) – Inställningen återgår till Windows standardvärde, som är av.
  - **Användardefinierad**
  - **Aktivera** – Försök att stjäla autentiseringsuppgifter via lsass.exe blockeras.
  - **Gransknings läge** – Användare blockeras inte från farliga domäner och Windows-händelser höjs i stället.

- **Blockera Adobe Reader från att skapa underordnade processer**  
  [Minska attackytan med regler för minskning av attackytan](https://go.microsoft.com/fwlink/?linkid=853979)
  
  Den här ASR-regeln styrs via följande GUID: 7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c
  - **Inte konfigurerat** (*standard*) – Windows standardvärde återställs, som är att inte blockera skapandet av underordnade processer.
  - **Användardefinierad**
  - **Aktivera** – Adobe Reader får inte skapa underordnade processer.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera underordnade processer.

- **Blockera Office-program från att infoga kod i andra processer**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=872974)

  Den här ASR-regeln styrs via följande GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Inte konfigurerat** (*standard*) – Inställningen återgår till Windows standardvärde, som är av.
  - **Blockera** – Office-program blockeras från att infoga kod i andra processer.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.

- **Blockera Office-program från att skapa körbart innehåll**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=872975)

  Den här ASR-regeln styrs via följande GUID: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Inte konfigurerat** (*standard*) – Inställningen återgår till Windows standardvärde, som är av.
  - **Blockera** – Office-program får inte skapa körbart innehåll.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.

- **Blockera Office-program från att skapa underordnade processer**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=872976)

  Den här ASR-regeln styrs via följande GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Inte konfigurerat** (*standard*) – Inställningen återgår till Windows standardvärde, som är av.
  - **Blockera** Office-program får inte skapa underordnade processer.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.

- **Blockera Win32-API-anrop från Office-makron**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=872977)

  Den här ASR-regeln styrs via följande GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Inte konfigurerat** (*standard*) – Inställningen återgår till Windows standardvärde, som är av.
  - **Blockera** – Office-makron får inte använda anrop till Win32-API:er.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.

- **Blockera Office-kommunikationsprogram från att skapa underordnade processer**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=874499)  

  Den här ASR-regeln styrs via följande GUID: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Inte konfigurerat** (*standard*) – Windows standardvärde återställs, som är att inte blockera skapandet av underordnade processer.
  - **Användardefinierad**
  - **Aktivera** – Office-kommunikationsprogram får inte skapa underordnade processer.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera underordnade processer.

- **Blockera körning av potentiellt dolda skript (js/vbs/ps)**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=872978)

  Den här ASR-regeln styrs via följande GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Inte konfigurerat** (*standard*) – Inställningen återgår till Windows standardvärde, som är av.
  - **Blockera** – Defender blockerar körning av dolda skript.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.

- **Blockera JavaScript eller VBScript från att starta nedladdat körbart innehåll**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=872979)

   Den här ASR-regeln styrs via följande GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Inte konfigurerat** (*standard*) – Inställningen återgår till Windows standardvärde, som är av.
  - **Blockera** – Defender blockerar körning av JavaScript- och VBScript-filer som har laddats ned från internet.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.

- **Blockera skapande av processer från PSExec- och WMI-kommandon**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=874500)

  Den här ASR-regeln styrs via följande GUID: d1e49aac-8f56-4280-b9ba-993a6d77406c
  - **Inte konfigurerat** (*standard*) – Inställningen återgår till Windows standardvärde, som är av.
  - **Blockera** – Det går inte att skapa processer med PSExec- eller WMI-kommandon.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.

- **Blockera obetrodda och osignerade processer som körs via USB**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=874502)

  Den här ASR-regeln styrs via följande GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **Inte konfigurerat** (*standard*) – Inställningen återgår till Windows standardvärde, som är av.
  - **Blockera** – Obetrodda och osignerade processer som körs från en USB-enhet blockeras.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.

- **Blockera körbara filer från att köras om de inte uppfyller ett villkor för användningsmönster, ålder eller betrodd lista**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=874503)

  Den här ASR-regeln styrs via följande GUID: 01443614-cd74-433a-b99e-2ecdc07bfc25e
  - **Inte konfigurerat** (*standard*) – Inställningen återgår till Windows standardvärde, som är av.
  - **Blockera**
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.

- **Blockera körbart innehåll från e-postklient och webbaserad e-post**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Inte konfigurerat** (*standard*) – Inställningen återgår till Windows standardvärde, som är av.
  - **Blockera** – Körbart innehåll från e-postklienter och webbaserad e-post blockeras.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.

- **Använd avancerat skydd mot utpressningstrojaner**  
   [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=874504)

  Den här ASR-regeln styrs via följande GUID: c1db55ab-c21a-4637-bb3f-a12568109d35
  - **Inte konfigurerat** (*standard*) – Inställningen återgår till Windows standardvärde, som är av.
  - **Användardefinierad**
  - **Aktivera**
  - **Granskningsläge** – Windows-händelser eskaleras i stället för att blockeras.

- **Aktivera mappskydd**  
  CSP: [EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)

  - **Inte konfigurerad** (*standard*) – Den här inställningen återgår till standardvärdet, som är att inte blockera läsning eller skrivning.
  - **Aktivera** – För ej betrodda appar blockerar Defenter försök att ändra eller ta bort filer i skyddade mappar eller skriva till disksektorer. Defender avgör automatiskt vilka program som är betrodda. Du kan också definiera en egen lista med betrodda program.
  - **Granskningsläge** – Windows-händelser eskaleras när obetrodda program använder kontrollerade mappar, men de blockeras inte.
  - **Blockera diskändring** – Endast försök att skriva till disksektorer blockeras.
  - **Granska diskändrings** – Windows-händelser eskaleras i stället för att blockera försök att skriva till disksektorer.
  
- **Exkludera filer och sökvägar från reglerna för att minska attackytan**  
  CSP: [AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)

  Expandera listrutan och välj sedan **Lägg till** för att definiera en **Sökväg** till en fil eller mapp som ska undantas från reglerna för att minska attackytan.

## <a name="device-control-profile"></a>Profilen Enhetskontroll

### <a name="device-control"></a>Enhetskontroll

- **Hardware device installation by device identifiers** (Installation av maskinvaruenheter efter enhets-ID)  
  [PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  Med den här inställningen kan du ange en lista med ID:n för Plug and Play-maskinvara och kompatibla ID:n för enheter som Windows hindrar från att installeras. Den här inställningen har företräde framför alla andra principinställningar som tillåter att Windows installerar en enhet.  Om du aktiverar den här principinställningen på en fjärrskrivbordsserver påverkar principinställningen omdirigeringen av de angivna enheterna från en fjärrskrivbordsklient till fjärrskrivbordsservern.

  - **Inte konfigurerat**
  - **Tillåt installation av maskinvaruenheter** – Enheter kan installeras och uppdateras beroende på vad som tillåts eller förhindras av andra principinställningar.
  - **Blockera installation av maskinvaruenheter** (*standard*) – Windows hindras från att installera en enhet vars maskinvaru-ID eller kompatibelt ID visas i listan som du definierar.

  När värdet är *Blockera installation av maskinvaruenheter* kan du konfigurera följande inställningar:

  - **Remove matching hardware devices** (Ta bort matchande maskinvaruenheter)

    Den här inställningen är endast tillgänglig när *Hardware device installation by device identifiers* (Installation av maskinvaruenheter efter enhets-ID) har inställningen *Block hardware device installation* (Blockera installation av maskinvaruenheter).
    - **Ja**
    - **Inte konfigurerat**

  - **Hardware device identifiers that are blocked** (ID:n för blockerade maskinvaruenheter)  

    Den här inställningen är endast tillgänglig när *Hardware device installation by device identifiers* (Installation av maskinvaruenheter efter enhets-ID) har inställningen *Block hardware device installation* (Blockera installation av maskinvaruenheter).

    Välj **Lägg till** och ange sedan maskinvarans enhets-ID som du vill blockera.

- **Hardware device installation by setup classes** (Installation av maskinvaruenheter efter installationsklass)  
  CSP: [DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://go.microsoft.com/fwlink/?linkid=2067048)  
  
  Med den här principinställningen kan du ange en lista med klass-GUID för enhetsinstallation för enhetsdrivrutiner som Windows hindrar från att installeras. Den här inställningen har företräde framför alla andra principinställningar som tillåter att Windows installerar en enhet. Om du aktiverar den här principinställningen på en fjärrskrivbordsserver påverkar principinställningen omdirigeringen av de angivna enheterna från en fjärrskrivbordsklient till fjärrskrivbordsservern.

  - **Inte konfigurerat**
  - **Tillåt installation av maskinvaruenheter** – Windows kan installera och uppdatera enheter beroende på vad som tillåts eller förhindras av andra principinställningar.
  - **Blockera installation av maskinvaruenheter** (*standard*) – Windows hindras från att installera en enhet vars klass-GUID för installation visas i en lista som du definierar.

  När du har angett *Blockera installation av maskinvaruenheter* kan du konfigurera *Ta bort matchande maskinvaruenheter* och *ID:n för blockerade maskinvaruenheter*.

  - **Remove matching hardware devices** (Ta bort matchande maskinvaruenheter)

    Den här inställningen är endast tillgänglig när *Hardware device installation by device identifiers* (Installation av maskinvaruenheter efter enhets-ID) har inställningen *Block hardware device installation* (Blockera installation av maskinvaruenheter).
    - **Ja**
    - **Inte konfigurerat**

  - **Hardware device identifiers that are blocked** (ID:n för blockerade maskinvaruenheter)

    Den här inställningen är endast tillgänglig när *Hardware device installation by device identifiers* (Installation av maskinvaruenheter efter enhets-ID) har inställningen *Block hardware device installation* (Blockera installation av maskinvaruenheter).

    Välj **Lägg till** och ange sedan maskinvarans enhets-ID som du vill blockera.

- **Genomsök flyttbara enheter vid fullständig genomsökning**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946)

  - **Inte konfigurerat** (*standard*) – Inställningen återgår till klientens standardvärde som är att söka igenom flyttbara enheter, men användaren kan inaktivera den här genomsökningen.
  - **Ja** – Under en fullständig genomsökning genomsöks flyttbara enheter (som USB-minnen).
  
## <a name="exploit-protection-profile"></a>Profilen Sårbarhetsskydd

### <a name="exploit-protection"></a>Sårbarhetsskydd

- **Ladda upp XML**  
  CSP: [ExploitProtectionSettings](https://go.microsoft.com/fwlink/?linkid=2067035)

  Gör det möjligt för IT-administratören att distribuera en konfiguration som representerar önskade system- och programskyddsalternativ till alla enheter i organisationen. Konfigurationen representeras av en XML-fil. Sårbarhetsskydd kan hjälpa dig att skydda enheter mot skadlig kod som utnyttjar kryphål för att spridas och infektera. Du kan använda Windows Security-appen eller PowerShell för att skapa en uppsättning skyddsåtgärder (kallas en konfiguration). Du kan exportera den här konfigurationen som en XML-fil och dela den med flera datorer i nätverket så att alla har samma uppsättning skyddsåtgärder. Du kan också konvertera och importera en befintlig EMET XML-konfigurationsfil till en XML-konfigurationsfil för sårbarhetsskydd.

  Välj **Välj XML-fil**, ange XML-filen och klicka sedan på **Välj**.
  - **Ej konfigurerat** (*standard*)
  - **Ja**

- **Blockera användare från att redigera gränssnittet för Exploit Guard Protection**  
  CSP: [DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Inte konfigurerat** (*standard*) – Lokala användare kan göra ändringar i inställningsområdet för sårbarhetsskydd.
  - **Ja** – Förhindra att användare gör ändringar i inställningsområdet för sårbarhetsskydd i Microsoft Defender Security Center.

## <a name="next-steps"></a>Nästa steg

[Endpoint Security-policyn ASR](../protect/endpoint-security-asr-policy.md)
