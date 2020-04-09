---
title: Registrera enheter med ett konto för enhetsregistreringshanteraren
titleSuffix: Microsoft Intune
description: Använda kontot för enhetsregistreringshanteraren för att registrera flera enheter i Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7196b33e-d303-4415-ad0b-2ecdb14230fd
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 27ec9e4c407dd8ef1a94e9c443f62ea5456866dc
ms.sourcegitcommit: 252e718dc58da7d3e3d3a4bb5e1c2950757f50e2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/07/2020
ms.locfileid: "80808132"
---
# <a name="enroll-devices-in-intune-by-using-a-device-enrollment-manager-account"></a>Registrera enheter i Intune med ett konto för enhetsregistreringshanteraren

Du kan registrera upp till 1 000 mobila enheter med ett enda Azure Active Directory-konto med hjälp av ett konto för enhetsregistreringshantering (DEM). DEM är en Intune-behörighet som kan tillämpas på ett AAD-användarkonto och gör att användaren kan registrera upp till 1 000 enheter. Ett DEM-konto är användbart för scenarier där enheterna registreras och förbereds innan de delas ut till användarna. Microsoft Intune har en gräns på 150 DEM-konton (enhetsregistreringshanterare).

## <a name="limitations-of-devices-that-are-enrolled-with-a-dem-account"></a>Begränsningar för enheter som registreras med ett DEM-konto

DEM-användarkonton och enheter som har registrerats med ett DEM-användarkonto har följande begränsningar:

- En DEM-kontoanvändare måste tilldelas en Intune-licens.
- Rensning kan inte utföras från företagsportalen. Rensning av en enhet som har registrerats med ett DEM-användarkonto kan göras från Intune på Azure-portalen.
- Endast den lokala enheten visas i företagsportalappen eller webbplatsen.
- DEM-användarkonton kan inte använda apparna för Apples volymköpsprogram (VPP) med Apple VPP-användarlicenser på grund av Apple-ID-kraven per användare för apphantering.
- DEM-konton kan inte användas när du registrerar enheter via Apples automatiserade enhetsregistrering (ADE).
- Enheter kan installera VPP-appar om de har Apple VPP-enhetslicenser.
- Enheter har blockerats för villkorlig åtkomst med undantag för Windows 10 1803+
- Alla enheter som registreras med DEM-konton måste vara korrekt licensierade för att hanteras av Intune. Licensen kan vara en Intune-användarlicens eller en Intune-enhetslicens.
- Om du [registrerar Android Enterprise-arbetsprofilenheter](android-work-profile-enroll.md) med hjälp av ett DEM-konto går det att registrera högst 10 enheter per konto.
- [Registrering av fullständigt hanterade Android Enterprise-enheter](android-fully-managed-enroll.md) för DEM-konton stöds inte.

## <a name="add-a-device-enrollment-manager"></a>Lägg till en enhetsregistreringshanterare

1. Logga in på [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och välj **Enheter** > **Registrera enheter** > **Enhetsregistreringshanterare**.

2. Välj **Lägg till**.

3. På bladet **Lägg till användare** anger du ett huvudnamn för DEM-användaren och väljer **Lägg till**. DEM-användaren läggs till i listan över DEM-användare.

## <a name="permissions-for-dem"></a>Behörigheter för DEM

AD-rollen Global administratör eller Intune-tjänstadministratör krävs för att
- tilldela DEM-behörighet till ett Azure AD-användarkonto
- visa alla DEM-användare

Användare som inte har tilldelats rollen Global administratör eller Intune-tjänstadministratör, men som har läsbehörigheter för rollen Enhetsregistreringshanterare, kan bara se de DEM-användare som de har skapat.


## <a name="remove-device-enrollment-manager-permissions"></a>Ta bort behörigheter för enhetsregistreringshanterare

Redan registrerade enheter påverkas inte av att en enhetsregistreringshanterare tas bort.

**Ta bort en enhetsregistreringshanterare**

1. Logga in på [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och välj **Enheter** > **Registrera enheter** > **Enhetsregistreringshanterare**.
2. På bladet **Enhetsregistreringshanterare** väljer du enhetsregistreringshanteraren och **Ta bort**.

