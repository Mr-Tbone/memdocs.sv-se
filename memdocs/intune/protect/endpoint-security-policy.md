---
title: Hantera Endpoint Security-policyer i Microsoft Intune | Microsoft Docs
description: Lär dig hur säkerhetsadministratörer kan använda policyer och profiler för Endpoint Security som fokuserar på enheternas säkerhetskonfiguration i Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 071cab69b652193b835282603e187e4f3d0c7b0d
ms.sourcegitcommit: 97f150f8ba8be8746aa32ebc9b909bb47e22121c
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879719"
---
# <a name="manage-device-security-with-endpoint-security-policies-in-microsoft-intune"></a>Hantera enhetssäkerhet med Endpoint Security-policyer i Microsoft Intune

Som säkerhetsadministratör kan du använda säkerhetspolicyer från *Slutpunktssäkerhet* i Intune till att konfigurera enhetssäkerhet utan att behöva navigera bland de många fler inställningarna i enhetskonfigurationsprofiler och säkerhetsbaslinjer.

Varje policytyp har stöd för en eller flera profiler. Det är i profilerna du konfigurerar inställningar och kan gruppera inställningar för olika plattformar, eller för olika fokusområden i det större policyområdet.

Du hittar de här policyerna under *Hantera* i noden **Slutpunktssäkerhet** i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

![Hantera principer](./media/endpoint-security-policy/endpoint-security-policies.png)

Nedan ges en kort beskrivning av de olika typerna av Endpoint Security-policyer. Om du vill veta mer om dem, bland annat vilka profiler som är tillgängliga för var och en, följer du länkarna till innehållet om respektive typ av policy:

- [Antivirus](../protect/endpoint-security-antivirus-policy.md) – policyn Antivirus hjälper säkerhetsadministratörer att fokusera på att hantera olika grupper av antivirusinställningar för hanterade enheter. Om du vill använda en antiviruspolicy ska du integrera Intune med Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) som en Mobile Threat Defense-lösning.

- [Diskkryptering](../protect/endpoint-security-disk-encryption-policy.md) – diskkrypteringsprofilerna för Endpoint Security fokuserar bara på de inställningar som är relevanta för enheters inbyggda krypteringsmetod, som FileVault eller BitLocker. Det här gör att säkerhetsadministratörer enklare kan hantera diskkrypteringsinställningar utan att behöva navigera bland en massa irrelevanta inställningar.

- [Brandvägg](../protect/endpoint-security-firewall-policy.md) – använd Endpoint Security-policyn Brandvägg i Intune till att konfigurera den inbyggda brandväggen för enheter som kör macOS och Windows 10. 

- [Slutpunktsidentifiering och svar](../protect/endpoint-security-edr-policy.md) – när du integrerar Microsoft Defender ATP med Intune kan du använda Endpoint Security-policyn EDR (slutpunktsidentifiering och svar) till att hantera EDR-inställningarna och registrera enheter i Microsoft Defender ATP.

- [Minskning av attackytan](../protect/endpoint-security-asr-policy.md) – när du använder Defender Antivirus på dina Windows 10-enheter kan du använda Intunes Endpoint Security-policy Minskning av attackytan till att hantera de här inställningarna på dina enheter.

- [Kontoskydd](../protect/endpoint-security-account-protection-policy.md) - policyn Kontoskydd hjälper dig att skydda användarnas identitet och konton. Kontoskyddspolicyns fokus är inställningar för Windows Hello och Credential Guard som ingår i Windows hantering av identiteter och åtkomst.

Följande avsnitt gäller för alla Endpoint Security-policyer.

## <a name="create-an-endpoint-security-policy"></a>Skapa en Endpoint Security-policy

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Slutpunktssäkerhet**, välj den typ av policy du vill konfigurera och välj sedan **Skapa policy**. Välj bland följande typer av policyer:
   - Antivirus
   - Diskkryptering
   - Brandvägg
   - Slutpunktsidentifiering och svar
   - Minska attackytan
   - Kontoskydd

3. Ange följande egenskaper:
   - **Plattform**: Välj den plattform du skapar policyn för. Vilka alternativ som är tillgängliga beror på vilken policytyp du valde:
     - macOS
     - Windows 10 och senare
   - **Profil**: Välj bland de tillgängliga profilerna för den plattform du har valt. Information om profilerna finns i avsnittet om den valda policytypen i den här artikeln.

4. Välj **Skapa**.

5. På sidan **Grundläggande inställningar** anger du ett namn och en beskrivning för profilen. Välj sedan **Nästa**.

6. På sidan **Konfigurationsinställningar** expanderar du varje inställningsgrupp och konfigurerar de inställningar du vill hantera med den här profilen.

   När du har konfigurerat inställningarna väljer du **Nästa**.

7. På sidan **Omfångstaggar** väljer du **Välj omfångstaggar** för att öppna fönstret *Välj taggar* där du kan tilldela omfångstaggar till profilen.
  
   Fortsätt genom att välja **Nästa**.

8. På sidan **Tilldelningar** väljer du de grupper som profilen ska tillämpas på. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](../configuration/device-profile-assign.md).

   Välj **Nästa**.

9. Välj **Skapa**på sidan **Granska + skapa** när du är klar. Den nya profilen visas i listan när du väljer policytypen för den profil du har skapat.

## <a name="duplicate-a-policy"></a>Kopiera en policy

Du kan skapa en kopia av en ursprunglig Endpoint Security-policy. Ett scenario när det är praktiskt att kopiera en princip är om du behöver tilldela liknande policyer till olika grupper men inte vill behöva återskapa hela policyn manuellt. I stället kan du kopiera den ursprungliga policyn och sedan bara införa de ändringar som krävs för den nya policyn. Du kanske bara ändrar en viss inställning och den grupp som policyn hör till.

När du skapar en kopia ger du den ett nytt namn. Kopian skapas med samma inställningskonfiguration och omfångstaggar som originalet, men har inga tilldelningar. Du måste redigera den nya policyn senare och skapa tilldelningar.  

Följande policytyper har stöd för kopiering:

- Antivirus
- Diskkryptering
- Brandvägg
- Slutpunktsidentifiering och svar
- Minska attackytan
- Kontoskydd

När du har skapat den nya policyn granskar och redigerar du den för att göra ändringar i konfigurationen.

### <a name="to-duplicate-a-policy"></a>Kopiera en policy

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj den policy du vill kopiera. Välj sedan **Duplicera** eller välj ellipsen ( **...** ) till höger om policyn och välj **Duplicera**.
3. Ange ett **Nytt namn** för policyn och välj sedan **Spara**.

### <a name="to-edit-a-policy"></a>Redigera en policy

1. Välj den nya policyn och välj sedan **Egenskaper**.
2. Välj Inställningar för att expandera en lista med policyns konfigurationsinställningar. Du kan inte ändra inställningarna från den här vyn, men du kan granska hur de är konfigurerade.
3. Om du vill ändra policyn väljer du **Redigera** för varje kategori där du vill göra ändringar:
   - Grunderna
   - Tilldelningar
   - Omfångstaggar
   - Konfigurationsinställningar
4. När du har gjort dina ändringar väljer du **Spara** för att spara ändringarna.  Du måste spara ändringar i en kategori innan du kan införa nya ändringar i andra kategorier.

## <a name="manage-conflicts"></a>Hantera konflikter

Många av de enhetsinställningar du kan hantera med Endpoint Security-policyer (säkerhetspolicyer) kan du hantera via andra policytyper i Intune. De här andra policytyperna är bland annat *enhetskonfigurationer* och *säkerhetsbaslinjer*. Eftersom du kan hantera en inställning med flera olika policytyper eller flera instanser av samma policytyp måste du vara beredd på att identifiera och lösa policykonflikter om en enhet inte följer den konfiguration du förväntar dig.

- Säkerhetsbaslinjer kan ange ett annat värde än standardvärdet för en inställning i syfte att uppfylla den rekommenderade konfigurationen som baslinjen gäller.
- Andra policytyper, som Endpoint Security-policyer, anger som standard värdet *Inte konfigurerat*. För de här andra policytyperna måste du uttryckligen konfigurera inställningarna i policyn.

Oavsett vilken metod som används för policyn kan det uppstå konflikter när du hanterar samma inställning på samma enhet via olika policytyper, eller via flera instanser av samma policytyp, och det här bör undvikas.

Informationen på följande länkar kan vara till hjälp när du ska identifiera och lösa konflikter:

- [Felsöka principer och profiler i Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Övervaka dina säkerhetsbaslinjer](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>Nästa steg

[Hantera slutpunktssäkerhet i Intune](../protect/endpoint-security.md)
