---
title: Vanliga sätt att använda Microsoft Intune
description: Läs mer om sex av de vanligaste uppgifterna som Microsoft Intune kan hjälpa dig att hantera.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 11/29/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1f37d4ff-b5a7-4a89-8884-a6184908b09c
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: f2244f484b44673454b1bbb6ba6286c253021517
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079271"
---
# <a name="common-ways-to-use-microsoft-intune"></a>Vanliga sätt att använda Microsoft Intune

Innan du ger dig in på implementeringsåtgärder, är det viktigt att samla företagets intressenter för Enterprise Mobility kring affärsmålen att använda Intune. Intressentanpassningen är viktig, oavsett om ni precis har börjat med Enterprise Mobility eller om ni migrerar från en annan produkt.  

Behovet av företagsmobilitet utvecklas dynamiskt och Microsofts metoder för att möta dem skiljer sig ibland från andra lösningar på marknaden. Det bästa sättet att sätta affärsmål är att formulera dem utifrån de scenarier som du vill möjliggöra för anställda, partner och IT-avdelningen.  

Nedan följer korta introduktioner till de sex vanligaste scenarierna som förlitar sig på Intune, tillsammans med länkar till mer information om hur du planerar och distribuerar respektive scenario.

>[!NOTE]
>Vill du veta hur Microsofts IT-avdelning använder Intune för ge åtkomst till företagsresurser på mobila enheter, samtidigt som företagets data skyddas? [Läs denna tekniska fallstudie](https://www.microsoft.com/itshowcase/Article/Content/588) för att få reda på hur Microsoft IT använder Intune och andra tjänster för att hantera identitet, enheter, appar och data.  

>[!IMPORTANT]
>Vi vill säkerställa att mobila enheter är uppdaterade med hänsyn till de senaste ”Trident”-attackerna på iOS/iPadOS-enheter. Därför har vi publicerat blogginlägget [Kontrollera att mobila enheter är uppdaterade med hjälp av Microsoft Intune](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/26/ensuring-mobile-devices-are-up-to-date-using-microsoft-intune/). Här hittar du information om hur Intune kan hjälpa dig att hålla dina enheter skyddade och uppdaterade.

## <a name="protecting-your-on-premises-email-and-data-so-it-can-be-safely-accessed-by-mobile-devices"></a>Skydda lokal e-post och lokala data så att det går att komma åt dem på ett säkert sätt från mobila enheter

De flesta Enterprise Mobility-strategier börjar med en plan för att möjliggöra säker åtkomst till e-post för anställda med mobila enheter som ansluter till Internet. Många organisationer har fortfarande lokala data och programservrar, t.ex. Microsoft Exchange, som finns i företagets nätverk.

Intune och Microsoft Enterprise Mobility + Security (EMS) tillhandahåller en unik integrerad [lösning för villkorlig åtkomst](../protect/conditional-access.md) för Exchange Server, som ser till att ingen mobilapp kan komma åt e-post förrän enheten har registrerats med Intune. Du kan implementera den här typen av e-poståtkomst utan att distribuera ytterligare en gatewaydator till företagets nätverksgräns.

Med Intune kan du också aktivera åtkomst till mobilappar som kräver säker åtkomst till lokala data, t.ex. servrar för affärsappar. Den här typen av åtkomst görs normalt med [Intune-hanterade certifikat](../protect/certificates-configure.md) för åtkomstkontroll som kombineras med en VPN-gateway eller proxy av standardtyp i perimeternätverket, t.ex. Microsoft Azure Active Directory-programproxy.

I dessa fall är det enda sättet att komma åt företagets data att registrera enheten i hanteringen. När enheterna har registrerats kontrollerar hanteringssystemet att de är kompatibla med dina principer innan de kan komma åt företagsdata. Dessutom kan Intunes [programhanteringsverktyg och App SDK](../developer/apps-prepare-mobile-application-management.md) användas för att hålla kvar data i den verksamhetsspecifika appen, så att det inte går att vidareföra företagsdata till konsumentappar eller konsumenttjänster.

<!-- Learn more about how to plan and deploy Intune to help secure on-premises email and data. -->

## <a name="protecting-your-office-365-email-and-data-so-it-can-be-safely-accessed-by-mobile-devices"></a>Skydda e-post och data i Office 365 så att det går att komma åt dem på ett säkert sätt från mobila enheter

Det kan inte bli enklare för dig eller smidigare för användarna att skydda företagets data i Office 365 (e-post, dokument, snabbmeddelanden, kontakter).

Intune och Microsoft Enterprise Mobility + Security ger en unikt integrerad lösning för villkorlig åtkomst som säkerställer att inga användare, appar eller enheter kan få åtkomst till Office 365-data om de inte uppfyller företagets efterlevnadskrav (genomförd [multifaktorautentisering](../enrollment/multi-factor-authentication.md), registrering med Intune, använder hanterad app, OS-version som stöds, PIN-kod för enhet, profil med låg användarrisk osv.).

Office-mobilapparna i deras respektive appbutiker är redo att användas med datainneslutningsprinciper som du kan konfigurera via Intune. Det gör att du kan förhindra att data delas med appar (t.ex. med interna e-postappar) och lagringsplatser (t.ex. Dropbox) som inte hanteras av IT. Alla dessa funktioner är inbyggda i Office 365 och EMS. Du behöver inte distribuera ytterligare infrastruktur för att dra nytta av detta mervärde.

En vanlig Office 365-distributionsmetod är att kräva att enheterna registreras för hantering om de måste vara helt konfigurerade med företagsappar, certifikat, Wi-Fi eller VPN-konfigurationer, som är ett vanligt scenario för företagsägda enheter.  

Om användaren bara behöver åtkomst till företagets e-post och dokument, vilket ofta är fallet med personligt ägda enheter, kan du kräva att användaren använder Office-mobilapparna (där du har tillämpat [appskyddsprinciper](../apps/app-protection-policies.md). Då behöver inte enheten registreras.  

Vilken metod som än används skyddas Office 365-data av principer som du har definierat.

<!-- Learn more about how to plan and deploy Intune to help secure Office 365 email and data. -->

## <a name="offer-a-bring-your-own-device-program-to-all-employees"></a>Erbjuder ett BYOD-program (”Bring Your Own Device”) för alla anställda

BYOD blir allt populärare hos organisationer som ett sätt att minska maskinvaruutgifterna eller öka medarbetarnas valmöjligheter för mobil produktivitet. I princip alla har en egen telefon idag så varför ska de behöva en till att bära på? Den främsta utmaningen har alltid varit att övertyga medarbetarna att registrera sina personliga enheter i hantering, eftersom de är oroliga för vad IT-avdelningen kommer att kunna se och göra med enheten.  

Om enhetsregistrering inte är ett genomförbart alternativ erbjuder Intune en alternativ BYOD-metod som innebär att helt enkelt [hantera de appar som innehåller företagsdata](../apps/app-protection-policies.md). Intune skyddar företagets data även om appen i fråga har åtkomst till både företagsrelaterade och personliga data, som är fallet för Office-mobilappar.  

Som administratör kan du kräva att användarna kommer åt Office 365 från Office-mobilapparna och konfigurera apparna med principer som ser till att data är skyddade (t.ex. kryptering, PIN-kod och så vidare). Dessa appskyddsprinciper förhindrar dataförlust från ohanterade appar och lagringsplatser – i eller utanför dessa appar. Principerna förhindrar till exempel att en användare kopierar text från en e-postprofil för företaget till en privat e-postprofil, även om båda profilerna är konfigurerade i Outlook Mobile. Liknande konfigurationer kan distribueras för andra tjänster och program som krävs av BYOD-användarna.

<!-- Learn more about how to plan and deploy Intune to support BYOD.-->

## <a name="issue-corporate-owned-phones-to-your-employees"></a>Dela ut företagsägda telefoner till anställda

I dag är många anställda mobila, vilket i konkurrensavseende gör det viktigt att kunna upprätthålla produktiviteten även på mobila enheter. Dessa medarbetare behöver smidig åtkomst till alla företagets appar och data, när som helst, var som helst. Du måste se till att företagets data är säkra och att de administrativa kostnaderna är låga.  

Intune erbjuder [massetablering och hanteringslösningar](../enrollment/device-enrollment.md) som är integrerade med de flesta stora enhetshanteringsplattformar som finns på marknaden i dag, inklusive Apples program för enhetsregistrering och mobilsäkerhetsplattformen Samsung Knox. Centraliserad redigering av enhetskonfigurationer med Intune gör att det i hög grad går att automatisera etableringen av företagsenheter.  

Tänk dig detta: ge en medarbetare en oöppnad låda med en iPhone. Medarbetaren aktiverar den och går igenom ett företagsanpassat konfigurationsflöde där användaren måste autentisera sig. iPhone konfigureras smidigt med [säkerhetsprinciper](../configuration/device-profiles.md).

Den anställda startar sedan Intune-företagsportalappen för att komma åt valfria företagsappar som är tillgängliga.

<!-- Learn more about how to plan and deploy Intune to support corporate owned devices. -->

## <a name="issue-limited-use-shared-tablets-to-your-employees"></a>Dela ut delade surfplattor med begränsad användning till anställda

Anställda utnyttjar i allt högre grad mobila tekniker. Exempelvis används delade surfplattor ofta av anställda inom detaljhandeln.  Oavsett om de används för att hantera en försäljning eller för att snabbt kontrollera lagret hjälper surfplattorna till att skapa positiva kundmöten.

Den enkla användarupplevelsen är avgörande i detta fall. Därför får anställda ofta surfplattor med begränsad användning, så att en enda verksamhetsspecifik app är allt de kan interagera med. Med Intune kan man massetablera, skydda och centralt hantera dessa delade [iOS- och Android](../configuration/device-profiles.md)-enheter, som kan konfigureras för att köras i detta läge med begränsad användning.

<!-- Learn more about how to plan and deploy Intune to support shared tablets. -->

## <a name="enable-your-employees-to-securely-access-office-365-from-an-unmanaged-public-kiosk"></a>Gör det möjligt för medarbetarna att på ett säkert sätt få åtkomst till Office 365 från en ej hanterad offentlig dator

Ibland behöver anställda använda enheter, appar eller webbläsare som du inte kan hantera, t.ex. offentliga datorer på mässor och hotell.

Ska du tillåta att medarbetarna får åtkomst till företagets e-post från dem? Med Intune och Microsoft Enterprise Mobility + Security kan du enkelt välja att ”inte” göra det, genom att [begränsa e-poståtkomsten till enheter som hanteras av din organisation](../protect/conditional-access.md). Detta säkerställer att en autentiserad anställd oavsiktligt lämnar företagsdata på den icke-betrodda datorn.
