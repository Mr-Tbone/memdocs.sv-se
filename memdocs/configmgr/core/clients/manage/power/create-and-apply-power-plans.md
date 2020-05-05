---
title: Skapa och använda energi scheman
titleSuffix: Configuration Manager
description: Skapa och Använd energi scheman i Configuration Manager.
ms.date: 04/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 738eddaa-52e2-467f-b453-821ef2884d47
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ba5479a4c75d3ab8f91a8439a6799589b93972d0
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076704"
---
# <a name="how-to-create-and-apply-power-plans-in-configuration-manager"></a>Skapa och använda energi scheman i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Med energispar funktionerna i Configuration Manager kan du använda energi scheman som medföljer Configuration Manager till samlingar med datorer i hierarkin, eller skapa egna anpassade energi scheman. Följ stegen i det här avsnittet om du vill använda ett inbyggt eller anpassat energischema för datorer.  

> [!IMPORTANT]  
>  Du kan bara använda Configuration Manager energi scheman för enhets samlingar.  

 Om en dator tillhör flera grupper och varje grupp har ett eget energischema, gäller följande:  

- Energischema: Om flera värden för energiinställningar används på en dator används det minst restriktiva värdet.  

- Väckningstid: Om flera väckningstider används på en skrivbordsdator används tiden närmast midnatt.  

  Använd rapporten **Datorer med flera scheman** om du vill visa alla datorer som har flera tilldelade energischeman. Den här informationen kan hjälpa dig att identifiera datorer som har energikonflikter. Mer information om rapporter om energispar funktioner finns i [övervaka och planera för](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)energispar funktioner.  

> [!IMPORTANT]  
>  Energi inställningar som konfigureras med hjälp av Windows grupprincip åsidosätter inställningar som kon figurer ATS av Configuration Manager energispar funktioner.  

 Använd följande procedur för att skapa och tillämpa ett Configuration Manager energi schema.  

### <a name="to-create-and-apply-a-power-plan"></a>Så här skapar du och använder ett energischema  

1. Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

2. I arbetsytan **Tillgångar och efterlevnad** klickar du på **Enhetssamlingar**.  

3. Klicka på den samling i listan **Enhetssamlingar** som du vill tillämpa inställningar för energisparfunktioner på och klicka sedan på **Egenskaper** i gruppen **Egenskaper** på fliken **Start**.  

4. På fliken **energispar funktioner** i dialog rutan**Egenskaper** för <em><samlings namn\></em>väljer du **Ange inställningar för energispar funktioner för den här samlingen**.  

   > [!NOTE]  
   >  Du kan också klicka på **Bläddra** och sedan kopiera energisparinställningarna från en viss samling till den valda samlingen.  

5. I fälten **Start** och **Slut** anger du start- och sluttiden för hög belastning (eller kontorstid).  

6. Aktivera **Väckningstid (stationära datorer)** om du vill ange en tid när en stationär dator ska vakna från strömsparläge eller viloläge för att installera schemalagda uppdateringar eller programinstallationer.  

   > [!IMPORTANT]  
   >  Energisparfunktionerna använder den interna väckningsfunktionen i Windows för att väcka datorer från viloläge eller strömsparläge. Inställningarna för väckningstid tillämpas inte på bärbara datorer för att förhindra scenarier där de kan aktiveras när datorn inte är ansluten. Väckningstiden är slumpmässig och datorerna aktiveras under en timme från den angivna väckningstiden.  

7. Om du vill konfigurera ett anpassat energischema för tider med hög belastning (eller kontorstid) väljer du **Anpassad vid hög belastning (ConfigMgr)** i listrutan **Schema vid hög belastning** och klickar sedan på **Redigera**. Om du vill konfigurera ett anpassat energischema för tider med låg belastning (eller utanför kontorstid) väljer du **Anpassad vid låg belastning (ConfigMgr)** i listrutan **Schema vid låg belastning** och klickar sedan på **Redigera**.  

   > [!NOTE]  
   >  Du kan använda rapporten **Datoraktivitet** för att avgöra vilka scheman du ska använda för tider med hög och låg belastning när du tillämpar energischeman på samlingar med datorer. Mer information finns i [övervaka och planera för energispar funktioner](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

    Du kan också välja ett inbyggt energischema. Välj **Balanserad (ConfigMgr)**, **Höga prestanda (ConfigMgr)** eller **Energisparläge (ConfigMgr)** och klicka på **Visa** om du vill visa egenskaperna för respektive energischema.  

   > [!NOTE]  
   >  Du kan inte ändra inbyggda energischeman.  

8. Konfigurera följande inställningar i dialog rutan<**Egenskaper** för <em>energi schema namn\></em>:  

   -   **Namn:** Ange ett namn för energischemat eller använd det angivna standardvärdet.  

   -   **Beskrivning:**  Ange en beskrivning för energischemat eller använd det angivna standardvärdet.  

   -   **Ange egenskaperna för energischemat:** Konfigurera egenskaperna för energischemat. Avmarkera kryssrutan om du vill inaktivera en egenskap. Information om de tillgängliga inställningarna finns i [Available power management plan settings](#BKMK_Plans) i den här artikeln.  

       > [!IMPORTANT]  
       >  Aktiverade inställningar tillämpas på datorer när energischemat används. Om du avmarkerar kryssrutan för en energiinställning ändras inte värdet på klientdatorn när energischemat tillämpas. Om du avmarkerar en kryssruta återställs inte energiinställningen till det tidigare värdet som var aktiverat innan ett energischema tillämpades.  

9. Klicka på **OK** för att stänga dialog rutan<**Egenskaper** för <em>energi\>schemats namn</em>.  

10. Stäng dialog rutan <em><samlings namn\></em>**Inställningar** och Använd energischemat genom att klicka på **OK** .  

##  <a name="available-power-management-plan-settings"></a><a name="BKMK_Plans"></a> Available power management plan settings  
 I följande tabell visas de tillgängliga inställningarna för energispar funktioner i Configuration Manager. Du kan konfigurera olika inställningar för när datorn är ansluten eller körs med batteridrift. Beroende på vilken version av Windows som du använder kanske det inte går att konfigurera vissa inställningar.  

> [!NOTE]  
>  Energiinställningar som du inte konfigurerar behåller sitt aktuella värde på klientdatorer.  

|Name|Beskrivning|  
|----------|-----------------|  
|**Stäng av skärm efter (minuter)**|Anger hur lång tid i minuter som datorn måste vara inaktiv innan skärmen stängs av. Ange värdet **0** om du inte vill att energisparfunktionerna ska stänga av skärmen.|  
|**Strömsparläge efter (minuter)**|Anger hur lång tid i minuter som datorn måste vara inaktiv innan den försätts i strömsparläge. Ange värdet **0** om du inte vill att energisparfunktioner ska försätta datorn i viloläge.|  
|**Kräv lösenord när datorn startas**|Ett **Ja** eller **Nej** -värde anger om ett lösen ord krävs för att låsa upp datorn när den går in i vilo läge.|  
|**Åtgärd för strömbrytare**|Anger vilken åtgärd som vidtas när datorns ström knapp trycks ned. Möjliga värden är **ingenting**, **vilo läge**, **vilo läge**och **avstängning**.|  
|**Strömknappen på Start-menyn**|Anger vad som händer när du trycker på ström knappen på datorns **Start** -meny. Möjliga värden är **ström spar läge**, **vilo läge**och **avstängning**.|  
|**Åtgärd för vila-knappen**|Anger vad som händer när du trycker på datorns **vila** -knapp. Möjliga värden är **ingenting**, **vilo läge**, **vilo läge**och **avstängning**.|  
|**Åtgärd när locket stängs**|Anger vad som händer när användaren stänger locket på en bärbar dator. Möjliga värden är **ingenting**, **vilo läge**, **vilo läge**och **avstängning**.|  
|**Stäng av hårddisk efter (minuter)**|Anger hur lång tid i minuter som datorns hård disk måste vara inaktiv innan den stängs av. Ange värdet **0** om du inte vill att energispar funktionerna ska stänga av datorns hård disk.|  
|**Viloläge efter (minuter)**|Anger hur lång tid i minuter som datorn måste vara inaktiv innan den försätts i viloläge. Ange värdet **0** om du inte vill att energisparfunktionerna ska försätta datorn i viloläge.|  
|**Åtgärd för låg energinivå**|Anger vad som händer när datorns batteri når den angivna meddelande nivån för låg batteri nivå. Möjliga värden är **ingenting**, **vilo läge**, **vilo läge**och **avstängning**.|  
|**Åtgärd vid kritisk energinivå**|Anger vilken åtgärd som vidtas när datorns batteri når den angivna meddelande nivån för kritisk batteri nivå. Vid **batteri drift** kan värden vara **ström spar**läge, **vilo läge**och **avstängning**. När du är **ansluten till** möjliga värden **händer ingenting**, **vilo läge**, **vilo läge**och **stängs av**.|  
|**Tillåt hybridviloläge**|Om du väljer värdet **för på** eller **av** anges om Windows sparar en vilo läges fil när den försätts i vilo läge, som kan användas för att återställa datorns tillstånd i händelse av strömavbrott när den har försatts i vilo läge.<br /><br /> Hybridviloläge är avsett för stationära datorer och är som standard inte aktiverat på bärbara datorer. Om du aktiverar hybridviloläge på datorer som kör Windows 7 inaktiveras vilolägesfunktionen.|  
|**Tillåt väntelägestillstånd vid strömsparåtgärd**|Om du väljer värdet **på** eller **av** aktive RAS datorn på vänte läge, vilket fortfarande förbrukar en ström, men gör att datorn kan väckas snabbare. Om den här inställningen har värdet **Av**kan datorn bara försättas i viloläge eller stängas av.|  
|**Inaktivitetskrav för strömsparläge (%)**|Anger inaktivitetstiden i procent av datorns processortid som krävs för att datorn ska försättas i strömsparläge. För datorer som kör Windows 7 är det här värdet alltid **0**.|  
|**Aktivera Windows väckningstimer för stationära datorer**|Om du väljer värdet **Aktivera** eller **inaktivera** kan den inbyggda Windows-timern användas av energispar funktioner för att aktivera en stationär dator. När en stationär dator aktiveras med hjälp av väckningstimern i Windows förblir den aktiv i 10 minuter som standard för att ge datorn tid att installera eventuella uppdateringar eller ta emot principer.<br /><br /> Väckningstimers stöds inte på bärbara datorer för att förhindra scenarier där de kan aktiveras när datorn inte är ansluten.|  
