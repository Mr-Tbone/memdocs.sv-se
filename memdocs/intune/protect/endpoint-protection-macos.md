---
title: Lägga till slutpunktsskydd i macOS i Microsoft Intune – Azure | Microsoft Docs
description: På macOS-enheter använder du gatekeepern för att avgöra var appar kan installeras, inklusive Mac App Store. Genom att aktivera eller konfigurera en brandvägg kan man också tillåta eller blockera specifika appar, använda Stealthläge och även blockera vissa typer av inkommande anslutningar med Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5e857cdd7028851f14f607739ba7e37c744fa2f1
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359455"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Inställningar av slutpunktsskydd för macOS i Intune  

I den här artikeln visas inställningarna för slutpunktsskydd som du kan konfigurera för enheter som kör macOS. Du konfigurerar de här inställningarna med hjälp av en macOS-enhetskonfigurationsprofil för [slutpunktsskydd](endpoint-protection-configure.md) i Intune.  

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en profil för slutpunktsskydd för macOS](endpoint-protection-configure.md).

## <a name="gatekeeper"></a>Gatekeeper  

- **Tillåt nedladdade appar från de här platserna**  
  Begränsa de appar som tjänsten kan starta beroende på varifrån apparna laddas ned. Avsikten är att skydda enheter mot skadlig kod och tillåta appar endast från källor som du litar på.  

  - **Inte konfigurerat**  
  - **Mac App Store**  
  - **Mac App Store och identifierade utvecklare**  
  - **Överallt**  

  **Standard**: Inte konfigurerat  

- **Användaren kan åsidosätta Gatekeeper**  
  Förhindrar användare från att åsidosätta denna inställning och från att installera en app genom att Ctrl-klicka. När den är aktiverad kan användare installera appar med Ctrl+klick.  
 
  - **Inte konfigurerat** – användare kan installera appar med Ctrl+klick.  
  - **Blockera** – hindrar användare från att installera appar med Ctrl+klick.  

  **Standard**: Inte konfigurerat  

## <a name="firewall"></a>Brandvägg  

Använd brandväggen för att styra anslutningar per program i stället för per port. Med programspecifika inställningar är det lättare att använda brandväggsskyddet. Du också förhindra att oönskade appar tar kontroll över nätverksportar som är öppna för legitima appar.  

**Allmänt**
- **Brandvägg**  
  Aktivera brandväggen om du vill konfigurera hur inkommande anslutningar ska hanteras i din miljö.  
  - **Inte konfigurerat**  
  - **Aktivera**  

  **Standard**: Inte konfigurerat  

- **Inkommande anslutningar**  
  Blockera alla inkommande anslutningar utom de anslutningar som krävs för grundläggande Internet-tjänster, till exempel DHCP, Bonjour och IPSec. Funktionen blockerar också alla delade tjänster, till exempel fildelning och skärmdelning. Om du använder delningstjänster behåller du inställningen som *Inte konfigurerad*.  
  - **Inte konfigurerat**  
  - **Blockera**  

  **Standard**: Inte konfigurerat  

**Tillåta eller blockera inkommande anslutningar för specifika appar.**  

  - **Tillåtna appar**  
    Välj de appar som uttryckligen ska tillåtas ta emot inkommande anslutningar.  

  - **Blockerade appar**  
    Välj de appar som ska blockera inkommande anslutningar.  

  - **Dolt läge**  
    Aktivera detta om du vill förhindra att datorn svarar på avsökningsförfrågningar. Enheten fortsätter att besvara inkommande begäranden för godkända appar. Oväntade begäranden, till exempel ICMP (ping) ignoreras.  
    - **Inte konfigurerat**  
    - **Aktivera**  

    **Standard**: Inte konfigurerat  

## <a name="filevault"></a>FileVault  
Mer information om Apple FileVault-inställningarna finns i [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault) i Apple-utvecklarinnehållet. 

> [!IMPORTANT]  
> Från och med macOS 10.15 kräver FileVault-konfiguration användargodkänd MDM-registrering. 

- **FileVault**  
  Du kan *aktivera* fullständig diskkryptering med hjälp av XTS-AES 128 med FileVault på enheter som kör macOS 10.13 och senare.  
  - **Inte konfigurerat**  
  - **Aktivera**  

  **Standard**: Inte konfigurerat  

  - **Typ av återställningsnyckel**  
    *Personliga* återställningsnycklar skapas för enheter. Konfigurera följande inställningar för den personliga nyckeln.  

    - **Plats för privat återställningsnyckel** – ange ett kort meddelande till användarna som förklarar hur och var de kan hämta sin personliga återställningsnyckel. Den här texten infogas i det meddelande som visas för användare på inloggningsskärmen när de uppmanas att ange sin personliga återställningsnyckel om de glömmer bort lösenordet.  

    - **Rotering av privat återställningsnyckel** – ange hur ofta den privata återställningsnyckeln för en enhet ska rotera. Du kan välja standardinställningen **Inte konfigurerat** eller ett värde på **1** till **12** månader.  

  - **Inaktivera fråga vid utloggning**  
    Förhindra uppmaningen till användare att aktivera FileVault när de loggar ut.  När det här anges till Inaktivera visas inget meddelande vid utloggning. I stället får användarna en uppmaning när de loggar in.  
    - **Inte konfigurerat**  
    - **Inaktivera** – inaktivera meddelandet vid utloggning.

    **Standard**: Inte konfigurerat  

  - **Antal gånger som ignorering tillåts**  
  Ange det antal gånger som användare kan ignorera frågor om att aktivera FileVault innan FileVault krävs för att de ska kunna logga in. 

    - **Inte konfigurerat** – kryptering på enheten krävs innan nästa inloggning tillåts.  
    - **1** till **10** – tillåt användare att ignorera uppmaningen från 1 till 10 gånger innan kryptering på enheten krävs.  
    - **Ingen gräns, fråga alltid** – användaren uppmanas att aktivera FileVault, men kryptering krävs aldrig.  
 
    **Standard**: *Varierar* – om inställningen *Inaktivera fråga vid utloggning* anges till **Inte konfigurerat** får den här inställningen standardvärdet **Inte konfigurerat**. Om *Inaktivera fråga vid utloggning* anges till **Inaktivera** får den här inställningen standardvärdet **1**, och värdet **Inte konfigurerat** är inte ett alternativ.

Mer information om FileVault med Intune finns i [FileVault-återställningsnycklar](encryption-monitor.md#filevault-recovery-keys).

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](../configuration/device-profile-assign.md) och [övervaka dess status](../configuration/device-profile-monitor.md).

Du kan också konfigurera slutpunktsskydd på [enheter med Windows 10 och senare](endpoint-protection-windows-10.md).
