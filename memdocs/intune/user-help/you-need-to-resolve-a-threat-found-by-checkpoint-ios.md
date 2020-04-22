---
title: Åtgärda hot som upptäckts av SandBlast Mobile Protect på iOS | Microsoft Docs
description: Lär dig att åtgärda ett hot som hittades av SandBlast Mobile Protect för iOS.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/05/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 5b2a69e7-cc86-4f1b-81d9-35b8b23b937b
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 3966560e48d0a409b592e33b22cf5e79b223e30a
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79346397"
---
# <a name="resolve-a-threat-found-by-sandblast-mobile-protect"></a>Åtgärda ett hot som har upptäckts av SandBlast Mobile Protect

SandBlast Mobile Protect är en tjänst för skydd mot mobila hot som identifierar och bedömer potentiella hot på iOS-enheter. Den rapporterar sedan hoten så att du kan se dem från företagsportalappen. Hot visas i appen som olösta, ej kompatibla problem. Så länge dessa hot finns kvar kan du inte:   

* Ansluta till företagets e-post
* Ansluta till företagets Wi-Fi
* Ansluta till SharePoint Online
* Synkronisera företagsfiler med OneDrive
* Få åtkomst till företagsappar

Den här artikeln beskriver hur du kan känna igen hotaviseringar från SandBlast Mobile Protect och vad du kan göra för att lösa dem.  

## <a name="troubleshoot-virus-or-security-threat"></a>Felsöka virus- eller säkerhetshot  
Om ett virus- eller säkerhetshot identifieras agerar SandBlast Mobile Protect-appen enligt organisationens åtkomstprinciper. Åtkomstprinciper kan förhindra att du kommer åt arbetets nätverk, appar och e-post.  

![Exempel på skärmbild för ett aviseringsmeddelande från SEP Mobile-appen.](./media/skycure-list-of-potential-issues-android.png)  
SandBlast Mobile Protect uppmanar dig att vidta åtgärder för att återfå den åtkomst som du har förlorat. Välj hotet och följ instruktionerna i appen för att lösa det.

Eftersom appen är integrerad med företagets MDM-provider kan du även se en varning om begränsad åtkomst till företagsportalappen. Varningen ger dig instruktioner om att öppna Sandblast Mobile Protect för att åtgärda virus- eller säkerhetshotet.  

  ![Exempel på skärmbild av enhetssidan på företagsportalen, som visar varningen från Sandblast Mobile Protect.](./media/CP-lookout-virus-banner-1808.png)  

## <a name="troubleshoot-an-app-threat"></a>Felsöka ett apphot  

Om du installerar en app som ses som ett hot mot din enhet får du ett meddelande i SandBlast Mobile Protect. Om den berörda appen finns kvar på enheten kan du inte komma åt företagsresurser.  

Lös detta genom att välja appen i listan över hot i SandBlast Mobile Protect. Följ sedan anvisningarna för att ta bort och avinstallera appen.  

Behöver du fortfarande hjälp? Kontakta företagets support. Du hittar kontaktinformationen på [Företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).  
