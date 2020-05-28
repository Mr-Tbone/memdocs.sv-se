---
title: Så här stänger du ditt konto
titleSuffix: Configuration Manager
description: Ta bort Desktop Analytics från ditt Azure-konto
ms.date: 10/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: e24c2ee19093dd12af6e87280a31851a1f593782
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268478"
---
# <a name="how-to-close-your-account"></a>Så här stänger du ditt konto

Om du konfigurerar Desktop Analytics i din miljö och sedan bestämmer dig för att ta bort det, använder du den här processen för att stänga ditt konto.

## <a name="prerequisites"></a>Förutsättningar

Endast en **Global administratör** kan stänga eller återaktivera kontot i Azure Portal.

## <a name="process-to-offboard"></a>Bearbeta till avpublicera

1. Öppna [Skriv bords analys portalen](https://aka.ms/desktopanalytics) i Microsoft 365 enhets hantering som en användare med rollen **Global administratör** .

1. I menyn **globala inställningar** väljer du **anslutna tjänster**. I avsnittet registrera enheter väljer du alternativet **avpublicera**.

1. Om du väljer att fortsätta är ditt konto stängt.

> [!Important]
> Fortsätt bara med resten av den här artikeln efter 90 dagar, eller om du inte vill återaktivera.
>
> Om du vill stänga ditt konto helt utan att vänta i 90 dagar måste du först [återställa](account-reset.md) ditt konto.

## <a name="reactivate"></a>Återaktivera

Under de kommande 90 dagarna ser alla administratörer från din organisation som har åtkomst till Skriv bords analys portalen ett meddelande om att du valt att avpublicera.

En global administratör kan återaktivera kontot inom 90 dagar. Välj alternativet för att **ta mig tillbaka**om du vill återställa Desktop Analytics för din organisation.

## <a name="delete-the-solution"></a>Ta bort lösningen

> [!Warning]
> Fortsätt bara med resten av den här artikeln efter 90 dagar, eller om du inte vill återaktivera. Om du tar bort och kopplar från dessa andra komponenter försöker du inte återaktivera.

1. Logga in på [Azure Portal](https://portal.azure.com) som en användare med rollen **Global administratör** .

1. Sök i **alla resurser** efter namnet på din Desktop Analytics-arbetsyta. Det här namnet är det du skapade när du registrerade dig för tjänsten.

1. Borttagning `Microsoft365Analytics(YourWorkspaceName)` av typ **lösning**.

Skriv bords analys data åldras utifrån din data bevarande princip för arbets ytan. Du kan fortsätta att använda andra lösningar i samma arbets yta.

> [!Important]  
> Om du använder Log Analytics arbets ytan med andra lösningar tar du inte bort arbets ytan.

## <a name="remove-user-and-app-access"></a>Ta bort användar-och app-åtkomst

1. Logga in på [Azure Portal](https://portal.azure.com) som en användare med rollen **Global administratör** . Gå till **Azure Active Directory**.

1. I **roller och administratörer**söker du efter **Administratörs rollen för Skriv bords analys** . Ta bort dess medlemmar.

1. Ta bort medlemmar i följande grupper i **grupper**:

    - **M365 Analytics-klient administratörer (Log Analytics ägare)**
    - **M365 Analytics-klient administratörer (Log Analytics deltagare)**

1. I **företags program**, ta bort eller återkalla åtkomst behörighet för följande appar:

    - `MaLogAnalyticsReader`

    - ConfigMgr-appen. Om du vill hitta namnet på den här appen går du till Configuration Manager-konsolen. I arbets ytan **Administration** expanderar du **Cloud Services**och väljer noden **Azure-tjänster** . Öppna egenskaperna för **Skriv bords analys** tjänsten och växla till fliken **program** . Webbappen är den här Azure **-** appen.

        > [!Important]  
        > Innan du gör ändringar i den här appen i Azure AD bör du kontrol lera att du inte använder den igen med en annan tjänst i Configuration Manager.

## <a name="disconnect-configuration-manager"></a>Koppla från Configuration Manager

1. Öppna Configuration Manager-konsolen som en användare med rollen **Fullständig administratör** .

1. Gå till arbets ytan **Administration** , expandera **Cloud Services**och välj noden **Azure-tjänster** .

1. Ta bort tjänsten Desktop Analytics.

### <a name="delete-collections-for-the-pilot-and-production-deployments"></a>Ta bort samlingar för pilot-och produktions distributionerna

1. I Configuration Manager-konsolen väljer du **enhets samlingar** på arbets ytan **till gångar och efterlevnad** .

1. Ta bort alla samlingar som du inte längre använder. Som standard finns samlingarna under mappen **distributions planer** .  

## <a name="reconfigure-clients"></a>Konfigurera om klienter

### <a name="unenroll-devices"></a>Avregistrera enheter

På registrerade enheter tar du bort värdet CommercialID från följande Windows-register nycklar:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Data konfiguration för Windows-diagnostik

Om du inte vill att enheterna ska kunna skicka diagnostikdata:

- Windows 10: ange nivån för diagnostikdata till **säkerhet**
- Windows 7 SP1 eller 8,1: inaktivera den **kommersiella data inloggnings nyckeln**

Ange dessa värden med någon av följande metoder:

- Grup princip, i **dator konfiguration**  >  **administrativa mallar**  >  **Windows Components**  >  **data insamling och för hands versioner** av Windows-komponenter
- Hantering av mobila enheter (MDM), till exempel [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

Mer information finns i [Konfigurera Windows-diagnostikdata i din organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> När du tillämpar dessa ändringar slutar enheterna omedelbart att skicka diagnostikdata. Det kan ta 24-48 timmar för Microsoft att sluta bearbeta insikter för din arbets yta. Microsoft tar bort dessa data från sina moln tjänster inom 30 dagar eller mindre.
