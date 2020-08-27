---
author: brenduns
ms.author: brenduns
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: include
ms.date: 08/24/2020
ms.openlocfilehash: 01179c35274ff14d4a91283e9a38aa5e6fee8e03
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88823528"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. Använd en Configuration Manager-konsol som är ansluten till webbplatsen på den högsta nivån, högerklicka du på en enhetssamling du synkroniserar med administrationscentret för Microsoft Endpoint Manager och välj **Egenskaper**.

2. Aktivera alternativet **Gör den här samlingen tillgänglig för tilldelning av slutpunktssäkerhetsprinciper från Microsoft Endpoint Manager-administrationscenter** på fliken **Cloud Sync**.

   - Du kan inte välja det här alternativet om Configuration Manager-hierarkin inte är ansluten till klientorganisationen.
   - Samlingarna som är tillgängliga för det här alternativet begränsas av [samlingens omfattning som valts för uppladdningen av klientorganisationsanslutningen](../../../configmgr/tenant-attach/device-sync-actions.md#bkmk_edit). <!--CM7423168-->
  
   ![Konfigurera molnsynkronisering](../media/tenant-attach-intune/cloud-sync.png)

3. Välj **OK** för att spara konfigurationen.

   Enheter i den här samlingen kan nu registreras med Microsoft Defender ATP och har stöd för användning av säkerhetsprinciper för Intune-slutpunkter.
