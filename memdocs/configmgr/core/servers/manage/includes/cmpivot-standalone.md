---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 98e3dd75316acfeaf88715b8f80762b1d6c587c6
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128348"
---
<!--This file is shared by the cmpivot.md file and the cmpivot-changes.md file and contains information on how to run CMPivot standalone. H2s or HJ3s are determined by the article for which the include file is used.-->
<!--3555890, 4619340, 4683130 -->

Från och med version 1906 kan du använda CMPivot som en fristående app. CMPivot standalone finns bara på engelska. Kör CMPivot utanför Configuration Manager-konsolen för att Visa real tids status för enheter i din miljö. Den här ändringen gör att du kan använda CMPivot på en enhet utan att först installera-konsolen.

> [!Tip]  
> Den här funktionen introducerades först i version 1906 som en [för hands versions funktion](../pre-release-features.md). Från och med version 2002 är det inte längre en för hands versions funktion.  

Du kan dela kraften i CMPivot med andra personer, till exempel supportavdelningen eller säkerhets administratörer, som inte har konsolen installerad på datorn. Dessa andra personer kan använda CMPivot för att fråga Configuration Manager tillsammans med andra verktyg som de traditionellt använder. Genom att dela dessa omfattande hanterings data kan du samar beta för att proaktivt lösa affärs problem som uppstår mellan roller.

#### <a name="install-cmpivot-standalone"></a>Installera fristående CMPivot

1. Ställ in de behörigheter som krävs för att köra CMPivot. Mer information finns i [krav](../cmpivot.md#prerequisites). Du kan också använda [rollen säkerhets administratör](../cmpivot-changes.md#bkmk_cmpivot_secadmin1906) om behörigheterna är lämpliga för användaren.
2. Hitta installations programmet CMPivot på följande sökväg: `<site install path>\tools\CMPivot\CMPivot.msi` . Du kan köra den från den sökvägen eller kopiera den till en annan plats.
3. När du kör den fristående CMPivot-appen uppmanas du att ansluta till en-plats. Ange det fullständigt kvalificerade domän namnet eller dator namnet för antingen den centrala administrations servern eller den primära plats servern.
   - Varje gången du öppnar CMPivot fristående uppmanas du att ansluta till en plats Server.
4. Bläddra till den samling som du vill köra CMPivot på och kör sedan frågan.

   ![Bläddra till den samling som du vill köra frågan mot](../media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> - Högerklicka på åtgärder, till exempel **köra skript**, **Resursläsaren**och Webbs ökning inte är tillgängligt i CMPivot fristående. Den primära användningen av CMPivot-fristående frågor görs oberoende av den Configuration Manager infrastrukturen. För att hjälpa säkerhets administratörerna, innehåller CMPivot fristående möjlighet att ansluta till Microsoft Defender Security Center. <!--5605358-->
> - Från och med version 1910 kan du göra en [fråga om utvärdering av lokala enheter med CMPivot fristående](../cmpivot-changes.md#bkmk_local-eval). <!--3197353--> 