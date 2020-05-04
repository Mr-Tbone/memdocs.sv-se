---
title: Underhållsaktiviteter
titleSuffix: Configuration Manager
description: Förstå vilka underhålls aktiviteter som ska utföras för Configuration Manager-platser och-hierarkier och när de ska utföras.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e0a71fc2f09e967944adfc4266e25eb20acfb9fe
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713732"
---
# <a name="maintenance-tasks-for-configuration-manager"></a>Underhålls aktiviteter för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager platser och hierarkier kräver regelbundet underhåll och övervakning för att tillhandahålla tjänster effektivt och kontinuerligt. Regelbundet underhåll garanterar att maskin vara, program vara och Configuration Manager databas fortfarande fungerar korrekt och effektivt. Optimala prestanda minskar risken för problem avsevärt.  

 Information om hur du konfigurerar aviseringar och använder status systemet för att övervaka hälso tillståndet för Configuration Manager finns i [använda aviseringar och status systemet för Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

## <a name="maintenance-tasks"></a><a name="bkmk_MTs"></a>Underhålls aktiviteter

 Regelbundet underhåll är viktigt för att säkerställa korrekta plats åtgärder. Behåll en underhålls logg för att dokumentera underhålls datum, vem som gjorde underhåll och eventuella underhålls relaterade kommentarer om aktiviteterna. Om du vill underhålla din webbplats bör du överväga ett dagligt eller veckovis underhåll. Vissa aktiviteter kan kräva ett annat schema. Det vanliga underhållet kan omfatta både inbyggda underhålls aktiviteter och andra uppgifter som konto underhåll för att upprätthålla efterlevnaden av företagets principer.  

 Använd följande information som vägledning för att hjälpa dig att planera när du ska göra olika underhålls aktiviteter. Använd dessa listor som start punkt och Lägg till aktiviteter som du kan behöva.  

### <a name="daily-tasks"></a>Dagliga uppgifter
Följande är underhålls aktiviteter som du kan tänka på enligt ett dags schema:  

- Kontrol lera att fördefinierade underhålls aktiviteter som är schemalagda att köras dagligen körs.  

- Kontrol lera statusen för Configuration Manager databasen.  

- Kontrol lera status för plats Server.  

- Kontrol lera Configuration Manager plats systemets inkorgar för fil-loggfiler.  

- Kontrol lera status för plats system.  

- Kontrol lera händelse loggarna för operativ systemet från plats systemen.  

- Kontrol lera SQL Server fel loggen från plats databasens dator.  

- Kontrol lera system prestanda.  

- Kontrol lera Configuration Manager aviseringar.  

### <a name="weekly-tasks"></a>Veckovisa uppgifter

Följande är underhålls aktiviteter som du kan tänka på för ett vecko schema:  

- Kontrol lera att fördefinierade underhålls aktiviteter som är schemalagda att köras veckovis körs.  

- Ta bort onödiga filer från plats system.  

- Producera och distribuera slut användar rapporter om det behövs.  

- Säkerhetskopiera program, säkerhet och system händelse loggar och rensa dem.  

- Kontrol lera storleken på plats databasen och kontrol lera att det finns tillräckligt med ledigt disk utrymme på plats databas servern så att plats databasen kan växa.  

- Gör SQL Server databas underhåll på plats databasen enligt din SQL Server underhålls plan.  

- Kontrol lera tillgängligt disk utrymme på alla plats system.  

- Kör diskdefragmentering-verktyg på alla plats system.  

### <a name="periodic-tasks"></a>Periodiska uppgifter

Vissa uppgifter som inte kräver dagligt eller veckovis underhåll är viktiga för att säkerställa övergripande plats hälsa. Dessa uppgifter garanterar också att säkerhets-och katastrof återställnings planer är uppdaterade. Följande är underhålls aktiviteter som du kan överväga för ett mer periodiskt schema än de dagliga eller vecko Visa aktiviteterna:  

- Ändra konton och lösen ord, om det behövs, enligt din säkerhets plan.  

- Granska underhålls planen för att kontrol lera att schemalagda underhålls aktiviteter schemaläggs korrekt och på ett effektivt sätt beroende på konfigurerade plats inställningar.  

- Granska Configuration Manager hierarkins design för alla nödvändiga ändringar.  

- Kontrol lera nätverks prestanda för att se till att ändringarna inte har gjorts som påverkar plats åtgärder.  

- Kontrol lera att Active Directory inställningar som påverkar plats åtgärder inte har ändrats. Kontrol lera till exempel att undernät som har tilldelats Active Directory-platser och som används som gränser för Configuration Managers platsen inte har ändrats.  

- Granska din Disaster Recovery-plan för alla nödvändiga ändringar.  

- Gör en webbplats återställning i enlighet med katastrof återställnings planen i ett testlabb genom att använda en säkerhets kopia av den senaste säkerhets kopian som skapades av underhålls åtgärden plats Server för säkerhets kopiering.

- Kontrol lera om det finns några fel i maskin varan eller för tillgängliga maskin varu uppdateringar.  

- Kontrol lera platsens övergripande hälsa.  

## <a name="maintain-the-operational-health-of-your-site-database"></a><a name="BKMK_UseMTs"></a>Upprätthålla drift hälsan för plats databasen

 Medan Configuration Manager-platsen och-hierarkin utför de aktiviteter som du schemalägger och ställer in, lägger plats komponenter kontinuerligt till data i Configuration Manager-databasen. Allteftersom data mängden växer avvisar databas prestanda och det lediga lagrings utrymmet i databasen. Du kan konfigurera plats underhålls aktiviteter för att ta bort föråldrade data som du inte längre behöver.  

 Configuration Manager innehåller fördefinierade underhålls aktiviteter som du kan använda för att upprätthålla hälsan för Configuration Manager-databasen. Alla underhålls aktiviteter är inte tillgängliga på varje plats, som standard. Flera aktiviteter är aktiverade medan vissa inte är det och alla stöder ett schema som du kan konfigurera.  

 De flesta underhålls aktiviteter tar regelbundet bort inaktuella data från den Configuration Manager databasen. Att minska storleken på databasen genom att ta bort onödiga data förbättrar databasens prestanda och integritet, vilket ökar effektiviteten hos platsen och hierarkin. Andra aktiviteter, t. ex. **återuppbyggnad av index**, hjälper till att upprätthålla databasens effektivitet. Andra aktiviteter, t. ex. aktiviteten **säkerhetskopiera plats Server** , hjälper dig att förbereda för katastrof återställning.  

> [!IMPORTANT]
> När du planerar schemat för alla aktiviteter som tar bort data bör du överväga att använda dessa data i hela hierarkin. När en aktivitet som tar bort data körs på en plats tas informationen bort från Configuration Manager databasen och den här ändringen replikeras till alla platser i hierarkin. Borttagningen kan påverka andra uppgifter som förlitar sig på dessa data. På den centrala administrations platsen kan du till exempel ställa in identifieringen så att den körs en tid per månad för att identifiera datorer som inte är klient datorer. Du planerar att installera Configuration Manager-klienten på dessa datorer inom två veckor från identifieringen. Men på en plats i hierarkin konfigurerar en administratör att aktiviteten Ta bort föråldrade identifierings data ska köras var sjunde dag. Resultatet är att sju dagar efter att datorer som inte är klient datorer identifieras, tas de bort från Configuration Manager databasen. På den centrala administrations webbplatsen förbereder du att push-installera Configuration Manager-klienten på den nya datorn dag 10. Men eftersom aktiviteten Ta bort föråldrade identifierings data nyligen har kört och tagit bort data som är sju dagar eller äldre, är de nyligen identifierade datorerna inte längre tillgängliga i databasen.

När du har installerat en Configuration Manager plats granskar du de tillgängliga underhålls aktiviteterna och aktiverar de aktiviteter som krävs för dina åtgärder. Granska standardschemat för varje aktivitet och Ställ in schemat för att finjustera underhålls aktiviteten så att den passar din hierarki och miljö. Även om standardschemat för varje aktivitet bör passa de flesta miljöer, kan du övervaka prestanda för dina platser och databaser och förvänta dig att finjustera uppgifter för att öka effektiviteten i distributionen. Planera för att regelbundet granska plats-och databas prestanda och konfigurera om underhålls aktiviteterna och deras scheman för att bibehålla denna effektivitet.  

## <a name="set-up-maintenance-tasks"></a>Konfigurera underhålls aktiviteter

 Varje Configuration Manager-plats har stöd för underhålls aktiviteter som hjälper dig att underhålla plats databasens operativa effektivitet. Som standard aktive ras flera underhålls aktiviteter på varje plats, och alla aktiviteter stöder oberoende scheman. Underhålls aktiviteter konfigureras separat för varje plats och tillämpas på databasen på den platsen. Vissa åtgärder, t. ex. att **ta bort föråldrade identifierings data**, påverkar dock information som är tillgänglig på alla platser i en hierarki.  

 Endast de underhålls aktiviteter som du kan ställa in på en plats visas i Configuration Manager-konsolen. En fullständig lista över underhålls aktiviteter per plats typ finns i [referens för underhålls aktiviteter för Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 Använd följande procedur för att få hjälp att ställa in de vanliga inställningarna för underhålls aktiviteter.  

### <a name="to-set-up-maintenance-tasks-for-configuration-manager-version-1906"></a><a name="bkmk_MTs1906"></a>Konfigurera underhålls aktiviteter för Configuration Manager version 1906
<!--3555894-->
Från och med version 1906 kan nu underhålls aktiviteter för plats Server visas, redige ras och övervakas från en egen flik i vyn information på en plats Server. Du kan fortfarande redigera underhålls aktiviteter genom att välja **plats underhåll** i gruppen **Inställningar** som du gjorde tidigare Configuration Manager versioner.

1. I Configuration Manager-konsolen går du till **Administration** > **plats konfiguration** >**platser**.
1. Välj en plats i listan och klicka sedan på fliken **underhåll aktiviteter** i informations panelen.
1. Endast uppgifter som är tillgängliga på den valda platsen visas. Högerklicka på en av underhålls aktiviteterna och välj ett av följande alternativ:
   - **Aktivera** – aktivera uppgiften.
   - **Inaktivera** – Stäng av uppgiften.
   - **Redigera** – redigera aktivitets schemat eller dess egenskaper.

![Fliken för underhålls aktiviteter i detaljvyn för en plats Server](./media/3555894-maintenance-tasks.png)

Fliken **underhålls aktiviteter** innehåller information som:

- Om aktiviteten är aktive rad
- Aktivitets schemat
- Senaste start tid
- Senaste slut för ande tid
- Om uppgiften har slutförts
 
### <a name="to-set-up-maintenance-tasks-for-configuration-manager-version-1902-and-prior"></a>Konfigurera underhålls aktiviteter för Configuration Manager version 1902 och tidigare

1. I Configuration Manager-konsolen går du till **Administration** > **plats konfiguration** >**platser**.
2. Välj den plats som innehåller den underhålls aktivitet som du vill konfigurera.  
3. Välj **plats underhåll**i gruppen **Inställningar** på fliken **Start** och välj sedan den underhålls aktivitet som du vill konfigurera. Endast uppgifter som är tillgängliga på den valda platsen visas.

4. Konfigurera uppgiften genom att välja **Redigera**. Kontrol lera att kryss rutan **Aktivera den här uppgiften** är markerad och Ställ in ett schema för när aktiviteten körs. Om aktiviteten också tar bort föråldrade data ställer du in den ålder med data som ska tas bort från databasen när aktiviteten körs. Klicka på **OK** för att stänga aktivitets **egenskaperna**.

   > [!NOTE]  
   > För att **ta bort föråldrade status meddelanden**ställer du in ålder på de data som ska tas bort när du ställer in status filter regler.  

5. Om du vill aktivera eller inaktivera uppgiften utan att redigera aktivitets egenskaperna väljer du knappen **Aktivera** eller **inaktivera** . Knappens etikett ändras beroende på aktivitetens aktuella konfiguration.  
6. När du är klar med att konfigurera underhålls aktiviteterna väljer du **OK** för att slutföra proceduren.

## <a name="next-steps"></a>Nästa steg

[Referens för underhållsaktivitet](reference-for-maintenance-tasks.md)
