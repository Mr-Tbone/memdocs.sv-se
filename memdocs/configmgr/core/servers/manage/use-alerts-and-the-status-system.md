---
title: Aviseringar och status systemet
titleSuffix: Configuration Manager
description: Konfigurera aviseringar och Använd status systemet för att hålla dig informerad om tillståndet för din Configuration Manager-distribution.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7341cc6e-9e08-41e4-bcc6-6c1ff12e85ca
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c066a61380e09961192bcbe7192e2e945341c97c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720718"
---
# <a name="use-alerts-and-the-status-system-for-configuration-manager"></a>Använd aviseringar och status systemet för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Konfigurera aviseringar och Använd det inbyggda status systemet för att hålla dig informerad om tillståndet för din Configuration Manager-distribution.  


##  <a name="status-system"></a><a name="bkmk_Status"></a> Statussystem  
 Alla större komponenter genererar statusmeddelanden som ger feedback om plats- och hierarkiåtgärder.    Med den här informationen kan du hålla dig uppdaterad om hälsotillståndet för olika platsprocesser. Du kan finjustera aviseringssystemet om du vill ignorera kända problem men snabbt bli uppmärksammad på andra problem som kan kräva åtgärder.  

 Som standard fungerar Configuration Manager status system utan konfiguration med inställningar som är lämpliga för de flesta miljöer. Du kan dock konfigurera följande:  

-   **Statussammanfattningar:** Du kan ändra statussammanfattningarna på varje plats om du vill styra frekvensen för statusmeddelanden som genererar en statusförändring för följande fyra sammanfattningar:  

    -   Sammanfattning för programdistribution  

    -   Sammanfattning för programstatistik  

    -   Sammanfattning av komponentstatus  

    -   Statussammanfattning för platssystem  

-   **Statusfilterregler:** Du kan skapa nya statusfilterregler, ändra reglernas prioritetsordning, inaktivera eller aktivera regler eller ta bort regler som inte används på varje plats.  

    > [!NOTE]  
    >  Statusfilterregler har inte stöd för användning av miljövariabler för körning av externa kommandon.  

-   **Status rapportering:** Du kan konfigurera både server-och klient komponent rapportering för att ändra hur status meddelanden rapporteras till Configuration Manager status systemet och ange vart status meddelanden ska skickas.  

    > [!WARNING]  
    >  Eftersom standardrapporteringsinställningarna kan användas i de flesta miljöer bör du vara restriktiv med att ändra dem. När du ökar nivån för status rapportering genom att välja att rapportera all statusinformation kan du öka antalet status meddelanden som ska bearbetas, vilket ökar bearbetnings belastningen på Configuration Managers platsen. Om du minskar rapporteringsnivån kanske statussammanfattningarna inte blir så användbara som de kan vara.  

Eftersom statussystemet har separata konfigurationer för varje plats måste du redigera varje plats separat.  

###  <a name="procedures-for-configuring-the-status-system"></a><a name="bkmk_configstatus"></a> Procedurer för att konfigurera statussystemet  

##### <a name="to-configure-status-summarizers"></a>Konfigurera statussammanfattningar  

1.  I Configuration Manager-konsolen navigerar du till **Administration** > **plats konfiguration** >**platser**och väljer sedan den plats som du vill konfigurera status systemet för.  

2.  Klicka på **Statussammanfattningar** i gruppen **Inställningar** på fliken **Start**.  

3.  I dialogrutan **Statussammanfattningar** markerar du de statussammanfattningar som ska konfigureras. Klicka sedan på **Redigera** för att öppna egenskaperna för sammanfattningarna. Om du redigerar sammanfattningen Programdistribution eller Programstatistik fortsätter du med steg 5. Om du redigerar Komponentstatus hoppar du till steg 6. Om du redigerar sammanfattningen Status för platssystem hoppar du till steg 7.  

4.  Utför följande steg när du har öppnat egenskapssidan för sammanfattningen för programdistribution eller programstatistik:  

    1.  Ange sammanfattningsintervall på fliken **Allmänt** på egenskapssidan, och klicka sedan på **OK** för att stänga sidan.  

    2.  Klicka på **OK** så stängs dialogrutan **Statussammanfattningar** och den här åtgärden slutförs.  

5.  Utför följande steg när du har öppnat egenskapssidan för sammanfattning av komponentstatus:  

    1.  På fliken **Allmänt** på egenskaps sidan för sammanfattningar konfigurerar du värden för replikering och tröskelvärdes perioder.  

    2.  På fliken **Tröskel** markerar du den **Meddelandetyp** som ska konfigureras. Klicka sedan på ett komponentnamn i listan **Tröskel** .  

    3.  Redigera varningsvärden och kritiska tröskelvärden i dialogrutan **Egenskaper för statuströskelvärden** och klicka sedan på **OK**.  

    4.  Upprepa eventuellt steg 6 b och 6 c och klicka på **OK** för att stänga egenskaperna när du är klar.  

    5.  Klicka på **OK** så stängs dialogrutan **Statussammanfattningar** och den här åtgärden slutförs.  

6.  Utför följande steg när du har öppnat egenskapssidan för sammanfattning av platssystem:  

    1.  På fliken **Allmänt** på egenskaps sidan för sammanfattningar konfigurerar du replikerings-och schema värden.  

    2.  Definiera standardtröskelvärden för kritiska meddelanden och varningsmeddelanden genom att på fliken **Tröskel** ange värden i **Standardtröskelvärden** .  

    3.  När du vill redigera värden för specifika **lagringsobjekt**markerar du objektet i listan **Specifika tröskelvärden** och klickar sedan på knappen **Egenskaper** för att öppna och redigera lagringsobjekts varningar och kritiska tröskelvärden. Klicka på **OK** för att stänga lagringsobjektegenskaperna.  

    4.  Om du vill skapa ett nytt lagringsobjekt klickar du på knappen **Skapa objekt** och anger lagringsobjektvärden. Klicka på **OK** för att stänga objektegenskaperna.  

    5.  Om du vill radera ett lagringsobjekt markerar du objektet och klickar sedan på knappen **Ta bort** .  

    6.  Upprepa steg 7. b till 7. e efter behov. När du är klar klickar du på **OK** för att stänga sammanfattningsegenskaperna.  

    7.  Klicka på **OK** så stängs dialogrutan **Statussammanfattningar** och den här åtgärden slutförs.  

##### <a name="to-create-a-status-filter-rule"></a>Skapa en statusfilterregel  

1.  I Configuration Manager-konsolen navigerar du till **Administration** > **plats konfiguration** >**platser**och väljer sedan den plats där du vill konfigurera status systemet.  

2.  Klicka på **Statusfilterregler** i gruppen **Inställningar** på fliken **Start**. Dialogrutan **Statusfilterregler** öppnas.  

3.  Klicka på **Skapa**.  

4.  På sidan **Allmänt**i **guiden Skapa statusfilterregel** anger du ett namn för den nya regeln. Ange även kriterier för meddelandematchning och klicka sedan på **Nästa**.  

5.  På sidan **Åtgärder** anger du vilka åtgärder som ska utföras när ett statusmeddelande överensstämmer med filterregeln. Klicka sedan på **Nästa**.  

6.  På sidan **Sammanfattning** granskar du den sammanfattade informationen om den nya regeln innan du väljer att slutföra guiden.  

    > [!NOTE]  
    >  Configuration Manager kräver bara att den nya status filter regeln har ett namn. Om du skapar en regel utan att ange kriterier för matchning av statusmeddelanden, har statusfilterregeln ingen effekt. Det här innebär att du kan skapa och organisera regler innan du konfigurerar statusfilterkriterier för varje regel.  

##### <a name="to-modify-or-delete-a-status-filter-rule"></a>Modifiera eller ta bort en statusfilterregel  

1.  I Configuration Manager-konsolen navigerar du till **Administration** > **plats konfiguration** >**platser**och väljer sedan den plats där du vill konfigurera status systemet.  

2.  Klicka på **Statusfilterregler** i gruppen **Inställningar** på fliken **Start**.  

3.  Välj i dialogrutan **Statusfilterregler** den regel som ska ändras. Utför sedan något av följande:  

    -   Klicka på **Öka prioritet** eller **Minska prioritet** för att ändra regelns bearbetningsordning. Välj sedan någon annan åtgärd eller slutför uppgiften genom att gå till steg 8 i den här proceduren.  

    -   Klicka på **Inaktivera** eller **Aktivera** för att ändra regelns status. När du har ändrat regelns status väljer du någon annan åtgärd eller slutför uppgiften genom att gå till steg 8 i den här proceduren.  

    -   Klicka på **Ta bort** om du vill ta bort statusfilterregeln från platsen, och klicka sedan på **Ja** för att bekräfta åtgärden. När du har tagit bort en regel väljer du någon annan åtgärd eller slutför uppgiften genom att gå till steg 8 i den här proceduren.  

    -   Klicka på **Redigera** om du vill ändra kriterier för statusmeddelanderegeln. Fortsätt sedan med steg 5 i den här proceduren.  

4.  På fliken **Allmänt** i dialogrutan med statusfilteregenskaper ändrar du regeln och kriterier för meddelandematchning.  

5.  På sidan **Åtgärder** anger du vilka åtgärder som ska utföras när ett statusmeddelande överensstämmer med filterregeln.  

6.  Spara ändringarna genom att klicka på **OK**.  

7.  Klicka på **OK** för att stänga dialogrutan **Statusfilterregler** .  

##### <a name="to-configure-status-reporting"></a>Konfigurera statusrapportering  

1.  I Configuration Manager-konsolen navigerar du till **Administration** > **plats konfiguration** > **platser**och väljer sedan den plats där du vill konfigurera status systemet.  

2.  På fliken **Start** i gruppen **Inställningar** klickar du på **Konfigurera platskomponenter**och klickar sedan på **Statusrapportering**.  

3.  Ange i dialogrutan **Komponentegenskaper för statusrapportering** de server- och klientkomponentmeddelanden som ska rapporteras eller loggas:  

    1.  Konfigurera en **rapport** för att skicka status meddelanden till Configuration Manager-status meddelande systemet.  

    2.  Ange i **Logg** att meddelandetyp och allvarlighetsgrad ska skrivas till händelseloggen i Windows.  

4.  Klicka på **OK**.  

###  <a name="monitor-the-status-system-of-configuration-manager"></a><a name="BKMK_MonitorSystemStatus"></a> Övervaka statussystemet för Configuration Manager  
 **System status** i Configuration Manager ger en översikt över de allmänna åtgärderna för platser och plats Server åtgärder i hierarkin. Den kan avslöja drifts problem för plats system servrar eller-komponenter och du kan använda system statusen för att granska detaljerad information för olika Configuration Manager åtgärder. Du övervakar system status från noden **system status** på arbets ytan **övervakning** i Configuration Manager-konsolen.  

 De flesta Configuration Manager plats system roller och komponenter genererar status meddelanden. Statusmeddelandedetaljer loggas i aktivitetsloggen för varje komponent, men skickas även till platsdatabasen, där de sammanfattas och presenteras i en allmän sammanfattning av hälsotillståndet för varje komponent eller platssystem. Dessa sammanfattningar av statusmeddelanden ger detaljerad information om normal drift samt detaljer om varningar och fel. Du kan konfigurera de tröskelvärden vid vilka varningar eller fel utlöses och finjustera systemet så att den sammanfattade informationen ignorerar kända problem som inte är relevanta för dig, samtidigt som den uppmärksammar verkliga problem på servrarna eller för komponentaktiviteter som du kan vilja undersöka.  

 Systemstatus replikeras till andra platser i en hierarki som platsdata, inte globala data. Det innebär att du bara kan se status för den plats som Configuration Manager-konsolen ansluter till och alla underordnade platser under den platsen. Du bör därför överväga att ansluta Configuration Manager-konsolen till platsen på den högsta nivån i hierarkin när du visar system status.  

 Använd följande tabell för att identifiera de olika vyerna för systemstatus och när du ska använda dem.  

|Node|Mer information|  
|----------|----------------------|  
|Platsstatus|Använd den här noden för att visa en sammanfattning av varje platssystem för att granska hälsostatusen för varje platssystemserver. Platssystemets hälsostatus avgörs av tröskelvärden som du konfigurerar för varje plats i **Statussammanfattning för platssystem**.<br /><br /> Du kan visa statusmeddelanden för varje platssystem, ange tröskelvärden för statusmeddelanden och hantera komponenternas aktiviteter på platssystem med **Configuration Manager Service Manager**.|  
|Komponentstatus|Använd den här noden för att visa en sammanställning av status för varje Configuration Manager komponent för att granska komponentens operativa hälsa. Komponentens hälsostatus avgörs av tröskelvärden som du konfigurerar för varje plats i **Sammanfattning för komponentstatus**.<br /><br /> Du kan visa statusmeddelanden för varje komponent, ange tröskelvärden för statusmeddelanden och hantera komponenternas aktiviteter med **Configuration Manager Service Manager**.|  
|Poster i konflikt|Använd den här noden för att visa statusmeddelanden om klienter som kan ha poster i konflikt.<br /><br /> Configuration Manager använder maskinvaru-ID för att försöka identifiera klienter som kan vara dubbletter och varna dig för poster i konflikt. Om du t. ex. måste installera om en dator är maskinvaru-ID detsamma, men det GUID som Configuration Manager använder kan ändras.|  
|Frågor för statusmeddelanden|Använd den här noden för att fråga statusmeddelanden om specifika händelser och relaterade detaljer. Du kan använda statusmeddelandefrågor för att hitta de statusmeddelanden som hör till specifika händelser.<br /><br /> Du kan ofta använda status meddelande frågor för att identifiera när en enskild komponent, åtgärd eller Configuration Manager objekt har ändrats och det konto som användes för att göra ändringen. Du kan t.ex. använda den inbyggda frågan **Skapade, ändrade eller borttagna samlingar** för att identifiera när en specifik samling skapades och det användarkonto som användes för att skapa samlingen.|  

####  <a name="manage-site-status-and-component-status"></a><a name="bkmk_managestatus"></a> Hantera plats- och komponentstatus  
 Använd följande information för att hantera plats- och komponentstatus:  

-   Om du vill konfigurera tröskelvärden för statussystemet finns mer information i [Procedurer för att konfigurera statussystemet](#bkmk_configstatus).  

-   Om du vill hantera enskilda komponenter i Configuration Manager använder du **Configuration Manager Service Manager**.  

####  <a name="view-status-messages"></a><a name="bkmk_view"></a> Visa statusmeddelanden  
 Du kan visa statusmeddelanden för enskilda platssystemservrar och komponenter.  

 Om du vill visa status meddelanden i Configuration Manager-konsolen väljer du en plats system Server eller komponent och klickar sedan på **Visa meddelanden**. När du visar meddelanden kan du välja att visa specifika typer av meddelanden eller meddelanden från ett speciellt tidsintervall, och du kan filtrera resultatet baserat på detaljerna om statusmeddelandena.  

##  <a name="alerts"></a><a name="bkmk_Alerts"></a>Aviseringar  
 Configuration Manager aviseringar genereras av vissa åtgärder när ett visst villkor inträffar.  

- Normalt genereras aviseringar när ett fel inträffar som du måste lösa.  

- Aviseringar kan genereras för att varna dig om en situation som har uppstått, så att du kan fortsätta att övervaka den.  

- Vissa aviseringar konfigurerar du, till exempel aviseringar för Endpoint Protection och klientstatus, medan andra aviseringar konfigureras automatiskt.  

- Du kan också konfigurera prenumerationer med aviseringar som sedan kan skicka information via e-post och göra dig uppmärksam på viktiga problem.  

  Använd följande tabell för att hitta information om hur du konfigurerar aviseringar och aviserings prenumerationer i Configuration Manager:  


|Action|Mer information|  
|------------|----------------------|  
|Konfigurera Endpoint Protection aviseringar för en samling|Information om **hur du konfigurerar aviseringar för Endpoint Protection i Configuration Manager** i [konfigurera Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md)|  
|Konfigurera klientstatusvarningar för en samling|Se [Konfigurera klient status](../../../core/clients/deploy/configure-client-status.md).|  
|Hantera Configuration Manager aviseringar|Se [Management tasks for alerts](#BKMK_Manage) i det här avsnittet.|  
|Konfigurera e-postprenumerationer med aviseringar|Se avsnittet [hanterings aktiviteter för aviseringar](#BKMK_Manage) i det här avsnittet..|  
|Övervaka aviseringar|Se [Övervaka aviseringar](#BKMK_MonitorAlerts)|  

###  <a name="management-tasks-for-alerts"></a><a name="BKMK_Manage"></a> Management tasks for alerts  

##### <a name="to-manage-general-alerts"></a>Så här hanterar du allmänna aviseringar  

1. I Configuration Manager-konsolen navigerar du till **övervaknings** > **aviseringar**och väljer sedan en hanterings aktivitet.  

   I följande tabell finns mer information om hanteringsaktiviteter som du kan behöva veta lite mer om innan du väljer dem.  

|Hanteringsaktivitet|Information|  
    |---------------------|-------------|  
    |**Konfigurera**|Öppnar dialog rutan\>**Egenskaper** för * &lt;aviserings namn*där du kan ändra namn, allvarlighets grad och tröskelvärden för den valda aviseringen. Om du ändrar allvarlighets graden för aviseringen påverkar den här konfigurationen hur aviseringarna visas i Configuration Manager-konsolen.|  
    |**Redigera kommentar**|Ange en kommentar för de valda aviseringarna. Kommentarerna visas med aviseringen i Configuration Manager-konsolen.|  
    |**Senarelägg**|Pausar övervakningen av aviseringen fram till det angivna datumet. Då uppdateras aviseringens status.<br /><br /> Du kan bara skjuta upp en avisering när den är aktiverad.|  
    |**Skapa prenumeration**|Öppnar dialogrutan **Ny prenumeration** där du kan skapa en e-postprenumeration för den valda aviseringen.|  

<!--##### To configure Endpoint Protection alerts for a collection  

1.  pending  -->

##### <a name="to-configure-client-status-alerts-for-a-collection"></a>Så här konfigurerar du klientstatusvarningar för en samling  

1.  I Configuration Manager-konsolen klickar du på **till gångar och efterlevnad** >   **enhets samlingar**.  

2.  Välj i listan **Enhetssamlingar** den samling som du vill konfigurera aviseringar för. Klicka sedan på **Egenskaper** i gruppen **Egenskaper** på fliken **Start**.  

    > [!NOTE]  
    >  Det går inte att konfigurera aviseringar för användarsamlingar.  

3.  På fliken **aviseringar** i dialog rutan\>**Egenskaper** för * &lt;samlings namn*klickar du på **Lägg till**.  

    > [!NOTE]  
    >  Fliken **Aviseringar** visas endast om den säkerhetsroll som du är associerad med har behörighet för aviseringar.  

4.  I dialogrutan **Lägg till nya samlingsvarningar** väljer du de aviseringar som ska genereras när klientstatusgränsvärdena blir lägre än ett specifikt definierat värde. Klicka sedan på **OK**.  

5.  I listan **Villkor** på fliken **Aviseringar** markerar du varje klientstatusavisering och anger följande information.  

    -   **Aviserings namn** – acceptera standard namnet eller ange ett nytt namn för aviseringen.  

    -   **Allvarlighets grad för avisering** – Välj den aviserings nivå som ska visas i Configuration Managers konsolen i list rutan.  

    -   **Generera avisering** – ange tröskel procent andelen för aviseringen.  

6.  Stäng dialog rutan\>**Egenskaper** för * &lt;samlings namn*genom att klicka på **OK** .  

##### <a name="to-configure-email-notification-for-alerts"></a>Så här konfigurerar du e-postmeddelanden med aviseringar  

1.  I Configuration Manager-konsolen navigerar du till **övervaka** > **aviserings** > **prenumerationer**.  

2.  På fliken **Start** i gruppen **Skapa** klickar du på **Konfigurera e-postmeddelande**.  

3.  Ange följande information i dialogrutan **Egenskaper för e-postaviseringskomponent** :  

    -   **Aktivera e-postavisering för aviseringar**: Markera den här kryss rutan om du vill att Configuration Manager använda en SMTP-server för att skicka e-postaviseringar.  

    -   **FQDN eller IP-adress till SMTP-servern dit e-postaviseringar ska skickas**: Ange det fullständigt kvalificerade domännamnet (FQDN) eller IP-adressen och SMTP-porten för e-postservern som du vill använda för dessa aviseringar.  

    -   **Konto för SMTP-server anslutning**: Ange autentiseringsmetoden för Configuration Manager som ska användas för att ansluta e-postservern.  

    -   **Avsändaradress för e-postaviseringar**: Ange den e-postadress som meddelandena ska skickas från.  

    -   **Testa SMTP-server**: Skickar ett testmeddelande till den e-postadress som angetts i **Avsändaradress för e-postaviseringar**.  

4.  Spara inställningarna och stäng dialogrutan **Komponentegenskaper för e-postinställningar** genom att klicka på **OK** .  

##### <a name="to-subscribe-to-email-alerts"></a>Så här prenumererar du på e-postaviseringar  

1.  I Configuration Manager-konsolen navigerar du till **övervaknings** > **aviseringar**.  

2.  Välj en avisering och klicka sedan på **Skapa prenumeration** i gruppen **Prenumeration** på fliken **Start**.  

3.  Ange följande information i dialogrutan **Ny prenumeration** :  

    -   **Namn**: Ange ett namn som identifierar e-postprenumerationen. Du kan använda upp till 255 tecken.  

    -   **E-postadress**: Ange de e-postadresser som du vill att aviseringen ska skickas till. Du kan avgränsa flera e-postadresser med semikolon.  

    -   **E-postspråk**: Ange språket för e-postmeddelandet från listan.  

4.  Stäng dialogrutan **Ny prenumeration** och skapa e-prenumerationen genom att klicka på **OK** .  

    > [!NOTE]  
    >  Du kan ta bort och redigera prenumerationer på arbetsytan **Övervakning** . Expandera noden **Aviseringar** och klicka sedan på noden **Prenumerationer** .  

###  <a name="monitor-alerts"></a><a name="BKMK_MonitorAlerts"></a>Övervaka aviseringar  
 Du kan visa aviseringar i noden **Aviseringar** på arbetsytan **Övervakning** . Aviseringar har något av dessa aviseringstillstånd:  

- **Aldrig utlöst**: Villkoret för aviseringen är inte uppfyllt.  

- **Aktiv**: Villkoret för aviseringen är uppfyllt.  

- **Avbruten**: Villkoret för en aktiv avisering är inte längre uppfyllt. Det här tillståndet anger att den situation som orsakade aviseringen är löst.  

- **Uppskjuten**: en administrativ användare har konfigurerat Configuration Manager att utvärdera status för aviseringen vid ett senare tillfälle.  

- **Inaktiverad**: Aviseringen har inaktiverats av en administrativ användare. När en avisering är i det här läget uppdaterar Configuration Manager inte aviseringen även om status för aviseringen ändras.  

  Du kan vidta någon av följande åtgärder när Configuration Manager genererar en avisering:  

- Lös den situation som orsakade aviseringen. Du kan t.ex. lösa ett nätverks- eller konfigurationsproblem som orsakade aviseringen. När Configuration Manager har identifierat att problemet inte finns, ändras aviserings läget till **Avbryt**.  

- Om aviseringen är ett känt problem kan du skjuta upp aviseringen under en bestämd tidsperiod. Vid detta tillfälle uppdaterar Configuration Manager aviseringen till dess aktuella tillstånd.  

   Du kan bara skjuta upp en aktiv avisering.  

- Du kan redigera aviseringens **Kommentar** så att andra administrativa användare kan se att du är medveten om aviseringen. I kommentaren kan du t.ex. beskriva hur situationen ska lösas, lämna information om situationens aktuella status eller förklara varför du sköt upp aviseringen.  
