---
title: Villkorlig åtkomst med samhantering
titleSuffix: Configuration Manager
description: Kontrol lera användarnas åtkomst till organisations resurser baserat på regler för efterlevnad från Intune
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f5b9addd35dd3e9252c1b988de4bb006e9a5bc0d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694975"
---
# <a name="conditional-access-with-co-management"></a>Villkorlig åtkomst med samhantering

Villkorlig åtkomst säkerställer att endast betrodda användare får åtkomst till organisations resurser på betrodda enheter med hjälp av betrodda appar. Den är byggd från grunden i molnet. Oavsett om du hanterar enheter med Intune eller utökar din Configuration Manager-distribution med samhantering fungerar det på samma sätt.

I följande videoklipp är Senior program hanterare Joey Glocke och Ainley för produkt marknadsförings chef att diskutera och Visa villkorlig åtkomst med samhantering:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

Med samhantering utvärderar Intune varje enhet i nätverket för att fastställa hur tillförlitlig den är. Den här utvärderingen sker på följande två sätt:

1. Intune kontrollerar att en enhet eller app hanteras och konfigureras på ett säkert sätt. Den här kontrollen beror på hur du ställer in organisationens efterlevnadsprinciper. Kontrol lera till exempel att alla enheter har kryptering aktiverat och inte är jailbrokade.  

    - Den här utvärderingen är för säkerhets brott och konfigurations baserad  

    - För samhanterade enheter Configuration Manager även konfigurations baserad utvärdering. Till exempel, nödvändiga uppdateringar eller appar uppfyller kraven. Intune kombinerar den här utvärderingen tillsammans med sin egen utvärdering.  

2. Intune identifierar aktiva säkerhets incidenter på en enhet. Den använder intelligent säkerhet för [Microsoft Defender Avancerat skydd](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (tidigare Windows Defender ATP) och andra leverantörer av [skydd mot mobila hot](https://www.lookout.com/about/partners/microsoft). Dessa partner kör pågående beteende analyser på enheter. Den här analysen identifierar aktiva incidenter och skickar sedan den här informationen till Intune för utvärdering av kompatibilitet i real tid.  

    - Den här utvärderingen är ett brott mot säkerhets överträdelse och incident-baserad  

Microsoft corporate vice president Bengt Anderson diskuterar villkorlig åtkomst i djupet med direktsända demonstrationer under självtändningen 2018-presentationen. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

Med villkorlig åtkomst får du också en central plats för att se hälso tillståndet för alla nätverks anslutna enheter. Du får fördelarna med moln skala, vilket är särskilt värdefullt för testning Configuration Manager produktions instanser.


## <a name="benefits"></a>Fördelar

Varje IT-team är Obsessed med nätverks säkerhet. Det är obligatoriskt att se till att alla enheter uppfyller dina säkerhets-och affärs krav innan du får åtkomst till nätverket. Med villkorlig åtkomst kan du fastställa följande faktorer: 
- Om varje enhet är krypterad  
- Om skadlig kod har installerats  
- Om inställningarna uppdateras  
- Om den är jailbrokade eller rotad  

Villkorlig åtkomst kombinerar detaljerad kontroll över organisations data med en användar upplevelse som maximerar arbets produktiviteten på alla enheter var som helst.

Följande video visar hur [Advanced Thread Protection](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) är integrerat i vanliga scenarier som du regelbundet upplever:

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

Med samhantering kan Intune införliva Configuration Managers ansvar för att utvärdera dina säkerhets standarders kompatibilitet för nödvändiga uppdateringar eller appar. Det här beteendet är viktigt för alla IT-organisationer som vill fortsätta använda Configuration Manager för komplex hantering av appar och korrigeringar.

Villkorlig åtkomst är också en viktig del av att utveckla din nätverks arkitektur med [inget förtroende](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/) . Med villkorlig åtkomst behandlar kompatibla enhets åtkomst kontroller de grundläggande lagren i nätverket med förtroende för noll. Den här funktionen är en stor del av hur du skyddar din organisation i framtiden.

Mer information finns i blogg inlägget om att [förbättra villkorlig åtkomst med dator risk data från Microsoft Defender Avancerat skydd](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559).



## <a name="case-studies"></a>Fallstudier

Wipro för IT-konsultering använder villkorlig åtkomst för att skydda och hantera de enheter som används av alla 91 000-anställda. I en ny fallstudie, anges vice president på Wipro:

> *Att uppnå villkorlig åtkomst är en stor chans för Wipro. Nu har alla anställda mobil åtkomst till information på begäran.* 
>  *Vi har förbättrat vår säkerhets position och produktivitet för anställda. Nu 91 000 anställda drar nytta av hög säker åtkomst till mer än 100 appar från vilken enhet som helst, var som helst.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Andra exempel är: 

- Nestlé, som använder app-baserad villkorlig åtkomst för över 150 000 anställda  

- Automation Software-företaget takt, som nu kan se till att "endast hanterade enheter har åtkomst till Microsoft 365 appar som team och företagets intranät." De kan också erbjuda sin personal "säkrare åtkomst till andra molnbaserade appar, till exempel Workday och Salesforce." Mer information om takt-upplevelsen med Intune finns i [takt ökar affärs takten med verktyg för mobil samarbete i Microsoft 365](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365).

Intune är också fullständigt integrerat med partners som Cisco ISE, Aruba Clear pass och Citrix NetScaler. Med dessa partner kan du upprätthålla åtkomst kontroller baserat på Intune-registreringen och enhetens kompatibilitetstillstånd på dessa plattformar.

Mer information finns i följande videor:
- [Bengt Anderson-demonstrationer villkorlig åtkomst i detalj](https://youtu.be/8321obNofgM?t=547)  
- [Ytterligare information från slut punkts zon 1805](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>Värde förslag

Med villkorlig åtkomst och ATP-integrering är du fortifying en grundläggande komponent i varje IT-organisation: säker åtkomst till molnet.

I mer än 63% av alla data överträdelser får angriparna åtkomst till organisationens nätverk genom svaga, standardiserade eller stulna användarautentiseringsuppgifter. Eftersom villkorlig åtkomst fokuserar på att skydda användar identiteten begränsar den stöld av autentiseringsuppgifter. Villkorlig åtkomst hanterar och skyddar dina identiteter, oavsett om de är privilegierade eller icke-privilegierade. Det finns inget bättre sätt att skydda enheterna och data på dem.

Eftersom villkorlig åtkomst är en kärn komponent i Enterprise Mobility + Security (EMS) krävs ingen lokal installation eller arkitektur. Med Intune och Azure Active Directory (Azure AD) kan du snabbt konfigurera villkorlig åtkomst i molnet. Om du för närvarande använder Configuration Manager kan du enkelt utöka din miljö till molnet med samhantering och börja använda det just nu.

Mer information om ATP-integrering finns i det här blogg inlägget [Microsoft Defender ATP-enhets risk Poäng exponerar nya cyberattack, enheter villkorlig åtkomst för att skydda nätverk](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/). Den beskriver hur en erfaren erfaren hackare som aldrig använts innan de såg några verktyg. Microsoft-molnet upptäckte och stoppade dem eftersom de riktade användarna hade villkorlig åtkomst. Intrånget aktiverade enhetens riskfyllda princip för villkorlig åtkomst. Även om angriparen redan har upprättat en fäste i nätverket begränsades de utnyttjade datorerna automatiskt från åtkomst till organisations tjänster och data som hanteras av Azure AD.



## <a name="configure"></a>Konfigurera

Villkorlig åtkomst är enkelt att använda när du [aktiverar samhantering](how-to-enable.md). Det kräver att arbets belastningen för **efterlevnadsprinciper** flyttas till Intune. Mer information finns i [så här växlar du Configuration Manager-arbetsbelastningar till Intune](how-to-switch-workloads.md). 

Mer information om hur du använder villkorlig åtkomst finns i följande artiklar: 

- [Villkorlig åtkomst för Azure AD](/azure/active-directory/conditional-access/overview)  

- [Efterlevnadsprinciper för Intune-enheter](/intune/device-compliance)  

- [Appbaserad villkorlig åtkomst med Intune](/intune/app-based-conditional-access-intune)  

> [!Note]  
> Villkorliga åtkomst funktioner blir tillgängliga omedelbart för Hybrid Azure AD-anslutna enheter. Dessa funktioner omfattar Multi-Factor Authentication och hybrid Azure AD Join Access Control. Detta beror på att de är baserade på Azure AD-egenskaper. Aktivera samhantering för att utnyttja den konfigurations utvärderingen från Intune och Configuration Manager. Med den här konfigurationen får du åtkomst kontroll direkt från Intune för kompatibla enheter. Det ger dig också Intunes utvärderings funktion för efterlevnadsprinciper.