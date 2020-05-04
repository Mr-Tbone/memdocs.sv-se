---
title: Paketomvandlingshanteraren
titleSuffix: Configuration Manager
description: Lär dig om Package Conversion Manager för att konvertera paket till program i Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f053fa73-c553-4522-a6b9-f885f23fe57c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 075dd860d20662679e5bdf58dae23d0220fa751e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709917"
---
# <a name="package-conversion-manager"></a>Paketomvandlingshanteraren

*Gäller för: Configuration Manager (aktuell gren)*

<!--1357861-->

Från och med version 1806 hjälper Package Conversion Manager dig att konvertera Configuration Manager äldre paket till program. Program har ytterligare fördelar, till exempel beroenden, krav regler, identifierings metoder och mappning mellan användare och enhet.

> [!Tip]  
> Den här funktionen introducerades först i version 1806 som en [för hands versions funktion](../../core/servers/manage/pre-release-features.md). Från och med version 1810 är den här funktionen inte längre en för hands versions funktion.  


Ett Configuration Manager-program innehåller filer och program som du distribuerar till klient enheter. Men till skillnad från äldre paket och program innehåller ett program ytterligare ininriktade funktioner. Ett program kan exempelvis innehålla distributions typer för en lokal installation av ett program varu paket, ett virtuellt programpaket eller en version av programmet för mobila enheter.

Mer information finns i följande artiklar: 
- [Introduktion till programhantering](../understand/introduction-to-application-management.md)  
- [Paket och program](../deploy-use/packages-and-programs.md)  

> [!Important]  
> Om du tidigare har installerat en äldre version av Package Conversion Manager måste du först avinstallera den innan du uppgraderar platsen. Den här integrerade versionen kräver inte installation, men kan orsaka konflikter med befintliga versioner.  

Den här integrerade versionen av Package Conversion Manager fungerar på paket i Configuration Manager aktuella gren platsen. Det är inte ett fristående verktyg. Om du har paket och program i en äldre version av Configuration Manager migrerar du först paketen till den aktuella gren platsen. Mer information finns i [migrera data mellan hierarkier](../../core/migration/migrate-data-between-hierarchies.md).

<!-- SCCMDocs-pr issue #3357 -->
Configuration Manager version 1902 innehåller följande förbättringar:
- Schemalagda paket analyser körs var sjunde dag som standard
- PowerShell-cmdletar för att analysera och konvertera paket
- Allmänna fel korrigeringar och förbättringar



## <a name="planning"></a>Planering

Innan du börjar konvertera paket till program bör du först utveckla en plan. Följande process är en exempel plan:

- [Definiera en detaljerad paket konverterings plan](#bkmk_define)  

- [Välj och Förbered paket för konvertering](#bkmk_prepare)  

- [Välj test paket](#bkmk_test)  

- [Analysera, Undersök och konvertera paket](#bkmk_analyze)  

- [Testa och distribuera programmen](#bkmk_deploy)  


### <a name="define-a-detailed-package-conversion-plan"></a><a name="bkmk_define"></a>Definiera en detaljerad paket konverterings plan

I det här avsnittet beskrivs två exempel på paket konverterings planer:  

- [En test miljö med hög resurs](#bkmk_define-high): du har en test miljö med resurser, behörigheter och arkitektur för att fullständigt replikera produktions miljön.  

- [En test miljö med begränsad resurs](#bkmk_define-limited): du har ingen test miljö som fullständigt replikerar din produktions miljö.  

Justera dessa planer efter behov för andra problem som är specifika för din miljö.

#### <a name="sample-plan-for-a-high-resource-test-environment"></a><a name="bkmk_define-high"></a>Exempel plan för en test miljö med hög resurs

Din test miljö har resurser, behörigheter och arkitektur som liknar din produktions miljö. Använd test miljön för att effektivt analysera och konvertera alla dina paket och testa sedan alla Configuration Manager-program. När du har slutfört det arbetet överför du det till produktions miljön. 

Paket konverterings planen kan se ut ungefär så här:  

1.  Välj de paket som du vill konvertera.  

2.  Migrera paketen för konvertering till din test miljö.  

3.  Förbered paketen för konvertering.  

4.  Välj test paket.  

5.  Analysera, Undersök och konvertera test paketen.  

6.  Testa de konverterade programmen.  

7.  Analysera och konvertera de återstående paketen (icke-test).  

8.  Exportera programmen från test miljön. Importera dem till produktions miljön.  

#### <a name="sample-plan-for-a-limited-resource-test-environment"></a><a name="bkmk_define-limited"></a>Exempel plan för en test miljö med begränsad resurs

Din test miljö har inte resurser, behörigheter och arkitektur som liknar din produktions miljö. Du kan inte analysera, testa och konvertera alla dina paket. I det här scenariot analyserar du bara, undersöker, konverterar och testar dina test paket. Migrera sedan återstående paket till produktions miljön för att analysera och konvertera. 

Paket konverterings planen kan se ut ungefär så här:

1.  Välj de paket som du vill konvertera.  

2.  Välj test paket.  

3.  Migrera test paketen till din test miljö.  

4.  Förbered test paketen för konvertering.  

5.  Analysera, Undersök och konvertera test paketen.  

6.  Testa de konverterade programmen.  

7.  Exportera test programmen från test miljön. Importera dem sedan till produktions miljön.  

8.  Migrera återstående paket till produktions miljön och Förbered dem för konvertering.  

9.  Analysera, Undersök och konvertera återstående paket i produktions miljön.  

10. Släpp de återstående programmen i produktions miljön.  


### <a name="select-and-prepare-packages-for-conversion"></a><a name="bkmk_prepare"></a>Välj och Förbered paket för konvertering

#### <a name="select-the-packages-that-you-want-to-convert"></a><a name="bkmk_prepare-select"></a>Välj de paket som du vill konvertera

Alla paket är inte lämpliga för att konverteras till program. Innan du börjar konvertera paket ska du identifiera de paket som inte kommer att konverteras. 

De bästa typerna av paket för konvertering till program är de som innehåller program vara som riktas mot användaren, till exempel:  

- Windows Installer-filer (. msi och. msu)  

- Program för Microsoft Application Virtualization (App-V)  

- Körbara Windows-filer (. exe)  

De typer av paket som är bäst bevarade som paket och inte konverteras till program är:

- Verktyg för system underhåll. Till exempel skript eller säkerhets kopierings verktyg.  

- Paket för program vara som inte stöds.

> [!Tip]  
> När du har identifierat paket som inte är lämpliga för att konvertera till program flyttar du dem till en separat mapp i Configuration Manager-konsolen. Så här skapar du en Package-mapp i Configuration Manager-konsolen:  
> - Högerklicka på noden **paket** .  
> - Välj **mappar**och välj sedan **Skapa mapp**.  
> - Ange mappens namn, till exempel `Not Converted`.  
> - Klicka på **OK**.  

#### <a name="prepare-the-packages-for-conversion"></a>Förbered paketen för konvertering

För varje paket som du vill konvertera kontrollerar du att de uppfyller följande villkor:  

- Käll filens plats är en fullständig UNC-sökväg, till `\\Server\Share\File`exempel.  

- Windows Installer-filer använder bara en unik produkt kod.  


### <a name="select-test-packages"></a><a name="bkmk_test"></a>Välj test paket

Om möjligt bör gruppen med test paket innehålla paket som uppfyller följande kriterier:  

- Minst ett test paket med beredskaps tillstånd **Automatisk**.  

- Minst ett test paket med beredskaps tillstånd **manuell**.  

Vi rekommenderar att dina test paket är kärn paket, till exempel:  

- Paket som du känner till väl.  

- Paket som är viktigast för din organisation.  

- Paket som du enkelt kan testa.  

Identifiera de paket som är lämpliga för testning. Flytta dem sedan till en separat mapp i Configuration Manager-konsolen.


### <a name="analyze-investigate-and-convert-packages"></a><a name="bkmk_analyze"></a>Analysera, Undersök och konvertera paket

#### <a name="analyze-packages"></a>Analysera paket

Om du vill analysera ett enskilt paket eller en liten grupp använder du Package Conversion Manager integrerad i Configuration Manager-konsolen. Mer information finns i [analysera och konvertera paket](how-to-analyze-and-convert.md).  

> [!NOTE]  
> Se noden **paket konverterings status** på arbets ytan **övervakning** . Den visar sammanfattnings information om analys-och konverterings processerna.  

#### <a name="investigate-analysis-results"></a>Undersök analys resultat

När du har analyserat test paketen kan du undersöka paketen med beredskaps status **manuell** eller **fel**. Fastställ skälen till att de har det aktuella läget. Några vanliga orsaker till beredskaps statusen **manuell** eller **fel** är:

- Paketet innehåller inte den information som krävs för att skapa en identifierings metod i en program distributions typ.  

- Paketet innehåller inte den information som krävs för att konvertera samlingar till globala villkor och krav.  

- Paketet innehåller fler än ett program.  

- Paketet är beroende av ett annat paket som du inte har konverterat till ett program.  

Om du vill ha mer information använder du följande resurser:  

- Granska fel meddelanden och korrigeringar i [teknisk referens för fel meddelanden i Package Conversion Manager](error-messages.md)  

- Granska logg filen **PCMtrace. log**  

- [Felsök Package Conversion Manager](troubleshoot-pcm.md)  

#### <a name="convert-the-packages"></a>Konvertera paketen

Mer information om hur du konverterar paket finns i [analysera och konvertera paket](how-to-analyze-and-convert.md).

> [!NOTE]  
> Se noden **paket konverterings status** på arbets ytan **övervakning** . Den visar sammanfattnings information om analys-och konverterings processerna.  


### <a name="test-and-deploy-the-applications"></a><a name="bkmk_deploy"></a>Testa och distribuera programmen

Testa programmen, antingen i din test miljö eller i produktions miljön, enligt den detaljerade paket konverterings planen.



## <a name="recommendations"></a>Rekommendationer

- Använd noden **paket konverterings status** på arbets ytan **övervakning** . Den visar sammanfattnings information om analys-och konverterings processerna.  

- Undersök programmen i dina paket som kallas omslag. Använd plugin-programmet Package Conversion Manager för att konvertera sina funktioner till motsvarande Configuration Manager-funktioner.  

- Kontrol lera att du testar varje konverterad app noggrant innan du distribuerar det i en produktions miljö.  



## <a name="next-steps"></a>Nästa steg

[Så här analyserar och konverterar du paket](how-to-analyze-and-convert.md)
