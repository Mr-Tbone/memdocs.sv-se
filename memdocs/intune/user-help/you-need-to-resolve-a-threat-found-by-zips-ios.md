---
title: Lösa hot som upptäckts av Zimperium zIPS på iOS | Microsoft Docs
description: Lär dig hur du löser hot som har hittats på en iOS-enhet.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/05/2018
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: eaccd9c0-cd46-48e2-8675-4c022c74f672
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: f72415900067793d41b0e6086cf3ee0c78e9ee85
ms.sourcegitcommit: 2ee50bfc416182362ae0b8070b096e1cc792bf68
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87865660"
---
# <a name="resolve-a-threat-found-by-zimperium-zips-on-ios"></a>Åtgärda ett hot som Zimperium zIPS har påträffat på iOS

Zimperium zIPS är en tjänst för skydd mot mobila hot som identifierar potentiella hot på iOS-enheter. Dessa hot rapporteras till företagsportalappen och visas som olösta, ej kompatibla problem. Om enheten identifieras som ej kompatibel kanske du inte kan:

* Ansluta till företagets e-post
* Ansluta till företagets Wi-Fi
* Ansluta till SharePoint Online
* Synkronisera företagsfiler med OneDrive
* Få åtkomst till företagsappar

Den här artikeln beskriver hur du kan känna igen hotaviseringar från Zimperium zIPS och vad du kan göra för att lösa dem. 

## <a name="troubleshoot-virus-or-security-threat"></a>Felsöka virus- eller säkerhetshot  
Om ett virus- eller säkerhetshot identifieras agerar Zimperium zIPS enligt organisationens åtkomstprinciper. Företagets åtkomstprinciper kan förhindra att du kommer åt arbetets nätverk, appar och e-post från enheten.  

Zimperium zIPS uppmanar dig att vidta åtgärder för att återfå den åtkomst som du har förlorat. Välj hotet och följ instruktionerna i appen för att lösa det.

Eftersom appen är integrerad med företagets MDM-provider kan du även se en varning om begränsad åtkomst till företagsportalappen. Varningen ger dig instruktioner om att öppna Zimperium zIPS för att åtgärda virus- eller säkerhetshotet.  

  ![Exempel på skärmbild av enhetssidan i företagsportalen, som visar varningen från Zimperium zIPS.](./media/CP-lookout-virus-banner-1808.png)  
  
## <a name="troubleshoot-an-app-threat"></a>Felsöka ett apphot

Om du installerar en app som ses som ett hot mot din enhet får du ett meddelande i Zimperium zIPS. Om den berörda appen finns kvar på enheten kan du inte komma åt företagsresurser.  

Lös detta genom att välja appen i listan över hot i Zimperium zIPS. Följ sedan anvisningarna på skärmen för att ta bort och avinstallera appen.  

Behöver du fortfarande hjälp? Kontakta företagets support. Du hittar kontaktinformationen på [Företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).   
