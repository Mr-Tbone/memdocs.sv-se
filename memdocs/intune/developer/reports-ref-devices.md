---
title: Enheter – Intune-informationslager
titleSuffix: Microsoft Intune
description: Referensavsnitt för kategorin Program för entitetssamlingar i API:et för Intune-informationslager.
keywords: Intune-informationslager
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/03/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6955E12D-70D7-4802-AE3B-8B276F01FA4F
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: ae1f0117f6dbf186b3a4bdddb393d053c33c914a
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79359800"
---
# <a name="reference-for-devices-entities"></a>Referens för enhetsentiteter

Kategorin **enheter** innehåller entiteter för mobilenheter som spårar information, till exempel:

- Enhetstyp
- Enhetsregistrering och registreringsstatus
- Äganderätt till enhet
- Status för enhetshantering
- Enhetsmedlemskap i Azure AD-status
- Registreringsstatus
- Tidigare information om enheten
- Inventering av appar på enheten

## <a name="devicetypes"></a>deviceTypes

Entiteten **deviceTypes** representerar den enhetstyp som andra informationslagerentiteter refererar till. Enhetstypen beskriver vanligtvis antingen enhetsmodell, tillverkare eller både och.

| Egenskap  | Beskrivning |
|---------|------------|
| deviceTypeID |Unikt id för enhetstyp |
| deviceTypeKey |Unikt id för enhetstypen i informationslagret – surrogatnyckel |
| deviceTypeName |Enhetstyp |

### <a name="example"></a>Exempel

| deviceTypeID  | Name | Beskrivning |
|---------|------------|--------|
| 0 |Skrivbord |Windows Desktop-enhet |
| 1 |WindowsRT |WindowsRT-enhet |
| 2 |WinMO6 |Windows Mobile 6.0-enhet |
| 3 |Nokia |Nokia-enhet |
| 4 |WindowsPhone |Windows Phone-enhet |
| 5 |Mac |Mac-enhet |
| 6 |WinCE |Windows CE-enhet |
| 7 |WinEmbedded |Windows Embedded-enhet |
| 8 |IPhone |iPhone-enhet |
| 9 |iPad |iPad-enhet |
| 10 |iPod |iPod-enhet |
| 11 |Android |Android-enhet som hanteras via enhetsadministratören |
| 12 |ISocConsumer |iSoc Consumer-enhet |
| 14 |MacMDM |Mac OS X-enhet som hanteras med den inbyggda MDM-agenten |
| 15 |HoloLens |HoloLens-enhet |
| 16 |SurfaceHub |Surface Hub-enhet |
| 17 |AndroidForWork |Android-enhet som hanteras med hjälp av Android-profilens ägare |
| 100 |Blackberry |Blackberry-enhet |
| 101 |Palm |Palm-enhet |
| 255 |Okänt |Okänd typ av enhet |

## <a name="enrollmentactivities"></a>enrollmentActivities 
Entiteten **enrollmentActivity** visar en enhetsregistrerings aktivitet.

| Egenskap                      | Beskrivning                                                               |
|-------------------------------|---------------------------------------------------------------------------|
| dateKey                       | Nyckeln för det datum då den här registreringsaktiviteten registrerades.               |
| deviceEnrollmentTypeKey       | Nyckeln för registreringens typ.                                        |
| deviceTypeKey                 | Nyckeln för enhetens typ.                                                |
| enrollmentEventStatusKey      | Nyckeln för den status som visar om registreringen lyckades eller misslyckades.    |
| enrollmentFailureCategoryKey  | Nyckeln för registreringsfelets kategori (om registreringen misslyckades).        |
| enrollmentFailureReasonKey    | Nyckeln för registreringsfelets orsak (om registreringen misslyckades).          |
| osVersion                     | Enhetens operativsystemversion.                               |
| count                         | Totalt antal registreringsaktiviteter som matchar klassificeringarna ovan.  |

## <a name="enrollmenteventstatuses"></a>enrollmentEventStatuses 
Entiteten **enrollmentEventStatus** visar en enhetsregistrerings resultat.

| Egenskap                   | Beskrivning                                                                       |
|----------------------------|-----------------------------------------------------------------------------------|
| enrollmentEventStatusKey   | Unik identifierare för registreringsstatusen i informationslagret (surrogatnyckel)  |
| enrollmentEventStatusName  | Namnet på registreringsstatusen. Se exemplen nedan.                            |

### <a name="example"></a>Exempel

| enrollmentEventStatusName  | Beskrivning                            |
|----------------------------|----------------------------------------|
| Klart                    | En lyckad enhetsregistrering         |
| Misslyckades                     | En misslyckad enhetsregistrering             |
| Inte tillgängligt              | Registreringsstatusen är inte tillgänglig.  |

## <a name="enrollmentfailurecategories"></a>enrollmentFailureCategories 
Entiteten **EnrollmentFailureCategory** visar varför en enhetsregistrering misslyckades. 

| Egenskap                       | Beskrivning                                                                                 |
|--------------------------------|---------------------------------------------------------------------------------------------|
| enrollmentFailureCategoryKey   | Unik identifierare för registreringsfelets kategori i informationslagret (surrogatnyckel)  |
| enrollmentFailureCategoryName  | Namnet på registreringsfelets kategori. Se exemplen nedan.                            |

### <a name="example"></a>Exempel

| enrollmentFailureCategoryName   | Beskrivning                                                                                                   |
|---------------------------------|---------------------------------------------------------------------------------------------------------------|
| Ej tillämpligt                  | Registreringsfelets kategori är inte tillämplig.                                                            |
| Inte tillgängligt                   | Registreringsfelets kategori är inte tillgänglig.                                                             |
| Okänt                         | Okänt fel.                                                                                                |
| Autentisering                  | Autentiseringen misslyckades.                                                                                        |
| Auktorisering                   | Anropet har autentiserats, men inte auktoriserats för registrering.                                                         |
| AccountValidation               | Det gick inte att verifiera kontot för registrering. (Kontot är blockerat, registrering är inte aktiverat)                      |
| UserValidation                  | Det gick inte att verifiera användaren. (Användaren finns inte, licens saknas)                                           |
| DeviceNotSupported              | Enheten stöds inte för hantering av mobilenheter.                                                         |
| InMaintenance                   | Kontot genomgår underhåll.                                                                                    |
| BadRequest                      | Klienten skickade en begäran som inte förstås/stöds av tjänsten.                                        |
| FeatureNotSupported             | Funktioner som används av den här registreringen stöds inte för det här kontot.                                        |
| EnrollmentRestrictionsEnforced  | Registreringsbegränsningar som konfigurerats av administratören blockerade den här registreringen.                                          |
| ClientDisconnected              | Tidsgränsen gick ut för klienten eller så avbröts registreringen av slutanvändaren.                                                        |
| UserAbandonment                 | Registreringen lämnades av slutanvändaren. (Slutanvändaren inledde registrering men slutförde den inte inom rimlig tid)  |

## <a name="enrollmentfailurereasons"></a>enrollmentFailureReasons  
Entiteten **EnrollmentFailureReason** visar en mer detaljerad orsak till ett enhetsregistreringsfel inom en viss felkategori.  

| Egenskap                     | Beskrivning                                                                               |
|------------------------------|-------------------------------------------------------------------------------------------|
| enrollmentFailureReasonKey   | Unik identifierare för registreringsfelets orsak i informationslagret (surrogatnyckel)  |
| enrollmentFailureReasonName  | Namnet på registreringsfelets orsak. Se exemplen nedan.                            |

### <a name="example"></a>Exempel

| enrollmentFailureReasonName      | Beskrivning                                                                                                                                                                                            |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Ej tillämpligt                   | Registreringsfelets orsak är inte tillämplig.                                                                                                                                                       |
| Inte tillgängligt                    | Registreringsfelets orsak är inte tillgänglig.                                                                                                                                                        |
| Okänt                          | Okänt fel.                                                                                                                                                                                         |
| UserNotLicensed                  | Användaren hittades inte i Intune eller har inte någon giltig licens.                                                                                                                                     |
| UserUnknown                      | Användaren är inte känd i Intune.                                                                                                                                                                           |
| BulkAlreadyEnrolledDevice        | Endast en användare kan registrera en enhet. Den här enheten har tidigare registrerats av en annan användare.                                                                                                                |
| EnrollmentOnboardingIssue        | Intune som utfärdare för hantering av mobilenheter (MDM) har inte konfigurerats ännu.                                                                                                                                 |
| AppleChallengeIssue              | Installationen av iOS-hanteringsprofilen försenades eller misslyckades.                                                                                                                                         |
| AppleOnboardingIssue             | Ett Apple MDM-pushcertifikat krävs för registrering i Intune.                                                                                                                                       |
| DeviceCap                        | Användaren försökte registrera fler enheter än maximalt tillåtna.                                                                                                                                        |
| AuthenticationRequirementNotMet  | Intune-registreringstjänsten kunde inte auktorisera den här begäran.                                                                                                                                            |
| UnsupportedDeviceType            | Den här enheten uppfyller inte minimikraven för Intune-registrering.                                                                                                                                  |
| EnrollmentCriteriaNotMet         | Det gick inte att registrera den här enheten på grund av en konfigurerad regel för registreringsbegränsning.                                                                                                                          |
| BulkDeviceNotPreregistered       | Den här enhetens IMEI (International Mobile Equipment Identifier) eller serienummer hittades inte.  Utan den här identifieraren betraktas enheter som privatägda enheter som för närvarande blockeras.  |
| FeatureNotSupported              | Användaren försökte få åtkomst till en funktion som ännu inte har släppts för alla kunder eller inte är kompatibel med Intune-konfigurationen.                                                            |
| UserAbandonment                  | Registreringen lämnades av slutanvändaren. (Slutanvändaren inledde registrering men slutförde den inte inom rimlig tid)                                                                                           |
| APNSCertificateExpired           | Apple-enheter kan inte hanteras med ett Apple MDM-pushcertifikat som har upphört att gälla.                                                                                                                            |
## <a name="ownertypes"></a>ownerTypes

Entiteten **enrollmentTypes** visar om en enhet är företagsägd, privat ägd eller okänd.

| Egenskap  | Beskrivning | Exempel |
|---------|------------|--------|
| ownerTypeID |Unikt id för ägartyp. | |
| ownerTypeKey |Unikt id för ägartypen i informationslagret – surrogatnyckel. | |
| ownerTypeName |Representerar enheternas ägartyp:  <br>Företag – enheten är företagsägd. <br>Privat – enheten är privatägd (BYOD).  <br>Okänd – det finns ingen information om enheten. |Företag Privat Okänd |

> [!Note]  
> För `ownerTypeName` i AzureAD måste du ange filtervärdet `deviceOwnership` som `Company` när du skapar dynamiska grupper för enheter. Mer information finns i [Regler för enheters](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices). 

## <a name="managementstates"></a>managementStates

Entiteten **managementStates** innehåller information om enhetens tillstånd. Informationen kan vara användbar i fall där fjärråtgärder tillämpas, om enheten är jailbrokad eller rotad.

| Egenskap  | Beskrivning |
|---------|------------|
| managementStateID | Unikt id för hanteringstillståndet. |
| managementStateKey | Unikt id för hanteringstillståndet i informationslagret – surrogatnyckel. |
| managementStateName | Visar status för den fjärranslutna åtgärden som utförts på den här enheten. |

### <a name="example"></a>Exempel

| managementStateID  | Name | Beskrivning |
|---------|------------|--------|
| 0 |Hanterade | Hanterad utan väntande fjärråtgärder. |
| 1 |RetirePending | Ett kommando för tillbakadragande väntar på enheten. |
| 2 |RetireFailed | Det gick inte att utföra kommandot för tillbakadragande på enheten. |
| 3 |WipePending | Ett rensningskommando väntar på enheten. |
| 4 |WipeFailed | Det gick inte att utföra rensningskommandot på enheten. |
| 5 |Ohälsosamt | Ej felfritt tillstånd. |
| 6 |DeletePending | Ett borttagningskommando väntar på enheten. |
| 7 |RetireIssued | Ett kommando om tillbakadragande har utfärdats till enheten. |
| 8 |WipeIssued | Ett rensningskommando har utfärdats. |
| 9 |WipeCanceled | Rensningskommandot har avbrutits. |
| 10 |RetireCanceled | Kommandot för tillbakadragande har avbrutits. |
| 11 |Discovered | Enheten har nyligen identifierats av Intune. När den checkar in för första gången övergår den i tillståndet Managed (hanterad). |

## <a name="managementagenttypes"></a>managementAgentTypes

Entiteten **managementAgentType** representerar de agenter som används för att hantera en enhet.

| Egenskap  | Beskrivning |
|---------|------------|
| managementAgentTypeID | Unikt id för typ av hanteringsagent. |
| managementAgentTypeKey | Unikt id för typ av hanteringsagent i informationslagret – surrogatnyckel. |
| managementAgentTypeName |Visar vilken typ av agent som används för att hantera enheten. |

### <a name="example"></a>Exempel

| ManagementAgentTypeID  | Name | Beskrivning |
|---------|------------|--------|
| 1 |EAS | Enheten hanteras via Exchange Active Sync |
| 2 |MDM | Enheten hanteras med hjälp av en agent för mobilenhetshantering |
| 3 |EasMdm | Enheten hanteras både av Exchange Active Sync och en agent för mobilenhetshantering |
| 4 |IntuneClient | Enheten hanteras av Intune PC-agenten |
| 5 |EasIntuneClient | Enheten hanteras både av Exchange Active Sync och Intune PC-agenten |
| 8 |ConfigManagerClient | Enheten hanteras av Configuration Manager-agenten |
| 16 |Okänt | Okänd typ av hanteringsagent |

## <a name="devices"></a>devices

Entiteten **enheter** innehåller en lista över registrerade hanterade enheter och deras respektive egenskaper.

|          Egenskap          |                                                                                       Beskrivning                                                                                      |
|:--------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| deviceKey                  | Unik identifierare för enheten i informationslagret – surrogatnyckel.                                                                                                               |
| deviceId                   | Unik identifierare för enheten.                                                                                                                                                     |
| deviceName                 | Namnet på enheten på plattformar som tillåter namngivning av enheter. På andra plattformar skapar Intune ett namn utifrån övriga egenskaper. Det här attributet kan inte göras tillgängligt för alla enheter. |
| deviceTypeKey              | Nyckeln för attributet enhetstyp för den här enheten.                                                                                                                                    |
| deviceRegistrationState    | Nyckeln för attributet klientregistreringstillstånd för den här enheten.                                                                                                                      |
| ownerTypeKey               | Nyckeln för attributet ägartyp för den här enheten: företag, privat eller okänd.                                                                                                    |
| enrolledDateTime           | Datum och tid då enheten registrerades.                                                                                                                                         |
| lastSyncDateTime           | Senast kända incheckning på Intune.                                                                                                                                              |
| managementAgentKey         | Nyckeln för den hanteringsagent som är kopplad till den här enheten.                                                                                                                             |
| managementStateKey         | Nyckeln för det hanteringstillstånd som är kopplat till enheten och som visar det senaste tillståndet för en fjärråtgärd eller om den har brutits upp/rotats.                                                |
| azureADDeviceId            | Azure-deviceID för den här enheten.                                                                                                                                                  |
| azureADRegistered          | Om enheten är registrerad i Azure Active Directory.                                                                                                                             |
| deviceCategoryKey          | Nyckeln för den kategori som är kopplad till den här enheten.                                                                                                                                     |
| deviceEnrollmentType       | Nyckeln för den registreringstyp som är kopplad till den här enheten och som visar registreringsmetod.                                                                                             |
| complianceStateKey         | Nyckel för den kompatibilitetsstatus som är kopplad till den här enheten.                                                                                                                             |
| osVersion                  | Enhetens operativsystemversion.                                                                                                                                                |
| easDeviceId                | Exchange ActiveSync-ID för enheten.                                                                                                                                                  |
| serialNumber               | Serienummer                                                                                                                                                                           |
| userId                     | Unik identifierare för användaren som är kopplad till enheten.                                                                                                                           |
| rowLastModifiedDateTimeUTC | Datum och tid i UTC när den här enheten senast ändrades i informationslagret.                                                                                                       |
| manufacturer               | Enhetstillverkaren                                                                                                                                                             |
| modell                      | Enhetsmodell                                                                                                                                                                    |
| operatingSystem            | Enhetens operativsystem. Windows, iOS/iPadOS och så vidare.                                                                                                                                   |
| isDeleted                  | Binärt tal för att visa om enheten har tagits bort eller inte.                                                                                                                                 |
| androidSecurityPatchLevel  | Nivå för Android-säkerhetsuppdatering                                                                                                                                                           |
| MEID                       | MEID                                                                                                                                                                                   |
| isSupervised               | Status för övervakad enhet                                                                                                                                                               |
| freeStorageSpaceInBytes    | Ledigt lagringsutrymme i byte.                                                                                                                                                                 |
| totalStorageSpaceInBytes   | Totalt lagringsutrymme i byte.                                                                                                                                                                |
| encryptionState            | Krypteringstillstånd på enheten.                                                                                                                                                      |
| subscriberCarrier          | Abonnentens operatör på enheten                                                                                                                                                       |
| phoneNumber                | Enhetens telefonnummer                                                                                                                                                             |
| IMEI                       | IMEI                                                                                                                                                                                   |
| cellularTechnology         | Enhetens mobilteknik                                                                                                                                                    |
| WiFiMacAddress             | Wi-Fi MAC                                                                                                                                                                              |
| ICCD                       | Integrated Circuit Card Identifier (identifierare för integrerat kretskort)                                                                                                                                                     |

## <a name="devicepropertyhistories"></a>devicePropertyHistories

Entiteten **devicePropertyHistory** innehåller samma egenskaper som enhetstabellen och dagliga ögonblicksbilder av varje enhetspost per dag under de senaste 90 dagarna. I kolumnen DateKey visas dagen för varje rad.

|          Egenskap          |                                                                                      Beskrivning                                                                                     |
|:--------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| dateKey                    | Referens till datumtabellen som visar dag.                                                                                                                                          |
| deviceKey                  | Unik identifierare för enheten i informationslagret – surrogatnyckel. Det här är en referens till enhetstabellen som innehåller Intune-enhetens ID.                               |
| deviceName                 | Namn på enheten på plattformar som tillåter namngivning av enheter. På andra plattformar skapar Intune ett namn för andra egenskaper. Det här attributet kan inte göras tillgängligt för alla enheter. |
| deviceRegistrationStateKey | Nyckeln för attributet enhetsregistreringstillstånd för den här enheten.                                                                                                                    |
| ownerTypeKey               | Nyckeln för attributet ägartyp för den här enheten: företag, privat eller okänd.                                                                                                  |
| managementStateKey         | Nyckeln för det hanteringstillstånd som är kopplat till enheten och som visar det senaste tillståndet för en fjärråtgärd eller om den har brutits upp/rotats.                                                |
| azureADRegistered          | Om enheten är registrerad i Azure Active Directory.                                                                                                                             |
| complianceStateKey         | En nyckel för ComplianceState.                                                                                                                                                            |
| OSVersion                  | OS-version.                                                                                                                                                                          |
| jailBroken                 | Om enheten har brutits upp eller rotats.                                                                                                                                         |
| deviceCategoryKey          | Nyckeln för attributet enhetskategori för den här enheten. 

