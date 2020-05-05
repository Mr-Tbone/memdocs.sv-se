---
title: Hjälp om Endpoint Protection-klienten
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner och förbättringar i Endpoint Protection som bättre hjälper dig att skydda din dator mot hot.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: fdcee455-22e3-451d-bcf3-e7b62792f04a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: eba7de1705212bb5cb329282bc407317995b82f3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724344"
---
# <a name="endpoint-protection-client-help"></a>Hjälp om Endpoint Protection-klienten

*Gäller för: Configuration Manager (aktuell gren)*


Den här versionen av Windows Defender eller Endpoint Protection innehåller följande funktioner som hjälper dig att skydda din dator mot hot:  

-   **Integrering med Windows-brandväggen.** Konfigurationen av Endpoint Protection gör det möjligt att aktivera eller inaktivera Windows-brandväggen.  
-   **kontrollsystem för nätverk.** Den här funktionen förbättrar realtidsskyddet genom att kontrollera nätverkstrafiken och proaktivt bidra till att blockera utnyttjande av kända nätverksbaserade säkerhetsrisker.  
-   **Skydds motor.** Real tids skyddet hittar och stoppar skadlig kod från att installeras eller köras på datorn. Den uppdaterade motorn erbjuder förbättrade identifierings- och rensningsfunktioner med bättre prestanda.  

Windows Defender ingår i operativ systemet Windows 10.  I tidigare versioner av Windows kan administratören tillhandahålla antingen Windows Defender eller Endpoint Protection med hjälp av hanterings program.

Du hittar också en lista över [vanliga frågor och svar om Windows Defender och Endpoint Protection](endpoint-protection-client-faq.md). Information om fel sökning finns i [Felsöka Windows Defender eller Endpoint Protection-klienten](troubleshoot-endpoint-client.md). En lista över nya funktioner finns i [Vad är nytt i Windows Defender-klienten](https://support.microsoft.com/help/29276/windows-10-whats-new-in-windows-defender).

## <a name="windows-firewall-integration"></a>Integrering med Windows-brandväggen  
 Windows-brandväggen kan förhindra attacker och motverka att skadlig programvara får åtkomst till datorn via Internet eller ett nätverk. Nu när du installerar Endpoint Protection verifierar guiden att Windows-brandväggen är aktiverad. Om du avsiktligt har inaktiverat Windows-brandväggen kan du undvika att aktivera den genom att avmarkera en kryssruta. Du kan ändra inställningarna för Windows-brandväggen när som helst via system- och säkerhetsinställningarna på Kontrollpanelen.  

## <a name="network-inspection-system"></a>Kontrollsystem för nätverk  
 Angripare genomför i allt högre grad nätverksbaserade attacker mot utsatta säkerhetspunkter innan programvaruleverantörerna hinner utveckla och distribuera säkerhetsuppdateringar. Studier av utsatta säkerhetspunkter visar att det kan ta en månad eller längre från det att en inledande attackrapport görs tills att en lämplig säkerhetsuppdatering utvecklas, testas och släpps. Detta tidsglapp gör att många datorer är sårbara för attacker och utnyttjande under mycket lång tid. Kontrollsystem för nätverk i kombination med realtidsskydd bidrar till att bättre skydda dig mot nätverksbaserade attacker genom att avsevärt minska tiden från det att säkerhetsrisken upptäcks till att distributionen uppdateras – från veckor till några timmar.  

## <a name="award-winning-protection-engine"></a>Prisbelönt skyddsmotor  
 Under Windows Defender eller Endpoint Protection är den prisbelönta skydds motorn som uppdateras regelbundet. Bakom motorn står en grupp antivirusforskare från Microsoft Malware Protection Center, som arbetar med att hitta lösningar på de senaste hoten med skadlig kod 24 timmar om dygnet.  

## <a name="windows-defender-settings"></a>Inställningar för Windows Defender
Windows Defender-inställningar aktiverar inställningar som skyddar datorn från skadlig program vara. Din administratör kan hantera vissa Windows Defender-inställningar åt dig. Du kan hantera andra med hjälp av Windows Defender-inställningarna. Vi rekommenderar att du aktiverar Windows Defender-inställningar för att skydda din dator och dina data.

Om du vill visa Windows Defender-inställningar `Windows Defender` söker du efter på din dator. Öppna **Windows Defender** och välj **Inställningar**. Windows Defender-inställningar omfattar:
- **Real tids skydd** – hitta och stoppa skadlig kod från att installeras eller köras på datorn.
- **Molnbaserad skydd** – Windows Defender skickar information till Microsoft om möjliga säkerhetshot.
- **Automatisk exempel sändning** – Tillåt att Windows Defender skickar exempel på misstänkta filer till Microsoft för att förbättra identifieringen av skadlig kod.
- **Undantag** – du kan Uteslut vissa filer, mappar, fil namns tillägg eller processer från Windows Defender-genomsökning.
- **Förbättrat meddelande** – aktiverar meddelanden som informerar om datorns hälso tillstånd. Du **får** även viktiga aviseringar.
- **Windows Defender Offline** – du kan köra Windows Defender Offline för att hitta och ta bort skadlig program vara. Den här genomsökningen startar om datorn och tar cirka 15 minuter.

### <a name="see-also"></a>Se även  
 [Vanliga frågor och svar om Endpoint Protection klient](endpoint-protection-client-faq.md)   
 [Felsöka Windows Defender eller Endpoint Protection-klient](troubleshoot-endpoint-client.md)
