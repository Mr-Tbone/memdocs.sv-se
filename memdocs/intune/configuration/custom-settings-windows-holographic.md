---
title: Anpassade inställningar – Windows Holographic for Business-enheter – Microsoft Intune | Microsoft Docs
description: Lägg till eller skapa en anpassad profil för att använda OMA-URI-inställningar för enheter som kör Windows Holographic for Business i Microsoft Intune, inklusive Microsoft Hololens. Du kan ange CSP-principinställningarna AllowFastReconnect, AllowVPN, AllowUpdateService, UpdateServiceURL, RequireUpdatesApproval, ApprovedUpdates och ApplicationLaunchRestrictions.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.article: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.topic: reference
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3928cd13b5368c8ab196a67669cb3a9f7d3fc2e9
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910034"
---
# <a name="use-custom-settings-for-windows-holographic-for-business-devices-in-intune"></a>Använda anpassade inställningar för Windows Holographic for Business-enheter i Intune

Med Microsoft Intune kan du lägga till eller skapa anpassade inställningar för dina Windows Holographic for Business-enheter med hjälp av ”anpassade profiler”. Anpassade profiler är en funktion i Intune. De gör att du kan lägga till enhetsinställningar och funktioner som inte är inbyggda i Intune.

Windows Holographic for Business-anpassade profiler använder OMA-URI-inställningar (Open Mobile Alliance Uniform Resource Identifier) för att konfigurera olika funktioner. De här inställningarna används vanligtvis av tillverkare av mobila enheter till att styra funktioner på enheten.

Windows Holographic for Business gör många inställningar för konfigurationstjänstleverantörer tillgängliga. En översikt över CSP finns i [Introduction to configuration service providers (CSPs) for IT pros](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers) (Introduktion till konfigurationstjänstleverantörer (CSP:er) för IT-proffs). Specifika CSP:er som stöds av Windows Holographic visas i [CSPs supported in Windows Holographic](/windows/client-management/mdm/configuration-service-provider-reference#hololens) (CSP:er som stöds i Windows Holographic).

Glöm inte att [Windows Holographic for Business-enhetsbegränsningsprofilen](device-restrictions-windows-holographic.md) innehåller många inbyggda inställningar som du kan använda. Det betyder att du kanske inte behöver ange anpassade värden.

Den här artikeln beskriver hur du skapar en anpassad profil för Windows Holographic for Business-enheter. Den innehåller också en lista med rekommenderade OMA-URI-inställningar.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en anpassad Windows 10-profil](custom-settings-configure.md#create-the-profile).

## <a name="custom-oma-uri-settings"></a>Anpassade OMA-URI-inställningar

**Lägg till**: Ange följande inställningar:

- **Namn**: Ange ett unikt namn för OMA-URI-inställningen som hjälper dig att identifiera den i listan över inställningar.
- **Beskrivning**: Ange en beskrivning som ger en översikt över inställningen, samt annan viktig information.
- **OMA-URI** (skiftlägeskänslig): Ange den OMA-URI som du vill använda som inställning.
- **Datatyp**: Välj den datatyp som du vill använda för den här OMA-URI-inställningen. Alternativen är:

  - Sträng
  - Sträng (XML-fil)
  - Datum och tid
  - Heltal
  - Flyttal
  - Boolesk
  - Base64 (fil)

- **Värde**: Ange det datavärde som du vill associera med den OMA-URI som du har angett. Värdet beror på vilken datatyp du valt. Om du till exempel valde **Datum och tid**, väljer du värdet från en datumväljare.

När du har lagt till några inställningar kan du välja **Exportera**. **Exportera** skapar en lista över alla värden som du har lagt till i en fil med kommaavgränsade värden (.csv).

## <a name="recommended-custom-settings"></a>Rekommenderade anpassade inställningar

Följande inställningar är användbara för enheter som kör Windows Holographic for Business:

### <a name="allowfastreconnect"></a>[AllowFastReconnect](/windows/client-management/mdm/policy-csp-authentication#authentication-allowfastreconnect)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datatyp|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Authentication/AllowFastReconnect|Heltal<br/>0 – inte tillåten<br/>1 – tillåten (standard)|

### <a name="allowupdateservice"></a>[AllowUpdateService](/windows/client-management/mdm/policy-csp-update#update-allowupdateservice)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datatyp|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/AllowUpdateService|Heltal<br/>0 – Uppdateringstjänsten är inte tillåten <br/>1 – Uppdateringstjänsten är tillåten (standard).|

### <a name="allowvpn"></a>[AllowVPN](/windows/client-management/mdm/policy-csp-settings#settings-allowvpn)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datatyp|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Settings/AllowVPN|Heltal<br/>0 – inte tillåten<br/>1 – tillåten (standard)|

### <a name="requireupdateapproval"></a>[RequireUpdateApproval](/windows/client-management/mdm/policy-csp-update#update-requireupdateapproval)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datatyp|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/RequireUpdateApproval|Den här inställningen är tillgänglig i RS5 (version 17763) och tidigare. Från och med 19H1 (version 18362) använder du [Windows Update för företag](../protect/windows-update-for-business-configure.md).<br/><br/>Heltal<br/>0 – Inte konfigurerat. Enheten installerar alla tillämpliga uppdateringar.<br/>1 – Enheten installerar endast uppdateringar som både är tillämpliga och finns i listan med godkända uppdateringar. Ställ in principen på 1 om IT-avdelningen vill styra distributionen av uppdateringar till enheter, till exempel när testning krävs före distributionen.|

### <a name="scheduledinstalltime"></a>[ScheduledInstallTime](/windows/client-management/mdm/policy-csp-update#update-scheduledinstalltime)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datatyp|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/ScheduledInstallTime|Heltal 0–23, där 0 = 12AM och 23 = 11PM<br/>Standardvärdet är 3.|

### <a name="updateserviceurl"></a>[UpdateServiceURL](/windows/client-management/mdm/policy-csp-update#update-updateserviceurl)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datatyp|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/UpdateServiceUrl|Den här inställningen är tillgänglig i RS5 (version 17763) och tidigare. Från och med 19H1 (version 18362) använder du [Windows Update för företag](../protect/windows-update-for-business-configure.md).<br/><br/>Sträng<br/>URL – Enheten söker efter uppdateringar från WSUS-servern med angiven URL.<br/>Inte konfigurerad – Enheten söker efter uppdateringar från Microsoft Update.|

### <a name="approvedupdates"></a>[ApprovedUpdates](/windows/client-management/mdm/update-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datatyp|
> |---|---|
> |./Vendor/MSFT/Update/ApprovedUpdates/*GUID*<br/><br/>**Viktigt!**<br/>Du måste läsa och godkänna uppdateringens användaravtal åt dina slutanvändare. Om detta inte utförs uppstår en juridisk säkerhetsöverträdelse eller ett avtalsbrott.|Nod för godkännanden av uppdateringar och licensavtal åt slutanvändaren.<br/><br/>Mer information finns i [Uppdatera CSP](/windows/client-management/mdm/update-csp).|

### <a name="applicationlaunchrestrictions"></a>[ApplicationLaunchRestrictions](/windows/client-management/mdm/applocker-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datatyp|
> |----|---|
> |./Vendor/MSFT/AppLocker/ApplicationLaunchRestrictions/*Grouping*/*ApplicationType*/Policy<br/><br/>**Viktigt!**<br/>I AppLocker CSP-artikeln används undantagna XML-exempel. Om du vill konfigurera inställningarna med anpassade Intune-profiler, måste du använda vanlig XML.|Sträng<br/>Mer information finns i [AppLocker CSP](/windows/client-management/mdm/applocker-csp).|

### <a name="deletionpolicy"></a>[DeletionPolicy](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datatyp|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/DeletionPolicy|Heltal<br/>0 – ta bort omedelbart när enheten återgår till ett tillstånd utan aktiva användare<br/>1 – ta bort vid tröskelvärde för lagringskapacitet (standard)<br/>2 – ta bort både vid tröskelvärde för lagringskapacitet och vid tröskelvärde för profilinaktivitet|

### <a name="enableprofilemanager"></a>[EnableProfileManager](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datatyp|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/EnableProfileManager|Boolesk<br/>True – aktivera<br/>False – inaktivera (standard)|

### <a name="profileinactivitythreshold"></a>[ProfileInactivityThreshold](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datatyp|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/ProfileInactivityThreshold|Heltal<br/>Standardvärdet är 30.|

### <a name="storagecapacitystartdeletion"></a>[StorageCapacityStartDeletion](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datatyp|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStartDeletion|Heltal<br/>Standardvärdet är 25.|

### <a name="storagecapacitystopdeletion"></a>[StorageCapacityStopDeletion](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Datatyp|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStopDeletion|Heltal<br/>Standardvärdet är 50.|

## <a name="find-the-policies-you-can-configure"></a>Hitta principer som du kan konfigurera

Du hittar en fullständig lista över alla konfigurationstjänstleverantörer (CSP:er) som Windows Holographic har stöd för i [CSPs supported in Windows Holographic](/windows/client-management/mdm/configuration-service-provider-reference#hololens) (CSP:er som stöds i Windows Holographic). Alla inställningar är inte kompatibla med alla versioner av Windows Holographic. Tabellen i avsnittet med [CSP:er som stöds i Windows Holographic](/windows/client-management/mdm/configuration-service-provider-reference#hololens) innehåller en lista över versionerna som stöds för varje CSP.

Observera att Intune inte stöder alla inställningar som anges i avsnittet med [CSP:er som stöds i Windows Holographic](/windows/client-management/mdm/configuration-service-provider-reference#hololens). Om du vill veta om Intune har stöd för den inställning som du vill använda, kan du öppna artikeln för den inställningen. Varje inställningssida visar den åtgärd som stöds. Om du vill arbeta med Intune måste inställningen ha stöd för åtgärderna **Lägg till** eller **Ersätt**.

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Skapa en anpassad profil på [Windows 10-enheter](custom-settings-windows-10.md).

Läs mer om [anpassade profiler](custom-settings-configure.md) i Intune.