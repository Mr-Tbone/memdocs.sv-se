---
title: Registrera enheter för lokal MDM
titleSuffix: Configuration Manager
description: Lär dig mer om metoder för att registrera enheter för lokal hantering av mobila enheter (MDM) i Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ca7f792bb6b419dd1d20d495bdb53bc7c2be506
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720676"
---
# <a name="enroll-devices-for-on-premises-mdm-in-configuration-manager"></a>Registrera enheter för lokal MDM i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Om du vill hantera enheter med Configuration Manager lokal hantering av mobila enheter (MDM) måste du först registrera dem. Configuration Manager kan sedan kommunicera med enheterna för hanterings uppgifter. Configuration Manager tillhandahåller två metoder för att registrera enheter:

- **Användar registrering**: användare startar registrerings processen på sin enhet. För att användar registrering ska lyckas, installerar du det betrodda rot certifikatet på enheten och etablerar användaren för registrering i klient inställningar. Användaren behöver bara ange sina autentiseringsuppgifter för att registrera en enhet.

    Mer information finns i [hur användare registrerar enheter](user-enroll-devices-on-premises-mdm.md).

- **Mass registrering**: användare av enheten startar inte registrering. Du skapar ett Mass registrerings paket i Configuration Manager. När du öppnar den på enheten tillhandahåller paketet den information som krävs för att registrera enheten.

    Mer information finns i [så här gör du för att registrera enheter](bulk-enroll-devices-on-premises-mdm.md).

Mer information om de OS-versioner som Configuration Manager stöder för enhets registrering i lokal MDM finns i [konfigurationer som stöds](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).
