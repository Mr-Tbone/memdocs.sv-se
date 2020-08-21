---
title: 'Anpassa avbildningar av operativsystem '
titleSuffix: Configuration Manager
description: Använd Capture-och-build-aktivitetssekvenser, manuell konfiguration eller en kombination av båda för att anpassa en operativ system avbildning.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 95033a9b-ff13-4b70-b1de-bcb25bcb6024
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4f1d89707fa3e1765067c264d2abec12116bde88
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697729"
---
# <a name="customize-operating-system-images-with-configuration-manager"></a>Anpassa operativ system avbildningar med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Operativ system avbildningar i Configuration Manager är WIM-filer och representerar en komprimerad samling med säkerhetskopierade filer och mappar som krävs för att installera och konfigurera ett operativ system på en dator. En anpassad operativsystemavbildning byggs och sammanställs från en referensdator som du konfigurerar med alla nödvändiga operativsystemsfiler, stödfiler, programvaruuppdateringar, verktyg och andra filer och appar. Du bestämmer själv i vilken grad du konfigurerar referensdatorn manuellt. Du kan automatisera konfigurationen av referensdatorn helt och hållet genom att använda en aktivitetssekvens för att skapa och göra en avbildning. Du kan också konfigurera vissa aspekter av referensdatorn manuellt och automatisera resten med hjälp av aktivitetssekvenser. Om du vill kan du även konfigurera referensdatorn helt manuellt, utan aktivitetssekvenser. Använd följande avsnitt för att anpassa ett operativ system.

##  <a name="prepare-for-the--reference-computer"></a><a name="BKMK_PrepareReferenceComputer"></a> Förbereda för referens datorn  
 Innan du hämtar en operativsystemavbildning från en referensdator finns det några saker som du bör tänka på.  

###  <a name="decide-between-an-automated-or-manual-configuration"></a><a name="BKMK_RefComputerDecide"></a> Bestäm mellan en automatiserad eller manuell konfiguration  
 Här beskrivs för- och nackdelar med automatisk och manuell konfiguration av referensdatorn.  

#### <a name="automated-configuration"></a>Automatiserad konfigurering  
 **Fördelar**  

- Konfigureringen kan vara helt oövervakad. Ingen administratör eller användare behöver vara närvarande.  

- Du kan återanvända aktivitetssekvensen för att upprepa konfigureringen av ytterligare referensdatorer med hög tillförlitlighet.  

- Du kan ändra aktivitetssekvensen efter skillnader i referensdatorerna utan att behöva återskapa hela aktivitetssekvensen.  

  **Nackdelar**  

- Det kan ta lång tid att skapa och testa en aktivitetssekvens.  

- Om kraven på referensdatorn ändras i stor utsträckning kan det ta lång tid att bygga om och testa om aktivitetssekvensen.  

#### <a name="manual-configuration"></a>Manuell konfiguration  
 **Fördelar**  

- Du behöver inte skapa en aktivitetssekvens, och alltså inte heller testa och felsöka den.  

- Du kan installera direkt från CD-skivor utan att lägga alla program varu paket (inklusive Windows) i ett Configuration Manager-paket.  

  **Nackdelar**  

- Hur korrekt referensdatorns konfiguration är beror på administratören eller användaren som konfigurerat datorn.  

- Du måste själv verifiera och testa att referensdatorn är korrekt konfigurerad.  

- Du kan inte återanvända konfigureringsmetoden.  

- Kräver att en person är aktivt inblandad under hela processen.  

###  <a name="considerations-for-the-reference-computer"></a><a name="BKMK_RefComputerConsiderations"></a> Att tänka på för referens datorn  
 Här visas grundläggande saker att tänka på när du konfigurerar en referensdator.  

-   **Operativsystem som ska distribueras**  

     Det operativsystem som du avser att distribuera till måldatorerna måste vara installerat på referensdatorn. Mer information om de operativ system som du kan distribuera finns i [infrastruktur krav för operativ Systems distribution](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

-   **Lämpligt Service Pack**  

     Det operativsystem som du avser att distribuera till måldatorerna måste vara installerat på referensdatorn.  

-   **Lämpliga programuppdateringar**  

     Installera all programvara som du vill ha med i den operativsystemavbildning som du skapar från referensdatorn. Du kan även installera programvara när du distribuerar den skapade operativsystemavbildningen till måldatorerna.  

-   **Medlemskap i arbetsgrupp**  

     Referensdatorn måste vara konfigurerad som en medlem i en arbetsgrupp.  

-   **Funktionen**  

     Sysprep-verktyget (System Preparation) är en teknik som kan användas tillsammans med andra distributionsverktyg för att installera Windows-operativsystem på ny maskinvara. Sysprep förbereder en dator för diskavbildning eller leverans till kund genom att datorn konfigureras för att skapa en ny säkerhetsidentifierare (SID) för datorn när den startas om. Dessutom rensar Sysprep bort användar- och datorspecifika inställningar och data som inte får kopieras till en måldator.  

     Du kan köra Sysprep manuellt på måldatorn genom att köra följande kommando:  

     `Sysprep /quiet /generalize /reboot`  

     Alternativet /generalize instruerar Sysprep att ta bort systemspecifika data från Windows-installationen. Exempel på systemspecifik information är händelseloggar, unika säkerhetsidentifierare (SID) och annan unik information. Datorn startar när den unika systeminformationen tas bort.  

     Du kan automatisera Sysprep genom att använda aktivitetssekvenssteget [Förbered Windows för avbildning](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) eller avbildningsmedia.  

    > [!IMPORTANT]  
    >  Aktivitetssekvenssteget [Förbered Windows för avbildning](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) försöker återställa det lokala administratörslösenordet på referensdatorn till ett tomt värde innan Sysprep körs. Om den lokala säkerhetsprincipen **Lösenord måste uppfylla krav på komplexitet** aktiverats återställer det här aktivitetssekvenssteget inte administratörslösenordet. Inaktivera i så fall säkerhetsprincipen innan du kör aktivitetssekvensen.  

     Mer information om Sysprep finns i [Översikt över Sysprep (System preparation)](/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview).  

-   **Lämpliga verktyg och skript som krävs för att underlätta installationsscenarier**  

     Lämpliga verktyg och skript som krävs för att underlätta installationsscenarier  

-   **Lämplig skrivbordsanpassning, t.ex. bakgrund, organisationsanpassning och standardanvändarprofil**  

     Du kan konfigurera referensdatorn med de egenskaper för skrivbordsanpassning som du vill ta med när du skapar operativsystemavbildningen från referensdatorn. Exempel på skrivbordsegenskaper är bakgrund, företagsprofilering och en standardanvändarprofil.  

##  <a name="manually-build-a-reference-computer"></a><a name="BKMK_ManuallyBuildReference"></a> Bygga en referens dator manuellt  
 Följ stegen nedan om du vill bygga en referensdator manuellt.  

> [!NOTE]  
>  Om du bygger referensdatorn manuellt kan du skapa operativsystemavbildningen med avbildningsmedia. Mer information finns i [skapa avbildnings medier](../deploy-use/create-capture-media.md).  

#### <a name="to-manually-build-the-reference-computer"></a>Så här bygger du referensdatorn manuellt  

1. Identifiera den dator du vill använda som referensdator.  

2. Konfigurera referensdatorn med lämpligt operativsystem och eventuell annan programvara som krävs för att skapa den operativsystemavbildning du vill distribuera.  

   > [!WARNING]  
   >  Som minimum installerar du lämpligt operativsystem och Service Pack, drivrutiner som krävs samt nödvändiga programuppdateringar.  

3. Konfigurera referensdatorn så att den är medlem i en arbetsgrupp.  

4. Återställ det lokala administratörslösenordet på referensdatorn så att lösenordet är tomt.  

5. Kör Sysprep med kommandot: **sysprep/quiet / generalize/reboot**. Alternativet /generalize instruerar Sysprep att ta bort systemspecifika data från Windows-installationen. Exempel på systemspecifik information är händelseloggar, unika säkerhetsidentifierare (SID) och annan unik information. Datorn startar när den unika systeminformationen tas bort.  

   När referensdatorn är klar använder du en aktivitetssekvens för att skapa operativsystemavbildningen från referensdatorn.  Detaljerade anvisningar finns i [Skapa en operativsystemavbildning från en befintlig referensdator](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_CaptureExistingRefComputer).  

##  <a name="use-a-task-sequence-to-build-a-reference-computer"></a><a name="BKMK_UseTSToBuildReference"></a> Använda en aktivitetssekvens för att bygga en referens dator  
 Du kan automatisera processen med att skapa en referensdator genom att använda en aktivitetssekvens för att distribuera operativsystemet, drivrutiner, program och så vidare.  När referensdatorn är klar använder du följande steg för att skapa operativsystemavbildningen från referensdatorn.  

-   Använd en aktivitetssekvens för att bygga och avbilda operativsystemavbildningen från referensdatorn.  Mer detaljerad information finns i [Använd en aktivitetssekvens för att bygga och avbilda en referensdator](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_BuildCaptureTS).