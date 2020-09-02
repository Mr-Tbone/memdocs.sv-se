---
title: Förstå skillnaderna mellan enhetsbegränsningar i Intune och Azure
titleSuffix: ''
description: Förstå skillnaderna mellan Intunes enhetsbegränsningar och begränsningarna i Azure AD.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 63c9d9e4752e4b0d317667162255e368fc5a099c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908562"
---
# <a name="understand-intune-and-azure-ads-device-limit-restrictions"></a>Förstå skillnaderna mellan enhetsbegränsningar i Intune och Azure AD

Enhetsbegränsningar kan konfigureras på två sätt:
- Intune-registrering
- AD-anslutning (Azure Active Directory) eller Azure AD-registrering

Den här artikeln förklarar när de här begränsningarna tillämpas baserat på din konfiguration.

## <a name="intune-device-limit-restrictions"></a>Enhetsbegränsningar i Intune

Enhetsbegränsningarna i Intune anger hur många enheter en användare kan kontrollera (maxinställningen är 15). Du ställer in den här **enhetsgränsen** genom att gå till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter** > **Registreringsbegränsningar**. Mer information finns i [Skapa en enhetsbegränsning](enrollment-restrictions-set.md#create-a-device-limit-restriction)

## <a name="azure-device-limit-restriction"></a>Enhetsbegränsningar i Azure

Enhetsbegränsningar i Azure anger hur många enheter Azure AD kan ansluta eller registrera. Om du vill ställa in **Maximalt antal enheter per användare** går du till Azure-portalen > **Azure Active Directory** > **Enheter**. Mer information finns i [Konfigurera enhetsinställningar](/azure/active-directory/devices/device-management-azure-portal)

## <a name="settings-applied-based-on-user-affinity"></a>Inställningarna tillämpas utifrån användarnas tillhörighet

Om du har angett enhetsbegränsningar för både Intune och Azure kan du se vilken inställning som tillämpas baserat på användarens tillhörighet.

| Enhetsplattform | Användarens tillhörighet | Azure gäller | Intune gäller |
| ----- | ----- | ----- | ----- | ----- |
| Android Enterprise-arbetsprofil | Ja | Ja | Ja|
| Dedikerad Android Enterprise-enhet | Nej | Nej | Nej |
| Fullständigt hanterad Android Enterprise | Ja | Ja | Ja |
| Android-enhetsadministratör | Ja | Ja | Ja |
| Android-enhetsadministratör DEM | Nej | | Nej | 
| iOS/macOS BYOD | Ja | Ja | Ja |
| iOS/macOS Automatisk enhetsregistrering (ADE) | Ja | Ja | Ja |
| iOS/macOS ADE | Nej | Ja | Nej |
| Windows BYOD | Ja | Ja | Ja |
| Windows endast MD | | Ja | Ja |
| Windows Azure AD-ansluten| Ja | Ja | Nej |
| Windows Autopilot | Ja | Ja | Nej |
| Windows Azure AD-hybridansluten | Nej | Nej | Ja |
| Windows samhantering | Nej | Ja | Nej |
| Windows DEM | Nej | Ja | Nej |
| Windows massregistrering | Nej | Ja | Nej |


## <a name="android-and-ios-devices"></a>Android- och iOS-enheter

### <a name="ios-or-android-devices-example-1"></a>iOS- eller Android-enheter exempel 1

- Azure-inställningen **Maximalt antal enheter per användare** har värdet 3.
- Intune-inställningen **Enhetsgräns** har värdet 5.
 
**Resultat:** Det maximala antalet gäller per användare. Om du till exempel registrerar tre Intune-enheter kommer Azure-registreringen för den fjärde enheten inte att kunna utföras på grund av inställningarna som begränsar antalet registreringar för enheterna.

### <a name="ios-or-android-devices-example-2"></a>iOS- eller Android-enheter exempel 2

- Azure-inställningen **Maximalt antal enheter per användare** har värdet 20.
- Intune-inställningen **Enhetsgräns** har värdet 2.

**Resultat:** Du kan registrera två enheter. Intune-registreringen blockeras för ytterligare enheter. En ADE utan användartillhörighet begränsas av Azures begränsningar för enhetsregistrering även om den inte är associerad med en användare.

## <a name="windows-devices"></a>Windows-enheter

Enhetsbegränsningar i Intune gäller inte för följande typer av Windows-registrering:
- Samhanterade registreringar
- Registreringar med grupprincipobjekt (GPO)
- Azure AD-anslutna registreringar
- Azure AD-anslutna massregistreringar
- Autopilot-registreringar
- Registreringar med enhetsregistreringshanteraren

Du kan inte tillämpa enhetsbegränsningar för de här typerna av registreringar eftersom de anses vara scenarier för delade enheter. Du kan ange fasta gränser för de här typerna av registreringar i Azure Active Directory.

För enhetsbegränsning i Azure gäller inställningen **Maximalt antal enheter per användare** för enheter som antingen är Azure AD-anslutna eller Azure AD-registrerade. Inställningen gäller inte för Azure AD-hybridanslutna enheter.

### <a name="windows-10-example-1"></a>Windows 10 exempel 1

- Azure-inställningen **Maximalt antal enheter per användare** har värdet 5.
- Intune-inställningen **Enhetsgräns** har värdet 3.
- Enheterna är Azure AD-hybridanslutna och registreras automatiskt (konfigureras via GPO).

**Resultat:** Eftersom registreringen push-överförs via grupprincipobjektet gäller inte Azure-gränsen för enhetsregistrering.  Intune-gränsen för antalet enheter gäller inte heller.

### <a name="windows-10-example-2"></a>Windows 10 exempel 2

- Azure-inställningen **Maximalt antal enheter per användare** har värdet 5.
- Intune-inställningen **Enhetsgräns** har värdet 2.
- Enheterna är lokalt domänanslutna och registrerade med **Inställningar** > **Åtkomst till arbete eller skola** > **Anslut**.

**Resultat:** Du kan bara registrera två enheter innan de blockeras. Du kan registrera upp till fem enheter.


## <a name="next-steps"></a>Nästa steg

- [Skapa en enhetsgränsbegränsning i Azure.](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)
- [Konfigurera enhetsinställningar i Azure.](enrollment-restrictions-set.md#create-a-device-limit-restriction)
- [Läs mer om registrering och domänanslutning.](/azure/active-directory/devices/overview#getting-devices-in-azure-ad)