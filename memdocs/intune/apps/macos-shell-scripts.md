---
title: Använda shell-skript på macOS-enheter i Microsoft Intune | Microsoft Docs
description: Skapa, tilldela, övervaka och felsöka shell-skript för macOS-enheter i Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ba099e3614c11e10ce4cd9ae94668a1648bfc150
ms.sourcegitcommit: 252e718dc58da7d3e3d3a4bb5e1c2950757f50e2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/07/2020
ms.locfileid: "80808049"
---
# <a name="use-shell-scripts-on-macos-devices-in-intune-public-preview"></a>Använda shell-skript på macOS-enheter i Intune (allmänt tillgänglig förhandsversion)

> [!NOTE]
> Shell-skript för macOS-enheter finns just nu i förhandsversion. Granska listan med [kända problem i förhandsversionen](macos-shell-scripts.md#known-issues) innan du använder den här funktionen.

Använd shell-skript för att utöka funktionerna för enhetshantering i Intune utöver vad som stöds av operativsystemet macOS. 

## <a name="prerequisites"></a>Krav
Se till att följande krav uppfylls när du skriver in shell-skript och tilldelar dem till macOS-enheter. 
 - Enheterna kör macOS 10.12 eller senare.
 - Enheterna hanteras av Intune. 
 - Shell-skript börjar med `#!` och måste finnas på en giltig plats, till exempel `#!/bin/sh` eller `#!/usr/bin/env zsh`.
 - Kommandoradstolkar för tillämpliga gränssnitt är installerade.

## <a name="important-considerations-before-using-shell-scripts"></a>Viktiga överväganden innan du använder shell-skript
 - Shell-skript kräver att Microsoft Intune MDM-agenten har installerats på macOS-enheten. Mer information finns i [Microsoft Intune MDM Agent for macOS](macos-shell-scripts.md#microsoft-intune-mdm-agent-for-macos) (Microsoft Intune MDM-agenten för macOS).
 - Shell-skript körs parallellt på enheter som separata processer.
 - Shell-skript som körs som den inloggade användaren körs för alla användarkonton som är inloggade på enheten vid körningstillfället.
 - En slutanvändare måste logga in på enheten för att kunna köra skript som körs som en inloggad användare.
 - Rotanvändarbehörigheter krävs om skriptet kräver ändringar som ett standardanvändarkonto inte kan göra.
 - Shell-skript försöker köra oftare än den valda skriptfrekvensen för vissa villkor, till exempel om disken är full, om lagringsplatsen har ändrats, om den lokala cachen tas bort eller om Mac-enheten startas om.
 
## <a name="create-and-assign-a-shell-script-policy"></a>Skapa och tilldela en skriptprincip
1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **macOS** > **Skript** > **Lägg till**.
3. I **Grundläggande** anger du följande egenskaper och väljer sedan **Nästa**:
   - **Namn**: Ange ett namn på shell-skriptet.
   - **Beskrivning**: Ange en beskrivning för shell-skriptet. Denna inställning är valfri, men rekommenderas.
4. I **Skriptinställningar** anger du följande egenskaper och väljer **Nästa**:
   - **Ladda upp skript**: Bläddra till shell-skriptet. Skriptfilen måste vara mindre än 200 KB.
   - **Köra skript som inloggad användare**: Välj **Ja** för att köra skriptet med användarens autentiseringsuppgifter på enheten. Välj **Nej** (standard) om du vill köra skriptet som rotanvändaren. 
   - **Dölja skriptmeddelanden på enheter:** Som standard visas skriptmeddelanden för varje skript som körs. På macOS-enheter ser slutanvändarna en avisering från Intun om att *IT konfigurerar datorn*.
   - **Skriptfrekvens:** Välj hur ofta skriptet ska köras. Välj **Inte konfigurerat** (standard) för att bara köra skriptet en gång.
   - **Maximalt antal nya försök om skriptet misslyckas:** Välj hur många gånger skriptet ska köras om det returnerar en slutkod som inte är noll (noll innebär att det är klart). Välj **Inte konfigurerat** (standard) för att inte försöka igen när ett skript misslyckas.
5. I **Omfångstaggar** väljer du om du vill lägga till omfångstaggar för skriptet och väljer sedan **Nästa**. Du kan använda omfångstaggar för att bestämma vem som kan se skript i Intune. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).
6. Välj **Tilldelningar** > **Välj grupper att ta med**. En befintlig lista över Azure AD-grupper visas. Välj en eller flera enhetsgrupper som innehåller de användare vars macOS-enheter ska ta emot skriptet. Välj **Välj**. De grupper du väljer visas i listan och tilldelas din skriptprincip.
   > [!NOTE]
   > - Shell-skript i Intune kan bara tilldelas till säkerhetsgrupper för Azure AD-enheter. Tilldelning av användargrupper stöds inte i förhandsversionen. 
   > - Vid uppdatering av tilldelningar för shell-skript uppdateras även tilldelningar för [Microsoft Intune MDM-agent för macOS](macos-shell-scripts.md#microsoft-intune-mdm-agent-for-macos).
7. I **Granska + lägg till** visas en sammanfattning av de inställningar som du har konfigurerat. Välj **Lägg till** för att spara skriptet. När du väljer **Lägg till** distribueras skriptprincipen till de grupper som du har valt.

Skriptet som du har skapat visas nu i listan över skript. 

## <a name="monitor-a-shell-script-policy"></a>Övervaka en princip för shell-skript
Du kan övervaka körningsstatus för alla tilldelade skript för användare och enheter genom att välja någon av följande rapporter:
- **Skript** > **välj skriptet som ska övervakas** > **Enhetsstatus**
- **Skript** > **välj skriptet som ska övervakas** > **Användarstatus**

>[!IMPORTANT]
> Oberoende av den valda **skriptfrekvensen** rapporteras körningsstatus för skript endast den första gången ett skript körs. Skriptkörningsstatus uppdateras inte vid efterföljande körningar. Däremot behandlas uppdaterade skript som nya skript och rapporterar körningsstatus igen.

När ett skript körs returnerar det något av följande tillstånd:
- Skriptkörningsstatusen **Misslyckades** anger att skriptet returnerade en slutkod som inte är noll eller att skriptet har fel format. 
- Skriptkörningsstatusen **Lyckades** anger att skriptet returnerade noll som slutkod. 

## <a name="frequently-asked-questions"></a>Vanliga frågor och svar
### <a name="why-are-assigned-shell-scripts-not-running-on-the-device"></a>Varför körs inte tilldelade shell-skript på enheten?
Det här kan ha flera orsaker:
* Agenten kan behöva checka in för att ta emot nya eller uppdaterade skript. Incheckningsprocessen sker var åttonde timme och skiljer sig från MDM-incheckningen. Kontrollera att enheten är igång och ansluten till ett nätverk för en lyckad agentinloggning, och vänta tills agenten checkar in.
* Agenten kanske inte är installerad. Kontrollera att agenten är installerad på `/Library/Intune/Microsoft Intune Agent.app` på macOS-enheten.
* Agenten kanske inte är i felfritt tillstånd. Agenten kommer att försöka återställa i 24 timmar och sedan ta bort och ominstallera sig själv om shell-skripten fortfarande är tilldelade.

### <a name="how-frequently-is-script-run-status-reported"></a>Hur ofta rapporteras skriptkörningsstatus?
Skriptkörningsstatus rapporteras till Microsoft Endpoint Manager-administratörskonsolen så fort skriptkörningen har slutförts. Om ett skript har schemalagts för regelbunden körning med en angiven frekvens, rapporterar det bara status första gången det körs.

### <a name="when-are-shell-scripts-run-again"></a>När körs shell-skript igen?
Ett skript körs bara igen när inställningen för **högsta antal nya försök om skriptet misslyckas** har konfigurerats och skriptet misslyckas vid körning. Om inställningen för **högsta antal nya försök om skriptet misslyckas** inte har konfigurerats och ett skript inte kan köras, körs det inte igen och körningsstatusen rapporteras som **misslyckad**. 

### <a name="what-intune-role-permissions-are-required-for-shell-scripts"></a>Vilka rollbehörigheter i Intune krävs för shell-skript?
Din tilldelade Intune-roll kräver behörigheter för **enhetskonfiguration** för att ta bort, tilldela, skapa, uppdatera eller läsa shell-skript.

## <a name="microsoft-intune-mdm-agent-for-macos"></a>Microsoft Intune MDM-agent för macOS
 ### <a name="why-is-the-agent-required"></a>Varför behövs agenten?
 Microsoft Intune MDM-agenten behöver installeras på hanterade macOS-enheter för att möjliggöra avancerade funktioner för enhetshantering som inte stöds av det inbyggda operativsystemet macOS.
 
 ### <a name="how-is-the-agent-installed"></a>Hur installeras agenten?
 Agenten installeras automatiskt och tyst på Intune-hanterade macOS-enheter som du tilldelar minst ett shell-skript i administrationscentret för Microsoft Endpoint Manager. Agenten installeras på `/Library/Intune/Microsoft Intune Agent.app` när det är tillämpligt och visas inte i **Finder** > **Program** på macOS-enheter. Agenten visas som `IntuneMdmAgent` i **Aktivitetskontroll** när den körs på macOS-enheter.

### <a name="what-does-the-agent-do"></a>Vad gör agenten?
 - Agenten autentiseras tyst med Intune-tjänster innan den checkar in för att ta emot tilldelade shell-skript för macOS-enheten.
 - Agenten tar emot tilldelade shell-skript och kör skripten baserat på det konfigurerade schemat, nya försök, meddelandeinställningar och andra inställningar som angetts av administratören.
 - Agenten söker normalt efter nya eller uppdaterade skript hos Intune-tjänster var 8:e timme. Incheckningsprocessen sker oberoende av MDM-incheckningen. 
 
 ### <a name="how-can-i-manually-initiate-an-agent-check-in-from-a-mac"></a>Hur kan jag starta en agentincheckning manuellt från en Mac?
På en hanterad Mac-dator som har agenten installerad öppnar du **Terminal** och kör `IntuneMdmAgent` kommandot för att avsluta `sudo killall IntuneMdmAgent` processen. Processen `IntuneMdmAgent` startas om omedelbart, vilket initierar en incheckning hos Intune.

Som alternativ kan du göra följande:
1. Öppna **Aktivitetskontroll** > **Visa** > *välj **Alla processer**.* 
2. Sök efter processer med namnet `IntuneMdmAgent`. 
3. Avsluta processen som körs för **rot**-användaren. 

> [!NOTE]
> Åtgärden **Kontrollera inställningar** i Företagsportal och åtgärden **Synkronisera** för enheter i Microsoft Endpoint Manager-administratörskonsolen initierar en MDM-incheckning och tvingar inte fram en agentincheckning.

 ### <a name="when-is-the-agent-removed"></a>När tas agenten bort?
 Det finns flera villkor som kan orsaka att agenten tas bort från enheten, till exempel:
 - Shell-skripten tilldelas inte längre till enheten. 
 - macOS-enheten hanteras inte längre.
 - Agenten är i ett oåterkalleligt tillstånd i mer än 24 timmar (enhetens aktiva tid).

 ### <a name="how-to-turn-off-usage-data-sent-to-microsoft-for-shell-scripts"></a>Vill du veta hur du stänger av de användningsdata som skickas till Microsoft för shell-skript?
 Om du vill stänga av användningsdata som skickas till Microsoft från Intune MDM-agenten öppnar du Företagsportal och väljer **Meny** > **Inställningar** > *avmarkera Tillåt att Microsoft samlar in användningsdata*. Åtgärden stänger av användningsdata som skickas för både Intune MDM-agenten och Företagsportal.

## <a name="known-issues"></a>Kända problem
- **Tilldelning av användargrupp:** Shell-skript som är tilldelade till användargrupper gäller inte för enheter. Tilldelning av användargrupper stöds för närvarande inte i förhandsversionen. Använd tilldelning av användargrupper för att tilldela skript.
- **Samla in loggar:** Åtgärden ”Samla in loggar” är synlig. Vid försök till logginsamling visas dock meddelandet ”ett fel uppstod” och loggarna registreras inte. Insamling av loggar stöds för närvarande inte i förhandsversionen.
- **Ingen körningsstatus för skript:** Skulle det osannolika inträffa att ett skript tas emot på enheten och enheten kopplas från innan körningsstatusen rapporteras, kommer enheten inte att rapportera körningsstatus för skriptet i administratörskonsolen.
- **Användarstatusrapport:** Problem med att en rapport är tom har uppstått. Välj [Övervaka](https://go.microsoft.com/fwlink/?linkid=2109431) i **administrationscentret för Microsoft Endpoint Manager**. Användarstatusen visar en tom rapport.

## <a name="next-steps"></a>Nästa steg

- [Skapa en efterlevnadsprincip i Microsoft Intune](..\protect\create-compliance-policy.md)
