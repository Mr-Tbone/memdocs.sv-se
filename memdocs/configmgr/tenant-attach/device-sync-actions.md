---
title: Ansluta Microsoft Endpoint Manager-klientorganisation
titleSuffix: Configuration Manager
description: Ladda upp dina Configuration Manager-enheter till moln tjänsten och vidta åtgärder från administrations centret.
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: bac86ca5a74d35b64e211936806ef1735f4e0eea
ms.sourcegitcommit: 231e2c3913a1d585310dfab7ffcd5c78c6bc5703
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88970472"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a> Microsoft Endpoint Manager-klient ansluter: synkronisering av enhet och enhets åtgärder
<!--3555758 live 3/4/2020-->
*Gäller för: Configuration Manager (aktuell gren)*

Microsoft Endpoint Manager är en integrerad lösning för att hantera alla dina enheter. Microsoft sammanför Configuration Manager och Intune i en enda konsol som kallas **administrations Center för Microsoft Endpoint Manager**.

Från och med Configuration Manager version 2002 kan du ladda upp dina Configuration Manager-enheter till moln tjänsten och vidta åtgärder från bladet **enheter** i administrations centret.

## <a name="prerequisites"></a>Förutsättningar

- Ett konto som är en *Global administratör* för att logga in när du tillämpar den här ändringen. Mer information finns i [Administratörs roller för Azure Active Directory (Azure AD)](/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles).
   - Onboarding skapar en app från tredje part och ett första parts tjänst objekt i din Azure AD-klient.
- En offentlig Azure-moln miljö.
- De användar konton som utlöser enhets åtgärder har följande krav:
   - Har identifierats med både [Azure Active Directory användar identifiering](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) och [Active Directory användar identifiering](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
      - Det innebär att användar kontot måste vara ett synkroniserat användar objekt i Azure AD.
   - Behörigheten **initiera Configuration Managers åtgärd** under **fjärraktiviteter** i administrations centret för Microsoft Endpoint Manager.
- Om den centrala administrations platsen har en [fjärran sluten leverantör](../core/plan-design/hierarchy/plan-for-the-sms-provider.md), följer du anvisningarna för [CAS](../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) i CMPivot-artikeln. <!--7796824-->

## <a name="internet-endpoints"></a>Internet slut punkter

[!INCLUDE [Internet endpoints for tenant attach](../core/plan-design/network/includes/internet-endpoints-tenant-attach.md)]

Tjänst anslutnings punkten gör en lång, utgående anslutning till dessa slut punkter. Kontrol lera att proxyn som används för tjänst anslutnings punkten inte har nått tids gränsen för utgående anslutningar för snabbt. Vi rekommenderar 3 minuter för utgående anslutningar till dessa Internet slut punkter. <!--7820969-->

## <a name="enable-device-upload-when-co-management-is-already-enabled"></a><a name="bkmk_edit"></a> Aktivera enhets uppladdning när samtidig hantering redan har Aktiver ATS

Om du har aktiverat samhantering för närvarande använder du egenskaper för samhantering för att aktivera enhets uppladdning. När samhantering inte redan har Aktiver ATS [använder du guiden **Konfigurera samhantering** ](#bkmk_config) för att aktivera enhets uppladdning i stället.

När samhantering redan har Aktiver ATS redigerar du egenskaperna för samhantering för att aktivera enhets uppladdning enligt anvisningarna nedan:

1. Gå till **Administration** > **Översikt** > **Molntjänster** > **Samhantering** i administrationskonsolen för Configuration Manager.
1. I menyfliksområdet väljer du **Egenskaper** för produktions principen för samhantering.
1. På fliken **Konfigurera uppladdning** väljer du **Ladda upp till administrationscentret för Microsoft Endpoint Manager**. Välj **Använd**.
   - Standardinställningen för uppladdning av enheter är **Alla mina enheter som hanteras av Microsoft Endpoint Configuration Manager**. Om det behövs kan du begränsa överföringen till en enda enhets samling.
1. Markera alternativet om du vill **Aktivera slut punkts analys för enheter som laddats upp till Microsoft Endpoint Manager** om du också vill få insikter för att optimera slut användar upplevelsen i [slut punkts analys](../../analytics/overview.md).

   [![Ladda upp enheter till administrations Center för Microsoft Endpoint Manager](../../analytics/media/6051638-configure-upload-configmgr.png)](../../analytics/media/6051638-configure-upload-configmgr.png#lightbox)
1. Logga in med ditt *globala administratörskonto* när du uppmanas till det.
1. Välj **Ja** om du vill acceptera meddelandet om att **skapa AAD-program** . Den här åtgärden etablerar ett huvudnamn för tjänsten och skapar en Azure AD-programregistrering för att underlätta synkroniseringen.
1. Välj **OK** för att avsluta egenskaperna för samhantering när du är klar med att göra ändringar.


## <a name="enable-device-upload-when-co-management-isnt-enabled"></a><a name="bkmk_config"></a> Aktivera enhets uppladdning när samtidig hantering inte är aktiverat

Om du inte har samhantering aktive rad använder du guiden **Konfigurera samhantering** för att aktivera enhets uppladdning. Du kan ladda upp dina enheter utan att aktivera automatisk registrering för samhantering eller för att växla arbets belastningar till Intune. Alla enheter som hanteras av Configuration Manager som har **Ja** i kolumnen **klient** kommer att överföras. Om det behövs kan du begränsa överföringen till en enda enhets samling. Om samhantering redan har Aktiver ATS i din miljö kan du [Redigera egenskaper för samhantering](#bkmk_edit) för att aktivera enhets uppladdning i stället.

När samhantering inte har Aktiver ATS kan du använda instruktionerna nedan för att aktivera enhets uppladdning:

1. Gå till **Administration** > **Översikt** > **Molntjänster** > **Samhantering** i administrationskonsolen för Configuration Manager.
1. I menyfliksområdet väljer du **Konfigurera samhantering** för att öppna guiden.
1. På sidan **Registrering av klientorganisation** väljer du **AzurePublicCloud** som miljö. Azure Government Cloud och Azure Kina 21Vianet stöds inte.
1. Välj **Logga in.** Logga in med ditt *globala administratörskonto*.
1. Se till att alternativet **Ladda upp till Microsoft Endpoint Manager Admin Center** är markerat på sidan **innehavaradministration** .
   - Se till att alternativet **Aktivera automatisk klient registrering för samhantering** inte är markerat om du inte vill aktivera samhantering nu. Om du vill aktivera samhantering väljer du alternativet.
   - Om du aktiverar samhantering tillsammans med enhets uppladdning får du ytterligare sidor i guiden att slutföra. Mer information finns i [Aktivera samhantering](../comanage/how-to-enable.md).

   [![Konfigurations guide för samhantering](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. Välj **Nästa** och sedan **Ja** för att godkänna funktionen för att **skapa AAD-program** . Den här åtgärden etablerar ett huvudnamn för tjänsten och skapar en Azure AD-programregistrering för att underlätta synkroniseringen.
     - Du kan också importera ett tidigare skapat Azure AD-program under klient kopplings etableringen (från och med version 2006). Mer information finns i avsnittet [Importera ett tidigare skapat Azure AD-program](#bkmk_aad_app) .
1. På sidan **Konfigurera uppladdning** väljer du den rekommenderade inställningen för enhets uppladdning för **alla mina enheter som hanteras av Microsoft Endpoint Configuration Manager**. Om det behövs kan du begränsa överföringen till en enda enhets samling.
1. Markera alternativet om du vill **Aktivera slut punkts analys för enheter som laddats upp till Microsoft Endpoint Manager** om du också vill få insikter för att optimera slut användar upplevelsen i [slut punkts analys](../../analytics/overview.md)
1. Välj **Sammanfattning** för att granska ditt val och välj sedan **Nästa**.
1. När guiden är klar väljer du **Stäng**.  

## <a name="perform-device-actions"></a>Utföra enhets åtgärder

1. I en webbläsare navigerar du till `endpoint.microsoft.com`
1. Välj **enheter** och sedan **alla enheter** för att se de överförda enheterna. Du ser **ConfigMgr** i kolumnen **hanterad av** för uppladdade enheter.
   [![Alla enheter i administrations Center för Microsoft Endpoint Manager](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. Välj en enhet för att läsa in sidan **Översikt** .
1. Välj någon av följande åtgärder:
   - **Synkronisera enhetsprincip**
   - **Synkronisera användarprincip**
   - **Apputvärderingscykel**

   [![Enhets översikt i administrations Center för Microsoft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="import-a-previously-created-azure-ad-application-optional"></a><a name="bkmk_aad_app"></a> Importera ett tidigare skapat Azure AD-program (valfritt)
<!--6479246-->
*(Lanseras i version 2006)*

Under en [ny onboarding](#bkmk_config)kan en administratör ange ett program som skapats tidigare under onboarding to klient anslutning. Dela eller Återanvänd inte Azure AD-program över flera hierarkier. Om du har flera hierarkier kan du skapa separata Azure AD-program för var och en.

På sidan **klient** integrering i **guiden för konfiguration av samhantering**väljer **du om du vill importera en separat webbapp för att synkronisera Configuration Manager klient data till Microsoft Endpoint Manager administrations Center**. Med det här alternativet uppmanas du att ange följande information för din Azure AD-App:

- Namn på Azure AD-klient
- Azure AD-klient-ID
- Programnamn
- Klient-ID
- Hemlig nyckel
- Förfallo datum för hemlig nyckel
- URI för app-id

### <a name="azure-ad-application-permissions-and-configuration"></a>Behörigheter och konfiguration för Azure AD-program

Att använda ett tidigare skapat program vid registrering till klient anslutning kräver följande behörigheter:

- Configuration Manager mikrotjänstens behörigheter:
   - CmCollectionData. Read
   - CmCollectionData. Write

- Microsoft Graph behörigheter:
   - Directory. Read. all [program behörighet](/graph/permissions-reference#application-permissions)
   - Directory. Read. alla [delegerade katalog behörigheter](/graph/permissions-reference#directory-permissions)

- Se till att **bevilja administratörs medgivande för klient organisationen** valt för Azure AD-programmet. Mer information finns i [Granting admin medgivande i Appregistreringar](/azure/active-directory/manage-apps/grant-admin-consent).

- Det importerade programmet måste konfigureras på följande sätt:
   - Endast registrerat för **konton i den här organisations katalogen**. Mer information finns i [ändra vem som har åtkomst till ditt program](/azure/active-directory/develop/quickstart-modify-supported-accounts#to-change-who-can-access-your-application).
   -  Har en giltig program-ID-URI och hemlighet



## <a name="next-steps"></a>Nästa steg

- [Registrera Configuration Manager enheter i slut punkts analys](../../analytics/enroll-configmgr.md#bkmk_cm_enroll)
- Information om klient organisationen bifoga loggfiler finns i [Felsöka klient anslutning](troubleshoot.md).