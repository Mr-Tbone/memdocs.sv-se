---
title: Granska loggar för appskyddsprinciper
titleSuffix: Microsoft Intune
description: Det här avsnittet beskriver hur du konfigurerar loggar för appskyddsprinciper.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/09/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 4CD5EE94-7BA6-4F59-8E28-1EBCA7CA6436
ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe508dac691f922ec638709e04d6d4dd9f47f078
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79341704"
---
# <a name="review-client-app-protection-logs"></a>Granska loggarna för klientappskydd

Läs om vilka inställningar du kan granska i appskyddsloggarna. Få åtkomst till loggarna genom att aktivera Intune-diagnostik på en mobil klient. 

Processen för att aktivera och samla in loggar varierar efter plattform:
- **iOS/iPadOS-enheter** – Använd Microsoft Edge för iOS/iPadOS för att samla in loggar. Mer information finns i [Hantera webbåtkomst med Microsoft Edge med Microsoft Intune](manage-microsoft-edge.md#use-microsoft-edge-on-ios-to-access-managed-app-logs). 
- **Windows 10-enheter** – Använd *MDMDiag* och händelseloggar. Se [Diagnostisera MDM-fel i Windows 10](https://docs.microsoft.com/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10) i Windows-klientens hanteringsinnehåll och bloggen [Felsökning av Windows 10 vid Intune-principfel](https://blogs.technet.microsoft.com/configmgrdogs/2018/08/09/troubleshooting-windows-10-intune-policy-failures/).
- **Android-enheter** – inga diagnostikdata för appskyddsprinciper (app) på Android-enheter.

I följande tabell visas namnet på appskyddsprincipen och de värden som stöds och som sparas i loggen. Dessutom identifierar varje inställning principinställningen som finns i Microsoft Endpoint Manager-portalen. Detaljerad information om varje inställning finns i [Inställningar för iOS/iPadOS-appskyddsprinciper](app-protection-policy-settings-ios.md).

## <a name="app-protection-policy-settings"></a>Principinställningar för appskydd

| Name                        | Värdeinformation                                                                                                                                                                                                                                                                                            | Inställning i Microsoft Endpoint Manager-princip för programskydd                                                                                                                            |
|-----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AccessRecheckOfflineTimeout | x minuter                                                                                                                                                                                                                                                                                                   | **Avsnitt**: Villkorlig start<br>**Inställning**: Offlinerespitperiod med åtgärden Blockera åtkomst (minuter)           |
| AccessRecheckOnlineTimeout  | _x_ minuter                                                                                                                                                                                                                                                                                                   | **Avsnitt**: Åtkomstkrav<br>**Inställning**: Kontrollera åtkomstbehörigheterna på nytt efter (minuters inaktivitet) |
| AllowedOutboundClipboardSharingExceptionLength               | x tecken                                                                                                                                                                                                                                                                                           | **Avsnitt**: Dataskydd<br>**Inställning**: Gräns för att klippa ut och kopiera tecken för alla appar 
| AppPinDisabled              | 0 = Kräv<br>1 = Krävs inte                                                                                                                                                                                                                                                                                           | **Avsnitt**: Åtkomstkrav<br>**Inställning**: PIN-appkod när enhetens PIN-kod har ställts in                                                                                                                                     |
| AppSharingFromLevel         | 0 = Inga<br>1 = Principhanterade appar<br>2 = Alla appar                                                                                                                                                                                                                                                              | **Avsnitt**: Dataskydd<br>**Inställning**: Ta emot data från andra appar                                                                                                                        |
| AppSharingToLevel           | 0 = Inga<br>1 = Principhanterade appar<br>2 = Alla appar                                                                                                                                                                                                                                                              | **Avsnitt**: Dataskydd<br>**Inställning**: Skicka organisationsdata till andra appar                                                                                                                         |
| ProtectManagedOpenInData           | 0 = Falskt<br>1 = Sant                                                                                                                                                                                                                                                              | **Avsnitt**: Dataskydd<br>**Inställning**: Skicka organisationsdata till andra appar har ställts in på Principhanterade appar med Öppna i/dela-filtrering när värdet är sant                                                                                                                         |
| AuthenticationEnabled       | 0 = Krävs inte<br>1 = Kräv                                                                                                                                                                                                                                                                                           | **Avsnitt**: Åtkomstkrav<br>**Inställning**: Arbets- eller skolkontoautentiseringsuppgifter för åtkomst                                                                                                                      |
| ClipboardSharingLevel       | 0 = Blockerad<br>1 = Principhanterade appar<br>2 = Principhanterade appar med inklistring<br>3 = Alla appar                                                                                                                                                                                                                            | **Avsnitt**: Dataskydd<br>**Inställning**: Begränsa klipp ut, kopiera och klistra in mellan andra appar                                                                                                                         |
| ContactSyncDisabled         | 0 = Tillåt<br>1 = Blockera                                                                                                                                                                                                                                                                                           | **Avsnitt**: Dataskydd<br>**Inställning**: Synkronisera app med inbyggd kontaktapp                                                                                                                                                 |
| DataBackupDisabled          | 0 = Tillåt<br>1 = Blockera                                                                                                                                                                                                                                                                                           | **Avsnitt**: Dataskydd<br>**Inställning**: Förhindra säkerhetskopiering                                                                                                                                     |
| DeviceComplianceEnabled     | 0 = Falskt<br>1 = Sant                                                                                                                                                                                                                                                                                           | **Avsnitt**: Villkorlig start<br>**Inställning**: Jailbrokade/rotade enheter                                                                                                                |
| DeviceComplianceFailureAction           | 0 = blockera åtkomst<br>1 = Rensa data                                                                                                                                                                                                                                                                                                         | **Avsnitt**: Villkorlig start<br>**Inställning**: Jailbrokade/rotade enheter                                                                                                                                                |
| DisableShareSense           | E.t.                                                                                                                                                                                                                                                                                                         | Ej tillämpligt: Används inte aktivt av Intune-tjänsten.                                                                                                                                                |
| FileEncryptionLevel         | 0 = När enheten är låst<br>1 = När enheten är låst och det finns öppna filer<br>2 = Efter omstart av enheten<br>3 = Använd enhetsinställningarna                                                                                                                                                                      | **Avsnitt**: Dataskydd<br>**Inställning**: Kryptera organisationsdata                                                                                                                                                      |
| FileSharingSaveAsDisabled   | 0 = Tillåt<br>1 = Blockera                                                                                                                                                                                                                                                                                           | **Avsnitt**: Dataskydd<br>**Inställning**: Spara kopior av organisationsdata                                                                                                                                                     |
| IntuneIdentityUPN           | UPN för Intune MAM-användaren                                                                                                                                                                                                                                                                                  | E.t.                                                                                                                                                                                     |
| ManagedBrowserRequired      | 0 = Falskt<br>1 = Sant                                                                                                                                                                                                                                                                                           | **Avsnitt**: Dataskydd<br>**Inställning**: Begränsa webbinnehåll till att visas i Intune Managed Browser-appen.                                                                                                     |
| ManagedLocations            | Ett värde som representerar antalet hanterade lagringsplatser där appen kan spara data. <br>1 = OneDrive<br>2 = SharePoint<br>3 = OneDrive och SharePoint<br>32 = Lokal lagring<br>33 = Lokal lagring och OneDrive<br>34 = Lokal lagring och SharePoint<br>35 = Lokal lagring, OneDrive och SharePoint | **Avsnitt**: Dataskydd<br>**Inställning**: Tillåt användaren att spara kopior i valda tjänster                                                                                                          |
| MinAppVersion               | ”0.0” = ingen minsta appversion<br>allt annat = minsta appversion                                                                                                                                                                                                                                       | **Avsnitt**: Villkorlig start<br>**Inställning**: Lägsta appversion med åtgärden Blockera åtkomst                                                                                                                                                    |
| MinAppVersionWarning        | ”0.0” = ingen minsta appversion.<br>allt annat = minsta appversion                                                                                                                                                                                                                                       | **Avsnitt**: Villkorlig start<br>**Inställning**: Lägsta appversion med åtgärden Varna                                                                                                                                    |
| MinAppVersionWipe                | ”0.0” = ingen lägsta version på operativsystemet<br>allt annat = lägsta version på operativsystemet                                                                                                                                                                                                                                         | **Avsnitt**: Villkorlig start<br>**Inställning**: Lägsta appversion med åtgärden Rensa data                                                                                                                                           |
| MinOsVersion                | ”0.0” = ingen lägsta version på operativsystemet<br>allt annat = lägsta version på operativsystemet                                                                                                                                                                                                                                         | **Avsnitt**: Villkorlig start<br>**Inställning**: Lägsta operativsystemversion med åtgärden Blockera åtkomst                                                                                                                                          |
| MinOsVersionWarning         | ”0.0” = ingen lägsta version på operativsystemet<br>allt annat = lägsta version på operativsystemet                                                                                                                                                                                                                                         | **Avsnitt**: Villkorlig start<br>**Inställning**: Lägsta operativsystemversion med åtgärden Varna                                                                                                                            |
| MinOsVersionWipe         | ”0.0” = ingen lägsta version på operativsystemet<br>allt annat = lägsta version på operativsystemet                                                                                                                                                                                                                                         | **Avsnitt**: Villkorlig start<br>**Inställning**: Lägsta operativsystemversion med åtgärden Rensa data                                                                                                                            |
| MinSDKVersion               | ”0.0” = ingen lägsta SDK-version<br>allt annat = lägsta version på operativsystemet                                                                                                                                                                                                                                        | **Avsnitt**: Villkorlig start<br>**Inställning**: Lägsta SDK-systemversion med åtgärden Blockera åtkomst                                                                                                                       |
| MinSDKVersionWipe               | ”0.0” = ingen lägsta SDK-version<br>allt annat = lägsta version på operativsystemet                                                                                                                                                                                                                                        | **Avsnitt**: Villkorlig start<br>**Inställning**: Lägsta SDK-systemversion med åtgärden Blockera åtkomst                                                                                                                       |
| NotificationRestriction     | 0 = Tillåt<br>1 = Blockera organisationsdata<br>2 = Blockera                                                                                                                                                                                                                                                                   | **Avsnitt**: Dataskydd<br>**Inställning**: Meddelanden om organisationsdata                                                                                                                                                                                     |
| PINCharacterType            | 0 = Lösenkod<br>1 = Numerisk                                                                                                                                                                                                                                                                                                         | **Avsnitt**: Åtkomstkrav<br>**Inställning**: Typ av PIN-kod                                                                                                                                                                                     |
| PINEnabled                  | 0 = Krävs inte<br>1 = Kräv                                                                                                                                                                                                                                                                                           | **Avsnitt**: Åtkomstkrav<br>**Inställning**: PIN-kod för åtkomst                                                                                                                                                         |
| PINMinLength                | x tecken                                                                                                                                                                                                                                                                                                | **Avsnitt**: Åtkomstkrav<br>**Inställning**: Välja minimilängd för PIN-kod                                                                                                                                                                     |
| PINNumRetry                 | x försök                                                                                                                                                                                                                                                                                                  | **Avsnitt**: Villkorlig start<br>**Inställning**: Högsta antal PIN-försök                                                                                                                                            |
| MaxPinRetryExceededAction                 | 0 = Återställ PIN-kod<br>1 = Rensa data                                                                                                                                                                                                                                                                                                  | **Avsnitt**: Villkorlig start<br>**Inställning**: Högsta antal PIN-försök                                                                                                                                            |
| PrintingBlocked             | 0 = Tillåt<br>1 = Blockera                                                                                                                                                                                                                                                                                           | **Avsnitt**: Dataskydd<br>**Inställning**: Utskrift av organisationsdata                                                                                                                                                      |
| SimplePINAllowed            | 0 = Blockera<br>1 = Tillåt                                                                                                                                                                                                                                                                                           | **Avsnitt**: Åtkomstkrav<br>**Inställning**: Enkel PIN-kod                                                                                                                                                               |
| TouchIDEnabled              | 0 = Blockera<br>1 = Tillåt                                                                                                                                                                                                                                                                                           | **Avsnitt**: Åtkomstkrav<br>**Inställning**: Touch ID istället för PIN-kod för åtkomst (iOS 8+/iPadOS)                                                                                                                                      |
| ThirdPartyKeyboardsBlocked              | 0 = Tillåt<br>1 = Blockera                                                                                                                                                                                                                                                                                           | **Avsnitt**: Dataskydd<br>**Inställning**: Tangentbord från tredje part                                                                                                                                      |
| FaceIDEnabled              | 0 = Blockera<br>1 = Tillåt                                                                                                                                                                                                                                                                                           | **Avsnitt**: Åtkomstkrav<br>**Inställning**: Face ID istället för PIN-kod för åtkomst (iOS 11+/iPadOS)                                                                                                                                      |
| PINExpiryDays              | x tecken                                                                                                                                                                                                                                                                                           | **Avsnitt**: Åtkomstkrav<br>**Inställning**: PIN-återställning efter antal dagar > antalet dagar                                                                                                                                      |
| NonBioPassTimeOutRequired              | 0 = Krävs inte<br>1 = Kräv                                                                                                                                                                                                                                                                                           | **Avsnitt**: Åtkomstkrav<br>**Inställning**: Åsidosätt Touch ID med PIN-kod efter tidsgräns                                                                                                                                      |
| NonBioPassTimeOut              | x minuter                                                                                                                                                                                                                                                                                           | **Avsnitt**: Åtkomstkrav<br>**Inställning**: Åsidosätt Touch ID med PIN-kod efter tidsgräns > (minuters inaktivitet)                                                                                                                                      |
| DictationBlocked              | 0 = Tillåt<br>1 = Blockera                                                                                                                                                                                                                                                                                           | Ingen administrationskontroll för den här inställningen.                                                                                                                                      |
| OfflineWipeInterval              | x dagar                                                                                                                                                                                                                                                                                           | **Obs!** : Ingen administrationskontroll för den här inställningen.                                                                                                                                      |
| ProtocolExclusions              | 0 = Tillåt<br>1 = Blockera                                                                                                                                                                                                                                                                                           | **Avsnitt**: Dataskydd<br>**Inställning**: Välj vilka appar som ska undantas                                                                                                                                     |
| EnableOpenInFilter              | 0 = Inaktiverad<br>1 = Aktiverad                                                                                                                                                                                                                                                                                           | **Avsnitt**: Dataskydd<br>**Inställning**: Skicka organisationsdata till andra appar > Principhanterade appar med Öppen in/dela-filtrering                                                                                                                                     |
| MinimumRequiredDeviceThreatProtectionLevel              | 0 = Inte konfigurerat<br>1 = Skyddad<br>2 = Låg<br>3 = Medel<br>4 = Hög                                                                                                                                                                                                                                                                                           | **Avsnitt**: Villkorlig start<br>**Inställning**: Högsta tillåtna hotnivå för enhet                                                                                                                                      |
| MobileThreatDefenseRemediationAction              | 0 = Blockera åtkomst<br>1 = Rensa data                                                                                                                                                                                                                                                                                           | **Avsnitt**: Åtkomstkrav<br>**Inställning**: Åtgärden högsta tillåtna hotnivå på enhet)                                                                                                                                      |
| AllowedIOSModelsElseBlock              | x tecken                                                                                                                                                                                                                                                                                           | **Avsnitt**: Villkorlig start<br>**Inställning**: Enhetsmodell(er) med åtgärden Tillåt specifik (blockera icke-specifik)                                                                                                                                     |
| AllowedIOSModelsElseWipe              | x tecken                                                                                                                                                                                                                                                                                           | **Avsnitt**: Villkorlig start<br>**Inställning**: Enhetsmodell(er) med åtgärden Tillåt specifik (rensa icke-specifik)                                                                                                                                     |
| ProtectAllIncomingUnknownSourceData              | E.t.                                                                                                                                                                                                                                                                                           | **Obs!** : Används inte aktivt av Intune-tjänsten.                                                                                                                                     |

## <a name="next-steps"></a>Nästa steg

- Mer information om appskyddsprinciper finns i [vad är appskyddsprinciper?](app-protection-policy.md)
- Intune erbjuder ett antal verktyg för att hjälpa dig att felsöka problem i din miljö. Mer information finns i [använd felsökningsportalen för att hjälpa användare](../fundamentals/help-desk-operators.md).