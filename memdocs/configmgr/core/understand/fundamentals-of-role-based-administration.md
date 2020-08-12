---
title: Rollbaserade administrations grunderna
titleSuffix: Configuration Manager
description: Använd rollbaserad administration för att styra administrativ åtkomst till Configuration Manager och objekt som du hanterar.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a2d6c3f-a4e4-4c19-b087-3caada480de9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c39d3380212debe97c2d2f33de6a98fecfb8402e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126060"
---
# <a name="fundamentals-of-role-based-administration-for-configuration-manager"></a>Grunderna i rollbaserad administration för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Med Configuration Manager använder du rollbaserad administration för att skydda den åtkomst som behövs för att administrera Configuration Manager. Du kan också skydda åtkomsten till de objekt som du hanterar, t. ex. samlingar, distributioner och platser. När du har förstått koncepten som introducerats i den här artikeln kan du [Konfigurera rollbaserad administration för Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

 Den rollbaserade administrations modellen definierar och hanterar centralt säkerhets åtkomst inställningar i hela hierarkin för alla platser och plats inställningar med hjälp av följande objekt:  

- *Säkerhets roller* tilldelas till administrativa användare för att ge användare (eller grupper av användare) behörighet till olika Configuration Manager objekt. Till exempel behörighet att skapa eller ändra klient inställningar.  

- *Säkerhets omfattningar* används för att gruppera specifika instanser av objekt som en administrativ användare ansvarar för att hantera, till exempel ett program som installerar Microsoft 365 appar.  

- *Samlingar* används för att ange grupper med användare och enhets resurser som den administrativa användaren kan hantera.  

  Med kombinationen av säkerhets roller, säkerhets omfattningar och samlingar kan du åtskilja de administrativa tilldelningar som uppfyller organisationens krav. Används tillsammans definierar de den administrativa omfattningen för en användare, vilket är vad användaren kan visa och hantera i din Configuration Manager-distribution.  

## <a name="benefits-of-role-based-administration"></a>Fördelar med rollbaserad administration  

- Platser används inte som administrativa gränser.  
- Du skapar administrativa användare för en hierarki och behöver bara tilldela dem säkerhet en enda tid.  
- Alla säkerhets tilldelningar replikeras och är tillgängliga i hela hierarkin.  
- Det finns inbyggda säkerhets roller som används för att tilldela vanliga administrations uppgifter. Skapa dina egna anpassade säkerhets roller för att stödja dina specifika affärs behov.  
- Administrativa användare ser bara de objekt de har behörighet att hantera.  
- Du kan granska administrativa säkerhetsaktiviteter.  

När du utformar och implementerar administrativ säkerhet för Configuration Manager använder du följande för att skapa en *administrativ omfattning* för en administrativ användare:  

- [Säkerhetsroller](#bkmk_Planroles)  

- [Samlingar](#bkmk_planCol)  

- [Säkerhetsomfattningar](#bkmk_PlanScope)  

 Den administrativa omfattningen styr de objekt som en administrativ användare visar i Configuration Manager-konsolen och den styr de behörigheter som en användare har på dessa objekt. Konfigurationer för rollbaserad administration replikeras som globala data till varje plats i hierarkin, och används sedan för alla administrativa anslutningar.  

> [!IMPORTANT]  
> Fördröjningar vid replikering mellan platser kan förhindra att en plats tar emot ändringar för rollbaserad administration. Information om hur du övervakar databasreplikering mellan platser finns i avsnittet [data överföringar mellan platser](../plan-design/hierarchy/data-transfers-between-sites.md) .  

##  <a name="security-roles"></a><a name="bkmk_Planroles"></a>Säkerhets roller

 Använd säkerhetsroller för att tilldela administrativa användare säkerhetsbehörigheter. Säkerhetsroller är grupper av säkerhetsbehörigheter som du tilldelar administrativa användare, så att de kan utföra administrationsuppgifter. Säkerhetsbehörigheterna definierar vilka administrativa åtgärder som en administrativ användare kan utföra, och behörigheterna kan tilldelas för separata objekt. Som säkerhetsrutin bör du tilldela säkerhetsroller som ger minsta möjliga behörighet.  

 Configuration Manager har flera inbyggda säkerhets roller som stöder vanliga grupperingar av administrativa uppgifter, och du kan skapa egna anpassade säkerhets roller som stöder dina specifika affärs behov. Exempel på inbyggda säkerhetsroller:  

- *Fullständig administratör* beviljar alla behörigheter i Configuration Manager.  

- *Till gångs hanteraren* beviljar behörigheter att hantera tillgångsinformation plats för synkronisering, tillgångsinformation rapporterings klasser, program varu inventering, maskin varu inventering och mätnings regler.  

- *Program uppdaterings hanteraren* beviljar behörigheter att definiera och distribuera program uppdateringar. Administrativa användare som är associerade med den här rollen kan skapa samlingar, program uppdaterings grupper, distributioner och mallar.  

- *Säkerhets administratören* beviljar behörigheter att lägga till och ta bort administrativa användare och associera administrativa användare med säkerhets roller, samlingar och säkerhets omfattningar. Administrativa användare som är associerade med den här rollen kan också skapa, ändra och ta bort säkerhets roller och deras tilldelade säkerhets omfattningar och samlingar.

> [!TIP]  
> Du kan visa listan med inbyggda säkerhets roller och anpassade säkerhets roller som du skapar, inklusive deras beskrivningar, i Configuration Manager-konsolen. Om du vill visa rollerna i arbets ytan **Administration** expanderar du **säkerhet**och väljer sedan **säkerhets roller**.  

 Varje säkerhetsroll har specifika behörigheter för olika objekttyper. Säkerhets rollen *program författare* har till exempel följande behörighet för program: Godkänn, skapa, ta bort, ändra, ändra mapp, flytta objekt, läsa, köra rapport och ange säkerhets omfattning.

 Du kan inte ändra behörigheter för de inbyggda säkerhets rollerna, men du kan kopiera rollen, göra ändringar och sedan spara ändringarna som en ny anpassad säkerhets roll. Du kan också importera säkerhets roller som du har exporterat från en annan hierarki, till exempel från ett test nätverk. Granska säkerhets rollerna och deras behörigheter för att avgöra om du ska använda de inbyggda säkerhets rollerna eller om du behöver skapa egna anpassade säkerhets roller.  

### <a name="to-help-you-plan-for-security-roles"></a>För att hjälpa dig att planera för säkerhets roller  

1. Identifiera de uppgifter som administrativa användare utför i Configuration Manager. Uppgifterna kan ingå i en eller flera hanteringskategorier, och exempel på uppgifter är att distribuera program och paket, distribuera operativsystem och inställningar för kompatibilitet, konfigurera platser och säkerhet, utföra revisioner, fjärrkontrollera datorer och samla in inventeringsdata.  

2. Koppla de administrativa uppgifterna till en eller flera av de inbyggda säkerhetsrollerna.  

3. Om några av de administrativa användarna utför aktiviteterna för flera säkerhets roller, tilldelar du de administrativa användarna flera säkerhets roller i stället för att skapa en ny säkerhets roll som kombinerar aktiviteterna.  

4. Om de aktiviteter som du har identifierat inte mappar till de inbyggda säkerhets rollerna, skapar och testar du nya säkerhets roller.  

Information om hur du skapar och konfigurerar säkerhets roller för rollbaserad administration finns i [skapa anpassade säkerhets roller](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole) och [Konfigurera säkerhets roller](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole) i artikeln [Konfigurera rollbaserad administration för Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) .  

##  <a name="collections"></a><a name="bkmk_planCol"></a>Samlingar

 Med samlingar specificeras de användar- och datorresurser som en administrativ användare kan visa eller hantera. Till exempel måste en administrativ användare som ska distribuera program eller fjärrstyra datorer, tilldelas en säkerhetsroll som ger åtkomst till en samling innehållande resurserna. Du kan välja samlingar av användare och enheter.  

 Mer information om samlingar finns i [Introduktion till samlingar](../../core/clients/manage/collections/introduction-to-collections.md).  

 Innan du konfigurerar rollbaserad administration ska du kontrollera om du måste skapa nya samlingar av något av följande skäl:  

- Funktionell organisation. Till exempel separata samlingar av servrar och arbetsstationer.  
- Geografisk position. Till exempel separata samlingar för Nordamerika och Europa.  
- Säkerhetskrav och affärsprocesser. Till exempel separata samlingar för produktionsdatorer respektive testdatorer.  
- Organisatorisk anpassning. Till exempel separata samlingar för varje affärsenhet.  

Information om hur du konfigurerar samlingar för rollbaserad administration finns i [Konfigurera samlingar för att hantera säkerhet](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl) i artikeln [Konfigurera rollbaserad administration för Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) .  

## <a name="security-scopes"></a><a name="bkmk_PlanScope"></a>Säkerhets omfattningar

 Använd säkerhetomfattningar för att ge administrativa användare åtkomst till skyddsbara objekt. En säkerhets omfattning är en namngiven uppsättning skydds bara objekt som tilldelas administratörs användare som en grupp. Alla säkerhetsobjekt måste tilldelas en eller flera säkerhetsomfattningar. Configuration Manager har två inbyggda säkerhets omfattningar:  

- *All* inbyggd säkerhets omfattning beviljar åtkomst till alla omfattningar. Du kan inte tilldela objekt till denna säkerhets omfattning.  

- *Standardvärdet* för inbyggd säkerhets omfattning används för alla objekt som standard. När du först installerar Configuration Manager tilldelas alla objekt säkerhets omfattningen.  

Om du vill begränsa vilka objekt som administrativa användare kan visa och hantera, måste du skapa och använda egna säkerhetsomfattningar. Säkerhets omfattningar har inte stöd för en hierarkisk struktur och kan inte kapslas. Säkerhets omfattningar kan innehålla en eller flera objekt typer, som innehåller följande objekt:  

- Aviseringsprenumerationer  
- Program  
- Startavbildningar  
- Gränsgrupper  
- Konfigurationsobjekt  
- Anpassade klientinställningar  
- Distributionsplatser och distributionsplatsgrupper  
- Drivrutinspaket
- Mappar (från och med version 1906) <!--3600867-->
- Globala villkor  
- Migreringsjobb
- Operativsystemavbildningar
- Paket för operativsystemsinstallation  
- Paket  
- Frågor  
- Webbplatser  
- Regler för avläsning av programvara  
- Programuppdateringsgrupper  
- Programuppdateringspaket  
- Aktivitetssekvenspaket  
- Inställningsobjekt och paket för Windows CE-enheter  

Det finns även objekt som du inte kan inkludera i säkerhets omfattningar eftersom de endast skyddas av säkerhets roller. Administrativ åtkomst till dessa objekt kan inte begränsas till en delmängd av de tillgängliga objekten. Till exempel kanske det finns en administrativ användare som skapar gränsgrupper som används för en specifik plats. Eftersom gräns objektet inte stöder säkerhets omfattningar kan du inte tilldela den här användaren en säkerhets omfattning som ger åtkomst till endast de gränser som kan kopplas till den platsen. Eftersom ett begränsnings objekt inte kan associeras till en säkerhets omfattning, kan användaren komma åt alla gränser i hierarkin när du tilldelar en säkerhets roll som innehåller åtkomst till begränsnings objekt till en användare.  

Objekt som inte är begränsade av säkerhets omfattningar omfattar följande objekt:  

- Active Directory-skogar  
- Administrativa användare  
- Aviseringar  
- Principer för program mot skadlig kod  
- Gränser  
- Datorkopplingar  
- Standardklientinställningar  
- Distributionsmallar  
- Enhetsdrivrutiner  
- Exchange Server-anslutning  
- Mappningar för migrering mellan platser  
- Profiler för mobilenhetsregistrering  
- Säkerhetsroller  
- Säkerhetsomfattningar  
- Platsadresser  
- Platssystemroller  
- Programvarutitlar  
- Programuppdateringar  
- Statusmeddelanden  
- Mappningar mellan användare och enheter  

Skapa säkerhetsomfattningar när du vill begränsa åtkomsten till separata instanser av objekt. Till exempel:  

- Anta att du har en grupp av administrativa användare som måste kunna visa produktionsprogram men inte testprogram. Skapa en säkerhetsomfattning för produktionsprogram och en annan omfattning för testprogrammen.  

- Olika administrativa användare behöver olika åtkomst till instanser av en objekttyp. Till exempel kanske en viss grupp av administrativa användare behöver behörigheten Läsa för vissa programuppdateringsgrupper, medan en annan grupp av administrativa användare behöver behörigheterna Ändra och Ta bort för andra programuppdateringsgrupper. Skapa olika säkerhetsomfattningar för de olika programuppdateringsgrupperna.  

Information om hur du konfigurerar säkerhets omfattningar för rollbaserad administration finns i avsnittet [Konfigurera säkerhets omfattningar för ett objekt](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope) i artikeln [Konfigurera rollbaserad administration för Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) .  

## <a name="next-steps"></a>Nästa steg

[Konfigurera rollbaserad administration för Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
