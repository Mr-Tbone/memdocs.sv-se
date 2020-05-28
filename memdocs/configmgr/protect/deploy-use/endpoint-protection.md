---
title: Slutpunktsskydd
titleSuffix: Configuration Manager
description: Lär dig hur du hanterar principer för program mot skadlig kod och Windows-brandväggen för klienter.
ms.date: 03/18/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5bdfd566682156e39e1dbed7c55af85b20a78671
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906686"
---
# <a name="endpoint-protection"></a>Slutpunktsskydd

*Gäller för: Configuration Manager (aktuell gren)*

Endpoint Protection hanterar principer för skadlig kod och Windows-brandväggen för klient datorer i din Configuration Manager-hierarki.  

> [!IMPORTANT]  
>  Du måste vara licensierad att använda Endpoint Protection för att hantera klienter i din Configuration Manager-hierarki.  

 När du använder Endpoint Protection med Configuration Manager har du följande fördelar:  

-   Konfigurera principer för program mot skadlig kod, inställningar för Windows-brandväggen och hantera Microsoft Defender Avancerat skydd till valda grupper av datorer  
-   Använd Configuration Manager program uppdateringar för att ladda ned de senaste definitions filerna för program mot skadlig kod för att hålla klient datorerna uppdaterade  
-   Skicka e-postmeddelanden, använda övervakning i konsolen och Visa rapporter. De här åtgärderna informerar administrativa användare när skadlig kod upptäcks på klient datorer.  

Från och med Windows 10-och Windows Server 2016-datorer är Windows Defender redan installerat. För dessa operativ system installeras en hanterings klient för Windows Defender när den Configuration Manager-klienten installeras. På Windows 8,1 och tidigare datorer installeras Endpoint Protection-klienten med Configuration Manager-klienten. Windows Defender och Endpoint Protection-klienten har följande funktioner:  

-   Identifiering av skadlig kod och spionprogram och relevanta reparationsåtgärder  
-   Identifiering av spökprogram och relevanta reparationsåtgärder  
-   Utvärdering av kritiska säkerhetsrisker och automatisk uppdatering av definitioner och motor  
-   Upptäckt av säkerhetsproblem i nätverket via kontrollsystem för nätverk  
-   Integrering med moln skydds tjänsten för att rapportera skadlig kod till Microsoft. När du ansluter till den här tjänsten laddar Endpoint Protection-klienten eller Windows Defender de senaste definitionerna från Malware Protection Center när oidentifierad skadlig kod upptäcks på en dator.  

> [!NOTE]  
>  Endpoint Protection-klienten kan installeras på en server som kör Hyper-V och på virtuella gäst datorer med operativ system som stöds. För att förhindra överdriven CPU-användning har Endpoint Protection åtgärder en inbyggd slumpmässig fördröjning så att skydds tjänsterna inte körs samtidigt.  

 Dessutom kan du hantera inställningar för Windows-brandväggen med Endpoint Protection i Configuration Manager-konsolen.  

 [Exempel scenario: använda System Center Endpoint Protection för att skydda datorer mot skadlig kod](scenarios-endpoint-protection.md) Endpoint Protection och Windows-brandväggen.  


## <a name="managing-malware-with-endpoint-protection"></a>Hantera skadlig kod med Endpoint Protection  
 Med Endpoint Protection i Configuration Manager kan du skapa principer för program mot skadlig kod som innehåller inställningar för Endpoint Protection-klientkonfigurationer. Distribuera dessa principer för program mot skadlig kod till klient datorer. Övervaka sedan efterlevnaden i noden **Endpoint Protection status** under **säkerhet** i arbets ytan **övervakning** . Använd också Endpoint Protection rapporter i noden **rapportering** .  

 Ytterligare information:  

-   [Skapa och distribuera principer för program mot skadlig kod för Endpoint Protection](endpoint-antimalware-policies.md) -skapa, distribuera och övervaka principer för program mot skadlig kod med en lista över de inställningar som du kan konfigurera  

-   [Övervaka rapporter för Endpoint Protection övervakning av](monitor-endpoint-protection.md) aktiviteter, infekterade klient datorer med mera.  

-   [Hantera principer för program mot skadlig kod och brand Väggs inställningar för Endpoint Protection](endpoint-antimalware-firewall.md) Åtgärda skadlig kod som hittats på klient datorer  

-   [Loggfiler för Endpoint Protection](../../core/plan-design/hierarchy/log-files.md#BKMK_EPLog)  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Hantera Windows-brandväggen med Endpoint Protection  
 Endpoint Protection i Configuration Manager ger grundläggande hantering av Windows-brandväggen på klient datorer. Du kan konfigurera följande inställningar för varje nätverksprofil:  

-   Aktivera eller inaktivera Windows-brandväggen.  

-   Blockera inkommande anslutningar, även de som finns i listan över tillåtna program.  

-   Meddela användaren när ett nytt program blockeras av Windows-brandväggen.  

> [!NOTE]  
>  Endpoint Protection stöder endast hantering av Windows-brandväggen.  


 Mer information finns i [skapa och distribuera principer för Windows-brandväggen för Endpoint Protection](create-windows-firewall-policies.md).  


## <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

Endpoint Protection hanterar och övervakar Microsoft Defender Avancerat skydd (ATP), tidigare kallat Windows Defender ATP. Microsoft Defender ATP-tjänsten hjälper företag att upptäcka, undersöka och svara på avancerade attacker i företags nätverket. Mer information finns i [Microsoft Defender Avancerat skydd](windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Endpoint Protection-arbetsflöde  
 Använd följande diagram för att hjälpa dig att förstå arbets flödet för att implementera Endpoint Protection i din Configuration Manager-hierarki.  

 ![Endpoint Protection-arbetsflöde](../media/Endpoint-Protection-Workflow.gif)  



## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Endpoint Protection-klienten för Mac-datorer och Linux-servrar  

> [!Important]  
> Stöd för System Center Endpoint Protection (SCEP) för Mac och Linux (alla versioner) upphör den 31 december 2018. Tillgänglighet för nya virus definitioner för SCEP för Mac och SCEP för Linux kan komma att upphöra efter Supportens slut. Mer information finns i [blogg inlägget End of support](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257).  

 I System Center Endpoint Protection ingår en Endpoint Protection-klient för Linux och Mac-datorer. Dessa klienter levereras inte med Configuration Manager. Ladda ned följande produkter från [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx):  

-   System Center-Endpoint Protection för Mac  

-   System Center-Endpoint Protection för Linux  


> [!Note]  
>  Du måste vara en Microsoft Volume License-kund för att kunna ladda ned Endpoint Protection-installationsfilerna för Linux och Mac.  

 Dessa produkter kan inte hanteras från Configuration Manager-konsolen. Ett System Center Operations Manager hanterings paket medföljer installationsfilerna, som gör att du kan hantera-klienten för Linux.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Så här hämtar du Endpoint Protection-klienten för Mac-datorer och Linux-servrar

Använd följande steg för att hämta avbildnings filen som innehåller Endpoint Protection-klient program vara och dokumentation för Mac-datorer och Linux-servrar.
1. Logga in på [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. Välj fliken **nedladdningar och nycklar** överst på webbplatsen.
3. Filtrera på produkt **System Center Endpoint Protection (aktuell gren)**.
4. Klicka på länken för att **Ladda ned**
5. Klicka på **Fortsätt**. Du bör se flera filer, inklusive en namngiven: **System Center Endpoint Protection (aktuell gren version 1606) för Linux OS och Macintosh OS multilanguage 32/64 bit 1878 MB ISO**.
6. Klicka på pilen om du vill hämta filen. Fil namnet är **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-3_EptProt_Lin_Mac_MLF_X21-67050. ISO**.

Uppdateringen januari 2018 (X21-67050) innehåller följande versioner:

- System Center-Endpoint Protection för Mac-4.5.32.0 (stöd för macOS 10,13 med hög Sierra)
- System Center-Endpoint Protection för Linux-4.5.20.0 

  Mer information om hur du installerar och hanterar Endpoint Protection-klienter för Linux-och Mac-datorer finns i dokumentationen som medföljer dessa produkter. Den här produkt dokumentationen finns i mappen **dokumentation** i. ISO-fil.
