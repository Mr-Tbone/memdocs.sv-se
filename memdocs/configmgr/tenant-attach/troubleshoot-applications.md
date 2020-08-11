---
title: Felsöka programinstallation
titleSuffix: Configuration Manager
description: Felsöka programinstallationen för Configuration Manager klient anslutning
ms.date: 08/10/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 75f47456-cd8d-4c83-8dc5-98b336a7c6c8
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 6960c85f8e01e3686541e537dfb4823826a77920
ms.sourcegitcommit: 47ed9af2652495adb539638afe4e0bb0be267b9e
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/10/2020
ms.locfileid: "88057600"
---
# <a name="troubleshoot-application-installation-for-devices-uploaded-to-the-admin-center-preview"></a>Felsöka programinstallationen för enheter som har överförts till administrations centret (för hands version)
<!--6374854, 6521921-->
*Gäller för: Configuration Manager (aktuell gren)*

Använd följande för att felsöka Configuration Manager-program i administrations centret för Microsoft Endpoint Manager:

> [!Important]
> Den här informationen är relaterad till en förhands gransknings funktion som kan ändras avsevärt innan den släpps kommersiellt. Microsoft lämnar inga garantier, uttryckliga eller underförstådda, avseende informationen som visas här.

## <a name="common-errors-from-the-microsoft-endpoint-manager-admin-center"></a>Vanliga fel från administrations centret för Microsoft Endpoint Manager

När du visar eller installerar program från administrations centret för Microsoft Endpoint Manager kan du köra något av dessa fel.  

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a>Nödvändig konfiguration saknas i Azure Active Directory

**Fel meddelande:** Nödvändig konfiguration saknas i Azure Active Directory. Se till att koppla Configuration Manager-platsen till din Azure-klient och tilldela rätt användar roll i Azure AD.

**Möjlig orsak:** Användar kontot saknar antagligen **Administratörs användar** rollen för Configuration Manager mikrotjänstprogram i Azure AD. Lägg till rollen i Azure AD från **företags program**  >  **Configuration Manager mikrotjänst**  >  **användare och grupper**  >  **Lägg till användare**. Grupper stöds om du har Azure AD Premium. Det kan ta upp till en timme innan ändringar av den här behörigheten börjar gälla.

### <a name="unable-to-get-application-information"></a><a name="bkmk_noinfo"></a>Det gick inte att hämta programinformation

**Fel meddelande 1:** Det gick inte att hämta programinformation. Kontrol lera att Azure AD och AD-identifiering av användare har kon figurer ATS och att användaren identifieras av båda. Kontrol lera att användaren har rätt behörigheter i Configuration Manager.

**Möjliga orsaker:** Detta fel beror vanligt vis på ett problem med administratörs kontot. Nedan visas de vanligaste problemen med det administrativa användar kontot:

1. Använd samma konto för att logga in i administrations centret. Den lokala identiteten måste vara synkroniserad med och överensstämma med moln identiteten.
1. Kontrol lera att kontot har behörigheten **läsa** för enhetens **samling** i Configuration Manager.
1. Kontrol lera att Configuration Manager har identifierat det administrativa användar konto som du använder. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen. Välj noden **användare** och hitta ditt användar konto.

    Om ditt konto inte visas i noden **användare** kontrollerar du konfigurationen av platsens [Active Directory användar identifiering](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

1. Verifiera identifierings data. Välj ditt användarkonto. På fliken **Start** i menyfliksområdet väljer du **Egenskaper**. I fönstret Egenskaper bekräftar du följande identifierings data:

    - **Azure Active Directory klient-ID**: det här värdet ska vara ett GUID för Azure AD-klienten.
    - **Azure Active Directory användar-ID**: det här värdet ska vara ett GUID för det här kontot i Azure AD.
    - **Användarens huvud namn**: formatet för det här värdet är user@domain . Till exempel `jqpublic@contoso.com`.

    Om Azure AD-egenskaperna är tomma kontrollerar du konfigurationen för platsens identifiering av [Azure AD-användare](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc).

### <a name="unexpected-error-occurred"></a><a name="bkmk_1603"></a>Ett oväntat fel uppstod

**Fel meddelande:** Ett oväntat fel uppstod

**Möjliga orsaker:** Oväntade fel orsakas vanligt vis av antingen [tjänst anslutnings punkt](../core/servers/deploy/configure/about-the-service-connection-point.md), [administrations tjänst](../develop/adminservice/overview.md)eller anslutnings problem.

1. Kontrol lera att tjänst anslutnings punkten är ansluten till molnet med hjälp av **CMGatewayNotificationWorker. log**.
1. Kontrol lera att den administrativa tjänsten är felfri genom att granska SMS_REST_PROVIDER-komponenten från plats komponent övervakning på den centrala platsen.
1. IIS måste vara installerat på en-leverantörs dator. Mer information finns i [krav för administrations tjänsten](../develop/adminservice/overview.md#prerequisites).

### <a name="the-site-information-hasnt-yet-synchronized"></a><a name="bkmk_sync"></a>Plats informationen har ännu inte synkroniserats

**Fel meddelande:** Plats informationen har ännu inte synkroniserats från Configuration Manager till administrations centret för Microsoft Endpoint Manager. Vänta upp till 15 minuter efter att du har anslutit platsen till din Azure-klient.

**Möjliga orsaker:**
- Det här felet uppstår vanligt vis vid nyregistrering till klient anslutning. Vänta i 15 minuter för att synkronisera informationen.
- Det här felet kan också visas om den centrala administrations platsen har uppgraderats till en ny Configuration Manager-version men vissa underordnade primära platser ännu inte har uppgraderats.

### <a name="application-shows-as-installed-after-creating-a-new-deployment"></a><a name="bkmk_installed"></a>Programmet visas som installerat när du har skapat en ny distribution

**Symptom:** Ett program visas som installerat i Microsoft Endpoint Manager administrations Center när du har skapat en ny enhet som är tillgänglig kräver distribution av godkännande eller en användare som är tillgänglig.

**Möjlig orsak:** Det program tillstånd som visas för enheten kommer från en annan aktiv eller tidigare distribution.

### <a name="errors-when-searching-or-retrying-an-installation"></a><a name="bkmk_hfru"></a>Fel vid sökning eller försök att installera igen

**Symptom:** Fel uppstod när följande åtgärder utförs:
- Använd Sök
- Välj **försök installera igen**

**Möjlig orsak:**  Se till att den [samlade uppdateringen för Microsoft Endpoint Configuration Manager version 2002](https://support.microsoft.com/help/4560496/) och motsvarande version av konsolen är installerad. Mer information finns i [krav för att installera ett program från administrations centret](applications.md#prerequisites).

## <a name="known-issues"></a>Kända problem

### <a name="unexpected-error-occurred-when-gettingapplications"></a>Ett oväntat fel uppstod när program hämtades

**Scenario:** Hämtning av listan över program tar längre tid än förväntat när du kör Configuration Manager version 2002 och du ser `unexpected error occurred` .

**Fel meddelande:** AdminService. log kommer att innehålla:

```log 
System.Data.Entity.Core.EntityCommandExecutionException: An error occurred while executing the command definition. See the inner exception for details.
System.Data.SqlClient.SqlException: Execution Timeout Expired.  The timeout period elapsed prior to completion of the operation or the server is not responding.
System.ComponentModel.Win32Exception: The wait operation timed out
```

**Lösning:** En lösning är för närvarande inte tillgänglig.

### <a name="application-installation-times-out-if-application-requires-restart"></a>Tids gränsen uppnåddes för program installationen om programmet kräver omstart

**Scenario:** Om du kör Configuration Manager version 2002 och ett program kräver en omstart för att slutföra installations processen, kan det hända att installationen tar slut.

**Symptom:** Användaren ser `restart pending` meddelanden och i Software Center. Från administrations centret för Microsoft Endpoint Manager förblir programmet i det här `Installing` läget.  

**Lösning:** När användaren startar om enheten visas rätt status i administrations centret.

## <a name="next-steps"></a>Nästa steg

[Felsöka klientkoppling](troubleshoot.md)
