---
title: Windows 10-appdistribution med hjälp av Microsoft Intune
titleSuffix: ''
description: Läs mer om de scenarier för Windows 10-appdistribution som är tillgängliga med Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: abebfb5e-054b-435a-903d-d1c31767bcf2
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 170a5b22362ee3bd9e347af2addc03ef3b542de2
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907819"
---
# <a name="windows-10-app-deployment-by-using-microsoft-intune"></a>Windows 10-appdistribution med hjälp av Microsoft Intune 

Microsoft Intune har stöd för en mängd olika typer av appar och distributionsscenarier på Windows 10-enheter. När du har lagt till en app till Intune kan du tilldela appen till användare och enheter. Den här artikeln innehåller mer information om de Windows 10-scenarier som stöds, samt viktig information att notera när du distribuerar appar till Windows. 

Verksamhetsspecifika appar (LOB) och Microsoft Store för företag-appar är de typer av appar som stöds på Windows 10-enheter. Filnamnstilläggen för Windows-appar är .msi, .appx och .appxbundle.  

> [!Note]
> Om du vill distribuera moderna appar behöver du minst:
> - För Windows 10 1803, [23 maj 2018 – KB4100403 (OS-version 17134.81)](https://support.microsoft.com/help/4100403/windows-10-update-kb4100403).
> - För Windows 10 1709 [21 juni 2018 – KB4284822 (OS-version 16299.522)](https://support.microsoft.com/help/4284822).
>
> Det är bara Windows 10 1803 och senare som har stöd för installation av appar när det inte finns någon primär användare associerad.
>
> Distribution av verksamhetsspecifika appar stöds inte på enheter som kör Windows 10 Home-utgåvor.

## <a name="supported-windows-10-app-types"></a>Windows 10-apptyper som stöds

Vissa apptyper stöds baserat på den version av Windows 10 som användarna kör. Följande tabell innehåller apptyp och support för Windows 10.

| Typ av app | Hem | Pro | Företag | Enterprise | Utbildning | S-Mode | HoloLens<sup>1 | Surface Hub | WCOS | Mobiltelefon |
|----------------|------|-----|----------|------------|-----------|--------|-----------|------------|------|--------|
|  .MSI | Nej | Ja | Ja | Ja | Ja | Nej | Nej | Nej | Nej | Nej |
| .IntuneWin | Nej | Ja | Ja | Ja | Ja | 19H2+ | Nej | Nej | Nej | Nej |
| Office C2R | Nej | Ja | Ja | Ja | Ja | RS4+ | Nej | Nej | Nej | Nej |
| VERKSAMHETSSPECIFIK: APPX/MSIX | Ja | Ja | Ja | Ja | Ja | Ja | Ja | Ja | Ja | Ja |
| MSFB Offline | Ja | Ja | Ja | Ja | Ja | Ja | Ja | Ja | Ja | Ja |
| MSFB Online | Ja | Ja | Ja | Ja | Ja | Ja | RS4+ | Nej | Ja | Ja |
| Web Apps | Ja | Ja | Ja | Ja | Ja | Ja | Ja<sup>2 | Ja<sup>2 | Ja | Ja<sup>2 |
| Store-länk | Ja | Ja | Ja | Ja | Ja | Ja | Ja | Ja | Ja | Ja |
| Microsoft Edge | Nej | Ja | Ja | Ja | Ja | 19H2+<sup>3 | Nej | Nej | Nej | Nej |

<sup>1</sup> Om du vill låsa upp apphantering måste du uppgradera din HoloLens-enhet till [Holographic for Business](../fundamentals/windows-holographic-for-business.md).<br />
<sup>2</sup> Starta endast från företagsportalen.<br />
<sup>3</sup> För att Edge-appen ska kunna installeras måste enheter också tilldelas en princip för S-läge.

> [!NOTE]
> Alla typer av Windows-appar kräver registrering.

## <a name="windows-10-lob-apps"></a>Verksamhetsspecifika appar i Windows 10

Du kan signera och ladda upp verksamhetsspecifika appar i Windows 10 till Intune-administratörskonsolen. Dessa kan innefatta både moderna appar, till exempel UWP-appar (Universell Windows-plattform) och Windows-appaket (AppX), samt Win 32-appar som exempelvis enkla Microsoft Installer-paketfiler (MSI). Administratören måste manuellt ladda upp och distribuera uppdateringar av verksamhetsspecifika appar. Dessa uppdateringar installeras automatiskt på användarenheter som har appen installerad. Inga åtgärder från användaren krävs och användaren har inte någon kontroll över uppdateringarna. 

## <a name="microsoft-store-for-business-apps"></a>Microsoft Store för företag-appar

Appar i Microsoft Store för företag är moderna appar som har köpts från Microsoft Store för företags administratörsportal. De synkroniseras sedan med Microsoft Intune för hantering. Apparna kan antingen vara onlinelicensierade eller offlinelicensierade. Microsoft Store hanterar uppdateringar direkt, utan att ytterligare åtgärder krävs av administratören. Du kan även förhindra uppdateringar till specifika appar med hjälp av en anpassad URI (Uniform Resource Identifier). Mer information finns på sidan om [Enterprise-apphantering – förhindra automatiska uppdateringar för appen](/windows/client-management/mdm/enterprise-app-management#prevent-app-from-automatic-updates). Användaren kan även inaktivera uppdateringar för alla appar från Microsoft Store för företag på enheten. 

### <a name="categorize-microsoft-store-for-business-apps"></a>Kategorisera appar i Microsoft Store för företag 
Så här kategoriserar du appar i Microsoft Store för företag: 

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Appar** > **Alla appar**. 
3. Välj en Microsoft Store för företag-app. Välj sedan **Egenskaper** > **Appinformation** > **Kategori**. 
4. Välj en kategori.

## <a name="install-apps-on-windows-10-devices"></a>Installera appar på Windows 10-enheter
Beroende på apptyp kan appen installeras på en Windows 10-enhet på något av följande två sätt:

- **Användarkontext**: När en app distribueras i användarkontext installeras den hanterade appen för användaren på enheten vid inloggningen. Observera att installationen av appen inte är klar förrän användaren loggar in på enheten. 
  - Moderna verksamhetsspecifika appar och Microsoft Store för företag-appar (både online och offline) kan distribueras i användarkontext. Apparna har stöd för avsikterna Nödvändig och Tillgänglig.
  - Win32-appar som skapats som Användarläge eller Dubbelläge kan distribueras i användarkontext och stöder avsikterna Nödvändig och Tillgänglig. 
- **Enhetskontext**: När en app distribueras i enhetskontext installeras den hanterade appen direkt på enheten av Intune.
  - Det är bara moderna verksamhetsspecifika appar och offlinelicensierade appar i Microsoft Store för företag som kan distribueras i enhetskontext. Dessa appar stöder bara avsikten Nödvändig.
  - Win32-appar som skapats som Datorläge eller Dubbelläge kan distribueras i enhetskontext och har endast stöd för avsikten Nödvändig.

> [!NOTE]
> För Win32-appar som skapats som Dubbelläge, måste administratören välja om appen ska användas som en app i Användarläge eller Datorläge för alla tilldelningar som är associerade med instansen. Distributionskontexten kan inte ändras per tilldelning.  

Appar kan bara installeras i enhetskontexten när de stöds av både enheten och Intune-apptypen. Enhetskontextinstallationer stöds på Windows 10-datorer och Teams-enheter, t. ex. Surface Hub. De har inte stöd för enheter som kör Windows Holographic for Business, som till exempel Microsoft HoloLens.

Du kan installera följande typer av appar i enhetskontexten och tilldela en enhetsgrupp dessa appar:

- Win32-appar
- Offline-licensierade Microsoft Store för företag-appar
- Verksamhetsspecifika appar (MSI, APPX och MSIX)
- Microsoft 365-appar för företag

Verksamhetsspecifika Windows-appar (i synnerhet APPX och MSIX) och Microsoft Store för företag-appar (offline-appar) som du har valt att installera i enhetskontext måste tilldelas till en enhetsgrupp. Installationen misslyckas om någon av dessa appar distribueras i användarkontexten. Följande status och fel visas i administratörskonsolen:
  - Status: Misslyckades.
  - Fel: Det går inte att rikta sig mot en användare med en installation för enhetskontext.

> [!IMPORTANT]
> När det används tillsammans med ett assisterat etableringsscenario för Autopilot, så finns det inga krav på att verksamhetsspecifika appar eller Microsoft Store för företag-appar som distribuerats i enhetskontexten ska vara inriktade på någon enhetsgrupp. Mer information finns i [Assisterad distribution av Windows Autopilot](/windows/deployment/windows-autopilot/white-glove).

> [!Note]
> När en apptilldelning har sparats med en specifik distribution går det inte att ändra kontexten för tilldelningen, förutom för moderna appar. För moderna appar kan du ändra kontexten från användarkontext till enhetskontext. 

Om det finns en konflikt i principerna för en enskild användare eller enhet, gäller följande prioriteringar:
- En enhetskontextprincip är en högre prioritet än en användarkontextprincip. 
- En installationsprincip är en högre prioritet än en avinstallationsprincip.

Mer information finns i [Inkludera och exkludera apptilldelningar i Microsoft Intune](apps-inc-exl-assignments.md). Mer information om apptyper i Intune finns i [Lägg till appar i Microsoft Intune](apps-add.md).

## <a name="next-steps"></a>Nästa steg

- [Tilldela appar till grupper med Microsoft Intune](apps-deploy.md)
- [Övervaka appar](apps-monitor.md)