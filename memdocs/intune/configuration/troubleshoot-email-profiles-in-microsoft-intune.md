---
title: Felsöka e-postprofiler i Microsoft Intune – Azure | Microsoft Docs
description: Se vanliga problem och lösningar med e-postprofiler i Microsoft Intune, inklusive duplicerade e-postprofiler och fel på Samsung KNOX Standard Android-enheter.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/20/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: f5c944ea-32a6-48af-bb57-16d5f1f3c588
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3d011d6111ede4bb5879e53e771d20b792bf00d3
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995134"
---
# <a name="common-issues-and-resolutions-with-email-profiles-in-microsoft-intune"></a>Vanliga problem och lösningar med e-postprofiler i Microsoft Intune

Se några vanliga problem med e-postprofiler samt hur du felsöker och löser dem.

## <a name="users-are-repeatedly-prompted-to-enter-their-password"></a>Användare uppmanas att ange sitt lösenord upprepade gånger

Användare kan uppmanas att ange sitt lösenord för e-postprofilen upprepade gånger. Om certifikat används för att autentisera och auktorisera användaren kontrollerar du tilldelningarna för alla certifikatprofiler. Certifikatprofilerna tilldelas vanligtvis till användargrupper, inte enhetsgrupper. Om något av certifikatprofilerna inte är riktad mot en användare försöker Intune att distribuera e-postprofilen igen.

Om e-postprofilkedjan är tilldelad till användargrupper måste du även vara säker på att dina certifikatprofiler har tilldelats till användargrupper.

## <a name="profiles-deployed-to-device-groups-show-errors-and-latency"></a>Profiler som distribueras till enhetsgrupper visar fel och svarstid

E-postprofiler tilldelas vanligtvis till användargrupper. Det kan finnas fall när de är tilldelade till enhetsgrupper.

- Om du till exempel vill distribuera en certifikatbaserad e-postprofil till endast Surface-enheter, inte stationära datorer. I det här scenariot kan enhetsgrupper passa bra. Observera att enheterna kan visas som icke-kompatibla, kan returnera fel och inte få dina e-postprofiler omedelbart.

  I det här exemplet skapar du e-postprofilen och tilldelar profilen till enhetsgrupper. Enheten startas om och det uppstår en fördröjning innan användaren loggar in. Under den här fördröjningen distribueras din PKCS-certifikatprofil, som är tilldelad till användargrupper. Eftersom det inte finns någon användare än gör PKCS-certifikatprofilen att enheten inte är kompatibel. Loggboken kan också visa fel på enheten.

  För att det ska bli kompatibelt loggar användaren in på enheten och synkroniserar med Intune för att ta emot principerna. Användare kan omsynkronisera manuellt eller vänta på nästa synkronisering.

- Du använder exempelvis dynamiska grupper. Om Azure AD inte uppdaterar de dynamiska grupperna omedelbart kan dessa enheter visas som inkompatibla.

I sådana scenarier bestämmer du om det är viktigast att använda enhetsgrupper eller viktigast att visa alla principer som kompatibla.

## <a name="device-already-has-an-email-profile-installed"></a>Enheten har redan en e-postprofil installerad

Om användare skapar en e-postprofil innan de registreras i Intune eller Microsoft 365 MDM, kanske e-postprofilen som distribueras av Intune inte fungerar som förväntat:

- **iOS/iPadOS**: Intune identifierar en befintlig, duplicerad e-postprofil baserat på värdnamn och e-postadress. Den användarskapade e-postprofilen blockerar distributionen av den Intune-skapade profilen. Det här scenariot är ett vanligt problem eftersom iOS/iPadOS-användare vanligtvis skapar en e-postprofil först och sedan registrerar sig. Företagsportalappen visar att användaren inte är kompatibel och kan uppmana användaren att ta bort e-postprofilen.

  Användaren bör ta bort sin e-postprofil så att Intune-profilen kan distribueras. Förhindra det här problemet genom att be dina användare att registrera sig så att Intune kan distribuera e-postprofilen. Användarna kan därefter skapa sin e-postprofil.

- **Windows**: Intune identifierar en befintlig, duplicerad e-postprofil baserat på värdnamn och e-postadress. Intune skriver över den befintliga e-postprofilen som skapats av användaren.

- **Samsung KNOX Standard**: Intune identifierar ett duplicerat e-postkonto baserat på e-postadressen och skriver över det med Intune-profilen. Om användaren konfigurerar kontot skrivs det över igen av Intune-profilen. Detta beteende kan orsaka förvirring för användaren vars kontokonfiguration skrivs över.

Samsung KNOX använder inte värdnamn för att identifiera profilen. Vi rekommenderar att du inte skapar flera e-postprofiler som ska distribueras till samma e-postadress på olika värdar, eftersom de kommer att skriva över varandra.

## <a name="error-0x87d1fde8-for-knox-standard-device"></a>Fel 0x87D1FDE8 för KNOX Standard-enhet

**Problem**: När en e-postprofil för Exchange Active Sync har skapats och distribuerats för Samsung KNOX Standard till olika Android-enheter så visas felet **0x87D1FDE8** eller **Åtgärden misslyckades** på enhetens egenskaper > princip-flik.

Granska konfigurationen av din EAS-profil för Samsung KNOX och källprincipen. Synkroniseringsalternativet Samsung Note stöds inte längre och det alternativet bör inte väljas i din profil. Se till att enheterna har fått tillräckligt med tid (upp till 24 timmar) för att bearbeta principen.

## <a name="unable-to-send-images-from--email-account"></a>Det går inte att skicka bilder från e-postkontot

Användare med automatiskt konfigurerade e-postkonton kan inte skicka foton eller bilder från sina enheter. Detta kan hända om **Tillåt att e-post skickas från tredjepartsprogram** inte är aktiverat.

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler**.
3. Välj din e-postprofil > **Egenskaper** > **Inställningar**.
4. Ange alternativet **Tillåt att e-post skickas från tredjepartsprogram**  till **Aktivera**.

## <a name="next-steps"></a>Nästa steg

Få [support från Microsoft](../fundamentals/get-support.md) eller använd [community-forumen](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
