---
title: Kravkontrollerare
titleSuffix: Configuration Manager
description: Lär dig hur du använder krav kontrollen för att identifiera och åtgärda problem som kan blockera installation av en plats eller plats system roll.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1ee871d99285bee3a4489d88bf0d203bf74cde3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718177"
---
# <a name="prerequisite-checker-for-configuration-manager"></a>Krav kontroll för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

 Innan du kör installations programmet för att installera eller uppgradera en Configuration Manager plats eller innan du installerar en plats system roll på en ny server kan du använda det här fristående programmet (**prereqchk. exe**) från den version av Configuration Manager som du vill använda för att kontrol lera Server beredskap. Använd krav kontrollen för att identifiera och åtgärda problem som blockerar en plats-eller plats system roll installation.  

> [!NOTE]  
>  Krav kontrollen körs alltid som en del av installationen.  

Som standard när krav kontrollen körs:  

-   Den verifierar servern där den körs.  
-   Den lokala datorn genomsöks efter en befintlig plats Server och endast de kontroller som är tillämpliga på platsen körs.  
-   Om inga befintliga platser hittas körs alla nödvändiga regler.  
-   Det kontrollerar regler för att kontrol lera att program varan och inställningarna som krävs för installationen är installerade. Det är möjligt att nödvändig program vara kräver ytterligare konfigurations-eller program uppdateringar som inte verifieras av krav kontrollen.  
-   Det loggar resultatet i filen **ConfigMgrPrereq. log** på datorns systemen het. Logg filen kan innehålla ytterligare information som inte visas i program gränssnittet.  

När du kör krav kontrollen i en kommando tolk och anger specifika kommando rads alternativ:  

-   Krav kontrollen utför bara de kontroller som är associerade med den plats Server eller de plats system som du anger på kommando raden.  
-   Ditt användar konto måste ha administratörs rättigheter till fjärrdatorn för att kunna kontrol lera en fjärrdator.  

Mer information om de kontroller som krav kontrollen utför finns i [lista över nödvändiga kontroller för Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>Kopiera nödvändiga kontroll filer till en annan dator  

1.  Gå till någon av följande platser i Utforskaren:  

    -   **&lt;*Configuration Manager installationsmedia*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager installations Sök väg*\>\BIN\X64**  

2.  Kopiera följande filer till målmappen på den andra datorn:  

    - prereqchk. exe
    - prereqcore. dll
    - prereqchkres. dll
      - Den här filen finns i undermappen för installations språket. Till exempel är engelska i `00000409` undermappen. <!--586808-->
    - basesql. dll
    - basesvr. dll
    - baseutil. dll

##  <a name="run-prerequisite-checker-with-default-checks"></a>Kör krav kontrollen med standard kontroller  

1.  Gå till någon av följande platser i Utforskaren:  

    -   **&lt;*Configuration Manager installationsmedia*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager installations Sök väg*\>\BIN\X64**  

2.  Kör **prereqchk. exe** för att starta krav kontrollen.   
    Krav kontrollen identifierar befintliga-platser och kontrollerar om det finns någon sökning efter uppgraderings beredskap. Om inga platser hittas utförs alla kontroller. I kolumnen **typ av webbplats** finns information om den plats Server eller det plats system som regeln är associerad med.  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>Kör krav kontrollen från en kommando tolk för alla standard kontroller  

1.  Öppna ett kommando tolks fönster och ändra kataloger till någon av följande platser:  

    -   **&lt;*Configuration Manager installationsmedia*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager installations Sök väg*\>\BIN\X64**  

2.  Starta krav kontrollen genom att skriva **prereqchk. exe/Local** och kör alla krav kontroller på servern.  

## <a name="run-prerequisite-checker-from-a-command-prompt-to-use-options"></a>Kör krav kontrollen från en kommando tolk för att använda alternativen  

1. Öppna ett kommando tolks fönster och ändra kataloger till någon av följande platser:  

   -   **&lt;*Configuration Manager installationsmedia*\>\SMSSETUP\BIN\X64**  
   -   **&lt;*Configuration Manager installations Sök väg*\>\BIN\X64**  

2. Ange **prereqchk. exe** med tillägg av ett eller flera av följande kommando rads alternativ.  

   Om du till exempel vill kontrol lera en primär plats kan du använda följande:  

      **prereqchk. exe [/NOUI]/PRI/SQL &lt;fqdn för SQL Server\> /SDK &lt;FQDN för SMS-\> Provider [ &lt;/Join FQDN för central administrations\>webbplats] &lt;[/MP FQDN för\>hanterings plats &lt;] [/DP FQDN\>för distributions plats]**  

   **Central administrations plats Server:**  

   -   **/NOUI**  

        Krävs inte. Startar krav kontrollen utan att Visa användar gränssnittet. Du måste ange det här alternativet före andra alternativ på kommando raden.  

   -   **/CAS**  

        Krävs. Kontrollerar att den lokala datorn uppfyller kraven för den centrala administrations platsen.  

   -   **/SQL &lt; *FQDN för SQL Server*>**  

        Krävs. Genom att använda det fullständigt kvalificerade domän namnet (FQDN) kontrollerar du att den angivna datorn uppfyller kraven för SQL Server som värd för Configuration Manager plats databasen.  

   -   **/SDK &lt; *FQDN för SMS-provider*>**  

        Krävs. Kontrollerar att den angivna datorn uppfyller kraven för SMS-providern.  

   -   **/Ssbport**  

        Krävs inte. Kontrollerar att ett brand Väggs undantag är aktiverat för att tillåta kommunikation på SSB-porten (SQL Server Service Broker). Standard porten för SSB är 4022.  

   -   **INSTALLDIR &lt; *Configuration Manager installations Sök väg*>**  

        Krävs inte. Kontrollerar det minsta disk utrymme som krävs för plats installationen.  

   **Primär plats Server:**  

   -   **/NOUI**  

       Krävs inte. Startar krav kontrollen utan att Visa användar gränssnittet. Du måste ange det här alternativet före andra alternativ på kommando raden.  

   -   **/PRI**  

        Krävs. Kontrollerar att den lokala datorn uppfyller kraven för den primära platsen.  

   -   **/SQL &lt; *FQDN för SQL Server*>**  

        Krävs. Kontrollerar att den angivna datorn uppfyller kraven för SQL Server att vara värd för Configuration Manager-plats databasen.  

   -   **/SDK &lt; *FQDN för SMS-provider*>**  

        Krävs. Kontrollerar att den angivna datorn uppfyller kraven för SMS-providern.  

   -   **/Join &lt; *FQDN för central administrations webbplats*>**  

        Krävs inte. Kontrollerar att den lokala datorn uppfyller kraven för att ansluta till den centrala administrations plats servern.  

   -   **/MP &lt; *FQDN för hanterings plats*>**  

        Krävs inte. Kontrollerar att den angivna datorn uppfyller kraven för hanterings platsens plats system roll. Det här alternativet stöds bara när du använder alternativet **/PRI** .  

   -   **/DP &lt; *FQDN för distributions plats*>**  

        Krävs inte. Kontrollerar att den angivna datorn uppfyller kraven för plats system rollen för distributions platsen. Det här alternativet stöds bara när du använder alternativet **/PRI** .  

   -   **/Ssbport**  

        Krävs inte. Kontrollerar att ett brand Väggs undantag är aktiverat för att tillåta kommunikation på SSB-porten. Standard porten för SSB är 4022.  

   -   **INSTALLDIR &lt; *Configuration Manager installations Sök väg*>**  

        Krävs inte. Kontrollerar det minsta disk utrymme som krävs för plats installationen.  

   **Sekundär plats Server:**  

   -   **/NOUI**  

        Krävs inte. Startar krav kontrollen utan att Visa användar gränssnittet. Du måste ange det här alternativet före andra alternativ på kommando raden.  

   -   **/SEK &lt; *FQDN för sekundär plats Server*>**  

        Krävs. Kontrollerar att den angivna datorn uppfyller kraven för den sekundära platsen.  

   -   **/INSTALLSQLEXPRESS**  

        Krävs inte. Verifierar att SQL Server Express kan installeras på den angivna datorn.  

   -   **/Ssbport**  

        Krävs inte. Kontrollerar att ett brand Väggs undantag är aktiverat för att tillåta kommunikation för SSB-porten. Standard porten för SSB är 4022.  

   -   **/Sqlport**  

        Krävs inte. Kontrollerar att ett brand Väggs undantag är aktiverat för att tillåta kommunikation för SQL Server-tjänstens port och att porten inte används av en annan namngiven instans av SQL Server. Standardporten är 1433.  

   -   **INSTALLDIR &lt; *Configuration Manager installations Sök väg*>**  

        Krävs inte. Kontrollerar det minsta disk utrymme som krävs för plats installationen.  

   -   **/SourceDir**  

        Krävs inte. Kontrollerar att dator kontot för den sekundära platsen har åtkomst till den mapp som är värd för källfilerna för installation.  

   **Configuration Manager-konsol:**  

   -   **/Adminui**  

        Krävs. Kontrollerar att den lokala datorn uppfyller kraven för att installera Configuration Manager.  

3. I användar gränssnittet för krav kontroll skapar krav kontrollen en lista över identifierade problem i avsnittet **krav resultat** .  

   -   Klicka på ett objekt i listan om du vill ha mer information om hur du löser problemet.  
   -   Du måste lösa alla objekt i listan med **fel** status innan du installerar plats servern, plats systemet eller Configuration Manager-konsolen.  
   -   Du kan också öppna filen **ConfigMgrPrereq. log** i system enhetens rot och granska resultatet från krav kontrollen. Logg filen kan innehålla ytterligare information som inte visas i användar gränssnittet för krav kontroll.  
