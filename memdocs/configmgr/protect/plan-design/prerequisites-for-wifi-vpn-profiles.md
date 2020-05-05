---
title: Krav för Wi-Fi- och VPN-profiler
titleSuffix: Configuration Manager
description: Läs om förutsättningarna för att hantera Wi-Fi-profiler och VPN-profiler i Configuration Manager
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9e7a557bab6b41be6e6335e3aa2744e8627d285b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722132"
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Krav för Wi-Fi-och VPN-profiler i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Wi-Fi-och VPN-profiler i Configuration Manager bara ha beroenden inom produkten.

Du behöver följande säkerhets behörigheter för att hantera åtkomst inställningar för företags resurser, t. ex. certifikat profiler, Wi-Fi-profiler och VPN-profiler:  

- Om du vill visa och hantera aviseringar och rapporter för Wi-Fi och profiler: **skapa**, **ta bort**, **ändra**, **Ändra rapport**, **läsa**och **köra rapport** för objektet **aviseringar** .  

- Om du vill skapa och hantera certifikat profiler: **författar princip**, **Ändra rapport**, **läsa**och **köra rapport** för objektet **certifikat profil** .  

- Om du vill hantera distributioner av Wi-Fi-, certifikat- och VPN-profiler: **Distribuera konfigurationsprinciper**, **Ändra varning för klientstatus**, **Läsa** och **Läsa resurs** för objektet **Samling**.  

- För att hantera alla konfigurations principer: **skapa**, **ta bort**, **ändra**, **läsa**och **Ange säkerhets omfång** för objektet **konfigurations princip** .  

- För att köra frågor som är relaterade till Wi-Fi-och VPN-profiler: behörigheten **läsa** för objektet **fråga** .  

- Om du vill visa information om Wi-Fi och VPN-profiler i Configuration Manager-konsolen: behörigheten **läsa** för objektet **plats** .  

- Om du vill visa status meddelanden för Wi-Fi-och VPN-profiler: behörigheten **läsa** för objektet **status meddelanden** .  

- Om du vill skapa och ändra certifikat profilen för den betrodda certifikat utfärdaren: **författar princip**, **Ändra rapport**, **läsa**och **köra rapport** för objektet **certifikat profil för betrodd certifikat utfärdare** .  

- Om du vill skapa och hantera VPN-profiler: **Skribentpolicy**, **Ändra rapport**, **Läsa** och **Köra rapport** för objektet **VPN-profil**.  

- Om du vill skapa och hantera Wi-Fi-profiler: **Skribentpolicy**, **Ändra rapport**, **Läsa** och **Köra rapport** för objektet **Trådlös profil**.  

Den inbyggda säkerhets rollen **åtkomst hanterare för företags resurs** omfattar de behörigheter som krävs för att hantera Wi-Fi-profiler i Configuration Manager. Mer information finns i [Konfigurera säkerhet](../../core/plan-design/security/configure-security.md).
