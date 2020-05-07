---
title: Kompatibilitetsinställningar för iOS-/iPadOS-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Visa en lista över alla inställningar som du kan använda när du ställer in kompatibilitet för iOS-/iPadOS-enheter i Microsoft Intune. Kräv ett e-postmeddelande, kontrollera jailbrokade eller rotade enheter, ange den lägsta och högsta tillåtna operativsystemversionen, ange begränsningar för lösenord, inklusive lösenordslängd och enhetsinaktivitet, begränsa appar och mycket mer.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 3cfb8222-d05b-49e3-ae6f-36ce1a16c61d
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 536ad36120a8fb5dc4ad0d16b8f265e56260d461
ms.sourcegitcommit: 56bb5419c41c2e150ffed0564350123135ea4592
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/02/2020
ms.locfileid: "82729265"
---
# <a name="iosipados-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>iOS-/iPadOS-inställningar för att markera enheter som kompatibla eller inkompatibla med hjälp av Intune

Den här artikeln innehåller en lista över och beskriver de olika kompatibilitetsinställningar som du kan konfigurera på iOS-/iPadOS-enheter i Intune. Som en del av din MDM-lösning för hantering av mobilenheter kan du använda dessa inställningar för att kräva ett e-postmeddelande, markera rotade (jailbreakade) enheter som inkompatibla, ange tillåten hotnivå, ange när lösenord ska upphöra att gälla och mycket mer.

Den här funktionen gäller för:

- iOS
- iPadOS

Som Intune-administratör kan du använda dessa kompatibilitetsinställningar för att skydda din organisations resurser. Mer om kompatibilitetsprinciper och vad de gör finns i [Komma igång med kompatibilitet](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en efterlevnadsprincip](create-compliance-policy.md#create-the-policy). Välj **iOS/iPadOS** som **Plattform**.

## <a name="email"></a>E-post

- **Det gick inte att konfigurera e-post på enheten**  
  - **Ej konfigurerad** (*standard*) – Ingen kompatibilitetskontroll görs för den här inställningen.
  - **Kräv** – Ett hanterat e-postkonto krävs. Om användaren redan har ett e-postkonto på enheten måste e-postkontot tas bort så att Intune kan konfigurera ett konto på rätt sätt. Om det inte finns något e-postkonto på enheten bör användaren kontakta IT-administratören för att konfigurera ett hanterat e-postkonto.

  Enheten betraktas som inkompatibel i följande situationer:  
  - E-postprofilen är associerad med en annan användargrupp än användargruppen som kompatibilitetsprincipen körs mot.
  - Användaren har redan konfigurerat ett e-postkonto på enheten som matchar Intune-e-postprofilen som distribuerats till enheten. Intune kan inte skriva över den användarkonfigurerade profilen och Intune kan inte hantera den. För att vara kompatibel måste slutanvändaren ta bort de befintliga e-postinställningarna. Sedan kan Intune installera den hantera e-postprofilen.  

Mer information om e-postprofiler finns i [Använda e-postprofiler med Intune för att konfigurera åtkomst till organisationens e-post](../configuration/email-settings-configure.md).

## <a name="device-health"></a>Enhetens hälsotillstånd

- **Jailbrokade enheter**  
  *Stöds för iOS 8.0 och senare*

  - **Ej konfigurerad** (*standard*) – Ingen kompatibilitetskontroll görs för den här inställningen.
  - **Blockera** – Markera rotade (jailbreakade) enheter som inkompatibla.  

- **Kräv att enheten ligger på eller under enhetshotnivån**  
  *Stöds för iOS 8.0 och senare*

  Använd den här inställningen för att använda riskbedömningen som ett villkor för efterlevnad. Välj den tillåtna hotnivån:
  - **Ej konfigurerad** (*standard*) – Ingen kompatibilitetskontroll görs för den här inställningen.
  - **Skyddad** – Det här alternativet är säkrast och innebär att enheten inte kan ha några hot. Om hot på någon nivå identifieras på enheten betraktas den som inkompatibel.
  - **Låg** – Enheten utvärderas som kompatibel om det bara finns lågnivåhot på den. Om hot på en högre nivå identifieras får enheten statusen icke-kompatibel.
  - **Medel** – Enheten utvärderas som kompatibel om hoten som finns på enheten är på en låg eller medelhög nivå. Om hot på en högre nivå identifieras på enheten får den statusen inkompatibel.
  - **Hög** – Det här alternativet är det minst säkra då det tillåter alla hotnivåer. Det skulle kunna vara användbart om lösningen endast används i rapporteringssyfte.

## <a name="device-properties"></a>Egenskaper för enhet

### <a name="operating-system-version"></a>Operativsystemversion  

- **Lägsta version av operativsystemet**  
  *Stöds för iOS 8.0 och senare*

  När en enhet inte uppfyller minimikravet på operativsystemversion, rapporteras den som inkompatibel. En länk med information om hur du uppgraderar visas. Slutanvändarna kan välja att uppgradera sina enheter. Därefter kan de komma åt organisationens resurser.

- **Högsta version av operativsystemet**  
  *Stöds för iOS 8.0 och senare*

  När en enhet använder en senare version av operativsystemet än den version som anges i regeln, så blockeras åtkomsten till organisationens resurser. Slutanvändaren uppmanas att kontakta IT-administratören. Enheten kan inte komma åt organisationens resurser förrän en regel ändras så att operativsystemversionen stöds.

- **Lägsta OS-byggversion**  
  *Stöds för iOS 8.0 och senare*

  När Apple publicerar säkerhetsuppdateringar, uppdateras normalt inte versionsnumret av operativsystemet. Använd denna funktion för att ange ett minsta tillåtna versionsnummer på enheten.

- **Högsta OS-byggversion*  
  *Stöds för iOS 8.0 och senare*

  När Apple publicerar säkerhetsuppdateringar, uppdateras normalt inte versionsnumret av operativsystemet. Använd denna funktion för att ange ett högsta tillåtna versionsnummer på enheten.

## <a name="system-security"></a>Systemsäkerhet

### <a name="password"></a>lösenordsinställning

> [!NOTE]
> När en efterlevnads- eller konfigurationsprincip används på en iOS-/iPadOS-enhet, uppmanas användarna att ange ett lösenord var 15:e minut. Användarna uppmanas kontinuerligt tills ett lösenord anges. När ett lösenord anges för iOS-/iPadOS-enheten startar krypteringsprocessen automatiskt. Enheten förblir krypterad tills lösenordet inaktiveras.

- **Kräv ett lösenord för att låsa upp mobila enheter**  
  - **Ej konfigurerad** (*standard*) – Ingen kompatibilitetskontroll görs för den här inställningen.  
  - **Kräv** – Användarna måste ange ett lösenord innan de får åtkomst till sina enheter. iOS-/iPadOS-enheter som använder lösenord krypteras.

- **Enkla lösenord**  
  *Stöds för iOS 8.0 och senare*

  - **Inte konfigurerad** (*standard*) – Användare kan skapa enkla lösenord som **1234** eller **1111**.
  - **Blockera** – Användarna kan inte skapa enkla lösenord, som exempelvis **1234** eller **1111**.

- **Minsta längd på lösenord**  
  *Stöds för iOS 8.0 och senare*

  Ange det minsta antal siffror eller tecken som lösenordet måste innehålla.

- **Lösenordstyp krävs**  
  *Stöds för iOS 8.0 och senare*

  Ange om ett lösenord endast ska ha **numeriska** tecken, eller om det ska vara en blandning av siffror och andra tecken (**alfanumeriska**).

- **Antal icke-alfanumeriska tecken i lösenord**  
  Ange det lägsta antalet specialtecken (`&`, `#`, `%`, `!` osv) som måste ingå i lösenordet.

  Om du anger en högre siffra måste användaren skapa ett lösenord som är mer komplext.

- **Maximalt antal minuter efter skärmlås innan ett lösenord krävs**  
  *Stöds för iOS 8.0 och senare*

  Ange hur lång tid det ska ta efter att skärmen har låsts innan en användare måste ange ett lösenord för att få åtkomst till enheten. Alternativen är *Inte konfigurerat* (standard), *Omedelbart* och från *1 minut* till *4 timmar*.

- **Maximalt antal minuter av inaktivitet innan skärmen låses**  
  Ange tiden innan enhetens skärm låses vid inaktivitet. Alternativen är *Inte konfigurerat* (standard), *Omedelbart* och från *1 minut* till *15 minuter*.

- **Lösenordets giltighetstid (i dagar)**  
  *Stöds för iOS 8.0 och senare*

  Ange antalet dagar tills lösenordet upphör att gälla och användaren måste skapa ett nytt.

- **Antal tidigare lösenord för att förhindra återanvändning**  
  *Stöds för iOS 8.0 och senare*

  Ange antal tidigare använda lösenord som inte får återanvändas.

### <a name="device-security"></a>Enhetssäkerhet

- **Begränsade appar**  
  Du kan begränsa appar genom att lägga till deras samlings-ID:n i principen. Om appen är installerad på en enhet markeras enheten som inkompatibel.

  - **Appnamn** – Ange ett användarvänligt namn som hjälper dig att identifiera samlings-ID:t.
  - **Appsamlings-ID** – Ange det unika samlings-ID som tilldelats av appleverantören. Information om hur du hittar paket-ID:t finns i [Hitta paket-ID:t för en iOS-/iPadOS-app](https://support.microsoft.com/help/4294074/how-to-find-the-bundle-id-for-an-ios-app) (en annan Microsoft-webbplats öppnas).  

## <a name="next-steps"></a>Nästa steg

- [Lägga till åtgärder för inkompatibla enheter](actions-for-noncompliance.md) och [Filtrera principer med hjälp av omfångstaggar](../fundamentals/scope-tags.md).
- [Övervaka dina kompatibilitetsprinciper](compliance-policy-monitor.md).
- Mer information finns i [Inställningar för kompatibilitetsprinciper för macOS-enheter](compliance-policy-create-mac-os.md).
