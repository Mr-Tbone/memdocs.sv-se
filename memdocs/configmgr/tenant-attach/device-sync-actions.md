---
title: Microsoft Endpoint Manager-klient anslutning
titleSuffix: Configuration Manager
description: Ladda upp dina Configuration Manager-enheter till moln tjänsten och vidta åtgärder från administrations centret.
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: e2b8c07a64265d33ade0b1c2c08c2d9c4096b741
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693472"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Microsoft Endpoint Manager-klient ansluter: synkronisering av enhet och enhets åtgärder
<!--3555758 live 3/4/2020-->
*Gäller för: Configuration Manager (aktuell gren)*

Microsoft Endpoint Manager är en integrerad lösning för att hantera alla dina enheter. Microsoft sammanför Configuration Manager och Intune i en enda konsol som kallas **administrations Center för Microsoft Endpoint Manager**.

Från och med Configuration Manager version 2002 kan du ladda upp dina Configuration Manager-enheter till moln tjänsten och vidta åtgärder från bladet **enheter** i administrations centret.

## <a name="prerequisites"></a>Krav

- Ett konto som är en *Global administratör* för att logga in när du tillämpar den här ändringen. Mer information finns i [Administratörs roller för Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles).
   - Onboarding skapar en app från tredje part och ett första parts tjänst objekt i din Azure AD-klient.
- En offentlig Azure-moln miljö.
- De användar konton som utlöser enhets åtgärder har följande krav:
   - Har identifierats med både [Azure Active Directory användar identifiering](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) och [Active Directory användar identifiering](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
      - Det innebär att användar kontot måste vara ett synkroniserat användar objekt i Azure AD.
   - Behörigheten **initiera Configuration Managers åtgärd** under **fjärraktiviteter** i administrations centret för Microsoft Endpoint Manager.


## <a name="internet-endpoints"></a>Internet slut punkter

- `https://aka.ms/configmgrgateway`
- `https://gateway.configmgr.manage.microsoft.com`
- `https://us.gateway.configmgr.manage.microsoft.com`
- `https://eu.gateway.configmgr.manage.microsoft.com`


## <a name="enable-device-upload"></a>Aktivera enhets uppladdning

- Om du har aktiverat samhantering kan du [Redigera egenskaper för samhantering](#bkmk_edit) för att aktivera enhets uppladdning.
- Om du inte har samhantering aktive rad [använder du guiden **Konfigurera samhantering** ](#bkmk_config) för att aktivera enhets uppladdning.
   - Du kan ladda upp dina enheter utan att aktivera automatisk registrering för samhantering eller för att växla arbets belastningar till Intune.
- Alla enheter som hanteras av Configuration Manager som har **Ja** i kolumnen **klient** kommer att överföras. Om det behövs kan du begränsa överföringen till en enda enhets samling.

### <a name="edit-co-management-properties-to-enable-device-upload"></a><a name="bkmk_edit"></a>Redigera egenskaper för samhantering för att aktivera enhets uppladdning

Om du har aktiverat samhantering kan du redigera egenskaper för samhantering för att aktivera enhets uppladdning enligt anvisningarna nedan:

1. I Configuration Manager administratörs konsolen går du till **Administration** > **Översikt** > **Cloud Services** > **samhantering**.
1. Högerklicka på inställningarna för samhantering och välj **Egenskaper**.
1. På fliken **Konfigurera uppladdning** väljer **du ladda upp till Microsoft Endpoint Manager administrations Center**. Klicka på **Använd**.
   - Standardvärdet för enhets uppladdning är **alla mina enheter som hanteras av Microsoft Endpoint Configuration Manager**. Om det behövs kan du begränsa överföringen till en enda enhets samling.

   [![Konfigurations guide för samhantering](./media/3555758-configure-upload.png)](./media/3555758-configure-upload.png#lightbox)
1. Logga in med ditt *globala administratörs* konto när du uppmanas till det.
1. Klicka på **Ja** för att acceptera meddelandet **skapa AAD-program** . Den här åtgärden etablerar ett huvud namn för tjänsten och skapar en Azure AD-programregistrering för att under lätta synkroniseringen.
1. Klicka på **OK** för att avsluta egenskaperna för samhantering när du är klar med att göra ändringar.


### <a name="use-the-configure-co-management-wizard-to-enable-device-upload"></a><a name="bkmk_config"></a>Använd guiden Konfigurera gemensam hantering för att aktivera enhets uppladdning
Om du inte har samhantering aktive rad använder du guiden **Konfigurera samhantering** för att aktivera enhets uppladdning. Du kan ladda upp dina enheter utan att aktivera automatisk registrering för samhantering eller för att växla arbets belastningar till Intune. Aktivera enhets uppladdning genom att följa anvisningarna nedan:

1. I Configuration Manager administratörs konsolen går du till **Administration** > **Översikt** > **Cloud Services** > **samhantering**.
1. I menyfliksområdet klickar du på **Konfigurera samhantering** för att öppna guiden.
1. På sidan **Tenant onboarding** väljer du **AzurePublicCloud** för din miljö. Azure Government molnet stöds inte.
1. Klicka på **Logga**in. Använd ditt *globala administratörs* konto för att logga in.
1. Se till att alternativet **Ladda upp till Microsoft Endpoint Manager Admin Center** är markerat på sidan **innehavaradministration** .
   - Se till att alternativet **Aktivera automatisk klient registrering för samhantering** inte är markerat om du inte vill aktivera samhantering nu. Om du vill aktivera samhantering väljer du alternativet.
   - Om du aktiverar samhantering tillsammans med enhets uppladdning får du ytterligare sidor i guiden att slutföra. Mer information finns i [Aktivera samhantering](../comanage/how-to-enable.md).

   [![Konfigurations guide för samhantering](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. Klicka på **Nästa** och sedan **Ja** för att godkänna funktionen för att **skapa AAD-program** . Den här åtgärden etablerar ett huvud namn för tjänsten och skapar en Azure AD-programregistrering för att under lätta synkroniseringen.
1. På sidan **Konfigurera uppladdning** väljer du den rekommenderade inställningen för enhets uppladdning för **alla mina enheter som hanteras av Microsoft Endpoint Configuration Manager**. Om det behövs kan du begränsa överföringen till en enda enhets samling.
1. Klicka på **Sammanfattning** för att granska ditt val och klicka sedan på **Nästa**.
1. När guiden är klar klickar du på **Stäng**.  


## <a name="review-your-upload"></a><a name="bkmk_review"></a>Granska din uppladdning

1. Öppna **CMGatewaySyncUploadWorker. log** från &lt;installations katalogen för ConfigMgr> \Loggar.
1. Nästa synkroniseringstid anges av logg poster som liknar `Next run time will be at approximately: 02/28/2020 16:35:31`.
1. Sök efter logg poster som liknar för enhets uppladdningar `Batching N records`. **N** är antalet enheter som har överförts till molnet. 
1. Uppladdningen sker var 15: e minut för ändringar. När ändringarna har laddats upp kan det ta ytterligare 5 till 10 minuter innan klient ändringarna visas i **administrations centret för Microsoft Endpoint Manager**.

## <a name="perform-device-actions"></a>Utföra enhets åtgärder

1. I en webbläsare navigerar du till`endpoint.microsoft.com`
1. Välj **enheter** och sedan **alla enheter** för att se de överförda enheterna. Du ser **ConfigMgr** i kolumnen **hanterad av** för uppladdade enheter.
   [![Alla enheter i administrations Center för Microsoft Endpoint Manager](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. Klicka på en enhet för att läsa in sidan **Översikt** .
1. Klicka på någon av följande åtgärder:
   - **Synkronisera dator princip**
   - **Synkronisera användar princip**
   - **Utvärderings cykel för program**

   [![Enhets översikt i administrations Center för Microsoft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="known-issues"></a>Kända problem

### <a name="specific-devices-dont-synchronize"></a>Vissa enheter synkroniseras inte

<!--7099564-->
Det är möjligt att vissa enheter, som är Configuration Manager klienter, inte överförs till tjänsten.

**Påverkade enheter:** Om en enhet är en distributions plats som använder samma PKI-certifikat för både distributions plats funktionerna och dess klient agent, kommer enheten inte att tas med i synkroniseringen av klient anslutningens enhet.

**Beteende:** När du utför en klient anslutning under den här fasen utförs en fullständig synkronisering första gången. Efterföljande synkroniseringsförsök är delta i synkroniseringar. Eventuella uppdateringar av de påverkade enheterna gör att enheten tas bort från synkroniseringen.

## <a name="log-files"></a>Loggfiler
Använd följande loggar som finns på tjänst anslutnings punkten:

- **CMGatewaySyncUploadWorker. log**
- **CMGatewayNotificationWorker. log**

## <a name="next-steps"></a>Nästa steg

Mer information om klient organisationen bifoga loggfiler finns i [Felsöka klient anslutning](technical-reference.md).
