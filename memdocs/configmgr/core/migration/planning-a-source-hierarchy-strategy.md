---
title: Käll hierarkins strategi
titleSuffix: Configuration Manager
description: Konfigurera en källhierarki och samla in data från en käll plats innan du konfigurerar ett Configuration Manager migreringsjobb.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4800a800-66c8-4c35-aebe-e413a23790c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28960753da06058ef181f94a5d11d9f2327ebf56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719682"
---
# <a name="plan-a-source-hierarchy-strategy-in-configuration-manager"></a>Planera en käll hierarkis strategi i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Innan du konfigurerar ett migreringsjobb i Configuration Managers miljön måste du konfigurera en källhierarki och samla in data från minst en käll plats i hierarkin. Använd följande avsnitt för att få hjälp att planera konfigurering av källhierarki, konfigurera käll platser och bestämma hur Configuration Manager samlar in information från käll platserna i källhierarkin. 

##  <a name="source-hierarchies"></a><a name="BKMK_Source_Hierarchies"></a>Käll-hierarkier  
En källhierarki är en Configuration Manager hierarki som innehåller data som du vill migrera. När du konfigurerar migrering och anger en källhierarki anger du platsen på den översta nivån i källhierarkin. Platsen kallas även för en källplats. Ytterligare platser som du kan migrera data från i källhierarkin kallas även för käll platser.  

-   När du konfigurerar ett migreringsjobb för att migrera data från en Configuration Manager 2007-källhierarki konfigurerar du den för att migrera data från en eller flera angivna käll platser i källhierarkin.  

-   När du konfigurerar ett migreringsjobb för att migrera data från en-källhierarki som kör System Center 2012 Configuration Manager eller senare, behöver du bara ange platsen på den översta nivån.  

Du kan bara konfigurera en källhierarki i taget.  

-   Om du konfigurerar en ny källhierarki blir den automatiskt den aktuella källhierarkin som ersätter den tidigare källhierarkin.  

-   När du konfigurerar en-källhierarki måste du ange platsen på den översta nivån i källhierarkin och ange autentiseringsuppgifter för Configuration Manager som ska användas för att ansluta till SMS-providern och plats databasen för den käll platsen.  

-   Configuration Manager använder dessa autentiseringsuppgifter för att köra data insamling för att hämta information om objekten och distributions platserna från käll platsen.  

-   Under informationshämtningen identifieras också underordnade platser i källhierarkin.  

-   Om källhierarkin är en Configuration Manager 2007-hierarki kan du konfigurera dessa ytterligare platser som käll platser med separata autentiseringsuppgifter för varje käll plats.  

Även om du kan konfigurera flera käll-hierarkier i följd, är migreringen aktiv för endast en källhierarki i taget.  

-   Om du ställer in ytterligare en källhierarki innan du Slutför migreringen från den aktuella källhierarkin, Configuration Manager avbryter alla aktiva migreringsjobb och skjuter upp schemalagda migreringsjobb för den aktuella källhierarkin.  

-   Den nyligen konfigurerade källhierarkin blir den aktuella källhierarkin, och den ursprungliga källhierarkin är nu inaktiv.  

-   Du kan sedan konfigurera autentiseringsuppgifter för anslutning, ytterligare käll platser och migreringsjobb för den nya källhierarkin.  

Om du återställer en inaktiv källhierarki och inte tidigare har använt **Rensa migrering**, kan du Visa de tidigare konfigurerade migreringsjobbna för den källhierarkin. Men innan du kan fortsätta att migrera från den hierarkin måste du omkonfigurera autentiseringsuppgifterna för att kunna ansluta till källplatserna i hierarkin. Du måste också schemalägga eventuella migreringsjobb som inte har slutförts.  

> [!CAUTION]  
>  Om du migrerar data från fler än en källhierarki måste varje extra källhierarki innehålla en unik uppsättning av platskoder.  
> Käll-och målhierarkin kräver också olika uppsättningar av plats koder.

Mer information om hur du konfigurerar en källhierarki finns i [Konfigurera käll-hierarkier och käll platser för migrering till Configuration Manager aktuella grenen](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

##  <a name="source-sites"></a><a name="BKMK_Source_Sites"></a>Käll platser  
 Källplatser är platser i källhierarkin som innehåller de data som ska migreras. Platsen på den översta nivån i källhierarkin är alltid den första källplatsen. När data samlas in (under migreringen) från den första källplatsen i en ny källhierarki, hämtas även information om ytterligare platser i hierarkin.  

 När datainsamlingen har slutförts för den första källplatsen, beror dina efterföljande åtgärder på källhierarkins produktversion.  

### <a name="source-sites-that-run-configuration-manager-2007-sp2"></a>Källplatser som kör Configuration Manager 2007 SP2  
 När data har samlats in från den första käll platsen i Configuration Manager 2007 SP2-hierarkin behöver du inte konfigurera ytterligare käll platser innan du skapar migreringsjobb. Innan du kan migrera data från ytterligare platser måste du dock konfigurera ytterligare platser som käll platser och Configuration Manager måste samla in data från dessa platser.  

 Om du vill samla in data från ytterligare platser konfigurerar du varje plats som en käll plats. Detta kräver att du anger autentiseringsuppgifterna för Configuration Manager att ansluta till SMS-providern och plats databasen för varje käll plats. När du har konfigurerat autentiseringsuppgifterna för en käll plats börjar data insamlings processen för den platsen.  

 När du konfigurerar ytterligare käll platser i en Configuration Manager 2007 SP2-källhierarki måste du konfigurera käll platserna uppifrån och ned, vilket innebär att du konfigurerar de platser på den nedre nivån sist. Du kan konfigurera käll platser i en gren i hierarkin när som helst, men du måste konfigurera en plats som en käll plats innan du konfigurerar någon av dess underordnade platser som käll platser.  

> [!NOTE]  
>  Endast primära platser i en Configuration Manager 2007 SP2-hierarki stöds för migrering.  

### <a name="source-sites-that-run-system-center-2012-configuration-manager-or-later"></a>Käll platser som kör System Center 2012 Configuration Manager eller senare  
 När data har samlats in från den första käll platsen i System Center 2012 Configuration Manager eller en senare hierarki behöver du inte konfigurera ytterligare käll platser i källhierarkin. Detta beror på att till skillnad från Configuration Manager 2007 använder dessa versioner av Configuration Manager en delad databas och den delade databasen gör att du kan identifiera och sedan migrera alla tillgängliga objekt från den ursprungliga käll platsen.  

 När du konfigurerar åtkomst kontona för att samla in data kan du behöva ge **käll platsens SMS-provider** åtkomst till flera datorer i källhierarkin. Det kan behövas när källplatsen stöder flera instanser av SMS-providern, med varje instans på en egen dator. När datainsamlingen börjar ansluts målhierarkins plats på den översta nivån till källhierarkins plats på den översta nivån, för att identifiera SMS-providern för platsen. Endast den första instansen av SMS-providern identifieras. Om SMS-providern inte är tillgänglig på den identifierade sökvägen, misslyckas datahämtningsprocessen och det görs inga försök att ansluta till andra datorer som kör en instans av SMS-providern.  

##  <a name="data-gathering"></a><a name="BKMK_Data_Gathering"></a>Data insamling  
 Direkt efter att du har angett en källhierarki, konfigurerat autentiseringsuppgifter för varje extra käll plats i en källhierarki eller delar distributions platserna för en käll plats, Configuration Manager börjar samla in data från käll platsen.  

 Datainsamlandet upprepas sedan enligt ett enkelt schema, så att alla data synkroniseras med eventuella ändringar på källplatsen. Som standard upprepas insamlingsprocessen var fjärde timme. Du kan ändra schemat för den här cykeln genom att redigera käll platsens **Egenskaper** . Den första data insamlings processen måste granska alla objekt i den Configuration Manager databasen och kan ta lång tid att slutföra. De efterföljande datainsamlingarna går snabbare, eftersom endast ändringar identifieras.  

 Inför insamlandet ansluts målhierarkiplatsen på den översta nivån till källplatsens SMS-provider och platsdatabasen, för hämtning av en lista med objekt och distributionsplatser. För anslutningarna används källplatsens åtkomstkonton. Information om vilka konfigurationer som krävs för att samla in data finns i [krav för migrering](../../core/migration/prerequisites-for-migration.md).  

 Du kan starta och stoppa data insamlings processen genom att använda **samla in data nu** och **sluta samla in data** i Configuration Manager-konsolen.  

 När du har använt **Avbryt data insamling** för en käll plats måste du konfigurera om autentiseringsuppgifterna för platsen innan du kan samla in data från den platsen igen. Configuration Manager kan inte identifiera nya objekt eller ändringar av tidigare migrerade objekt på platsen förrän du har konfigurerat om käll platsen.  

> [!NOTE]  
>  Innan du expanderar en fristående primär plats till en hierarki med en central administrations plats måste du stoppa all data insamling. Du kan konfigurera om data insamling när plats expansionen har slutförts.  

### <a name="gather-data-now"></a>Samla in data nu  
 När den första datainsamlingen har slutförts för en plats, upprepas insamlingsprocessen. Vid upprepningen identifieras objekt som har uppdaterats sedan den senaste datainsamlingscykeln. Du kan också använda åtgärden **samla in data nu** i Configuration Manager-konsolen för att starta processen direkt och återställa start tiden för nästa cykel.  

 När datainsamlingen har slutförts för en källplats kan du dela distributionsplatserna för källplatsen och konfigurera migreringsjobb för migrering av data från källplatsen. Data insamling är en upprepande process för migrering och fortsätter tills du ändrar källhierarkin eller använder **Avbryt data insamling** för att avsluta data insamlings processen för den platsen.  

### <a name="stop-gathering-data"></a>Avbryt datainsamling  
 Du kan använda **sluta samla in data** för att avsluta data insamlings processen för en käll plats om du inte längre vill Configuration Manager identifiera nya eller ändrade objekt från den platsen. Den här åtgärden förhindrar också Configuration Manager från att erbjuda klienter i målhierarkin delade distributions platser från källan som innehålls platser för det innehåll som du har migrerat.  

 Om du vill sluta samla in data från varje käll plats måste du köra **sluta samla in data** på de platser på den nedre nivån och upprepa sedan processen på varje överordnad plats. Platsen på den översta nivån i källhierarkin måste vara den sista du slutar samla in data på. Du måste sluta samla in data på varje underordnad plats innan denna åtgärd används för en överordnad plats. I normalfallet slutar du bara samla in data när du är beredd att slutföra migreringen.  

 När du har slutat samla in data för en käll plats, är information som tidigare samlats in om objekt och samlingar från den platsen tillgänglig för användning när du konfigurerar nya migreringsjobb. Men du ser inga nya objekt eller samlingar, eller så kan du inte se ändringar som gjorts i befintliga objekt. Om du konfigurerar om källplatsen och börjar samla in data på nytt, blir tidigare migrerade objekts information och statusdata tillgängliga igen.  
