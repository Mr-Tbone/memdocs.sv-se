---
title: Konfigurera klient status
titleSuffix: Configuration Manager
description: Välj inställningar för klient status i Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5bb77e1e9f55919a03368d549946ee4dd1cda58a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713578"
---
# <a name="how-to-configure-client-status-in-configuration-manager"></a>Konfigurera klient status i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Innan du kan övervaka Configuration Manager klient status och åtgärda problem som hittas måste du konfigurera platsen för att ange de parametrar som används för att markera klienter som inaktiva och konfigurera alternativ för att varna dig om klient aktiviteten sjunker under ett visst tröskelvärde. Du kan också inaktivera datorer från att automatiskt reparera eventuella problem som klient status hittar.  

##  <a name="to-configure-client-status"></a><a name="BKMK_1"></a>Konfigurera klient status  

1.  Klicka på **övervakning**i Configuration Manager-konsolen.  

2.  I arbets **ytan övervakning** klickar du **på klient status**och klickar sedan på **Inställningar för klient status**i gruppen **klient** status på fliken **Start** .  

3.  I dialog rutan **Egenskaper för klient status inställningar** anger du följande värden för att fastställa klient aktivitet:  

    > [!NOTE]  
    >  Om ingen av inställningarna är uppfyllda markeras klienten som inaktiv.  

    -   **Klient princip begär Anden under följande dagar:** Ange antalet dagar sedan en klient begärde en princip. Standardvärdet är **7** dagar.  

    -   **Pulsslags identifiering under följande dagar:** Ange antalet dagar sedan klient datorn skickade en pulsslags identifierings post till plats databasen. Standardvärdet är **7** dagar.  

    -   **Maskin varu inventering under följande dagar:** Ange antalet dagar sedan klient datorn skickade en maskin varu inventerings post till plats databasen. Standardvärdet är **7** dagar.  

    -   **Program varu inventering under följande dagar:** Ange antalet dagar sedan klient datorn skickade en program varu inventerings post till plats databasen. Standardvärdet är **7** dagar.  

    -   **Status meddelanden under följande dagar:** Ange antalet dagar sedan klient datorn skickade status meddelanden till plats databasen. Standardvärdet är **7** dagar.  

4.  I dialog rutan **Egenskaper för klient status inställningar** anger du följande värde för att avgöra hur länge klient status historik data kvarhålls:  

    -   **Behåll klient status historik i följande antal dagar:** Ange hur länge du vill att klient status historiken ska behållas i plats databasen. Standardvärdet är **31** dagar.  

5.  Klicka på **OK** för att spara egenskaperna och stänga dialog rutan **Egenskaper för klient status inställningar** .  

##  <a name="to-configure-the-schedule-for-client-status"></a><a name="BKMK_Schedule"></a>Så här konfigurerar du schemat för klient status  

1.  Klicka på **övervakning**i Configuration Manager-konsolen.  

2.  I arbets **ytan övervakning** klickar du på **klient status**och klickar sedan på **Schemalägg klient status uppdatering**i gruppen **klient status** på fliken **Start** .  

3.  I dialog rutan **Schemalägg klientens status uppdatering** konfigurerar du intervallet då du vill att klientens status ska uppdateras och klickar sedan på OK.  

    > [!NOTE]  
    >  När du ändrar schemat för klient status uppdateringar börjar uppdateringen inte gälla förrän nästa schemalagda klient status uppdatering (för det tidigare konfigurerade schemat).  

##  <a name="to-configure-alerts-for-client-status"></a><a name="BKMK_2"></a>Konfigurera aviseringar för klient status  

1. Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

2. I arbetsytan **Tillgångar och efterlevnad** klickar du på **Enhetssamlingar**.  

3. Välj i listan **Enhetssamlingar** den samling som du vill konfigurera aviseringar för. Klicka sedan på **Egenskaper** i gruppen **Egenskaper** på fliken **Start**.  

   > [!NOTE]  
   >  Det går inte att konfigurera aviseringar för användarsamlingar.  

4. På fliken **aviseringar** i dialog rutan**Egenskaper** för <em> &lt;\>samlings namn</em>klickar du på **Lägg till**.  

   > [!NOTE]  
   >  Fliken **Aviseringar** visas endast om den säkerhetsroll som du är associerad med har behörighet för aviseringar.  

5. I dialogrutan **Lägg till nya samlingsvarningar** väljer du de aviseringar som ska genereras när klientstatusgränsvärdena blir lägre än ett specifikt definierat värde. Klicka sedan på **OK**.  

6. I listan **Villkor** på fliken **Aviseringar** markerar du varje klientstatusavisering och anger följande information.  

   -   **Aviserings namn** – acceptera standard namnet eller ange ett nytt namn för aviseringen.  

   -   **Allvarlighets grad för avisering** – Välj den aviserings nivå som ska visas i Configuration Managers konsolen i list rutan.  

   -   **Generera avisering** – ange tröskel procent andelen för aviseringen.  

7. Stäng dialog rutan**Egenskaper** för <em> &lt;samlings\>namn</em>genom att klicka på **OK** .  

##  <a name="to-exclude-computers-from-automatic-remediation"></a><a name="BKMK_3"></a>Så här undantar du datorer från automatisk reparation  

1. Öppna Registereditorn på den klient dator för vilken du vill inaktivera automatisk reparation.  

   > [!WARNING]  
   >  Om du använder Registereditorn på ett felaktigt sätt kan det orsaka allvarliga problem som kräver att du installerar om operativ systemet. Microsoft kan inte garantera att du kan lösa problem som orsakas av felaktig användning av Registereditorn. Du använder Registereditorn på egen risk.  

2. Navigera till **HKEY_LOCAL_MACHINE \software\microsoft\ccm\ccmeval\notifyonly**.  

3. Ange ett av följande värden för den här register nyckeln:  

   -   **True** -klient datorn kommer inte att åtgärda eventuella problem som hittas automatiskt. Du kommer dock fortfarande att bli aviserad i arbets ytan **övervakning** om eventuella problem med den här klienten.  

   -   **Falskt** – klient datorn åtgärdar automatiskt problem när de hittas och du kommer att bli aviserad i arbets ytan **övervakning** . Det här är standardinställningen.  

4. Stäng Registereditorn.  

   Du kan också installera klienter med hjälp av egenskapen CCMSetup **NOTIFYONLY** installation för att utesluta dem från automatisk reparation. Mer information om den här klient installations egenskapen finns i [om klient installations egenskaper](../../../core/clients/deploy/about-client-installation-properties.md).  
