---
title: Serverhändelseloggar
titleSuffix: Configuration Manager
description: En teknisk referens för möjliga BitLocker (MBAM)-Server poster i händelse loggen i Windows
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: c3279b7d-654d-444b-bd17-1262894590c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe7d24bc1cad27094d720a5cb5aa487caec9199d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127873"
---
# <a name="server-event-logs"></a>Serverhändelseloggar

*Gäller för: Configuration Manager (aktuell gren)*

<!--3601034-->

Använd Windows-Loggboken för att visa händelse loggar för följande BitLocker Management Server-komponenter i Configuration Manager:

- Återställnings tjänst på hanterings platsen
- Självbetjäningsportalen
- Webbplats för administration och övervakning

Öppna Loggboken på en server som är värd för en eller flera av dessa komponenter. Gå sedan till **program-och tjänst loggar**, **Microsoft**, **Windows**och expandera **MBAM-Web**. Som standard finns det [Administratörs](#admin) -och [drift](#operational) händelse loggar.

Följande avsnitt innehåller meddelanden och felsöknings information för händelse-ID: n som kan uppstå med BitLocker-komponenter för hanterings servern.

## <a name="admin"></a>Administratör

### <a name="1-webappspnerror"></a>1: WebAppSpnError

Program: {webbplats namn} {VirtualDirectory} saknar följande SPN-namn (Service Principal Names): {ListOfSpns} registrera de nödvändiga SPN-namnen på kontot: {ExecutionAccount}.

För att integrerad Windows-autentisering ska fungera måste nödvändiga SPN: er finnas på plats. Det här meddelandet anger att det SPN som krävs för programmet inte har kon figurer ATS korrekt. Information som finns i den här händelsen bör ge mer information.

<!-- See "Service Principal Name (SPN)" in MBAM 2.5 Server Prerequisites for Stand-alone and Configuration Manager Integration Topologies for more information. -->

### <a name="100-adminservicerecoverydberror"></a>100: AdminServiceRecoveryDbError

Möjliga fel meddelanden:

- GetMachineUsers: ett fel uppstod när användar information skulle hämtas från databasen.
- GetRecoveryKey: ett fel uppstod vid hämtning av återställnings nyckeln från databasen.
- GetRecoveryKey: ett fel uppstod när användar information skulle hämtas från databasen.
- GetRecoveryKeyIds: ett fel uppstod vid hämtning av återställnings nyckel-ID från databasen.
- GetTpmHashForUser: ett fel uppstod när TPM-hashvärden hämtades från återställnings databasen.
- GetTpmHashForUser: ett fel uppstod när TPM-hashvärden hämtades från återställnings databasen.
- QueryDriveRecoveryData: ett fel uppstod när enhets återställnings data hämtades från databasen.
- QueryRecoveryKeyIdsForUser: ett fel uppstod vid hämtning av återställnings nyckel-ID från databasen.
- QueryVolumeUsers: ett fel uppstod när användar information skulle hämtas från databasen.

Det här meddelandet loggas när det finns ett undantag vid kommunikationen med återställnings databasen. Läs igenom informationen i spårningen för att få detaljerad information om undantaget.

### <a name="101-adminservicecompliancedberror"></a>101: AdminServiceComplianceDbError

Möjliga fel meddelanden:

- GetRecoveryKey: ett fel uppstod när en gransknings händelse skulle loggas till Compliance-databasen.
- GetRecoveryKeyIds: ett fel uppstod när en gransknings händelse skulle loggas till Compliance-databasen.
- GetTpmHashForUser: ett fel uppstod när en gransknings händelse skulle loggas till Compliance-databasen.
- QueryRecoveryKeyIdsForUser: ett fel uppstod när en gransknings händelse skulle loggas till Compliance-databasen.
- QueryDriveRecoveryData: ett fel uppstod när en gransknings händelse skulle loggas till Compliance-databasen.

Det här meddelandet loggas när det finns ett undantag vid kommunikationen med Compliance-databasen. Läs igenom informationen i spårningen för att få detaljerad information om undantaget.

### <a name="102-agentservicerecoverydberror"></a>102: AgentServiceRecoveryDbError

Det här meddelandet anger ett undantag när tjänsten försöker kommunicera med återställnings databasen. Läs igenom meddelandet i händelsen om du vill ha detaljerad information om undantaget.

Kontrol lera att MBAM-programpoolskontot har behörighet att ansluta till återställnings databasen.

### <a name="103-agentserviceerror"></a>103: AgentServiceError

Möjliga fel meddelanden:

- Det gick inte att identifiera klient dator kontot eller datamigreringens användar konto.

    När ett anrop görs till-, `PostKeyRecoveryInfo` - `IsRecoveryKeyResetRequired` `CommitRecoveryKeyRest` ,-eller `GetTpmHash` -webb metoderna hämtar den anropare kontext för att hämta autentiseringsuppgifter för anroparen. Om anrops kontexten är null eller tom loggar tjänsten det här meddelandet.

- Konto verifieringen misslyckades för anroparens identitet.

    Detta meddelande loggas om-webb metoden förväntar sig att anroparen ska vara ett dator konto och inte. Det kan också bero på att anroparen förväntar sig att anroparen ska vara ett användar konto, och det är inte ett användar konto eller medlem i ett konto för datamigrerings grupp.

### <a name="104-statusservicecompliancedbconfigerror"></a>104: StatusServiceComplianceDbConfigError

Databas anslutnings strängen för efterlevnad i registret är tom.

Detta meddelande loggas när databas anslutnings strängen för regelefterlevnad är ogiltig. Verifiera värdet i register nyckeln `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` .

### <a name="105-statusservicecompliancedberror"></a>105: StatusServiceComplianceDbError

Det här felet indikerar att webbplatserna eller webb tjänsterna inte kunde ansluta till Compliance-databasen. Verifiera att IIS-programpoolens konto kan ansluta till databasen.

### <a name="106-helpdeskerror"></a>106: HelpdeskError

Kända fel och möjliga orsaker:

- Begäran till URL orsakade ett internt fel.

    Ett ohanterat undantag har Aktiver ATS i programmet för administrations-och övervaknings webbplatsen (supportavdelningen). Granska logg posterna i **Administratörs** händelse loggen för att hitta det aktuella undantaget.

- Ett fel uppstod när information om körnings kontext skulle hämtas. Det gick inte att verifiera SPN-registreringen (Service Principal Name).

    Under den första inläsningen av support webbplatsen kontrollerar den SPN. För att verifiera SPN, kräver det konto information, IIS plats namn och ApplicationVirtualPath som motsvarar supportavdelningen. Det här fel meddelandet loggas när ett eller flera av dessa attribut är ogiltiga eller saknas.

- Ett fel uppstod när SPN-registreringen (Service Principal Name) verifierades.

    Det här meddelandet anger att ett säkerhets undantag uppstår när SPN verifieras. Mer information finns i undantaget i händelse informationen.

### <a name="107-selfserviceportalerror"></a>107: SelfServicePortalError

Kända fel och möjliga orsaker:

- Ett fel uppstod vid hämtning av återställnings nyckeln för en användare

    Indikerar att ett oväntat undantag uppstod när en begäran gjordes att hämta en återställnings nyckel. Referera till undantags meddelandet i händelse informationen. Om spårning är aktiverat i supportavdelningen, se spåra data för att få detaljerade undantags meddelanden.

- Ett fel uppstod när information om körnings kontext skulle hämtas. Det gick inte att verifiera SPN-registreringen (Service Principal Name)

    Under en inledande inläsning hämtar självbetjänings portalen konto information, IIS-namnområdet och ApplicationVirtualPath för självbetjänings webbplatsen för att verifiera SPN. Det här fel meddelandet loggas när ett eller flera av dessa attribut är ogiltiga.

- Ett fel uppstod när SPN-registreringen (Service Principal Name) verifierades. EventDetails: {ExceptionMessage}

    Det här meddelandet anger att ett säkerhets undantag uppstod när SPN verifierades. Mer information finns i undantaget i händelse informationen.

### <a name="108-domaincontrollererror"></a>108: DomainControllerError

Kända fel och möjliga orsaker:

- Ett fel uppstod vid matchning av domän namnet {domän namn}, ett minnesallokeringsfel uppstod.

    För att lösa domän namnet anropas `DsGetDcName` Windows-API: et. Det här meddelandet loggas när det här API: et returnerar `ERROR_NOT_ENOUGH_MEMORY` , vilket indikerar ett minnes tilldelnings fel.

- Det gick inte att anropa DsGetDcName-metoden

    Det här meddelandet anger att `DsGetDcName` API: t inte är tillgängligt på värden.

### <a name="109-webapprecoverydberror"></a>109: WebAppRecoveryDbError

Kända fel och möjliga orsaker:

- Ett fel uppstod när återställnings databasens konfiguration lästes. Anslutnings strängen till återställnings databasen har inte kon figurer ATS.

    Det här meddelandet anger att information om anslutnings strängen för återställnings databasen på `HKLM\Software\Microsoft\MBAM Server\Web\RecoveryDBConnectionString` är ogiltig. Verifiera värdet för register nyckeln.

Om du ser något av följande meddelanden kontrollerar du om autentiseringsuppgifterna för programpoolen från IIS-servern kan upprätta en anslutning till återställnings databasen:

- DoesUserHaveMatchingRecoveryKey: ett fel uppstod när återställnings nyckel-ID för en användare hämtades.
- QueryDriveRecoveryData: ett fel uppstod när enhets återställnings data hämtades.
- QueryRecoveryKeyIdsForUser: ett fel uppstod när återställnings nyckel-ID för en användare hämtades.
- Ett fel uppstod vid hämtning av TPM-lösenords-hash från återställnings databasen.

### <a name="110-webappcompliancedberror"></a>110: WebAppComplianceDbError

Kända fel och möjliga orsaker:

- Ett fel uppstod när konfigurationen av Compliance-databasen lästes. Anslutnings strängen till Compliance-databasen har inte kon figurer ATS.

    Det här meddelandet anger att information om databas anslutnings strängen för efterlevnad `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` är ogiltig. Verifiera värdet för den här register nyckeln.

Om du ser något av följande meddelanden kontrollerar du om autentiseringsuppgifterna för programpoolen från IIS-servern kan upprätta en anslutning till Compliance-databasen:

- GetRecoveryKeyForCurrentUser: ett fel uppstod när en gransknings händelse skulle loggas till Compliance-databasen.
- QueryRecoveryKeyIdsForUser: ett fel uppstod när en gransknings händelse skulle loggas till Compliance-databasen.
- QueryRecoveryKeyIdsForUser: ett fel uppstod när en gransknings händelse skulle loggas till Compliance-databasen.

### <a name="111-webappdberror"></a>111: WebAppDbError

Dessa fel indikerar något av följande två villkor

- MBAM-webbplatser/WebService kunde inte ansluta till efterlevnad eller återställnings databas
- MBAM webbplatser/WebServices-körnings konto (konto för programpool) kunde inte köra den `GetVersion` lagrade proceduren för efterlevnad eller återställnings databas

I meddelandet i händelsen finns mer information om undantaget.

Verifiera att programpoolskontot kan ansluta till databaserna för efterlevnad eller återställning. Bekräfta att den har behörighet att köra den `GetVersion` lagrade proceduren.

### <a name="112-webapperror"></a>112: WebAppError

Ett fel uppstod när SPN-registreringen (Service Principal Name) verifierades.

För att verifiera SPN frågar den Active Directory att hämta en lista över SPN-mappat körnings konto. Den frågar också `ApplicationHost.config` för att hämta webbplats bindningar. Det här fel meddelandet anger att det inte gick att kommunicera med Active Directory eller att filen inte kunde läsas in `ApplicationHost.config` .

Verifiera att programpoolskontot har behörighet att fråga Active Directory eller `ApplicationHost.config` filen. Kontrol lera också plats bindnings posterna i `ApplicationHost.config` filen.

## <a name="operational"></a>Operativ

### <a name="4-performancecountererror"></a>4: PerformanceCounterError

Ett fel uppstod vid hämtning av en prestanda räknare.

Spårnings meddelandet innehåller det faktiska undantags meddelandet, som visas här:

- ArgumentNullException: detta undantag uppstår om kategorin, räknaren eller en instans av begärd prestanda räknare är ogiltig.
- System. InvalidOperationException: kategori namn är en tom sträng (""). counterName är en tom sträng ("").
- Den begärda Läs-och skriv behörighets inställningen är ogiltig för den här räknaren.
- Den angivna kategorin finns inte (om readOnly är sant).
- Den angivna kategorin är inte en .NET Framework anpassad kategori (om readOnly är falskt).
- Den angivna kategorin har marker ATS som en Multiinstans och kräver att prestanda räknaren skapas med ett instans namn.
- instanceName är längre än 127 tecken.
- Kategori namn och counterName har lokaliserats till olika språk.
- System. ComponentModel. Win32Exception: ett fel uppstod vid åtkomst till ett system-API.
- System. UnauthorizedAccessException: kod som körs utan administratörs behörighet försökte läsa en prestanda räknare.

Meddelandet i händelsen innehåller mer information om undantaget.

För `System.UnauthorizedAccessException` kontrollerar du att programpoolskontot har åtkomst till API: er för prestanda räknare.

### <a name="200-helpdeskinformation"></a>200: HelpDeskInformation

Administrations webbplatsen har hittats och anslutits till en version som stöds av återställnings-/efterlevnadsprinciper.

Indikerar lyckad anslutning till återställnings-eller efterlevnadsprincip från support webbplatsen.

### <a name="201-selfserviceportalinformation"></a>201: SelfServicePortalInformation

Självbetjänings portalen har hittats och anslutits till en version som stöds av återställnings-/efterlevnads databasen.

Indikerar lyckad anslutning till återställnings-eller efterlevnadsprincip från självbetjänings portalen.

### <a name="202-webappinformation"></a>202: WebAppInformation

Programmets SPN har registrerats korrekt.

Anger att de SPN som krävs för supportavdelningen-webbplatsen har registrerats korrekt mot kontot som körs.

## <a name="see-also"></a>Se även

Mer information om hur du använder dessa loggar finns i [händelse loggar för BitLocker](about-event-logs.md).

Mer felsöknings information finns i [Felsöka BitLocker](troubleshoot.md).

Mer information om hur du installerar dessa webbplatser finns i [Konfigurera BitLocker-rapporter och portaler](../../deploy-use/bitlocker/setup-websites.md).
