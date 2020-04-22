---
title: Registrera dig eller logga in i Microsoft Intune
description: Så här registrerar du dig för en Microsoft Intune-prenumeration, eller loggar in för att starta din prenumeration.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 0f3ce07a-b718-42a9-bace-f99a8b8abd94
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: e4bec3347ec45f020fd4c8e128278dc619335442
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80401448"
---
# <a name="sign-up-or-sign-in-to-microsoft-intune"></a>Registrera dig eller logga in i Microsoft Intune

Det här avsnittet beskriver hur systemadministratörer kan registrera sig för ett Intune-konto.

Innan du registrerar dig för Intune kontrollerar du om du redan har ett Microsoft Online Services-konto, Enterprise-avtal eller motsvarande volymlicensavtal. Ett Microsoft-volymlicensavtal eller en annan prenumeration på Microsoft-molntjänster som Office 365 innefattar vanligtvis ett arbets- eller skolkonto.

Om du redan har ett arbets- eller skolkonto **loggar du in** med det kontot och lägger till Intune i din prenumeration. Annars kan du **registrera dig** för ett nytt konto så att du kan använda Intune i din organisation.

>[!WARNING]
>Du kan inte kombinera ett befintligt arbets- eller skolkonto efter att du har registrerat dig för ett nytt konto.

## <a name="how-to-sign-up-for-intune"></a>Så här registrerar du dig för Intune

1. Besök [Intune-registreringssidan](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20).

   ![Skärmbild av webbsidan med kontoregistrering för en utvärderingsversion av Microsoft Intune](./media/account-sign-up/account-sign-up-site.png)

2. Logga in eller registrera dig på inloggningssidan om du vill hantera en ny prenumeration på Intune.

## <a name="post-sign-up-considerations"></a>Att tänka på efter registreringen

När du har registrerat dig för en ny prenumeration skickas ett e-postmeddelande med din kontoinformation till den e-postadress som du angav när du registrerade dig. E-postmeddelandet bekräftar att din prenumeration är aktiv.

När du har slutfört registreringsprocessen dirigeras du till Administrationscenter för Microsoft 365, där du kan lägga till användare och tilldela licenser till dem. Om du bara ska använda molnbaserade konton med standarddomännamnet onmicrosoft.com kan du fortsätta och lägga till användare och tilldela licenser nu. Om du däremot planerar att använda din organisations [domännamn](custom-domain-name-configure.md) eller [synkronisera information om användarkonton](users-add.md#sync-active-directory-and-add-users-to-intune) från lokala Active Directory, kan du stänga webbläsarfönstret.

## <a name="sign-in-to-microsoft-intune"></a>Logga in på Microsoft Intune

När du har registrerat dig för Intune kan du använda valfri enhet med en [webbläsare som stöds](supported-devices-browsers.md#intune-supported-web-browsers) för att logga in på [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) för att administrera tjänsten.

Som standard måste ditt konto ha en av följande behörigheter i Azure AD:

- Global administratör
- Intune-tjänstadministratör (även kallat Intune-administratör)

Information om hur du beviljar åtkomst för att administrera tjänsten för användare med andra behörigheter finns i [Rollbaserad åtkomstkontroll](role-based-access-control.md)

### <a name="intune-admin-portal-url"></a>URL för Intune-administratörsportalen

Administrationscenter för Microsoft Endpoint Manager: https://endpoint.microsoft.com

Intune Azure Portal: https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade

Intune for Education: https://intuneeducation.portal.azure.com

Intunes klassiska portal: https://manage.microsoft.com Den klassiska Intune-portalen används bara för att hantera enheter som registrerats med Intune PC-klienten

### <a name="urls-for-intune-services-provided-by-office-365"></a>URL:er för Intune-tjänster som tillhandahålls av Office 365

Microsoft 365 Business: https://portal.microsoft.com/adminportal

Mobile Device Management för Office 365: https://admin.microsoft.com/adminportal/home#/MifoDevices

## <a name="see-also"></a>Se även

[Du kan inte logga in på Office 365, Azure eller Intune](https://support.microsoft.com/help/2412085)
