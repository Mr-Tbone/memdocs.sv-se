---
title: 'Installera en plats med 1606-bas mediet '
titleSuffix: Configuration Manager
description: Installera eller uppgradera till LTSB för System Center Configuration Manager.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d70611aff329f48c8223a47dfa238e5a4559972
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722804"
---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media"></a>Installera och uppgradera med version 1606 bas linje medium

*Gäller för: System Center Configuration Manager (långsiktig service gren)*

När du kör installations programmet från baseline-mediet för version 1606 för Configuration Manager kan du installera en långsiktig etablerings plats för System Center Configuration Manager.

Bas linje mediet är tillgängligt på DVD som en del av Microsoft System Center 2016 eller från System Center Configuration Manager långsiktigt underhålls gren version 1606. Mer information om bas linje medier finns i [bas linje-och uppdaterings versioner](../servers/manage/updates.md#bkmk_Baselines).


När du använder version 1606-bas linje mediet är den plats som du installerar eller uppgraderar till:
- En *Current Branch plats* som motsvarar en plats som först installerades med 1511-bas mediet och sedan uppdaterats till version 1606 plus den samlade uppdateringen av 1606-KB3186654.
- En *LTSB-plats* som motsvarar den Current Branch plats som kör version 1606 plus uppdateringen av 1606 Hotfix-KB3186654. Bas linje mediet innehåller redan samlad snabb korrigering.  Men LTSB har inte stöd för alla funktioner eller funktioner som är tillgängliga med Current Branch, enligt beskrivningen i [Introduktion till den långsiktiga service grenen för System Center Configuration Manager](introduction-to-the-ltsb.md).

Om du inte är bekant med de olika Configuration Managers grenar kan du se [vilken gren av Configuration Manager ska jag använda](which-branch-should-i-use.md).




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Ändringar i installationen med 1606-bas mediet
1606-bas linje mediet presenterar följande ändringar i installationen av Configuration Manager.

### <a name="branch-and-edition"></a>Gren och version
När du kör installations programmet visas nu en licens sida där du kan välja den gren av Configuration Manager som du vill installera. Du kan välja antingen Current Branch eller LTSB som en licensierad installation, eller så kan du välja en utvärderings version av Current Branch som en icke-licensierad installation.

Mer information finns i [licensiering och filialer för Configuration Manager](learn-more-editions.md).

### <a name="software-assurance-expiration"></a>Förfallo datum för Software Assurance
Under installationen har du möjlighet att ange värdet för **förfallo datum för Software Assurance** . Detta är ett valfritt värde som du kan ange som en bekväm påminnelse.

> [!NOTE]
> Microsoft validerar inte det utgångs datum som du anger och kommer inte att använda det här datumet för licens validering.  I stället kan du använda den som en påminnelse om ditt förfallo datum. Detta är användbart eftersom Configuration Manager regelbundet söker efter nya program uppdateringar online och din licens status för Software Assurance måste vara aktuell för att kunna använda dessa ytterligare uppdateringar.    

- Du kan ange datumvärdet på sidan **produkt nyckel** i installations guiden när du kör installations programmet från Configuration Manager version 1606-original medium.
- Du kan också ange det här datumet genom att välja **Inställningar för hierarkins egenskaper** > **licensiering** i Configuration Manager-konsolen.

Mer information finns i "Software Assurance-avtal" i [licensiering och filialer för Configuration Manager](learn-more-editions.md).


### <a name="additional-pre-upgrade-configurations"></a>Ytterligare konfigurationer före uppgradering
Innan du påbörjar en uppgradering av System Center 2012 Configuration Manager till LTSB måste du utföra följande ytterligare steg som en del av check listan före uppgradering.  
Avinstallera de plats system roller som LTSB inte stöder:
- Plats för synkronisering av tillgångsinformation
- Microsoft Intune Connector
- Molnbaserade distributionsplatser

Mer information finns i [Uppgradera till Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md).


### <a name="new-scripted-installation-options"></a>Nya installations alternativ för skript
Version 1606-bas linje media har stöd för en ny obevakad skript fil nyckel för skriptbaserade installationer av en ny plats på den översta nivån. Detta gäller för att installera en ny fristående primär plats eller lägga till en central administrations plats som en del av ett scenario för plats expansion.

När du använder ett obevakat skript för att installera en licensierad gren måste du lägga till följande avsnitt, nyckel namn och värden i avsnittet alternativ i skriptet. Du behöver inte använda dessa värden för att skripta installationen av en utvärderings version av Current Branch:  

 **SABranchOptions**
- **Nyckel namn: SAActive**
  - Värden: 0 eller 1.  
  - Information: 0 installerar en icke-licensierad utvärderings version av Current Branch, och 1 installerar en licensierad version.   

- **CurrentBranch**
  - Värden: 0 eller 1.  
  - Information: 0 installerar den långsiktiga service grenen och 1 installerar Current Branch.  

Om du till exempel vill installera en licensierad Current Branch-utgåva använder du:

**Nyckel namn: SABranchOptions**
- **SAActive = 1**
- **CurrentBranch = 1**


> [!IMPORTANT]  
> **SABranchOptions** fungerar bara med installations programmet från bas linje mediet. Den gäller inte när du kör installations programmet från CD: n. Den senaste mappen på en plats som du tidigare har installerat med hjälp av version 1606-bas linje mediet.
>
> **SABranchOptions** gäller inte för skriptbaserade uppgraderingar från System Center 2012 Configuration Manager och resulterar alltid i Current Branch.

Mer information finns i [använda en kommando rad för att installera Configuration Manager-platser](../servers/deploy/install/use-a-command-line-to-install-sites.md).


## <a name="install-a-new-site"></a>Installera en ny plats
När du använder 1606-baseline-mediet för att installera en ny plats för någon av grenarna, använder du de plats planerings-, förberedelse-och installations procedurer som beskrivs i avsnittet [installera Configuration Manager platser](../servers/deploy/install/installing-sites.md) med tillägg av följande överväganden för installation:

- Under installationen måste du välja den gren av Configuration Manager som du vill installera och du kan ange information om ditt Software Assurance-avtal.
- Alla platser i samma hierarki måste köra samma gren. Det finns inte stöd för att ha en hierarki med en blandning av LTSB och Current Branch på olika platser.
- Ny skriptad installation. Mer information finns i avsnittet nya installations alternativ för skript tidigare i den här artikeln.

## <a name="expand-a-stand-alone-primary-site"></a>Expandera en fristående primär plats
Du kan expandera en fristående primär plats som kör LTSB.  Processen skiljer sig inte från den som används för en Current Branch webbplats med ett villkor:

- När du installerar den nya centrala administrations platsen måste du använda installations programmet från det ursprungliga käll mediet som du använde för att installera LTSB-platsen. Kör installations programmet från CD: n. Den senaste mappen för det här scenariot stöds inte.

Mer information om hur du expanderar en plats finns i "expandera en fristående primär plats" i [installera en plats med hjälp av installations guiden](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md).

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>Uppgradera från System Center 2012 Configuration Manager
När du uppgraderar från System Center 2012 Configuration Manager använder du plats planering, förberedelser och procedurer som dokumenteras i avsnittet [Uppgradera till Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md) , men med följande ändringar:

**Uppgradera till Current Branch:**
- Under installationen måste du välja Current Branch och du kan ange information om ditt Software Assurance-avtal.
- Ny skriptad installation. Mer information finns i avsnittet nya installations alternativ för skript tidigare i den här artikeln.

**Uppgradera till LTSB:**  
- Ytterligare steg för att följa i check listan före uppgradering.
- Under installationen måste du välja LTSB och du kan ange information om ditt Software Assurance-avtal.
- Du kan bara uppgradera en plats som kör System Center 2012 Configuration Manager med Service Pack 1, System Center 2012 Configuration Manager med Service Pack 2, System Center 2012 R2 Configuration Manager med Service Pack 1 eller System Center 2012 R2 Configuration Manager utan service pack.

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>Uppgraderings vägar på plats för 1606-bas linje mediet
Du kan använda 1606-bas mediet för att uppgradera följande till en licensierad version av Configuration Manager:
- System Center 2012 R2 Configuration Manager med Service Pack 1
- System Center 2012 R2 Configuration Manager utan service pack (Detta kräver att bas linje medier används för version 1606 som gavs ut igen den 15 december 2016.)
- System Center 2012 Configuration Manager med Service Pack 2
- System Center 2012 Configuration Manager med Service Pack 1 (Detta kräver att bas linje medier används för version 1606 som gavs ut igen den 15 december 2016.)


Du kan också använda det här mediet för att uppgradera en icke-licensierad utvärderings version av Current Branch till en fullständigt licensierad version av Current Branch.

Det här mediet stöder inte uppgradering av:
- Andra versioner av System Center 2012 Configuration Manager.
- Configuration Manager 2007 eller tidigare.
- En Release Candidate-installation av Configuration Manager.

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>Om CD: n. Senaste mappen och LTSB
Följande är begränsningar när du använder media som Configuration Manager skapar på CD: n. Den senaste mappen på plats servern. Dessa begränsningar gäller för webbplatser som kör LTSB:

Mediet i CD-skivan. Den senaste mappen stöds för:
- Site Recovery.
- Plats underhåll.
- Installerar ytterligare underordnade primära platser.

Mediet i CD-skivan. Den senaste mappen stöds inte för:  
- Installera en central administrations plats som en del av scenariot för plats expansion.

Mer information finns [på CD-skivan. Senaste mappen](../servers/manage/the-cd.latest-folder.md).

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>Säkerhets kopiering, återställning och plats underhåll för LTSB
Om du vill säkerhetskopiera, återställa eller köra plats underhåll på en plats som kör LTSB, använder du vägledning och procedurer från [säkerhets kopiering och återställning för Configuration Manager](../servers/manage/backup-and-recovery.md).  

Använd installations programmet för Configuration Manager från CD-skivan. Den senaste mappen för säkerhets kopiering av din LTSB-webbplats.
