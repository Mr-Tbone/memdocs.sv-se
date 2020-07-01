---
title: Planera för Endpoint Protection
titleSuffix: Configuration Manager
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 7610bbd3-a67f-4a09-8115-e35d40d43b42
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2c733ef03482ddfc1f3e6502d7f5fe8ae0d20b76
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590515"
---
# <a name="planning-for-endpoint-protection-in-configuration-manager"></a>Planera Endpoint Protection i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*


Endpoint Protection i Configuration Manager kan du hantera principer för program mot skadlig kod och Windows-brandväggen för klient datorer i din Configuration Manager-hierarki.  

> [!IMPORTANT]  
>  Du måste vara licensierad att använda Endpoint Protection för att hantera klienter i din Configuration Manager-hierarki.  

När du använder Endpoint Protection med Configuration Manager har du följande fördelar:  

-   Konfigurera principer för program mot skadlig kod, inställningar för Windows-brandväggen och hantera Microsoft Defender Avancerat skydd till valda grupper av datorer  

-   Använd Configuration Manager program uppdateringar för att ladda ned de senaste definitions filerna för program mot skadlig kod för att hålla klient datorerna uppdaterade  

-   Skicka e-postmeddelanden, använda övervakning i konsolen och visa rapporter för att hålla administrativa användare informerade om skadlig kod upptäcks på klientdatorer  

Windows 10-datorer kräver ingen ytterligare klient för Endpoint Protection-hantering. På Windows 8,1 och tidigare datorer installerar Endpoint Protection sin egen klient utöver Configuration Manager-klienten. Endpoint Protection-klienten har följande funktioner:  

-   Identifiering av skadlig kod och spionprogram och relevanta reparationsåtgärder  

-   Identifiering av spökprogram och relevanta reparationsåtgärder  

-   Utvärdering av kritiska säkerhetsrisker och automatisk uppdatering av definitioner och motor  

-   Upptäckt av säkerhetsproblem i nätverket via kontrollsystem för nätverk  

-   Integrering med moln skydds tjänsten för att rapportera skadlig kod till Microsoft. När du ansluter till den här tjänsten kan Windows Defender eller Endpoint Protection klienten hämta de senaste definitionerna från Malware Protection Center när oidentifierad skadlig kod har identifierats på en dator.  

> [!NOTE]  
>  Endpoint Protection-klienten kan installeras på en server som kör Hyper-V och på virtuella gäst datorer med operativ system som stöds. För att förhindra överdriven CPU-användning har Endpoint Protection åtgärder en inbyggd, slumpmässig fördröjning så att tjänsterna inte körs samtidigt.  

  Dessutom kan du med Endpoint Protection i Configuration Manager hantera inställningar för Windows-brandväggen i Configuration Manager-konsolen.  

 [Exempel scenario: att använda System Center Endpoint Protection för att skydda datorer från skadlig kod](../deploy-use/scenarios-endpoint-protection.md) visar hur du kan konfigurera och hantera Endpoint Protection och Windows-brandväggen.  

## <a name="managing-malware-with-endpoint-protection"></a>Hantera skadlig kod med Endpoint Protection  

Med Endpoint Protection i Configuration Manager kan du skapa principer för program mot skadlig kod som innehåller inställningar för Endpoint Protection-klientkonfigurationer. Du kan sedan distribuera dessa principer för program mot skadlig kod till klient datorer och övervaka dem i noden **Endpoint Protection status** på arbets ytan **övervakning** eller genom att använda Configuration Manager rapporter.  

 Ytterligare information:  

-   [Skapa och distribuera principer för program mot skadlig kod för Endpoint Protection](../deploy-use/endpoint-antimalware-policies.md) -skapa, distribuera och övervaka principer för program mot skadlig kod med en lista över de inställningar som du kan konfigurera  

-   [Övervaka](../deploy-use/monitor-endpoint-protection.md) aktivitets rapporter i Endpoint Protection övervakning, infekterade klient datorer med mera.   

-   [Hantera principer för program mot skadlig kod och brand Väggs inställningar för Endpoint Protection](../deploy-use/endpoint-antimalware-firewall.md) – du kan ändra princip prioritet för [program mot skadlig kod](../deploy-use/endpoint-antimalware-firewall.md#manage-antimalware-policies) eller [brand vägg](../deploy-use/endpoint-antimalware-firewall.md#manage-windows-firewall-policies), [Åtgärda skadlig kod som finns på klient datorer](../deploy-use/endpoint-antimalware-firewall.md#remediate-detected-malware)och andra uppgifter

## <a name="managing-windows-firewall-with-endpoint-protection"></a>Hantera Windows-brandväggen med Endpoint Protection  
 Endpoint Protection i Configuration Manager ger grundläggande hantering av Windows-brandväggen på klient datorer. Du kan konfigurera följande inställningar för varje nätverksprofil:  

-   Aktivera eller inaktivera Windows-brandväggen.  

-   Blockera inkommande anslutningar, även de som finns i listan över tillåtna program.  

-   Meddela användaren när ett nytt program blockeras av Windows-brandväggen.  

> [!NOTE]  
>  Endpoint Protection stöder endast hantering av Windows-brandväggen.  

  Mer information om hur du skapar och distribuerar principer för Windows-brandväggen för Endpoint Protection finns i [skapa och distribuera principer för Windows-brandväggen för Endpoint Protection](../deploy-use/create-windows-firewall-policies.md).  

## <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

Från och med version 1606 av Configuration Manager (aktuell gren) kan Endpoint Protection hjälpa till att hantera och övervaka Microsoft Defender Advanced Threat Protection (ATP), tidigare kallat Windows Defender ATP. Microsoft Defender ATP är en tjänst som hjälper företag att upptäcka, undersöka och svara på avancerade attacker i sina nätverk. Se [Microsoft Defender Avancerat skydd](../deploy-use/defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Endpoint Protection-arbetsflöde  
 Använd följande diagram för att hjälpa dig att förstå arbets flödet för att implementera Endpoint Protection i din Configuration Manager-hierarki.  

 ![Endpoint Protection-arbetsflöde](../media/Endpoint-Protection-Workflow.gif)

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Endpoint Protection-klienten för Mac-datorer och Linux-servrar  
 System Center innehåller en Endpoint Protection-klient för Linux och för Mac-datorer. Dessa klienter levereras inte med Configuration Manager. i stället måste du ladda ned följande produkter från [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

> [!IMPORTANT]  
>  Du måste vara en Microsoft Volume License-kund för att kunna ladda ned Endpoint Protection-installationsfilerna för Linux och Mac.  

 Dessa produkter kan inte hanteras från Configuration Manager-konsolen. Ett System Center Operations Manager-hanteringspaket medföljer dock installationsfilerna och gör att du kan hantera klienten för Linux med hjälp av Operations Manager.  

 Mer information om hur du installerar och hanterar Endpoint Protection-klienter för Linux- och Mac-datorer finns i dokumentationen som medföljer dessa produkter, som du hittar i mappen **Dokumentation** .

## <a name="best-practices-for-endpoint-protection-in-configuration-manager"></a>Metodtips för Endpoint Protection i Configuration Manager  
 Följ dessa rekommendationer för Endpoint Protection i System Center 2012 Configuration Manager.  

### <a name="configure-custom-client-settings-for-endpoint-protection"></a>Konfigurera anpassade klientinställningar för Endpoint Protection  
 När du konfigurerar klient inställningar för Endpoint Protection ska du inte använda standard klient inställningarna eftersom de tillämpar inställningar på alla datorer i hierarkin. Konfigurera i stället anpassade klientinställningar och tilldela dessa inställningar till samlingar med datorer i hierarkin.  

 När du konfigurerar anpassade klientinställningar kan du göra följande:  

-   Anpassa inställningar för program mot skadlig kod och säkerhetsinställningar för olika delar av organisationen.  
-   Testa effekterna av att köra Endpoint Protection på en liten grupp datorer innan du distribuerar det till hela hierarkin.  
-   Lägg till fler klienter i samlingen över tid för att fasa distributionen av den Endpoint Protection klienten.  

### <a name="distributing-definition-updates-by-using-software-updates"></a>Distribuera definitionsuppdateringar med hjälp av programuppdateringar  
 Om du använder Configuration Manager program uppdateringar för att distribuera definitions uppdateringar bör du överväga att placera definitions uppdateringar i ett paket som inte innehåller andra program uppdateringar. På så sätt blir definitionsuppdateringspaketet mindre, vilket gör att det kan replikeras snabbare till distributionsplatser.
