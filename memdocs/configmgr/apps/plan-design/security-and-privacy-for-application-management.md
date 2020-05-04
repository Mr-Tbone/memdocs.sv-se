---
title: Säkerhet och sekretess för appar
titleSuffix: Configuration Manager
description: Vägledning och rekommendationer för säkerhet och sekretess när du hanterar program i Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f7085b7ee6f0f723c9bcf9d10cb85b03f990a44
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709959"
---
# <a name="security-and-privacy-for-application-management-in-configuration-manager"></a>Säkerhet och sekretess för program hantering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

## <a name="security-guidance-for-application-management"></a>Säkerhets vägledning för program hantering  

### <a name="use-the-software-center-without-the-application-catalog"></a>Använda Software Center utan program katalogen

<!--1358309-->

Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Den här konfigurationen hjälper dig att minska Server infrastrukturen som krävs för att leverera program till användare.

Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910. Att minska Server infrastrukturen minskar också risken för angrepp.

Använd Azure Active Directory och Cloud Management Gateway för att leverera en konsekvent och säker program upplevelse för Internetbaserade klienter.

Mer information finns i [Konfigurera Software Center](plan-for-software-center.md#bkmk_userex).

### <a name="use-https-with-the-application-catalog"></a>Använda HTTPS med program katalogen

> [!Important]  
> Support upphör för program katalog rollerna med version 1910. Mer information finns i [ta bort program katalogen](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Konfigurera program katalogens webbplats och webb tjänst platsen för program katalogen för att godkänna HTTPS-anslutningar. Med den här konfigurationen autentiseras servern för användare. Överförda data skyddas från manipulering och visning.

Hjälp till att förhindra angrepp från sociala medier genom att utbilda användarna till betrodda webbplatser. Utbilda användare om farorna med skadliga webbplatser.

Använd inte konfigurations alternativen för anpassning när du inte använder HTTPS. De här inställningarna visar namnet på din organisation i program katalogen som identitets bevis.  


### <a name="use-role-separation"></a>Använd rollseparering

> [!Important]  
> Support upphör för program katalog rollerna med version 1910. Mer information finns i [ta bort program katalogen](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Installera program katalogens webbplats och webb tjänst platsen för program katalogen på separata servrar. Om webbplats platsen har komprometterats är den separat från webb tjänst punkten. Den här designen hjälper till att skydda Configuration Manager-klienter och-infrastruktur. Den här konfigurationen är särskilt viktig om webbplats platsen accepterar klient anslutningar från Internet. Det gör servern mer sårbar för angrepp.  

### <a name="close-browser-windows"></a>Stäng webb läsar fönster

> [!Important]  
> Support upphör för program katalog rollerna med version 1910. Mer information finns i [ta bort program katalogen](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Utbilda användare att stänga webbläsarfönstret när de är klara med program katalogen. Om användarna bläddrar till en extern webbplats i samma webbläsarfönster som de använde för program katalogen, fortsätter webbläsaren att använda de säkerhets inställningar som är lämpliga för betrodda platser i intranätet.  

### <a name="centrally-specify-user-device-affinity"></a>Ange mappning mellan användare och enhet centralt

Ange mappning mellan användare och enhet manuellt i stället för att låta användarna identifiera sin primära enhet. Aktivera inte användnings-baserad konfiguration.

Överväg inte information som samlas in från användare eller från enheten för att vara auktoritativ. Om du distribuerar program vara med hjälp av mappning mellan användare och enhet som en betrodd administratör inte anger, kan program varan installeras på datorer och till användare som inte har behörighet att ta emot den program varan.  

### <a name="dont-run-deployments-from-distribution-points"></a>Kör inte distributioner från distributions platser

Konfigurera alltid distributioner så att innehåll laddas ned från distributionsplatser i stället för att köras från distributionsplatser. När du konfigurerar distributioner för att ladda ned innehåll från en distributions plats och körs lokalt, verifierar Configuration Manager klienten paketets hash när innehållet har laddats ned. Klienten ignorerar paketet om hashvärdet inte matchar hashen i principen.

Om du konfigurerar distributionen så att den körs direkt från en distributions plats, verifierar Configuration Manager klienten inte paketets hash. Det innebär att Configuration Manager-klienten kan installera program vara som har manipulerats.

Om du måste köra distributioner direkt från distributions platser bör du använda minst NTFS-behörigheter på paketen på distributions platserna. Använd också IPsec (Internet Protocol Security) för att skydda kanalen mellan klienten och distributions platserna och mellan distributions platserna och plats servern.

### <a name="dont-let-users-interact-with-elevated-processes"></a><a name="bkmk_interact"></a>Låt inte användarna interagera med utökade processer
  
Om du aktiverar alternativen för att **köra med administratörs behörighet** eller **Installera för system**ska du inte låta användarna interagera med dessa program. När du konfigurerar ett program kan du ställa in alternativet så att **användarna kan visa och interagera med programinstallationen**. Med den här inställningen kan användarna svara på eventuella obligatoriska meddelanden i användar gränssnittet. Om du även konfigurerar programmet att **köras med administratörs behörighet**, eller från och med version 1802 **Installera för system**, kan en angripare på datorn som kör programmet använda användar gränssnittet för att eskalera privilegier på klient datorn.

Använd program som använder Windows Installer för installations-och användar utökade behörigheter för program varu distributioner som kräver administratörs behörighet. Installationen måste köras i kontexten för en användare som inte har administratörs behörighet. Windows Installer utökade privilegier per användare ger det säkraste sättet att distribuera program som har det här kravet.

### <a name="restrict-whether-users-can-install-software-interactively"></a>Begränsa huruvida användarna kan installera program interaktivt

Konfigurera klient inställningen **Installera behörigheter** i **dator agent** gruppen. Den här inställningen begränsar vilka typer av användare som kan installera program vara i Software Center.

Du kan t.ex. skapa en anpassad klientinställning där **Installationsbehörigheter** har värdet **Bara administratörer**. Använd den här klient inställningen på en Server grupp. Den här konfigurationen förhindrar användare utan administratörs behörighet från att installera program vara på dessa servrar.  

### <a name="for-mobile-devices-deploy-only-applications-that-are-signed"></a>Distribuera bara signerade appar på mobila enheter

Distribuera bara mobila enhets program om de är kod-signerade av en certifikat utfärdare (CA) som den mobila enheten litar på.

Ett exempel:

- Ett program från en leverantör som är signerat av en välkänd certifikat utfärdare som VeriSign.  

- Ett internt program som du signerar oberoende av Configuration Manager med hjälp av din interna certifikat utfärdare.  

- Ett internt program som du loggar in med Configuration Manager när du skapar program typen och använder ett signerings certifikat.

### <a name="secure-the-location-of-the-mobile-device-application-signing-certificate"></a>Skydda platsen för den mobila enhetens program signerings certifikat

Om du signerar mobila enhets program med hjälp av **guiden Skapa program** i Configuration Manager ska du skydda platsen för signerings certifikat filen och skydda kommunikations kanalen. För att skydda mot höjning av privilegier och mot man-in-the-middle-attacker, lagrar du signerings certifikat filen i en skyddad mapp.

Använd IPsec mellan följande datorer:

- Datorn som kör Configuration Manager-konsolen
- Datorn som lagrar certifikat signerings filen
- Datorn som lagrar programmets källfiler

Du kan också signera programmet oberoende av Configuration Manager och innan du kör **guiden Skapa program**.

### <a name="implement-access-controls"></a>Implementera åtkomst kontroller

Implementera åtkomst kontroller för att skydda referens datorer. När du konfigurerar identifierings metoden i en distributions typ genom att bläddra till en referens dator kontrollerar du att datorn inte har komprometterats.

### <a name="restrict-and-monitor-administrative-users"></a>Begränsa och övervaka administrativa användare

Begränsa och övervaka de administrativa användare som du beviljar följande rollbaserade säkerhets roller för program hantering:

- **Programadministratör**
- **Programförfattare**
- **Programdistributionsansvarig**

Även om du konfigurerar rollbaserad administration kan administrativa användare som skapar och distribuerar program ha fler behörigheter än du inser. Administrativa användare som skapar eller ändrar ett program kan till exempel välja beroende program som inte tillhör säkerhets omfattningen.

### <a name="configure-app-v-apps-in-virtual-environments-with-the-same-trust-level"></a>Konfigurera App-V-appar i virtuella miljöer med samma förtroende nivå

När du konfigurerar virtuella Microsoft Application Virtualization-miljöer (App-V) väljer du program som har samma förtroende nivå i den virtuella miljön. Eftersom program i en virtuell App-V-miljö kan dela resurser, t. ex. Urklipp, konfigurerar du den virtuella miljön så att de valda programmen har samma förtroende nivå.

Mer information finns i [skapa virtuella App-V-miljöer](../deploy-use/create-app-v-virtual-environments.md).

### <a name="make-sure-macos-apps-are-from-a-trustworthy-source"></a>Kontrol lera att macOS-appar kommer från en betrodd källa

Om du distribuerar program för macOS-enheter kontrollerar du att källfilerna kommer från en betrodd källa. CMAppUtil-verktyget verifierar inte signaturen för käll paketet. Kontrol lera att paketet kommer från en källa som du litar på. Verktyget CMAppUtil kan inte identifiera om filerna har manipulerats.

### <a name="secure-the-cmmac-file-for-macos-apps"></a>Skydda cmmac-filen för macOS-appar

Om du distribuerar program för macOS-datorer skyddar du platsen för **. cmmac** -filen. Verktyget CMAppUtil genererar den här filen och importerar den sedan till Configuration Manager. Den här filen är inte signerad eller verifierad.

Skydda kommunikations kanalen när du importerar filen till Configuration Manager. Du kan förhindra manipulering av filen genom att lagra den i en skyddad mapp. Använd IPsec mellan följande datorer:

- Datorn som kör Configuration Manager-konsolen  
- Datorn som lagrar **. cmmac** -filen  

### <a name="use-https-for-web-applications"></a>Använda HTTPS för webb program

Om du konfigurerar en distributions typ för webb program använder du HTTPS för att skydda anslutningen. Om du distribuerar ett webb program med hjälp av en HTTP-länk i stället för en HTTPS-länk, skulle enheten kunna omdirigeras till en falsk Server. Data som överförs mellan enheten och servern kan manipuleras.


## <a name="security-issues-for-application-management"></a>Säkerhetsproblem för programhantering  

- Användare med begränsade rättigheter kan kopiera filer från klientcachen på klientdatorn.  

     Användare kan läsa-klientcachen men inte skriva till den. Med läsbehörighet kan en användare kopiera ett programs installationsfiler från en dator till en annan.  

- Användare med begränsade rättigheter kan ändra filer som registrerar program distributions historik på klient datorn.  

     Eftersom information om program historiken inte är skyddad, kan en användare ändra filer som rapporterar om ett program har installerats.  

- App-V-paket signeras inte.  

     App-V-paket i Configuration Manager stöder inte signering. Digitala signaturer verifierar att innehållet kommer från en betrodd källa och inte har ändrats under överföringen. Det finns ingen minskning av det här säkerhets problemet. Följ den rekommenderade säkerhets praxisen för att ladda ned innehållet från en betrodd källa och från en säker plats.  

- Publicerade App-V-program går att installera av alla användare på datorn.  

     När ett App-V-program publiceras på en dator, kan alla användare som loggar in på den datorn installera programmet. Du kan inte begränsa vilka användare som kan installera programmet när det har publicerats.  


## <a name="certificates-for-microsoft-silverlight-5-and-elevated-trust-mode-required-for-the-application-catalog"></a><a name="BKMK_CertificatesSilverlight5"></a>Certifikat för Microsoft Silverlight 5 och förhöjt förtroende krävs för program katalogen  

> [!Important]  
> Support upphör för program katalog rollerna med version 1910. Mer information finns i [ta bort program katalogen](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Configuration Manager-klienter version 1710 och tidigare kräver Microsoft Silverlight 5, som måste köras med förhöjt förtroende för att användare ska kunna installera program vara från program katalogen. Som standard körs Silverlight-program med partiellt förtroende för att hindra program från att komma åt användarnas data. Om den inte redan är installerad installerar Configuration Manager automatiskt Microsoft Silverlight 5 på klienter. Som standard anger Configuration Manager dator agenten **Tillåt att Silverlight-program körs med klient inställningen förhöjt förtroende läge** till **Ja**. Med den här inställningen kan signerade och betrodda Silverlight-program begära förhöjt förtroende läge.  

När du installerar plats system rollen webbplats för program katalog installerar klienten även ett signerings certifikat från Microsoft i certifikat arkivet Betrodda utgivare på varje Configuration Manager klient dator. Silverlight-program som signerats av detta certifikat körs i läget för förhöjt förtroende, vilka datorer som kräver att program vara installeras från program katalogen. Configuration Manager hanterar detta signerings certifikat automatiskt. Ta inte bort eller flytta detta signerings certifikat från Microsoft manuellt för att öka tjänst kontinuiteten.  

> [!WARNING]  
> När alternativet Tillåt att **Silverlight-program körs med förhöjt förtroende läge** kan alla Silverlight-program som är signerade av certifikat i certifikat arkivet Betrodda utgivare antingen i dator arkivet eller i användar arkivet köras med förhöjt förtroende. Klient inställningen kan inte aktivera förhöjt förtroende specifikt för Configuration Manager program katalog eller certifikat arkivet Betrodda utgivare i dator arkivet. Om skadlig kod lägger till ett falskt certifikat i arkivet Betrodda utgivare kan skadlig kod som använder sitt eget Silverlight-program nu också köras med förhöjt förtroende läge.  

Om du ställer in inställningen **Tillåt att Silverlight-program körs med förhöjt förtroende läge** till **Nej**tar klienterna inte bort Microsofts signerings certifikat.  

Mer information om betrodda program i Silverlight finns i [betrodda program](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/ee721083\(v=vs.95\)).  


## <a name="privacy-information-for-application-management"></a> Sekretessinformation för programhantering  

Med program hantering kan du köra program, program eller skript på alla klienter i hierarkin. Configuration Manager har ingen kontroll över vilka typer av program, program eller skript som du kör eller vilken typ av information som de skickar. Under program distributions processen kan Configuration Manager överföra information som identifierar enheten och inloggnings kontona mellan klienter och servrar.  

Configuration Manager behåller statusinformation om program distributions processen. Informationen om program varu distribution är inte krypterad under överföringen om inte klienten kommunicerar med hjälp av HTTPS. Statusinformationen lagras inte i krypterad form i databasen.  

Användning av Configuration Manager-Programinstallation för att fjärrans luta, interaktivt eller tyst installera program vara på klienter kan vara beroende av program varans licens villkor för program varan. Den här användningen är separat från licens villkoren för program vara för Configuration Manager. Läs alltid igenom och godkänn licens villkoren för program vara innan du distribuerar program vara med hjälp av Configuration Manager.  

Configuration Manager samlar in diagnostik-och användnings data om program, som används av Microsoft för att förbättra framtida versioner. Mer information finns i [diagnostik-och användnings data](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).

Program distribution sker inte som standard och kräver flera konfigurations steg.  

Följande funktioner hjälper till att effektivt program varu distribution:

- Mappning mellan **användare och enhet** mappar en användare till enheter. En Configuration Manager administratör distribuerar program vara till en användare. Klienten installerar automatiskt program varan på en eller flera datorer som användaren oftast använder.  

- **Software Center** installeras automatiskt på en enhet när du installerar Configuration Manager-klienten. Användare ändrar inställningar, söker efter och installerar program vara från Software Center.  

- **Program katalogen** är en webbplats där användare kan begära installation av program vara.  

    > [!Important]  
    > Support upphör för program katalog rollerna med version 1910. Mer information finns i [ta bort program katalogen](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

### <a name="user-device-affinity-privacy-information"></a><a name="bkmk_privacy-uda"></a>Sekretess information för mappning mellan användare och enhet

- Configuration Manager kan överföra information mellan klienter och hanterings plats system. Informationen kan identifiera datorn och inloggnings kontot och den sammanfattade användningen av inloggnings konton.  

- Den information som överförs mellan klienten och servern är inte krypterad, om inte hanterings platsen är konfigurerad för att kräva att klienter kommunicerar med hjälp av HTTPS.  

- Dator-och inloggnings kontots användnings information, som används för att mappa en användare till en enhet, lagras på klient datorer, skickas till hanterings platser och lagras sedan i Configuration Manager-databasen. Den gamla informationen tas som standard bort från databasen efter 90 dagar. Borttagningsbeteendet kan konfigureras genom att ange platshanteringsuppgiften **Ta bort föråldrade tillhörighetsdata för användarenhet** .  

- Configuration Manager hanterar statusinformation om mappning mellan användare och enhet. Statusinformation är inte krypterad under överföringen, om inte klienter har kon figurer ATS för att kommunicera med hanterings platser med hjälp av HTTPS. Statusinformationen lagras inte i krypterad form i databasen.  

- Information om dator-och inloggnings användning som används för att upprätta användar-och enhets tillhörighet är alltid aktive rad. Användare och administrativa användare kan ange information om mappning mellan användare och enhet.  

### <a name="software-center-privacy-information"></a><a name="bkmk_privacy-userex"></a>Sekretess information för Software Center

- Med Software Center kan Configuration Manager-administratören publicera alla program eller program eller skript som användarna kan köra. Configuration Manager har ingen kontroll över vilka typer av program eller skript som publiceras i katalogen eller vilken typ av information som de skickar.  

- Configuration Manager kan överföra information mellan klienter och hanterings platsen. Informationen kan identifiera dator-och inloggnings konton. Den information som överförs mellan klienten och servrarna är inte krypterad, om du inte konfigurerar hanterings platsen så att den kräver att klienter ansluter med hjälp av HTTPS.  

- Informationen om begäran om program godkännande lagras i Configuration Manager databasen. Begär Anden som har avbrutits eller nekas och motsvarande poster för begär ande historik tas bort som standard efter 30 dagar. Borttagningsbeteendet kan konfigureras genom att ange platshanteringsuppgiften **Ta bort föråldrade data för programbegäranden** . Begär Anden om program godkännande som har statusen Godkänd och väntar, tas aldrig bort.  

- Software Center installeras automatiskt när du installerar Configuration Manager-klienten på en enhet.  

### <a name="application-catalog-privacy-information"></a>Sekretess information för program katalog

> [!Important]  
> Support upphör för program katalog rollerna med version 1910. Mer information finns i [ta bort program katalogen](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

- Program katalogen installeras inte som standard. Installationen kräver flera konfigurationssteg.  

- Med program katalogen kan Configuration Manager-administratören publicera alla program eller program eller skript som användarna kan köra. Configuration Manager har ingen kontroll över vilka typer av program eller skript som publiceras i katalogen eller vilken typ av information som de skickar.  

- Configuration Manager kan överföra information mellan klienter och program katalogens plats system roller. Informationen kan identifiera dator-och inloggnings konton. Den information som överförs mellan klienten och servrarna är inte krypterad, om inte plats system rollerna är konfigurerade för att kräva att klienter ansluter med hjälp av HTTPS.  
