---
title: Teknisk för hands version 1711 | Microsoft Docs
titleSuffix: Configuration Manager
description: Lär dig mer om de funktioner som finns i teknisk för hands version 1711 för Configuration Manager.
ms.date: 11/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e68dc12-6776-437a-9138-45cd7d4bf9cf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e6f8ed1562392899b46a082bf8f64872c7e1b67d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721292"
---
# <a name="capabilities-in-technical-preview-1711-for-configuration-manager"></a>Funktioner i Technical Preview 1711 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1711. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. Innan du installerar den här versionen av Technical Preview kan du läsa [Technical Preview för Configuration Manager](../../core/get-started/technical-preview.md) för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Kända problem i den här tekniska för hands versionen:**
- **Stöd för Windows 10, version 1709 (även kallat uppdaterings uppdateringen)**.  Från och med den här Windows-versionen innehåller Windows Media flera versioner. När du konfigurerar en aktivitetssekvens för att använda ett uppgraderings paket för operativ system eller en operativ system avbildning måste du välja en [version som stöds för användning av Configuration Manager](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).
- **Uppdatering till en ny för hands version Miss lyckas när du har en plats server i passivt läge**. När du kör en för hands version som har en [primär plats server i passivt läge](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), måste du avinstallera plats servern för passivt läge innan du kan uppdatera för hands versions platsen till den nya för hands versionen. Du kan installera om den passiva läges plats servern efter att platsen har slutfört uppdateringen.

  Så här avinstallerar du plats servern för passivt läge:
  1. I-konsolen går du till **Administration** > **Översikt** > **plats konfigurations** > **servrar och plats system roller**och väljer sedan plats servern för passivt läge.
  2. I fönstret **plats system roller** högerklickar du på **plats Server** rollen och väljer sedan **ta bort roll**.
  3. Högerklicka på plats servern för passivt läge och välj sedan **ta bort**.
  4. När plats servern har avinstallerats startar du om tjänsten **CONFIGURATION_MANAGER_UPDATE**på den aktiva primära plats servern.

**Följande är nya funktioner som du kan prova med den här versionen.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-to-run-task-sequence"></a>Förbättringar för att köra aktivitetssekvensen
<!-- 1261338 -->

Den här tekniska för hands versionen kommer att förbättra steget Kör aktivitetssekvens. Förbättringarna omfattar följande objekt:

- Stöd för alla distributions scenarier för operativ system från Software Center, PXE och media.
- Förbättringar av konsol åtgärder som kopiering, import, export och varning vid borttagning av objekt.
- Stöd för guiden **skapa** förinstallerat innehåll.
- Integrering med distributions verifiering.
- Steget Kör aktivitetssekvens kan nu användas på flera nivåer av aktivitetssekvenser, inte bara en enda överordnad-underordnad relation. Relationer på flera nivåer ökar komplexiteten, så Använd med försiktighet. Relationerna är fortfarande markerade för cirkulära referenser.

### <a name="try-it-out"></a>prova!  

Försök att utföra följande uppgifter och skicka sedan oss **feedback** från fliken **Start** i menyfliksområdet så att vi kan se hur det fungerade:

1. I redigeraren för aktivitetssekvens klickar du på **Lägg till**, väljer **Allmänt**och klickar på **Kör aktivitetssekvens**.
2. Klicka på **Bläddra** för att välja den underordnade aktivitetssekvensen.

## <a name="allow-user-interaction-when-installing-an-application----1356976---"></a>Tillåt användar interaktion när du installerar ett program <!-- 1356976 -->

Med den här för hands versionen kan du låta en användare interagera med en programinstallation under körningen av aktivitetssekvensen. Du kan till exempel köra en installations process som efterfrågar slutanvändaren för olika alternativ. Vissa programinstallationer kan inte ha inaktive rad användar meddelanden eller så kanske installations processen kräver specifika konfigurations värden som bara är kända för användaren. Med den här funktionen kan du hantera dessa installations scenarier.

### <a name="try-it-out"></a>prova!

Försök att utföra följande uppgifter och skicka sedan **feedback** från fliken **Start** i menyfliksområdet så att vi kan se hur det fungerade:

1.  Skapa eller redigera ett program. Mer information finns i [skapa program med Configuration Manager](../../apps/deploy-use/create-applications.md).

    a. Välj fliken **användar upplevelse** i egenskaperna för **Windows Installer (\*MSI-filen)**.

    b. Välj **Installera för system** för **installations beteende**.

    c. Välj **om en användare är inloggad** för **inloggnings krav**.

    d. Välj **Normal** för **visning av installations program**. Du kan välja mellan tre alternativ: **minimerat**, **normalt**eller **maximerat**.

    e. Markera rutan **Tillåt att användare interagerar med programinstallationen** .

2.  Skapa eller redigera en aktivitetssekvens för att installera programmet med hjälp av steget **installera program** . Mer information finns i [installera program](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication) i stegen i [aktivitetssekvensen](../../osd/understand/task-sequence-steps.md).

    a. Avbildnings aktivitetssekvensen efter steget installera Windows och Configuration Manager.

    b. Aktivitetssekvens för uppgradering på plats i den efter bearbetnings gruppen.

3.  Distribuera aktivitetssekvensen till en klient.
4.  Installera aktivitetssekvensen från Software Center.

Under aktivitetssekvensen visas programinstallationens gränssnitt på mål slutanvändarens enhet. Förloppet för aktivitetssekvensen pausas tills slutanvändaren Slutför programinstallationens arbets flöde.

### <a name="install-using-the-wizard"></a>Installera med hjälp av guiden

Du kan också använda den här funktionen när du distribuerar en app med hjälp av guiden.

1. Skapa eller redigera ett program.
2. Distribuera programmet till en klient.
3. Installera programmet från Software Center. Programmets installations gränssnitt bör visas. Slutanvändaren bör följa installations guiden för programmet och programmet kommer att installeras.




<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Nästa steg
Information om hur du installerar eller uppdaterar den tekniska för hands versionen finns i [teknisk för hands version för Configuration Manager](technical-preview.md).    
