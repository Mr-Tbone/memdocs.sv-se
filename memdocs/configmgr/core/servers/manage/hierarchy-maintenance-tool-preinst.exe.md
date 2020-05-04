---
title: Verktyget underhåll av hierarki
titleSuffix: Configuration Manager
description: Förstå vad verktyget underhåll av hierarki gör och varför du kan använda det. Innehåller referens för kommando rads alternativ.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cead6825-6113-4ba5-a381-ac3598dfee86
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b564575dfc135a9c82c7e102a02d70f1b6dbf6eb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712444"
---
# <a name="hierarchy-maintenance-tool-preinstexe-for-configuration-manager"></a>Verktyget underhåll av hierarki (Preinst. exe) för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Verktyget underhåll av hierarki (Preinst. exe) skickar kommandon till Configuration Manager Hierarchy-hanteraren medan hierarkin Manager-tjänsten körs. Verktyget underhåll av hierarki installeras automatiskt när du installerar en Configuration Manager-plats. Du hittar Preinst. \\ &lt;exe i den delade mappen *SiteServerName*> \&lt;SMS_*SiteCode*\bin\X64\00000409 på plats servern.  

 Du kan använda verktyget Underhåll av hierarki i följande situationer:  

-   När säker nyckelutväxling krävs finns det situationer där du måste utföra den första utväxlingen av publika nycklar mellan platser manuellt. Mer information finns i [Utväxla publika nycklar mellan platser manuellt](#BKMK_ManuallyExchangeKeys) i det här ämnet.  

-   För att ta bort aktiva jobb som är för ett mål som inte längre är tillgängligt.  

-   För att ta bort en plats Server från Configuration Manager-konsolen när du inte kan avinstallera platsen med hjälp av installations programmet. Om du till exempel fysiskt tar bort en Configuration Manager plats utan att först köra installations programmet för att avinstallera platsen, finns plats informationen kvar i den överordnade platsens databas och den överordnade platsen fortsätter att försöka kommunicera med den underordnade platsen. För att lösa det här problemet måste du köra verktyget underhåll av hierarki och manuellt ta bort den underordnade platsen från den överordnade platsens databas.  

-   För att stoppa alla Configuration Manager-tjänster på en plats utan att behöva stoppa tjänsterna individuellt.  

-   När du återställer en plats kan du använda alternativet CHILDKEYS för att distribuera de publika nycklarna från flera underordnade platser till den plats som återställs.  

Den nuvarande användaren måste ha administrationsbehörighet på den lokala datorn för att köra verktyget Underhåll av hierarki. Användaren måste också explicit ha säkerhetsbehörigheten Plats - Administrera. Det räcker inte att användaren ärver den här behörigheten genom att vara medlem i en grupp som har behörigheten.  

## <a name="hierarchy-maintenance-tool-command-line-options"></a>Kommandoradsalternativ för verktyget Underhåll av hierarki  
När du använder verktyget Underhåll av hierarki måste du köra det lokalt på den centrala administrationsplatsen, den primära platsen eller en sekundär platsserver.  

När du kör verktyget underhåll av hierarki måste du använda följande syntax: Preinst. exe/&lt;alternativ.\> Följande är kommandoradsalternativ.  

 **> /DELJOB &lt; *SiteCode* ** – Använd det här alternativet på en plats för att ta bort alla jobb eller kommandon från den aktuella platsen till den angivna mål platsen.  

 **/DELSITE &lt;- *underordnadplatssomtasbort* > ** – Använd det här alternativet på en överordnad plats för att ta bort data för underordnade platser från plats databasen för den överordnade platsen. Normalt använder du det här alternativet om en platsserverdator tas ur drift innan du avinstallerat platsen från den.  

> [!NOTE]  
>  Alternativet /DELSITE avinstallerar inte platsen från den dator som anges av parametern UnderordnadPlatsSomTasBort. Det här alternativet tar bara bort plats informationen från Configuration Manager plats databasen.  

**> /Dump &lt; *SiteCode* ** – Använd det här alternativet på den lokala plats servern för att skriva plats kontroll bilder till rotmappen på den enhet där platsen är installerad. Du kan skriva en specifik platskontrollbild till mappen eller skriva alla platskontrollfiler i hierarkin.  

-   /DUMP &lt; *SiteCode*> skriver endast plats kontroll bilden för den angivna platsen.  

-   /DUMP skriver platskontrollfiler för alla platser.  

En avbildning är en binär representation av plats kontroll filen, som lagras i Configuration Manager plats databasen. Den dumpade platskontrollfilavbildningen är en summa av basavbildningen plus väntande förändringsavbildningar.  

Efter dumpning av en plats kontroll fil avbildning med verktyget underhåll av hierarki är fil namnet i formatet sitectrl_&lt;*SiteCode*>. CT0.  

**/STOPSITE** – Använd det här alternativet på den lokala plats servern för att starta en avslutnings cykel för tjänsten Configuration Manager Platskomponenthanteraren som delvis återställer platsen. När den här avstängnings cykeln körs stoppas vissa Configuration Manager-tjänster på en plats Server och dess fjärrplatssystem. Tjänsterna flaggas för ominstallation. En konsekvens av nedstängningscykeln är att vissa lösenord automatiskt ändras när tjänsterna installeras om.  

> [!NOTE]  
>  Om du vill se en lista med nedstängningar, ominstallationer och lösenordsändringar för Platskomponenthanteraren aktiverar du loggning för den här komponenten innan du använder det här kommandoradsalternativet.  

När nedstängningscykeln har startats fortsätter den automatiskt. Komponenter och datorer som inte svarar hoppas över. Men om tjänsten Platskomponenthanteraren inte kan komma åt ett fjärrplatssystem under nedstängningscykeln, kommer de komponenter som installeras på fjärrplatssystemet att installeras om när tjänsten Platskomponenthanteraren startas om. När den startas om försöker tjänsten Platskomponenthanteraren installera om alla tjänster som flaggats för ominstallation ända tills den lyckas.  

Du kan starta om tjänsten Platskomponenthanteraren med Service Manager. När den startats om kommer alla påverkade tjänster att avinstalleras, installeras om och startas om. När du har använt alternativet /STOPSITE för att starta nedstängningscykeln kan du inte undvika ominstallationscyklerna när tjänsten Platskomponenthanteraren startas om.  

**/KEYFORPARENT** – Använd det här alternativet på en plats för att distribuera platsens publika nyckel till en överordnad plats.  

Alternativet/keyforparent placerar platsens publika nyckel i filen &lt; *SiteCode*>. CT4 i roten på program fil enheten. När du har kört Preinst. exe med det här alternativet kopierar &lt;du *SiteCode*> manuellt. CT4-filen till den överordnade platsens. ..\Inboxes\hman.Box-mapp (inte hman. box\pubkey).  

**/KEYFORCHILD** – Använd det här alternativet på en plats för att distribuera platsens publika nyckel till en underordnad plats.  

Alternativet/keyforchild placerar platsens publika nyckel i filen &lt; *SiteCode*>. CT5 i roten på program fil enheten. När du har kört Preinst. exe med det här alternativet kopierar &lt;du *SiteCode*> manuellt. CT5-fil till den underordnade platsens. ..\Inboxes\hman.Box-mapp (inte hman. box\pubkey).  

**/CHILDKEYS** – Du kan använda det här alternativet på underordnade platser till en plats som du återställer. Använd det här alternativet på en plats för att distribuera publika nycklar från flera underordnade platser till den plats som återställs.  

Alternativet/CHILDKEYS placerar nyckeln från den plats där du kör alternativet, och alla de underordnade platserna offentliga nycklar till filen &lt; *SiteCode*>. CT6.  

När du har kört Preinst. exe med det här alternativet kopierar &lt;du *SiteCode*> manuellt. CT6-fil till den plats där platsens ..\Inboxes\hman.Box-mapp (inte hman. box\pubkey) återställs.  

**/PARENTKEYS** – Du kan använda det här alternativet på den överordnade platsen till en plats som du återställer. Använd det här alternativet på en plats för att distribuera publika nycklar från alla överordnade platser till den plats som återställs.  

Alternativet/PARENTKEYS placerar nyckeln från den plats där du kör alternativet, och nycklarna från varje överordnad plats ovanför platsen i filen &lt;SiteCode.\> CT7.  

När du har kört Preinst. exe med det här alternativet kopierar &lt;du *SiteCode*> manuellt. CT7-fil till den plats där platsens ..\Inboxes\hman.Box-mapp (inte hman. box\pubkey) återställs.  

##  <a name="manually-exchange-public-keys-between-sites"></a><a name="BKMK_ManuallyExchangeKeys"></a>Utväxla offentliga nycklar mellan platser manuellt  
Som standard är alternativet **Kräv säkert nyckel utbyte** aktiverat för Configuration Manager-platser. När säker nyckelutväxling krävs finns det två situationer där du måste utföra den första utväxlingen av nycklar mellan platser manuellt:  

-   Om Active Directory-schemat inte har utökats för Configuration Manager  

-   Configuration Manager platser publicerar inte plats data till Active Directory  

Du kan använda verktyget Underhåll av hierarki för att exportera de publika nycklarna för varje plats. När de har exporterats måste du manuellt utväxla nycklar mellan platserna.  

> [!NOTE]  
>  När de publika nycklarna har utväxlats manuellt kan du titta i loggfilen **hman.log**, som registrerar ändringar i platskonfigurationen och platsinformation som publiceras till Active Directory Domain Services, på den överordnade platsservern för att kontrollera att den primära platsen har behandlat den nya publika nyckeln.  

#### <a name="to-manually-transfer-the-child-site-public-key-to-the-parent-site"></a>Överföra den underordnade platsens publika nyckel till den överordnade platsen manuellt  

1.  Logga in på den underordnade platsen. Öppna en kommandotolk och gå till platsen där **Preinst.exe** finns.  

2.  Skriv följande för att exportera den underordnade platsens publika nyckel: **Preinst/keyforparent**  

3.  Alternativet/keyforparent placerar den underordnade platsens publika nyckel i ** &lt;plats koden\>. CT4** -fil som finns i roten på system enheten.  

4.  Flytta ** &lt;plats koden\>. CT4** -filen till den överordnade platsens ** &lt;installations\>katalog \Inboxes\hman.Box** -mapp.  

#### <a name="to-manually-transfer-the-parent-site-public-key-to-the-child-site"></a>Överföra den överordnade platsens publika nyckel till den underordnade platsen manuellt  

1.  Logga in på den överordnade platsen. Öppna en kommandotolk och gå till platsen där **Preinst.exe** finns.  

2.  Skriv följande för att exportera den överordnade platsens publika nyckel: **Preinst/keyforchild**.  

3.  Alternativet/keyforchild placerar den överordnade platsens publika nyckel i ** &lt;plats koden\>. CT5** -fil som finns i roten på system enheten.  

4.  Flytta ** &lt;plats koden\>. CT5** -fil till katalogen för ** &lt;installations katalogen\>\Inboxes\hman.Box** på den underordnade platsen.  
