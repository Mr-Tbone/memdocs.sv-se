---
title: Använda Intune för att åtgärda sårbarheter som upptäckts av Microsoft Defender ATP – Azure | Microsoft Docs
description: Se hur man hanterar säkerhetsuppgifter från Threat & Vulnerability Management, en del av Microsoft Defender Advanced Threat Protection (ATP), från Intune-konsolen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/06/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a1d410da2cbedb9bcd2418fac1ddb783529ee8c6
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262599"
---
# <a name="use-intune-to-remediate-vulnerabilities-identified-by-microsoft-defender-atp"></a>Använda Intune för att åtgärda sårbarheter som upptäckts av Microsoft Defender ATP

När du integrerar Intune med Microsoft Defender Advanced Threat Protection (ATP) kan du dra nytta av ATP:s Threat & Vulnerability Management (TVM) och använda Intune för att åtgärda sårbarheter i slutpunkterna som har upptäckts av TVM. Den här integreringen ger en riskbaserad metod för identifiering och prioritering av sårbarheter som kan förbättra svarstiden för åtgärder i din miljö.

[Threat & Vulnerability Management](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/next-gen-threat-and-vuln-mgt) är en del av [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/windows-defender-advanced-threat-protection).

## <a name="how-integration-works"></a>Så här fungerar integreringen

När du ansluter Intune till Microsoft Defender Advanced Threat Protection får ATP information om hot och säkerhetsrisker från hanterade enheter.

På Microsoft Defender Security Center-konsolen får ATP-säkerhetsadministratörer granska data om sårbarheter i slutpunkter. Administratörerna kan sedan med ett enda musklick skapa säkerhetsuppgifter som flaggar sårbara enheter för reparation. Säkerhetsuppgifterna skickas direkt till Intune-konsolen där Intune-administratörer kan se dem. Säkerhetsuppgiften anger typen av säkerhetsrisk, prioritet, status och vilka åtgärder som måste vidtas för att åtgärda säkerhetsrisken. Intune-administratören väljer att godkänna eller avvisa uppgiften.

När en uppgift accepteras arbetar sedan Intune-administratören för att åtgärda säkerhetsrisken genom Intune med hjälp av riktlinjer som tillhandahålls som en del av säkerhetsuppgiften.

Vanliga åtgärder är:

- **Blockera** ett program från att köras
- **Distribuera** en operativsystemuppdatering för att minska säkerhetsrisken.
- **Ändra**  ett registervärde.
- **Inaktivera** eller **aktivera** en konfiguration för att påverka säkerhetsrisken.
- Aviseringen **Kräver uppmärksamhet** informerar administratören om hotet när det inte finns någon lämplig rekommendation att tillhandahålla.

Ett exempel på ett arbetsflöde:

- Inom Microsoft Defender ATP upptäcks en säkerhetsrisk för en app med namnet Contoso Media Player v4 och en administratör skapar en säkerhetsåtgärd för att uppdatera appen. Contoso Media Player är en ohanterad app som distribuerades med Intune.

  Den här säkerhetsuppgiften visas i Intune-konsolen med statusen Väntar:

  ![Visa listan över säkerhetsuppgifter i Intune-konsolen](./media/atp-manage-vulnerabilities/temp-security-tasks.png)

- Intune-administratören väljer en säkerhetsuppgift att visa detaljer om den åtgärden.  Administratören väljer sedan **Acceptera**, vilket uppdaterar statusen i Intune och i ATP till *Accepterad*.

  ![Godkänna eller avvisa en säkerhetsuppgift](./media/atp-manage-vulnerabilities/temp-accept-task.png)

- Administratören utför sedan åtgärden baserat på vägledningen som tillhandahålls. Vägledningen varierar beroende på vilken typ av åtgärd som behövs. När det är tillgängligt innehåller åtgärdsvägledningen länkar till relevanta fönster för konfigurationer i Intune.

  Eftersom mediaspelaren i det här exemplet inte är en hanterad app kan Intune endast ge textinstruktioner. Om appen hade varit hanterad kunde Intune ha gett anvisningar för att hämta en uppdaterad version och visat en länk för att öppna distributionen för appen, så att de uppdaterade filerna kan läggas till i distributionen.

- När åtgärden har slutförts öppnar Intune-administratören säkerhetsuppgiften och väljer **Slutför uppgift**.  Status för åtgärden uppdateras för Intune och i ATP, där säkerhetsadministratörer bekräftar den ändrade statusen för säkerhetsrisken.

## <a name="prerequisites"></a>Krav  

**Prenumerationer**:

- Microsoft Intune  
- Microsoft Defender Advanced Threat Protection ([Registrera dig för en kostnadsfri utvärderingsversion](https://www.microsoft.com/WindowsForBusiness/windows-atp?ocid=docs-wdatp-main-abovefoldlink).)

**Intune-konfigurationer för ATP**:

- Konfigurera en tjänst-till-tjänst-anslutning med Microsoft Defender ATP.
- Distribuera en princip för enhetskonfiguration med profiltypen **Microsoft Defender ATP (Windows 10 Desktop)** till enheter med risk som utvärderas av ATP.

  Information om hur du ställer in Intune för att arbeta med ATP finns i [Tvinga fram kompatibilitet för Microsoft Defender ATP med villkorlig åtkomst i Intune](advanced-threat-protection-configure.md#enable-microsoft-defender-atp-in-intune).

## <a name="work-with-security-tasks"></a>Arbeta med säkerhetsuppgifter

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Slutpunktssäkerhet** > **Säkerhetsaktiviteter**.

3. Markera en aktivitet i listan för att öppna ett resursfönster som visar ytterligare information för den säkerhetsuppgiften.

   När du visar resursfönstret för säkerhetsuppgiften kan du välja ytterligare länkar:

   - HANTERADE APPAR – Visa den app som är sårbar. När det gäller sårbarheten för flera appar visas en filtrerad lista över appar.
   - ENHETER – Visa en lista över *Sårbara enheter*, från vilken du kan länka till en post med mer information för sårbarhetsbedömning på den enheten.
   - BEGÄRANDE – Använd länken för att skicka e-post till den administratör som skickade den här säkerhetsuppgiften.
   - INFORMATION – Läs anpassade meddelanden som skickas av förfrågaren när du öppnar säkerhetsuppgiften.

4. Välj **Godkänn** eller **Avvisa** för att skicka ett meddelande till ATP om din planerade åtgärd. När du godkänner eller avvisar en uppgift kan du skicka information som vidarebefordras till ATP.

5. När du har godkänt en uppgift ska du öppna säkerhetsuppgiften igen (om den är stängd) och följa anvisningarna för att åtgärda sårbarheten. Anvisningarna från ATP informationen om säkerhetsuppgiften varierar beroende på vilken typ av sårbarhet det gäller.

   När det är möjligt innehåller åtgärdsanvisningarna länkar till de relevanta konfigurationsobjekten i Intune-konsolen.

6. När du har slutfört åtgärdsanvisningarna ska du öppna säkerhetsuppgiften och välja **Slutför uppgift**.  Den här åtgärden uppdaterar säkerhetsuppgiftens status i både Intune och ATP.

När åtgärden har genomförts kan riskexponeringsbedömningen i ATP minska baserat på ny information från de åtgärdade enheterna.

## <a name="next-steps"></a>Nästa steg

Läs mer om Intune och [Microsoft Defender ATP](advanced-threat-protection.md).

Titta närmare på Intune [Mobile Threat Defense](mobile-threat-defense.md).

Titta närmare på [Threat & Vulnerability Management-instrumentpanelen](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/tvm-dashboard-insights) i Microsoft Defender ATP.
