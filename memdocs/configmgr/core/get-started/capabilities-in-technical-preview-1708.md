---
title: Teknisk för hands version 1708
titleSuffix: Configuration Manager
description: Lär dig mer om de funktioner som finns i teknisk för hands version 1708 för Configuration Manager.
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ab5cc83cc8e7bb51477d84a50f18d4f6b73f286d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721334"
---
# <a name="capabilities-in-technical-preview-1708-for-configuration-manager"></a>Funktioner i Technical Preview 1708 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1708. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. Innan du installerar den här versionen av Technical Preview kan du läsa [Technical Preview för Configuration Manager](../../core/get-started/technical-preview.md) för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Kända problem i den här tekniska för hands versionen:**
- **Det går inte att uppdatera till för hands version 1708 när du har en plats server i passivt läge**. När du kör för hands version 1706 eller 1707 och har en [primär plats server i passivt läge](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), måste du avinstallera plats servern för passivt läge innan du kan uppdatera för hands versionen till version 1708. Du kan installera om den passiva läges plats servern efter att platsen har kört version 1708.

  Så här avinstallerar du plats servern för passivt läge:
  1. I-konsolen går du till **Administration** > **Översikt** > **plats konfigurations** > **servrar och plats system roller**och väljer sedan plats servern för passivt läge.
  2. I fönstret **plats system roller** högerklickar du på **plats Server** rollen och väljer sedan **ta bort roll**.
  3. Högerklicka på plats servern för passivt läge och välj sedan **ta bort**.
  4. När plats servern har avinstallerats startar du om tjänsten **CONFIGURATION_MANAGER_UPDATE**på den aktiva primära plats servern.




**Följande är nya funktioner som du kan prova med den här versionen.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Förbättringar för att ange skript parametrar när du distribuerar PowerShell-skript från Configuration Manager
<!-- 1236459 -->

Från Configuration Manager 1706 och senare kan du [skapa och köra PowerShell-skript från Configuration Manager-konsolen](../../apps/deploy-use/create-deploy-scripts.md).

I [Technical Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)expanderade vi den här funktionen för att låta Configuration Manager läsa parametrar från skriptet.

I den här tekniska för hands versionen har vi utökat skript parameter funktionen för att identifiera vilka parametrar som är obligatoriska och vilka som är valfria och uppmanas att ange dessa.

### <a name="try-it-out"></a>prova!

1. Följ instruktionerna för att [skapa och köra PowerShell-skript från Configuration Manager-konsolen](../../apps/deploy-use/create-deploy-scripts.md).
2. På sidan ny **skript parametrar** i **guiden skapa skript**väljer du en parameter och redigerar sedan dess värden.
Guiden visar vilka parametrar som är obligatoriska och vilka som är valfria.
4. När du har redigerat parametrarna slutför du guiden.

När skriptet körs använder det alla parameter värden som du har konfigurerat. Om du inte konfigurerade en obligatorisk parameter uppmanas slutanvändaren att ange parametern när skriptet körs.

## <a name="management-insights"></a>Hanteringsinsikter
<!-- 1353967 -->
Nu kan du få insikter om den aktuella statusen för din miljö baserat på analys av data i plats databasen. Insights hjälper dig att bättre förstå din miljö och vidta åtgärder baserat på insikter. Granska Management Insights i Configuration Manager-konsolen i **administrations** > **hantering insikter** > om**alla insikter**. I den här versionen finns nu följande insikter:

- **Program utan distributioner**: visar en lista över de program i miljön som inte har aktiva distributioner. Detta hjälper dig att hitta och ta bort program som inte används för att förenkla listan över program som visas i-konsolen.
- **Tomma samlingar**: visar samlingar i din miljö som inte har några medlemmar. Du kan ta bort dessa samlingar för att förenkla listan över samlingar som visas när du distribuerar objekt, till exempel.


## <a name="restart-computers-from-the-configuration-manager-console"></a>Starta om datorer från Configuration Manager-konsolen   
<!-- 1356283 -->
Från och med den här versionen kan du använda Configuration Manager-konsolen för att identifiera klient enheter som kräver en omstart och sedan använda en klient meddelande åtgärd för att starta om dem.

För att identifiera enheter som väntar på en omstart, går du till **till gångar och efterlevnad** > **enheter** och väljer en samling med enheter som kan behöva startas om. När du har valt en samling kan du Visa status för varje enhet i informations fönstret i en ny kolumn med namnet **väntar på omstart**. Varje enhet har värdet **Ja**eller **Nej**.

Så här skapar du klient meddelandet för att starta om en enhet:
1. Leta upp den enhet som du vill starta om i noden enheter i-konsolen.
2. Högerklicka på enheten, Välj **klient meddelande**och välj sedan **starta om**. Då öppnas ett informations fönster om omstarten. Klicka på **OK** för att bekräfta restart-begäran.

När meddelandet tas emot av en klient öppnas ett meddelande fönster i **Software Center** som informerar användaren om omstarten. Som standard sker omstarten efter 90 minuter. Du kan ändra omstarts tiden genom att konfigurera [klient inställningar](../clients/deploy/configure-client-settings.md). Inställningarna för omstarts beteendet finns på fliken [dator omstart](../clients/deploy/about-client-settings.md#computer-restart) i standardinställningarna.


### <a name="try-it-out"></a>prova!
Försök att utföra följande uppgifter och skicka sedan oss **feedback** från fliken **Start** i menyfliksområdet så att vi kan se hur det fungerade:
1. Distribuera en app eller uppdatera till en enhet som kräver att enheten startas om för att slutföra installationen.
2. Leta upp enheten i noden **till gångar och efterlevnad** > **Devices** i-konsolen och bekräfta att den visar **Ja** i kolumnen **väntande omstart** . Det kan ta upp till 20 minuter innan statusen för väntande omstart visas i-konsolen.
3. Övervaka enheten för att bekräfta att Software Center-meddelandet öppnas och att enheten har startats om.


## <a name="software-center-customization"></a>Anpassning av Software Center
<!-- 1351224 -->
Du kan lägga till företags anpassnings element och ange synlighet för flikar i Software Center. Du kan lägga till ett visst företags namn för Software Center, ange ett färg schema för Software Center-konfiguration, ange en företags logo typ och ange de synliga flikarna för klient enheter.

### <a name="customize-software-center"></a>Anpassa Software Center

Så här ändrar du Software Center:

1. I **Configuration Manager** -konsolen väljer du **Administration** > **klient inställningar**. Klicka på önskad klient inställnings instans.
2. På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.
3. Välj **Software Center**i dialog rutan **standardinställningar** .
4. Välj **Ja** för att **välja nya inställningar för att ange företags information** för att aktivera inställningarna för anpassning av Software Center.
5. Ange **företagets namn**.
6. Välj ditt **färg schema för Software Center**.
7. Klicka på **Bläddra** för att gå till din logo typ för Software Center. Logo typen måste vara en JPEG eller PNG med 400 x 100 pixlar med en maximal storlek på 750 KB.
8. Välj **Ja** om du vill att flikar ska synas i Software Center för klient enheter. Minst en flik måste vara synlig:

    -  Fliken aktivera program
    -  Fliken aktivera uppdateringar
    -  Aktivera fliken operativ system
    -  Fliken aktivera installations status
    -  Aktivera fliken hälsoenhets krav
    -  Aktivera fliken Alternativ

### <a name="next-steps"></a>Nästa steg

Mer information om program hantering i Configuration Manager finns i [Introduktion till program hantering](../../apps/understand/introduction-to-application-management.md).
