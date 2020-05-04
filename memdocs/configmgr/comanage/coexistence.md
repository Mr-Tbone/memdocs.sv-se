---
title: Samexistens för tredje parts MDM
titleSuffix: Configuration Manager
description: Lär dig mer om att använda en MDM-tjänst från tredje part med Configuration Manager
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: ed4dc65e-e5d5-4f75-88ac-f4849ec8fc10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f22ba6f29e0c85e19ab66d1b052085db5303cc2c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710827"
---
# <a name="third-party-mdm-coexistence-with-configuration-manager"></a>MDM-samexistens från tredje part med Configuration Manager

När du samtidigt hanterar Windows 10-enheter med både Configuration Manager och Microsoft Intune kallas den [samhantering](overview.md). När du hanterar enheter med Configuration Manager och registrerar till en MDM-tjänst från tredje part kallas den här funktionen för *samexistens*. Att ha två hanterings myndigheter för en enskild enhet kan vara utmanande om de inte är korrekt dirigerade mellan de två. Med samhantering kan Configuration Manager och Intune utjämna [arbets belastningarna](workloads.md) för att se till att det inte finns några konflikter. Den här interaktionen finns inte med tjänster från tredje part, så det finns begränsningar med hanterings funktionerna för samexistens.

Configuration Manager-klienten kan samverka med en MDM-tjänst från tredje part på en enhet som kör Windows 10 version 1709 eller senare och som är ansluten till Azure Active Directory. Enheten kan vara någon av följande typer:

- Endast [Azure AD-ansluten](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) . (Den här typen kallas ibland "molnbaserad domän ansluten")  

- [Hybrid](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)domänanslutna, där enheten är ansluten till din lokala Active Directory och registrerats med din Azure Active Directory.  

> [!Note]  
> Den har inte stöd för [personligt ägda enheter](https://docs.microsoft.com/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device).  

När Configuration Manager-klienten upptäcker att en MDM-tjänst från tredje part också hanterar enheten inaktive ras automatiskt vissa arbets belastningar i Configuration Manager. Detta beteende gör att MDM-tjänsten kan ta över dessa funktioner. Den förhindrar också motstridiga inställningar på klienten som kan påverka enhetens och användarens upplevelse negativt. Följande arbets belastningar i Configuration Manager inaktive ras i det här fallet:

- Resurs åtkomst principer för VPN-, Wi-Fi-, e-post-och certifikat inställningar
- Program hantering, inklusive gamla paket
- Genomsökning och installation av program uppdatering
- Endpoint Protection, Windows Defender Suite för skydd mot skadlig kod
- Efterlevnadsprincip för villkorlig åtkomst
- Enhetskonfiguration
- Office Klicka-och-kör-hantering

Configuration Manager-klienten förhindrar en konflikt med hanterings auktoriteten för tredje part genom att fortsätta med följande skrivskyddade åtgärder:

- Inventering av maskin- och programvara
- Tillgångsinformation
- Avläsning av programvara
- Rapportering om energispar funktioner

Mer information om fördelarna med samhantering med Configuration Manager och Intune finns i [samhanterings förmåner](overview.md#benefits).
