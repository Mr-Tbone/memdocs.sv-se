---
title: Åtgärda hot som upptäckts av SandBlast Mobile Protect för Android | Microsoft Docs
description: Lär dig att åtgärda ett hot som hittades av SandBlast Mobile Protect för Android.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/28/2018
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 449c34ec-2d94-4c7f-8691-a5200efee3cb
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 2f6ba59ccc2832a66eb1a7b081008aa43b0c75bc
ms.sourcegitcommit: 2ee50bfc416182362ae0b8070b096e1cc792bf68
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87866238"
---
# <a name="resolve-a-threat-found-by-sandblast-mobile-protect-on-android"></a>Åtgärda ett hot som har upptäckts av SandBlast Mobile Protect på Android

SandBlast Mobile Protect är en tjänst för skydd mot mobila hot som identifierar potentiella hot på Android-enheter. Det rapporterar hot som du sedan kan se i företagsportalappen. Hot visas i appen som olösta, ej kompatibla problem. Så länge dessa hot finns kvar kanske du inte kan:   

* Ansluta till företagets e-post
* Ansluta till företagets Wi-Fi
* Ansluta till SharePoint Online
* Synkronisera företagsfiler med OneDrive
* Få åtkomst till företagsappar

Den här artikeln beskriver hur du kan känna igen hotaviseringar från SandBlast Mobile Protect och vad du kan göra för att lösa dem.  

## <a name="troubleshoot-virus-or-security-threat"></a>Felsöka virus- eller säkerhetshot  
Om ett virus- eller säkerhetshot identifieras agerar SandBlast Mobile Protect-appen enligt organisationens åtkomstprinciper. Företagets åtkomstprinciper kan förhindra att du kommer åt arbetets nätverk, appar och e-post.  

![Exempel på skärmbild för ett aviseringsmeddelande från SEP Mobile-appen.](./media/skycure-list-of-potential-issues-android.png)  

SandBlast Mobile Protect uppmanar dig dock även att vidta åtgärder för att återfå den åtkomst som du har förlorat. Välj hotet och följ instruktionerna i appen för att lösa det.

Eftersom appen är integrerad med företagets MDM-provider kan du även se en varning om begränsad åtkomst till företagsportalappen. Varningen ger dig instruktioner om att öppna Sandblast Mobile Protect för att åtgärda virus- eller säkerhetshotet.

  ![Exempel på skärmbild av enhetssidan i företagsportalen, som visar varningen från SandBlast Mobile Protect.](./media/CP-lookout-virus-banner-1808.png)  

## <a name="troubleshoot-an-app-threat"></a>Felsöka ett apphot  

Om du installerar en app som ses som ett hot mot din enhet får du ett meddelande i SandBlast Mobile Protect. Om den berörda appen finns kvar på enheten kan du inte komma åt företagsresurser.  

Lös detta genom att välja appen i listan över hot i SandBlast Mobile Protect. Följ sedan anvisningarna för att ta bort och avinstallera appen.     

Behöver du fortfarande hjälp? Kontakta företagssupporten. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).
