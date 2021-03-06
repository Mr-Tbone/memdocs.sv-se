---
title: Använda säkerhetsbaslinjer i Microsoft Intune – Azure | Microsoft Docs
description: Använd rekommenderade säkerhetsinställningar för Windows för att skydda användare och data på enheter som använder Microsoft Intune till att hantera mobilenheter. Aktivera kryptering, konfigurera Microsoft Defender Advanced Threat Protection, styr Internet Explorer, ange lokala säkerhetsprinciper, kräv ett lösenord, blockera hämtningar från Internet och mycket mer.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
ms.custom:
- intune-azure
- contperfq1
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a3954057d14aaf24a1a0147d9717cfc01413d51
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914930"
---
# <a name="use-security-baselines-to-configure-windows-10-devices-in-intune"></a>Använd baslinjer för säkerhet för att konfigurera Windows 10-enheter i Intune

Använd säkerhetsbaslinjer i Intune för att säkra och skydda dina användare och enheter. Säkerhetsbaslinjer är förkonfigurerad grupper av Windows-inställningar som hjälper dig att tillämpa en känd grupp av inställningar och standardvärden som rekommenderas av relevanta säkerhetsteam. När du skapar en säkerhetsbaslinjeprofil i Intune skapar du en mall som består av flera profiler för *enhetskonfiguration*.

Den här funktionen gäller för:

- Windows 10 version 1809 och senare

Du distribuerar säkerhetsbaslinjer till grupper av användare eller enheter i Intune. Inställningarna tillämpas på enheter som kör Windows 10 eller senare. Till exempel aktiverar *MDM-säkerhetsbaslinjen* automatiskt BitLocker för flyttbara enheter, kräver automatiskt ett lösenord för att låsa upp en enhet, inaktiverar automatiskt grundläggande autentisering och mycket mer. När ett standardvärde inte fungerar för din miljö kan du anpassa baslinjen för att tillämpa dina önskade inställningar.

Separata typer av baslinje kan innehålla samma inställningar men använder olika standardvärden för dessa inställningar. Det är viktigt att förstå standardinställningarna för dina valda baslinjer och sedan ändra varje baslinje så att de passar din organisations behov.

> [!NOTE]
> Microsoft rekommenderar inte att du använder förhandsversioner av säkerhetsbaslinjer i en produktionsmiljö. Inställningarna för en förhandsversion av en baslinje kan förändras medan förhandsversionen används.

Säkerhetsbaslinjer kan hjälpa dig få ett säkert arbetsflöde från slutpunkt till slutpunkt när du arbetar med Microsoft 365. Några av fördelarna är:

- En säkerhetsbaslinje innehåller metodtips och rekommendationer för inställningar som påverkar säkerheten. Intune samarbetar med samma Windows-säkerhetsteam som skapar grupprincipernas säkerhetsbaslinjer. De här rekommendationerna baseras på vägledning och omfattande erfarenhet.
- Om Intune är nytt för dig och du inte är säker på var du ska börja, kan säkerhetsbaslinjerna vara till hjälp. Du kan snabbt skapa och distribuera en säker profil, där du vet att du hjälper till att skydda din organisations data och resurser.
- Om du använder en grupprincip är det mycket enklare att migrera till Intune för hantering med dessa baslinjer. Baslinjerna är inbyggda i Intune och innehåller moderna hanteringsfunktioner.

[Windows säkerhetsbaslinjer](/windows/security/threat-protection/windows-security-baselines) är en bra resurs om man vill lära sig mer om den här funktionen. [Hantering av mobilenheter](/windows/client-management/mdm/) är en bra resurs om du vill lära dig mer om MDM och vad du kan göra på Windows-enheter.

## <a name="available-security-baselines"></a>Tillgängliga säkerhetsbaslinjer

Följande instanser av säkerhetsbaslinjer är tillgängliga för användning med Intune. Använd länkarna om du vill visa inställningarna för den senaste instansen av varje baslinje.

- **MDM-säkerhetsbaslinje**
  - [MDM-säkerhetsbaslinje för maj 2019](security-baseline-settings-mdm-all.md?pivots=mdm-may-2019)
  - [Förhandsversion: MDM-säkerhetsbaslinje för oktober 2018](security-baseline-settings-mdm-all.md?pivots=mdm-preview)

- **Microsoft Defender ATP-baslinje**
   *(Denna baslinje kan användas när din miljö uppfyller förhandskraven för att använda [Microsoft Defender Advanced Threat Protection](advanced-threat-protection.md#prerequisites))* .
  - [Microsoft Defender ATP-baslinje för april 2020 – version 4](security-baseline-settings-defender-atp.md?pivots=atp-april-2020)
  - [Microsoft Defender ATP-baslinje för mars 2020 – version 3](security-baseline-settings-defender-atp.md?pivots=atp-march-2020)

  > [!NOTE]
  > Säkerhetsbaslinjen för Microsoft Defender ATP är optimerad för fysiska enheter och rekommenderas inte för användning på virtuella datorer (VM) eller VDI-slutpunkter. Vissa baslinjeinställningar kan påverka fjärranslutna interaktiva sessioner i virtualiserade miljöer.  Mer information finns i [Öka efterlevnaden med säkerhetsbaslinjen i Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) i Windows-dokumentationen.

- **Microsoft Edge-baslinje**
  - [Microsoft Edge-baslinje för april 2020 (Edge version 80 och senare)](security-baseline-settings-edge.md?pivots-edge-april-2020)
  - [Förhandsversion: Microsoft Edge-baslinje för oktober 2019 (Edge version 77 och senare)](security-baseline-settings-edge.md?pivots=edge-october-2019)

Du kan fortsätta att använda och redigera profiler som du har skapat tidigare baserat på en förhandsvisningsmall, till och med när förhandsversionerna inte längre är tillgängliga för att skapa nya profiler.

När du är redo att flytta till en senare version av en baslinje du använder kan du läsa i [Ändra baslinjeversionen för en profil](#change-the-baseline-version-for-a-profile) i den här artikeln. 

## <a name="about-baseline-versions-and-instances"></a>Om baslinjeversioner och instanser

Varje ny versioninstans av en baslinje kan lägga till eller ta bort inställningar eller göra andra ändringar. När nya inställningar för Windows 10 blir tillgängliga tillsammans med nya versioner av Windows 10 kan MDM-säkerhetsbaslinjen få en ny versioninstans som innehåller de senaste inställningarna.

I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) under **Slutpunktssäkerhet** > **Säkerhetsbaslinjer** visas en lista över tillgängliga baslinjer. Listan innehåller:
- namnet på baslinjemallen
- antalet profiler som använder baslinjetypen
- antalet separata instanser (versioner) av baslinjetypen som är tillgängliga
- datumet *Senaste publicering* som anger när den senaste versionen av baslinjemallen blev tillgänglig.

Om du vill visa mer information om de baslinjeversioner du använder väljer du en baslinjetyp som *MDM-säkerhetsbaslinje* för att öppna fönstret *Profiler* och väljer sedan **Versioner**. Intune visar information om versionerna av den baslinje som används av dina profiler. I informationen anges den senaste och aktuella baslinjeversionen. Du kan välja en version för att visa mer information om de profiler som använder den versionen.

Du kan välja att [ändra versionen](#change-the-baseline-version-for-a-profile) för en baslinje som används med en specifik profil. När du byter version behöver du inte skapa någon ny baslinjeprofil för att använda den uppdaterade versionen. I stället kan du välja en baslinjeprofil och sedan använda det inbyggda alternativet för att ändra instansversionen för profilen till en ny.

### <a name="compare-baseline-versions"></a>Jämför baslinjeversioner

I fönstret **Versioner** för en säkerhetsbaslinje finns en lista över alla versioner av baslinjen som du har distribuerat. Den här listan innehåller även den senaste och den aktiva versionen av baslinjen. När du skapar en ny *säkerhetsbaslinjeprofil* använder profilen den senaste versionen av säkerhetsbaslinjen.  Du kan fortsätta använda och redigera profiler som du har skapat tidigare som använder en tidigare version av baslinjen, inklusive baslinjer som har skapats i en förhandsversion.

Du kan se vad som har ändrats mellan olika versioner genom att markera kryssrutorna för två olika versioner och sedan välja **Jämför baslinjer**. Så uppmanas du att ladda ned en CSV-fil som innehåller information om skillnaderna.

Filen visar varje inställning i de två baslinjeversionerna och anger om de har ändrats (*notEqual*) eller inte (*equal*). Informationen innehåller även standardvärdet för inställningen efter version, samt anger om inställningen har *lagts till* för den senaste versionen eller *tagits bort* från den senaste versionen.

![Jämför baslinjer](./media/security-baselines/compare-baselines.png)

## <a name="avoid-conflicts"></a>Undvika konflikter

Du kan använda en eller flera av de tillgängliga baslinjerna i din Intune-miljö på samma gång. Du kan också använda flera instanser av samma säkerhetsbaslinjer med olika anpassningar.

När du använder flera säkerhetsbaslinjer, ska du granska inställningarna i var och en för att identifiera när dina olika baslinjekonfigurationer introducerar motstridiga värden för samma inställning. Eftersom du kan distribuera säkerhetsbaslinjer som är utformade för olika syften och distribuera flera instanser av samma baslinje som innehåller anpassade inställningar, kan det hända att du skapar konfigurationskonflikter för enheter som då måste undersökas och lösas.

Dessutom hanterar säkerhetsbaslinjer ofta samma inställningar som du kan ange med [profiler för enhetskonfiguration](../configuration/device-profiles.md) eller andra typer av principer. Du bör därför vara medveten om och ta hänsyn till dina ytterligare principer och profiler för inställningar när du försöker undvika eller lösa konflikter.

Använd informationen på följande länkar för att identifiera och lösa konflikter:

- [Felsöka principer och profiler i Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Övervaka dina säkerhetsbaslinjer](security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="manage-baselines"></a>Hantera baslinjer

Vanliga uppgifter när du arbetar med säkerhetsbaslinjer är:

- [Skapa en profil](#create-the-profile) – konfigurera de inställningar som du vill använda och tilldela baslinjen till grupper.
- [Ändra versionen](#change-the-baseline-version-for-a-profile) – ändra den baslinjeversion som används av en profil.
- [Ta bort en baslinjetilldelning](#remove-a-security-baseline-assignment) – lär dig vad som händer när du slutar hantera inställningar med en säkerhetsbaslinje.


### <a name="prerequisites"></a>Krav

- För att hantera baslinjer i Intune måste ditt konto ha den inbyggda rollen [Princip- och profilhanterare](../fundamentals/role-based-access-control.md#built-in-roles).

- Användningen av vissa baslinjer kräver att du har en aktiv prenumeration för ytterligare tjänster, till exempel Microsoft Defender ATP.

### <a name="create-the-profile"></a>Skapa profilen

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Slutpunktssäkerhet** > **Säkerhetsbaslinjer** för att visa listan med tillgängliga baslinjer.

   ![Välj en säkerhetsbaslinje att konfigurera](./media/security-baselines/available-baselines.png)

3. Välj den baslinje som du vill använda och välj sedan **Skapa profil**.

4. På fliken **Grundinställningar** anger du följande egenskaper:

   - **Namn**: Ange ett namn på säkerhetsbaslinjernas profil. Ange till exempel *Standardprofil för Defender ATP*.

   - **Beskrivning**: Ange text som beskriver vad baslinjen gör. Du kan ange vilken text du vill i beskrivningen. Det är valfritt men rekommenderat.

   Välj **nästa** för att gå till nästa flik. När du har fortsatt till en ny flik kan du välja fliknamnet för att återgå till en tidigare flik.

5. På inställningsfliken Konfiguration visas grupperna av **Inställningar** som är tillgängliga i den baslinje som du har valt. Du kan expandera en grupp om du vill visa inställningarna i gruppen och standardvärdena för dessa inställningar i baslinjen. Så här hittar du specifika inställningar:
   - Välj en grupp att expandera och granska de tillgängliga inställningarna.
   - Använd *Sökfältet* och ange nyckelord som filtrera för att visa endast de grupper som innehåller dina sökkriterier.

   Varje inställning i en baslinje har en standardkonfiguration för denna baslinjeversion. Konfigurera om standardinställningarna för att uppfylla dina affärsbehov. Olika baslinjer kan innehålla samma inställning och använda olika standardvärden för inställningarna, beroende på baslinjens avsikt.

   ![Expandera en grupp om du vill visa inställningarna för den gruppen](./media/security-baselines/sample-list-of-settings.png)

6. På fliken **Omfångstaggar** väljer du **Välj omfångstaggar** för att öppna fönstret *Välj taggar* för att tilldela omfångstaggar till profilen.

7. På fliken **Tilldelningar** väljer du **Välj grupper som ska ingå** och tilldela sedan baslinjen till en eller flera grupper. Använd **Välj grupper att utesluta** för att finjustera tilldelningen.

   ![Tilldela en profil](./media/security-baselines/assignments.png)

8. När du är redo att distribuera baslinjen fortsätter du till fliken **Granska och skapa** för att granska informationen för baslinjen. Spara och distribuera profilen genom att välja **Skapa**.

   När du skapar profilen skickas den till den tilldelade gruppen och kan tillämpas direkt.

   > [!TIP]
   > Om du skapar en profil utan att först tilldela den till grupper kan du redigera profilen senare för att göra detta.

   ![Granska baslinjen](./media/security-baselines/review.png)

9. När du har skapat profilen kan du redigera den genom att gå till **Slutpunktsskydd** > **Säkerhetsbaslinjer**, välja den baslinjetyp du konfigurerat och sedan välja **Profiler**. Välj profilen i listan över tillgängliga profiler och välj sedan **Egenskaper**. Du kan redigera inställningarna från alla tillgängliga konfigurationsflikar och välja **Granska + spara** för att genomföra ändringarna.

### <a name="change-the-baseline-version-for-a-profile"></a>Ändra baslinjeversionen för en profil

Du kan ändra den version av baslinjeinstansen som används med en profil.  När du ändrar versionen väljer du en tillgänglig instans av samma baslinje. Det går inte att växla mellan två olika baslinjetyper, till exempel att ändra en profil så att den inte längre använder en baslinje för Defender ATP utan istället använder MDM-säkerhetsbaslinjen.

När du konfigurerar en ändring av baslinjeversionen kan du hämta en CSV-fil som skapar en lista över ändringarna mellan de två aktuella baslinjeversionerna. Du kan också välja att behålla alla anpassningar från den ursprungliga baslinjeversionen eller implementera den nya versionen med alla standardvärden. Du har inte möjlighet att göra ändringar i enskilda inställningar när du ändrar versionen av en baslinje för en profil.

När du sparar efter en slutförd konvertering kommer baslinjen att distribueras på nytt omedelbart till tilldelade grupper.

**Under konverteringen**:

- Nya inställningar som inte fanns i ursprungsversionen läggs till och använder standardvärdena.

- Inställningar som inte finns i den nya versionen av baslinjen som du väljer tas bort och kommer inte längre att tillämpas av den här säkerhetsprofilen.

  När en inställning inte längre hanteras av en baslinjeprofil återställs inte inställningen på enheten. Istället bibehåller enheten sin senaste inställning tills någon annan process hanterar inställningen så att den ändras. Exempel på processer som kan ändra en inställning när du inte längre hanterar den inkluderar en annan baslinjeprofil, en grupprincipinställning eller en manuell konfiguration på enheten.

#### <a name="to-change-the-baseline-version-for-a-profile"></a>Så här ändrar du baslinjeversionen för en profil

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). 

2. Välj **Slutpunktssäkerhet** > **Säkerhetsbaslinjer**. Välj sedan panelen för den baslinjetyp som har den profil du vill använda.

3. Välj sedan **Profiler**, och markera kryssrutan för den profil du vill redigera. Välj sedan **Ändra version**.

   ![välj en baslinje](./media/security-baselines/select-baseline.png)

4. I fönstret **Ändra version** använder du listrutan **Välj en säkerhetsbaslinje att uppdatera till** och välj den versioninstans som du vill använda.

   ![välj en version](./media/security-baselines/select-instance.png)

5. Välj **Granska uppdateringen** för att ladda ned en CSV-fil som visar skillnaden mellan profilens aktuella instansversion och den nyvalda versionen. Granska den här filen så att du förstår vilka inställningar som är ny eller har tagits bort och vilka standardvärdena för dessa inställningar som gäller för den uppdaterade profilen.

   När du är klar kan du fortsätta till nästa steg.

6. Välj något av de två alternativen för **Välj en motod för att uppdatera profilen**:
   - **Acceptera baslinje ändringar men behåll mina befintliga anpassade inställningar** – det här alternativet behåller dina ändringar i baslinjeprofilen och tillämpar dem på den nya versionen som du har valt att använda.
   - **Acceptera ändringar av baslinjen och ta bort befintliga anpassade inställningar** – det här alternativet skriver över din ursprungliga profil. Den uppdaterade profilen använder standardvärden för alla inställningar.

7. Välj **Skicka**. Profilen uppdaterar till den valda versionen av baslinjen. När konverteringen har slutförts distribueras baslinjen omedelbart till tilldelade grupper.

### <a name="remove-a-security-baseline-assignment"></a>Ta bort en tilldelning av en säkerhetsbaslinje

När en inställning för en säkerhetsbaslinje inte längre gäller för en enhet eller inställningar i baslinjen är inställda på *Inte konfigurerad* kommer dessa inställningar på enheten inte att återgå till en förhanterad konfiguration. Istället behåller de tidigare hanterade inställningarna på enheten sina senaste konfigurationer som har tagits emot från baslinjen fram tills dess att någon annan process uppdaterade dessa inställningar på enheten.

Andra processer som kan ändra inställningarna på enheten senare inkluderar en annan eller ny säkerhetsbaslinje, enhetskonfigurationsprofil, grupprincipkonfigurationer eller manuella ändringar av enhetens inställningar.

### <a name="duplicate-a-security-baseline"></a>Kopiera en säkerhetsbaslinje

Du kan kopiera dina säkerhetsbaslinjer. Ett scenario när det är användbart att kopiera en baslinje är när du vill tilldela en liknande men distinkt baslinje till en delmängd av enheterna. Genom att skapa en kopia behöver du inte återskapa hela baslinjen manuellt. I stället kan du kopiera valfri befintlig baslinje och sedan bara införa de ändringar som krävs för den nya instansen. Du kanske bara ändrar en viss inställning och den grupp som baslinjen hör till.

När du skapar en kopia ger du den ett nytt namn. Kopian skapas med samma inställningskonfiguration och omfångstaggar som originalet, men har inga tilldelningar. Du måste redigera den nya baslinjen och lägga till tilldelningar.

Alla säkerhetsbaslinjer har stöd för kopiering.

När du har kopierat en baslinje kan du granska och redigera den nya instansen för att göra ändringar i konfigurationen.

#### <a name="to-duplicate-a-baseline"></a>Kopiera en baslinje

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Gå till **Endpoint Security** > **Säkerhetsbaslinjer**, välj typen av baslinje du vill kopiera och välj **Profiler**.
3. Högerklicka på den profil du vill kopiera och välj **Duplicera** eller välj ellipsen ( **...** ) till höger om baslinjen och välj **Duplicera**.
4. Ange ett **Nytt namn** för baslinjen och välj sedan **Spara**.

Efter en *uppdatering* ser du den nya baslinjeprofilen i administrationscentret.

#### <a name="to-edit-a-baseline"></a>Redigera en baslinje

1. Välj baslinjen och sedan **Egenskaper**.
2. Välj **inställningar** för att expandera listan med inställningskategorier i baslinjen. Du kan inte ändra inställningarna från den här vyn, men du kan granska hur de är konfigurerade.
3. Om du vill ändra inställningarna väljer du **Redigera** för varje kategori där du vill göra ändringar:
   - Grunderna
   - Tilldelningar
   - Omfångstaggar
   - Konfigurationsinställningar
4. När du har gjort dina ändringar väljer du **Spara** för att spara ändringarna.  Du måste spara ändringarna i en kategori innan du kan införa nya ändringar i andra kategorier.

### <a name="older-baseline-versions"></a>Äldre baslinjeversioner

Microsoft Endpoint Manager uppdaterar versioner av inbyggda säkerhetsbaslinjer beroende på de varierande behoven i en typisk organisation. Varje ny version resulterar i en versionsuppdatering av en viss baslinje. Avsikten är att kunderna ska använda den senaste baslinjeversionen som en startpunkt för deras enhetskonfigurationsprofiler.

När det inte längre finns några profiler som använder en äldre baslinje i din klientorganisation visar Microsoft Endpoint Manager endast den senaste tillgängliga baslinjeversionen.

Om du har en profil som är associerad med en äldre baslinje, kommer den gamla baslinjen att fortsätta att visas.

## <a name="co-managed-devices"></a>Samhanterade enheter

Säkerhetsbaslinjer på Intune-hanterade enheter liknar samhanterade enheter med Configuration Manager. Samhanterade enheter använder Configuration Manager och Microsoft Intune för att kunna hantera flera Windows 10-enheter samtidigt. Det innebär att du kan använda din befintliga Configuration Manager i molnet tillsammans med Intunes fördelar. [Översikt över samhantering](/configmgr/comanage/overview) är en bra resurs om du använder Configuration Manager och vill ha fördelarna med molnet.

När du använder samhanterade enheter, måste du ändra arbetsbelastningen i **Enhetskonfiguration** (i dess inställningar) till Intune. Mer information finns i [Enhetskonfigurationens arbetsbelastningar](/configmgr/comanage/workloads#device-configuration).

## <a name="q--a"></a>Frågor och svar

### <a name="why-these-settings"></a>Varför ska man använda de här inställningarna?

Microsofts säkerhetsteam har många års erfarenhet av att arbeta direkt med Windows-utvecklare och säkerhets-communityn för att skapa de här rekommendationerna. Inställningarna i baslinjen anses vara de mest relevanta säkerhetsrelaterade konfigurationsalternativen. Teamet justerar sina rekommendationer baserat på nyligen utgivna funktioner i varje ny Windows-version.

### <a name="is-there-a-difference-in-the-recommendations-for-windows-security-baselines-for-group-policy-vs-intune"></a>Finns det någon skillnad i rekommendationerna för Windows säkerhetsbaslinjer för grupprinciper och Intune?

Det är samma Microsoft-säkerhetsteam som har valt och organiserat inställningarna för varje baslinje. Intune innehåller alla relevanta inställningar i Intunes säkerhetsbaslinje. Det finns vissa inställningar i grupprincipens baslinje som är specifika för en lokal domänkontrollant. De här inställningarna är undantagna från Intunes rekommendationer. De andra inställningarna är likadana.

### <a name="are-the-intune-security-baselines-cis-or-nsit-compliant"></a>Är Intune-säkerhetsbaslinjerna CIS- och NIST-kompatibla?

Egentligen inte. Microsofts säkerhetsteam har kontakt med organisationer, som exempelvis CIS, när man sammanställer sina rekommendationer. Men det finns inte någon en-till-en-mappning mellan ”CIS-kompatibel” och Microsofts baslinjer.

### <a name="what-certifications-does-microsofts-security-baselines-have"></a>Vilka certifieringar har Microsofts säkerhetsbaslinjer? 

- Microsoft fortsätter att publicera säkerhetsbaslinjer för grupprinciper (GPO:er) och [verktyg för säkerhetsefterlevnad](/windows/security/threat-protection/security-compliance-toolkit-10) på samma sätt som vi har gjort under många år. Dessa baslinjer används av många organisationer. Rekommendationerna i dessa baslinjer kommer från Microsoft-säkerhetsteamets samverkan med företagskunder och externa myndigheter, bland annat DoD (Department of Defense) och NIST (National Institute of Standards and Technology). Vi delar våra rekommendationer och baslinjer med dessa organisationer. Organisationerna har också egna rekommendationer som avspeglar Microsofts rekommendationer. Eftersom hantering av mobilenheter (MDM) fortsätter att växa i molnet, har Microsoft skapat motsvarande MDM-rekommendationer för dessa grupprincipbaslinjer. Dessa ytterligare baslinjer är inbyggda i Microsoft Intune och innehåller efterlevnadsrapporter för användare, grupper och enheter som följer (eller inte följer) baslinjen.

- Många kunder använder Intunes baslinjerekommendationer som utgångspunkt, och anpassar dem sedan för att uppfylla sina IT- och säkerhetskrav. Microsofts Windows 10 RS5 **MDM-säkerhetsbaslinje** är den första baslinjen som lanseras. Den här baslinjen har utformats som en allmän infrastruktur där kunderna kommer att kunna importera andra säkerhetsbaslinjer som baseras på CIS, NIST och andra standarder. För närvarande är den tillgänglig för Windows och kommer även att finnas för iOS/iPadOS och Android så småningom.

- Att migrera från lokala Active Directory-grupprinciper till en ren molnlösning med hjälp av Azure Active Directory (AD) och Microsoft Intune kan kännas övermäktigt. Som hjälp finns en grupp principmallar som ingår i [Verktyg för säkerhetsefterlevnad](/windows/security/threat-protection/security-compliance-toolkit-10) som kan hantera hybrid AD- och Azure AD-anslutna enheter. Dessa enheter kan hämta MDM-inställningar från molnet (Intune) och grupprincipinställningar från lokala domänkontrollanter när det behövs.

## <a name="next-steps"></a>Nästa steg

- Visa inställningarna i de senaste versionerna av de tillgängliga baslinjerna:
  - [MDM-säkerhetsbaslinje](security-baseline-settings-mdm-all.md)
  - [Microsoft Defender ATP-baslinje](security-baseline-settings-defender-atp.md)

- Kontrollera statusen och övervaka [baslinje och profil](security-baselines-monitor.md)