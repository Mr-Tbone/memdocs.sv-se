---
title: Övervaka Endpoint Protection-status
titleSuffix: Configuration Manager
description: Lär dig hur övervaknings Endpoint Protection i din Configuration Manager-hierarki.
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 18bbbfc6486a1e5a784603e6725629d966f6c11a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722279"
---
# <a name="how-to-monitor-endpoint-protection-status"></a>Övervaka Endpoint Protection status

*Gäller för: Configuration Manager (aktuell gren)*

Du kan övervaka Endpoint Protection i din Microsoft Configuration Manager-hierarki genom att använda noden **Endpoint Protection status** under **säkerhet** i arbets ytan **övervakning** , **Endpoint Protection** noden i arbets ytan **till gångar och efterlevnad** och med hjälp av rapporter.  

##  <a name="how-to-monitor-endpoint-protection-by-using-the-endpoint-protection-status-node"></a><a name="BKMK_1"></a>Övervaka Endpoint Protection med hjälp av noden Endpoint Protection status  

1. Klicka på **övervakning**i Configuration Manager-konsolen.  

2. I arbets ytan **övervakning** expanderar du **säkerhet** och klickar sedan på **Endpoint Protection status**.  

3. I listan **samling** väljer du den samling som du vill visa statusinformation för.  

   > [!IMPORTANT]
   >  Samlingar är tillgängliga för val i följande fall:  
   > 
   > - När du väljer **Visa den här samlingen i Endpoint Protection instrument panelen** på fliken **aviseringar** i dialog rutan**Egenskaper** för <em><samlings namn\></em>.  
   >   -   När du distribuerar en Endpoint Protection Antiskadlig kod-princip till samlingen.  
   >   -   När du aktiverar och distribuerar Endpoint Protection klient inställningar till samlingen.  

4. Granska informationen som visas i avsnitten **säkerhets tillstånd** och **drift status** . Klicka på en statuslänk om du vill skapa en tillfällig samling i noden **Enheter** i arbetsytan **Tillgångar och efterlevnad**. Den tillfälliga samlingen innehåller de datorer som har vald status.  

   > [!IMPORTANT]  
   >  Information som visas i noden **Endpoint Protection status** baseras på de senaste data som sammanfattades från Configuration Manager-databasen och kanske inte är aktuella. Om du vill hämta den senaste informationen klickar du på **Kör sammanfattning** på fliken **Start** eller klickar på **Schemalägg sammanfattning** för att anpassa sammanfattningsintervallet.  

##  <a name="how-to-monitor-endpoint-protection-in-the-assets-and-compliance-workspace"></a><a name="BKMK_2"></a>Övervaka Endpoint Protection i arbets ytan till gångar och efterlevnad  

1.  Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

2.  På arbets ytan **till gångar och efterlevnad** utför du någon av följande åtgärder:  

    -   Klicka på **Enheter**. I listan **Enheter** väljer du en dator och klickar sedan på fliken **Detalj för skadlig kod** .  

    -   Klicka på **enhets samlingar**. I listan **Enhetssamlingar** väljer du den samling som innehåller datorn som du vill övervaka. Gå sedan till gruppen **Kör sammanfattning** på fliken **Start** och klicka på **Visa medlemmar**.  

3.  I listan *<samlings\> namn* väljer du en dator och klickar sedan på fliken **detalj för skadlig kod** .  

##  <a name="how-to-monitor-endpoint-protection-by-using-reports"></a><a name="BKMK_3"></a>Övervaka Endpoint Protection med hjälp av rapporter  
 Använd följande rapporter för att få hjälp att visa information om Endpoint Protection i hierarkin. Du kan också använda dessa rapporter för att felsöka eventuella Endpoint Protection problem. Mer information om hur du konfigurerar rapportering i Configuration Manager finns i [Introduktion till rapporterings](../../core/servers/manage/introduction-to-reporting.md) -och [loggfiler](../../core/plan-design/hierarchy/log-files.md). Endpoint Protection rapporter finns i mappen Endpoint Protection.  

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Aktivitets rapport för program mot skadlig kod**|Visar en översikt över aktivitet för program mot skadlig kod för en angiven samling.|  
|**Infekterade datorer**|Visar en lista över datorer där ett angivet hot har hittats.|  
|**Användare med flest hot**|Visar en lista med användarna som har flest upptäckta hot.|  
|**Lista över användar hot**|Visar listan över hot som har hittats för ett angivet användarkonto.|  

## <a name="malware-alert-levels"></a>Aviserings nivåer för skadlig kod  
 Använd följande tabell för att identifiera de olika Endpoint Protection varnings nivåer som kan visas i rapporter eller i Configuration Manager-konsolen.  

|Aviseringsnivå|Beskrivning|  
|-----------------|-----------------|  
|**Misslyckades**|Endpoint Protection kunde inte reparera den skadliga koden. Mer information om felet finns i loggarna.<br /><br /> **Obs:** En lista över Configuration Manager och Endpoint Protection loggfiler finns i avsnittet "Endpoint Protection" i avsnittet [loggfiler](../../core/plan-design/hierarchy/log-files.md) .|  
|**Bort**|Endpoint Protection har tagit bort den skadliga koden.|  
|**I karantän**|Endpoint Protection flyttade den skadliga koden till en säker plats och hindrade den från att köras tills du tar bort den eller tillåter att den körs.|  
|**Rensad**|Den skadliga koden har rensats bort från den infekterade filen.|  
|**Tillåts**|En administrativ användare har valt att tillåta körning av programvaran som innehåller skadlig kod.|  
|**Ingen åtgärd**|Endpoint Protection vidtog ingen åtgärd för den skadliga koden. Detta kan inträffa om datorn startas om efter att den skadliga koden har upptäckts och den skadliga koden inte längre hittas, t.ex. om en mappad nätverksenhet där skadlig kod upptäcks inte återansluts när datorn startas om.|  
|**Blockerad**|Endpoint Protection blockerade den skadliga koden från att köras. Detta kan inträffa om en process på datorn visar sig innehålla skadlig kod.|
