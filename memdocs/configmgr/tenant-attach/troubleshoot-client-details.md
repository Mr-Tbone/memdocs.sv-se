---
title: Felsöka klient information
titleSuffix: Configuration Manager
description: Felsöka klient information för Configuration Manager klient anslutning
ms.date: 07/08/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 2a30e141bb5ea4d7508bf81f53f173e2a3154f08
ms.sourcegitcommit: 3806a1850813b7a179d703e002bcc5c7eb1cb621
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86210779"
---
# <a name="troubleshoot-configmgr-client-details-in-the-admin-center-preview"></a>Felsöka klient information för ConfigMgr i administrations Center (för hands version)
<!--6374854, 6521921-->
Använd följande för att felsöka information om ConfigMgr-klienten i administrations centret för Microsoft Endpoint Manager:

> [!Important]
> Den här informationen är relaterad till en förhands gransknings funktion som kan ändras avsevärt innan den släpps kommersiellt. Microsoft lämnar inga garantier, uttryckliga eller underförstådda, avseende informationen som visas här.

## <a name="common-errors-from-the-microsoft-endpoint-manager-admin-center"></a>Vanliga fel från administrations centret för Microsoft Endpoint Manager

När du visar information om ConfigMgr-klienten kan du köra något av dessa fel.  

### <a name="the-necessary-configuration-is-missing-in-azure-active-directory"></a><a name="bkmk_aad"></a>Nödvändig konfiguration saknas i Azure Active Directory

**Fel meddelande:** Nödvändig konfiguration saknas i Azure Active Directory. Se till att koppla Configuration Manager-platsen till din Azure-klient och tilldela rätt användar roll i Azure AD.

**Möjlig orsak:** Användar kontot saknar antagligen **Administratörs användar** rollen för Configuration Manager mikrotjänstprogram i Azure AD. Lägg till rollen i Azure AD från **företags program**  >  **Configuration Manager mikrotjänst**  >  **användare och grupper**  >  **Lägg till användare**. Grupper stöds om du har Azure AD Premium. Det kan ta upp till en timme innan ändringar av den här behörigheten börjar gälla.

### <a name="unable-to-get-device-or-collection-information"></a><a name="bkmk_noinfo"></a>Det gick inte att hämta enhets-eller samlings information

**Fel meddelande 1:** Det gick inte att hämta information om klient information (eller insamling). Kontrol lera att Azure AD och AD-identifiering av användare har kon figurer ATS och att användaren identifieras av båda. Kontrol lera att användaren har rätt behörigheter i Configuration Manager.

**Möjliga orsaker:** Detta fel beror vanligt vis på ett problem med administratörs kontot. Nedan visas de vanligaste problemen med det administrativa användar kontot:

1. Använd samma konto för att logga in i administrations centret. Den lokala identiteten måste vara synkroniserad med och överensstämma med moln identiteten.
1. Kontrol lera att kontot har behörigheten **läsa** för enhetens **samling** i Configuration Manager.
1. Kontrol lera att Configuration Manager har identifierat det administrativa användar konto som du använder. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen. Välj noden **användare** och hitta ditt användar konto.

    Om ditt konto inte visas i noden **användare** kontrollerar du konfigurationen av platsens [Active Directory användar identifiering](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

1. Verifiera identifierings data. Välj ditt användarkonto. På fliken **Start** i menyfliksområdet väljer du **Egenskaper**. I fönstret Egenskaper bekräftar du följande identifierings data:

    - **Azure Active Directory klient-ID**: det här värdet ska vara ett GUID för Azure AD-klienten.
    - **Azure Active Directory användar-ID**: det här värdet ska vara ett GUID för det här kontot i Azure AD.
    - **Användarens huvud namn**: formatet för det här värdet är user@domain . Ett exempel är `jqpublic@contoso.com`.

    Om Azure AD-egenskaperna är tomma kontrollerar du konfigurationen för platsens identifiering av [Azure AD-användare](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc).


### <a name="unexpected-error-occurred"></a><a name="bkmk_1603"></a>Ett oväntat fel uppstod

**Fel meddelande:** Ett oväntat fel uppstod

**Möjliga orsaker:** Oväntade fel orsakas vanligt vis av antingen [tjänst anslutnings punkt](../core/servers/deploy/configure/about-the-service-connection-point.md), [administrations tjänst](../develop/adminservice/overview.md)eller anslutnings problem.

1. Kontrol lera att tjänst anslutnings punkten är ansluten till molnet med hjälp av **CMGatewayNotificationWorker. log**.
1. Kontrol lera att den administrativa tjänsten är felfri genom att granska SMS_REST_PROVIDER-komponenten från plats komponent övervakning på den centrala platsen.
1. IIS måste vara installerat på en-leverantörs dator. Mer information finns i [krav för administrations tjänsten](../develop/adminservice/overview.md#prerequisites)
1. Kontrol lera att klockan på tjänst anslutnings punkten är synkroniserad. Om tjänst anslutnings punktens klocka är något bakom, använder du [KB4563473-Samlad uppdatering för Configuration Manager version 2002 klient kopplings problem](https://support.microsoft.com/help/4563473). Kontrol lera **AdminService. log** på leverantörs datorn för eventuella fel.

## <a name="known-issues"></a>Kända problem

### <a name="gettingresultstimedout"></a>Tids gränsen nåddes för hämtning av resultat

**Scenario:** Om du har en fjärran sluten tjänst anslutnings punkt och du har installerat 2002 tidig uppdaterings ring före 30 mars 2020 visas ett timeout-fel i administrations centret.

**Fel meddelande:** Tids gränsen nåddes för hämtning av resultat. Kontrol lera att anslutnings punkten för Configuration Managers tjänsten fungerar och har en anslutning till molnet.

**Lösning:** Kopiera `Microsoft.ConfigurationManagement.ManagementProvider.dll` från plats serverns `bin\x64` mapp till mappen för fjärrtjänstens anslutnings punkt `bin\x64` .  Starta om `SMS_EXECUTIVE` tjänsten på servern för tjänst anslutnings punkten.

### <a name="boundary-groups-list-is-empty"></a>Listan över gränser grupper är tom

**Fel meddelande**: inga avgränsnings grupper hittades eller så kanske användaren inte har behörighet att visa information om gränserna.

Den tomma listan är ett känt problem i Configuration Manager version 2002 om du har en hierarki med Configuration Manager-platser.

:::image type="content" source="media/6024387-known-issue-device-details.png" alt-text="Listan över gränser grupper är tom" lightbox="media/6024387-known-issue-device-details.png":::

## <a name="next-steps"></a>Nästa steg

[Felsöka klientkoppling](troubleshoot.md)
