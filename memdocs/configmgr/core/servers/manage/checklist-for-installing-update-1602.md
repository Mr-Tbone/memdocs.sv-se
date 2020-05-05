---
title: Check lista för 1602
titleSuffix: Configuration Manager
description: Lär dig mer om åtgärder som ska vidtas innan du uppdaterar från Configuration Manager version 1511 till version 1602.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b63ef197-01f0-4894-b929-5ef8403c5195
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b330c4049dce06b1e47d1088993b09ec16e724a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717862"
---
# <a name="checklist-for-installing-update-1602-for-configuration-manager"></a>Check lista för att installera uppdatering 1602 för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Innan du uppdaterar från Configuration Manager version 1511 till version 1602 bör du läsa följande information och check lista för åtgärder som ska vidtas innan du startar uppdateringen.  

 **Om att installera uppdatering 1602:**  

 Uppdatering 1602 kan bara installeras på den högsta nivån i hierarkin. Det innebär att du startar installationen från den centrala administrations platsen om du har en, eller från din fristående primära plats.  

-   Underordnade primära platser installerar uppdateringen automatiskt när den centrala administrations platsen har slutfört installationen av uppdateringen. Du kan använda underhålls fönster för att styra när en plats installerar uppdateringar. Från och med lanseringen av uppdatering 1602 har underhålls Fönstren bytt namn till *service fönster*. Mer information finns i [Service Windows for Site servers](service-windows.md).  

-   Du måste manuellt uppdatera sekundära platser inifrån Configuration Manager-konsolen när den primära överordnade platsen har slutfört installationen av uppdateringen. Automatiska uppdateringar av sekundära plats servrar stöds inte.  

När plats servern installerar uppdateringen uppdateras plats system roller som är installerade på plats servern och de som är installerade på fjärrdatorer automatiskt. Innan du installerar uppdateringen måste du därför kontrol lera att varje plats system Server uppfyller eventuella nya krav för åtgärder med den nya uppdaterings versionen.  

Första gången du använder en Configuration Manager-konsol när uppdateringen är färdig uppmanas du att uppdatera konsolen. För att göra det måste du köra Configuration Manager-installationen på den dator som är värd för konsolen och välja alternativet för att uppdatera konsolen. Vi rekommenderar att du inte väntar med att installera uppdateringen av konsolen.  

 **Initialiseringschecklistan**  

 **Se till att alla platser kör en version av Configuration Manager som stöds:**  Varje plats server i hierarkin måste köra Configuration Manager version 1511 innan du kan starta installationen av uppdatering 1602.  

 **Granska installerade Microsoft .net-versioner på plats system servrar:** När en plats installerar uppdatering 1602 installeras Configuration Manager automatiskt .NET Framework 4.5.2 på varje dator som är värd för någon av följande plats system roller (om .NET Framework 4,5 eller senare inte redan är installerad):  

-   Registreringsproxyplats  

-   Registreringsplats  

-   Hanteringsplats  

-   Tjänstanslutningspunkt  

Den här installationen kan försätta plats system servern i ett väntande tillstånd för omstart och rapportera fel till visnings programmet för Configuration Manager komponent status. Dessutom kan .NET-program på servern uppleva slumpmässiga problem innan servern startas om.  

 Mer information finns i [krav för plats och plats system](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Granska statusen för platsen och hierarkin och kontrollera om det finns några fel som inte har åtgärdats:** Innan du uppdaterar en plats löser du alla operativa problem som finns på platsservern, platsdatabasservern och i platssystemrollerna som är installerade på fjärrdatorer. En platsuppgradering kan misslyckas på grund av befintliga operativa problem.  

Mer information finns i [använda aviseringar och status systemet för Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Granska fil- och datareplikeringen mellan platser:**  Se till att fil- och databasreplikeringen mellan platser fungerar och är aktuell. Fördröjningar eller efter släpning i kan antingen förhindra en smidig och lyckad uppdatering.    

För databasreplikering kan du använda funktionen för replikeringslänkanalys för att lösa eventuella fel innan du startar uppdateringen.    

 Mer information finns i [om Replikeringslänkanalys](monitor-replication.md#BKMK_RLA).  

 **Installera alla tillämpliga viktiga uppdateringar för operativ system på datorer som är värdar för platsen, plats databas servern och fjärrplatsens system roller:** Innan du installerar en uppdatering för Configuration Manager bör du installera eventuella kritiska uppdateringar för varje tillämpligt plats system. Om en uppdatering som du installerar kräver en omstart, startar du om de tillämpliga datorerna innan du påbörjar uppgraderingen.  

 **Inaktivera databas repliker för hanterings platser på primära platser:** Configuration Manager kan inte uppdatera en primär plats som har en databas replik för hanterings platser aktive rad. Inaktivera databasreplikering innan du:  

-   Skapa en säkerhets kopia av plats databasen för att testa databas uppgraderingen.  

-   Installera en uppdatering för Configuration Manager.  

Mer information finns i [databas repliker för hanterings platser för Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Konfigurera om program uppdaterings platser som använder NLB:** Configuration Manager kan inte uppdatera en plats som använder ett NLB-kluster (utjämning av nätverks belastning) som värd för program uppdaterings platser.  Om du använder NLB-kluster för program uppdaterings platser kan du använda Windows PowerShell för att ta bort NLB-klustret.    

 Mer information finns i [Planera för program uppdateringar](../../../sum/plan-design/plan-for-software-updates.md).  

 **Inaktivera alla plats underhålls aktiviteter på varje plats under installationen av uppdateringen på platsen:** Innan du installerar uppdateringar inaktiverar du alla plats underhålls aktiviteter som kan köras under den tid då uppdaterings processen är aktiv. Dessa uppgifter inkluderar (men är inte begränsade) till följande:  

-   Platsserver för säkerhetskopiering  

-   Ta bort föråldrade klientåtgärder  

-   Ta bort föråldrade identifieringsdata  

Om en underhållsaktivitet för platsdatabasen körs under installationen av uppdateringen kan installationen av uppdateringen misslyckas. Innan du inaktiverar en aktivitet registrerar du schemat för aktiviteten så att du kan återställa dess konfiguration när uppdateringen har installerats.  

 Mer information finns i [underhålls aktiviteter för Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) och [referens för underhålls aktiviteter för Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Stoppa tillfälligt antivirus program på Configuration Manager servrar:** Innan du uppdaterar en plats kontrollerar du att du har stoppat antivirus program på Configuration Manager-servrarna. <!--SMS.503481--> 

 **Skapa en säkerhets kopia av plats databasen på den centrala administrations platsen och de primära platserna:** Innan du uppdaterar en plats måste du säkerhetskopiera plats databasen för att säkerställa att du har en lyckad säkerhets kopia som du kan använda för haveri beredskap.   

Mer information finns i [säkerhets kopiering och återställning för Configuration Manager](backup-and-recovery.md).  

 **Säkerhetskopiera en anpassad Configuration. MOF-fil:** Om du använder en anpassad Configuration. MOF-fil för att definiera data klasser som du använder med maskin varu inventering, skapar du en säkerhets kopia av den här filen innan du uppdaterar platsen. Efter uppdateringen återställer du filen till din version 1602-webbplats. När du uppdaterar en plats skrivs den aktuella filen över med den ursprungliga (standard) versionen av filen. Mer information om hur du använder den här filen finns i [så här utökar du maskin varu inventeringen](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 **Testa databas uppgraderingen på en kopia av den senaste säkerhets kopian av plats databasen:** Innan du uppdaterar en Configuration Manager Central administrations plats eller primär plats testar du uppgraderings processen för plats databasen på en kopia av plats databasen.  

-   Du bör testa uppgraderings processen för plats databasen eftersom du kan ändra plats databasen när du uppgraderar en plats.  

-   Även om det inte krävs en uppgradering av test databasen, kan det identifiera problem för uppgraderingen innan produktions databasen påverkas.  

-   Om uppgraderingen av platsdatabasen misslyckas kanske den inte går att använda, och det kan krävas en webbplatsåterställning för att funktionerna ska fungera.  

-   Även om plats databasen delas mellan platser i en hierarki, bör du planera att testa databasen på varje tillämplig plats innan du uppgraderar platsen.  

-   Om du använder databas repliker för hanterings platser på en primär plats inaktiverar du replikering innan du skapar säkerhets kopian av plats databasen.  

Configuration Manager stöder inte säkerhets kopiering av sekundära platser eller så stöder den inte test uppgraderingen av en sekundär plats databas.   
Kör inte en test databas uppgradering på produktions plats databasen. Då uppdateras platsdatabasen och det kan göra att platsen inte fungerar alls. Mer information finns i [steg 2: Testa databas uppgraderingen innan du installerar en uppdatering](install-in-console-updates.md#bkmk_step2) från **innan du installerar en uppdatering i konsolen**.  

 **Planera för klient pilot:** När du installerar en uppdatering som uppdaterar klienten kan du testa den nya klient uppdateringen i för produktion innan den distribueras och uppgraderar alla dina aktiva klienter.   

 Om du vill utnyttja det här alternativet måste du konfigurera platsen så att den stöder automatiska uppgraderingar för för produktion innan du påbörjar installationen av uppdateringen. Mer information finns i [Uppgradera klienter](../../../core/clients/manage/upgrade/upgrade-clients.md) och   
[Testa klient uppgraderingar i en för produktions samling](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Planera att använda underhålls fönster för att styra när plats servrar installerar uppdateringar:** Du kan använda underhålls Fönstren för att definiera en tids period under vilken uppdateringar av plats servern kan installeras. Detta kan hjälpa dig att styra när platser i hierarkin installerar uppdateringen.   

Från och med lanseringen av uppdatering 1602 har underhålls Fönstren bytt namn till *service fönster*. Mer information finns i [Service Windows for Site servers](service-windows.md).  

 **Kör krav kontrollen för installation:**  Innan du installerar uppdatering 1602 kan du köra krav kontrollen oberoende av installationen av uppdateringen. När du installerar uppdateringen på platsen körs krav kontrollen igen.  

Mer information finns i **steg 3: kör krav kontrollen innan du installerar en uppdatering** i avsnittet [uppdateringar för Configuration Manager](../../../core/servers/manage/updates.md) .  

> [!IMPORTANT]  
>  När krav kontrollen körs fristående eller som en del av en uppdaterings installation uppdaterar processen vissa produkt käll filer som används för plats underhålls aktiviteter. När du har kört krav kontrollen men innan du installerar 1602-uppdateringen måste du därför köra **Setupwfe. exe** (Configuration Manager installationen) från CD: n för att utföra en plats underhålls uppgift. Den senaste mappen på plats servern.  

 **Uppdatera platser:** Du är nu redo att starta installationen av uppdateringen för hierarkin. Vi rekommenderar att du planerar att installera uppdateringen utanför normal kontors tid för varje plats, när processen för att installera uppdateringen och dess åtgärder för att installera om plats komponenter och plats system roller har minst påverkan på din affärs verksamhet.

Mer information finns i [uppdateringar för Configuration Manager](../../../core/servers/manage/updates.md).  

## <a name="see-also"></a>Se även  
 [Uppdateringar för Configuration Manager](../../../core/servers/manage/updates.md)
