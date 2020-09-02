---
title: Hantera enheter med slutpunktssäkerhet i Microsoft Intune | Microsoft Docs
description: Lär dig hur säkerhetsadministratörer kan använda noden Endpoint Security till att visa enheter och hantera dem i Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
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
ms.openlocfilehash: 98b1380254a784dfe8939c607ab574f7bdaa8752
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914998"
---
# <a name="manage-devices-with-endpoint-security-in-microsoft-intune"></a>Hantera enheter med slutpunktssäkerhet i Microsoft Intune

Som säkerhetsadministratör använder du vyn *Alla enheter* i administrationscentret för Microsoft Endpoint Manager till att granska och hantera dina enheter. I vyn ser du en lista med alla dina enheter från Azure Active Directory (Azure AD). Här ingår enheter som hanteras av Intune, Configuration Manager och via [samhantering](/configmgr/comanage/overview) av både Intune och Configuration Manager. Enheterna kan finnas i molnet eller i din lokala infrastruktur när den är integrerad med Azure AD.

 Du hittar vyn genom att öppna [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och välja **Slutpunktssäkerhet** > **Alla enheter**.

I den första vyn *Alla enheter* ser du enheterna och viktig information om var och en:

- hur enheten hanteras
- efterlevnadsstatus
- information om operativsystemet
- när enheten senast checkade in
- och mycket mer.

![Vyn Alla enheter i administrationscentret](./media/endpoint-security-manage-devices/all-device-view.png)

När du visar enhetsinformation kan du välja en enhet och visa mer detaljerad information om den.

## <a name="available-details-by-management-type"></a>Tillgänglig information efter hanteringstyp

När du visar enheter i administrationscentret för Microsoft Endpoint Manager ska du tänka på hur enheten hanteras. Hanteringskällan påverkar vilken information som visas i administrationscentret och vilka hanteringsåtgärder som är tillgängliga för enheten.

Titta på följande fält:

- **Hanteras av** – I den här kolumnen anges hur enheten hanteras. Här är några av alternativen för Hanteras av:

  - **MDM** – De här enheterna hanteras av Intune. Intune samlar in och rapporterar efterlevnadsdata till administrationscentret.

  - **ConfigMgr** – De här enheterna visas i administrationscentret för Microsoft Endpoint Manager när du använder *anslut klientorganisation* för att lägga till de enheter du hanterar med Configuration Manager. För att du ska kunna hantera enheten måste den köra Configuration Manager-klienten och vara:

    - i en arbetsgrupp (AAD-ansluten eller inte)
    - kopplad till en domän
    - hybridkopplad till AAD (kopplad till AD och AAD).

    Efterlevnadsstatusen för enheter som hanteras av Configuration Manager visas inte i administrationscentret för Microsoft Endpoint Manager.

    Mer information finns i [Aktivera koppling av klientorganisation](/configmgr/tenant-attach/device-sync-actions) i Configuration Manager-dokumentationen.

  - **MDM/ConfigMgr-agent** – De här enheterna samhanteras mellan Intune och Configuration Manager.

    Med samhantering kan du [välja olika arbetsbelastningar i samhanteringen](/configmgr/comanage/how-to-switch-workloads) för att avgöra vilka aspekter som ska hanteras av Configuration Manager och av Intune. De här valen påverkar vilka policyer som används för enheten och hur efterlevnadsdata rapporteras till administrationscentret.

    Du kan till exempel använda Intune till att konfigurera policyer för antivirusprogram, brandväggar och kryptering. De här policyerna betraktas som policyer för *Endpoint Protection*. Om du vill att en samhanterad enhet ska använda Intune-policyer och inte Configuration Manager-policyer ställer du in samhanteringsreglaget för Endpoint Protection till antingen *Intune* eller *Pilot Intune*. Om reglaget är inställt på Configuration Manager använder enheten policyer och inställningar från Configuration Manager i stället.

- **Efterlevnad**: Efterlevnaden utvärderas enligt de efterlevnadspolicyer som har tilldelats till enheten. Källan till de här policyerna och vilken information som visas i konsolen beror på hur enheten hanteras: Intune, Configuration Manager eller samhantering. Om du vill att samhanterade enheter ska rapportera efterlevnad ställer du in samhanteringsreglaget för enhetens efterlevnad på antingen Intune eller Pilot Intune.  

  När efterlevnaden rapporteras till administrationscentret för en enhet kan du visa mer detaljerad information om efterlevnaden. När en enhet inte uppfyller efterlevnadskraven kan du visa mer information och se vilka policyer som inte uppfylls. Den här informationen kan hjälpa dig att undersöka och se till att enheten uppfyller efterlevnaden.

- **Senaste incheckning**: Det här fältet anger den senaste gången enheten rapporterade sin status.

## <a name="review-a-devices-policy"></a>Granska en enhetspolicy

När du visar listan med enheter kan du välja en enhet för att visa mer information om den genom att öppna sidan *Översikt* för enheten.

På sidan Översikt för en enhet kan du sedan välja **Konfiguration av slutpunktssäkerhet** för att visa de Endpoint Security-policyer som gäller för enheten. Policyinformationen är tillgänglig för enheter som hanteras av MDM och Intune.

![Visa detaljer om Endpoint Security-policyer](./media/endpoint-security-manage-devices/view-policy-details.png)

Du kan inte visa policyinformation för enheter som hanteras av Configuration Manager. Använd Configuration Manager-konsolen om du vill visa mer information om sådana enheter.

## <a name="remote-actions-for-devices"></a>Fjärråtgärder för enheter

Fjärråtgärder är åtgärder du kan starta eller tillämpa på en enhet från administrationscentret för Microsoft Endpoint Manager. När du visar information om en enhet kan du komma åt de fjärråtgärder som gäller för enheten.

Fjärråtgärder visas längst upp på sidan *Översikt* för enheten. Åtgärder som inte kan visas på grund av begränsat utrymme på skärmen blir tillgängliga när du väljer ellipsen till höger:

![Visa fler åtgärder](./media/endpoint-security-manage-devices/view-additional-actions.png)

Vilka fjärråtgärder som är tillgängliga beror på hur enheten hanteras:

- **Intune**: Alla [Intune-fjärråtgärder](../remote-actions/device-management.md) som gäller för enhetsplattformen är tillgängliga.  
- **Configuration Manager**: Du kan använda följande Configuration Manager-åtgärder:

  - Synkronisera enhetsprincip
  - Synkronisera användarprincip
  - Apputvärderingscykel

- **Samhantering**: Du kan komma åt både Intune-fjärråtgärder och Configuration Manager-åtgärder.

Vissa Intune-fjärråtgärder kan hjälpa till att skydda enheter eller data som finns på enheten. Med fjärråtgärder kan du:

- Låsa en enhet
- Återställa en enhet
- Ta bort företagsdata
- Söka efter skadlig kod utanför en schemalagd körning
- Rotera Bitlocker-nycklar

Följande Intune-fjärråtgärder är av intresse för säkerhetsadministratören och är en del av [hela listan](../remote-actions/device-inventory.md#view-the-device-details). Alla åtgärder är inte tillgängliga för alla enhetsplattformar. Länkarna går till mer detaljerad information om varje åtgärd.

- [Synkronisera enhet](../remote-actions/device-sync.md) – se till att enheten omedelbart checkar in i Intune. När en enhet checkar in tar den emot eventuella väntande åtgärder eller policyer som har tilldelats till den.  

- [Starta om](../remote-actions/device-restart.md) – tvinga en Windows 10-enhet att starta om inom fem minuter. Enhetens ägare meddelas inte automatiskt om omstarten och kan förlora sitt arbete.

- [Snabb genomsökning](../configuration/device-restrictions-windows-10.md) – låt Defender köra en snabb genomsökning av enheten efter skadlig kod och skicka sedan resultatet till Intune. Vid en snabbsökning letar Defender på vanliga platser där det kan finnas skadlig kod, som registernycklar och kända startmappar i Windows.

- [Fullständig genomsökning](../configuration/device-restrictions-windows-10.md) – låt Defender köra en fullständig genomsökning av enheten efter skadlig kod och skicka sedan resultatet till Intune. Vid en fullständig sökning letar Defender på vanliga platser där det kan finnas skadlig kod och även i alla filer och mappar på enheten.

- Uppdatera säkerhetsinformationen i Windows Defender – låt enheten uppdatera definitionerna för skadlig kod i Microsoft Defender Antivirus. Den här åtgärden startar ingen genomsökning.

- [Rotera BitLocker-nyckel](../protect/encrypt-devices.md#to-rotate-the-bitlocker-recovery-key) – fjärrotera BitLocker-återställningsnyckeln på en enhet som kör Windows 10 version 1909 eller senare.

Du kan också använda **Massenhetsåtgärder** till att hantera vissa åtgärder som att *Ta ur bruk* och *Rensa* för flera enheter samtidigt. [Massåtgärder](../remote-actions/bulk-device-actions.md) är tillgängliga från vyn *Alla enheter*. Du väljer plattform, åtgärd och sedan upp till 100 enheter.

![Välj massåtgärder](./media/endpoint-security-manage-devices/select-bulk-actions.png)

De alternativ du hanterar för enheter börjar inte gälla förrän enheten checkar in i Intune.

## <a name="next-steps"></a>Nästa steg

[Hantera slutpunktssäkerhet i Intune](../protect/endpoint-security.md)