---
title: Konfigurera slutpunktsskydd på macOS-enheter med Microsoft Intune | Microsoft Docs
description: Använd Intune till att konfigurera macOS-enheter att använda den inbyggda brandväggen till att tillåta eller blockera vissa appar eller använda dolt läge, att använda Gatekeeper till att fastställa var appar installeras och använda filkryptering med FileVault.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 506bb4672b84423204df5fce1401748ffbce0484
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107507"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Inställningar av slutpunktsskydd för macOS i Intune

I den här artikeln visas inställningarna för slutpunktsskydd som du kan konfigurera för enheter som kör macOS. Du konfigurerar de här inställningarna med hjälp av en macOS-enhetskonfigurationsprofil för [slutpunktsskydd](endpoint-protection-configure.md) i Intune.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en profil för slutpunktsskydd för macOS](endpoint-protection-configure.md).

## <a name="firewall"></a>Brandvägg

Använd brandväggen för att styra anslutningar per program i stället för per port. Med programspecifika inställningar är det lättare att använda brandväggsskyddet. Du också förhindra att oönskade appar tar kontroll över nätverksportar som är öppna för legitima appar.

- **Aktivera brandvägg**

  Aktivera brandväggen i macOS om du vill konfigurera hur inkommande anslutningar ska hanteras i din miljö.

  - **Ej konfigurerat** (*standard*)
  - **Ja**

- **Blockera alla inkommande anslutningar**

  Blockera alla inkommande anslutningar utom de anslutningar som krävs för grundläggande Internet-tjänster, till exempel DHCP, Bonjour och IPSec. Funktionen blockerar också alla delade tjänster, till exempel fildelning och skärmdelning. Om du använder delningstjänster behåller du inställningen som *Inte konfigurerad*.

  - **Ej konfigurerat** (*standard*)
  - **Ja**

  När du ställer in *Blockera alla inkommande anslutningar* på *Inte konfigurerat* kan du sedan konfigurera vilka appar som ska kunna ta emot inkommande anslutningar.

  **Tillåtna appar** Ange en lista med appar som ska kunna ta emot inkommande anslutningar.

  - **Lägg till appar efter paket-ID**: Ange appens [paket-ID](../configuration/bundle-ids-built-in-ios-apps.md). På Apple-webbplatsen finns en lista med [inbyggda Apple-appar](https://support.apple.com/HT208094).
  - **Lägg till Store-app**: Välj en Store-app du har lagt till i Intune. Du hittar mer information i [Lägg till appar i Microsoft Intune](../apps/apps-add.md).

  **Blockerade appar**: Ange en lista med appar där inkommande anslutningar är blockerade.

  - **Lägg till appar efter paket-ID**: Ange appens [paket-ID](../configuration/bundle-ids-built-in-ios-apps.md). På Apple-webbplatsen finns en lista med [inbyggda Apple-appar](https://support.apple.com/HT208094).
  - **Lägg till Store-app**: Välj en Store-app du har lagt till i Intune. Du hittar mer information i [Lägg till appar i Microsoft Intune](../apps/apps-add.md).

- **Aktivera dolt läge**

  Aktivera detta om du vill förhindra att datorn svarar på avsökningsförfrågningar. Enheten fortsätter att besvara inkommande begäranden för godkända appar. Oväntade begäranden, till exempel ICMP (ping) ignoreras.

  - **Ej konfigurerat** (*standard*)
  - **Ja**

## <a name="gatekeeper"></a>Gatekeeper

- **Tillåt nedladdade appar från de här platserna**

  Begränsa de appar som tjänsten kan starta beroende på varifrån apparna laddas ned. Avsikten är att skydda enheter mot skadlig kod och tillåta appar endast från källor som du litar på.

  - **Ej konfigurerat** (*standard*)
  - **Mac App Store**
  - **Mac App Store och identifierade utvecklare**
  - **Överallt**

- **Tillåt inte användaren att åsidosätta Gatekeeper**

  Förhindrar användare från att åsidosätta denna inställning och från att installera en app genom att Ctrl-klicka. När den är aktiverad kan användare installera appar med Ctrl+klick.

  - **Inte konfigurerat** (*standardvärdet*) – användare kan installera appar med Ctrl+klick.
  - **Ja** – förhindrar att användare installerar appar med Ctrl+klick.

## <a name="filevault"></a>FileVault

Mer information om Apple FileVault-inställningarna finns i [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault) i Apple-utvecklarinnehållet.

> [!IMPORTANT]
> Från och med macOS 10.15 kräver FileVault-konfiguration användargodkänd MDM-registrering.

- **Aktivera FileVault**  

  Du kan *aktivera* fullständig diskkryptering med hjälp av XTS-AES 128 med FileVault på enheter som kör macOS 10.13 och senare.

  - **Ej konfigurerat** (*standard*)
  - **Ja**

  När värdet för *Aktivera FileVault* är *Ja* kan du konfigurera följande inställningar:

  - **Typ av återställningsnyckel**

    *Personliga* återställningsnycklar skapas för enheter. Konfigurera följande inställningar för den personliga nyckeln.

  - **Beskrivning av depositionsplats för privat återställningsnyckel**

    Skriv ett kort meddelande till användarna som förklarar hur de kan hämta privata återställningsnycklar. Den här texten infogas i meddelandet som visas för användarna på inloggningsskärmen när de uppmanas att ange sin personliga återställningsnyckel om de glömmer bort lösenordet.

  - **Rotering av privat återställningsnyckel**

    Ange hur ofta den privata återställningsnyckeln för en enhet ska roteras. Du kan välja standardinställningen **Inte konfigurerat** eller ett värde på **1** till **12** månader.

  - **Dölj återställningsnyckel**

    Välj om du vill dölja den personliga nyckeln från enhetsanvändaren vid FileVault 2-kryptering.

    - **Inte konfigurerat** (*standardalternativ*) – den personliga nyckeln visas för enhetsanvändaren under krypteringen.
    - **Ja** – den personliga nyckeln är dold från enhetsanvändaren under krypteringen.

    Efter krypteringen kan enhetsanvändaren visa sin personliga återställningsnyckel för en krypterad macOS-enhet från följande platser:
    - företagsportalappen i iOS/iPadOS
    - Intune-appen
    - företagsportalens webbplats
    - företagsportalappen i Android.

    Om du vill visa nyckeln från appen eller webbplatsen går du till enhetsinformation om den krypterade macOS-enheten och väljer *Hämta återställningsnyckel*.

  - **Inaktivera fråga vid utloggning**

    Förhindra uppmaningen till användare att aktivera FileVault när de loggar ut.  När det här anges till Inaktivera visas inget meddelande vid utloggning. I stället får användarna en uppmaning när de loggar in.

    - **Ej konfigurerat** (*standard*)
    - **Ja** – inaktivera meddelandet vid utloggning.

  - **Antal gånger som ignorering tillåts**

    Ange det antal gånger som användare kan ignorera frågor om att aktivera FileVault innan FileVault krävs för att de ska kunna logga in.

    - **Inte konfigurerat** – kryptering på enheten krävs innan nästa inloggning tillåts.
    - **0** – kräv att enheter ska krypteras nästa gång en användare loggar in på enheten.
    - **1** till **10** – tillåt användare att ignorera uppmaningen från 1 till 10 gånger innan kryptering på enheten krävs.
    - **Ingen gräns, fråga alltid** – användaren uppmanas att aktivera FileVault, men kryptering krävs aldrig.

    Standardvärdet för den här inställningen beror på konfigurationen av *Inaktivera fråga vid utloggning*. När *Inaktivera fråga vid utloggning* har värdet **Inte konfigurerat** får den här inställningen standardvärdet **Inte konfigurerat**. När *Inaktivera fråga vid utloggning* har värdet **Ja** får den här inställningen standardvärdet **1** och värdet **Inte konfigurerat** är inte ett alternativ.

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](../configuration/device-profile-assign.md) och [övervaka dess status](../configuration/device-profile-monitor.md).

Du kan också konfigurera slutpunktsskydd på [enheter med Windows 10 och senare](endpoint-protection-windows-10.md).
