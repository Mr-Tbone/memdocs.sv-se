---
title: Introduktion till operativsystemdistribution
titleSuffix: Configuration Manager
description: Förstå begreppen innan du distribuerar operativ system i din Configuration Managers miljö.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d9a1c545-8301-492c-832f-2c108ff93c77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d53ab2221e3ee936f9b09592a7c7b383b200c928
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720389"
---
# <a name="introduction-to-operating-system-deployment-in-configuration-manager"></a>Introduktion till operativ Systems distribution i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan använda Configuration Manager för att distribuera operativ system på flera olika sätt. Använd informationen i det här avsnittet för att förstå hur du distribuerar operativ system och automatiserar uppgifter. 

##  <a name="the-operating-system-deployment-process"></a><a name="BKMK_OSDeploymentProcess"></a>Processen för operativ Systems distribution  
 Configuration Manager tillhandahåller flera metoder som du kan använda för att distribuera ett operativ system. Oavsett vilken distributionsmetod du använder finns det flera åtgärder du måste utföra:  

-   Identifiera alla Windows-enhetsdrivrutiner som krävs för att köra startavbildningen eller installera operativsystemavbildningen som du behöver distribuera.  

-   Identifiera startavbildningen som du vill använda för att starta måldatorn.  

-   Spara en avbildning av operativsystemet som du vill distribuera genom att använda en aktivitetssekvens. Alternativt kan du använda en avbildning av operativsystemet som är standard.  

-   Distribuera startavbildningen, operativsystemsavbildningen och eventuellt relaterat innehåll till en distributionsplats.  

-   Skapa en aktivitetssekvens med stegen för att distribuera startavbildningen och avbildningen av operativsystemet.  

-   Distribuera aktivitetssekvensen till en samling datorer.  

-   Övervaka distributionen.  

##  <a name="operating-system-deployment-scenarios"></a><a name="BKMK_OSDScenarios"></a>Scenarier för distribution av operativ system  
 Det finns många scenarier för operativ Systems distribution i Configuration Manager som du kan välja mellan beroende på din miljö och syftet med installationen av operativ systemet.  Du kan till exempel partitionera och formatera en befintlig dator med en ny version av Windows eller uppgradera Windows till den senaste versionen. För att hjälpa dig att avgöra vilken distributions metod som uppfyller dina behov kan du gå igenom [scenarier för att distribuera operativ system i företag](../deploy-use/scenarios-to-deploy-enterprise-operating-systems.md).  Du kan välja mellan följande scenarier för operativsystemsdistribution:  

-   [Uppgradera Windows till den senaste versionen](../deploy-use/upgrade-windows-to-the-latest-version.md)  

-   [Uppdatera en befintlig dator med en ny version av Windows](../deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installera en ny version av Windows på en ny dator (utan operativsystem)](../deploy-use/install-new-windows-version-new-computer-bare-metal.md)  

-   [Ersätta en befintlig dator och överföra inställningar](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="methods-to-deploy-operating-systems"></a><a name="BKMK_OSDMethods"></a>Metoder för att distribuera operativ system  
 Det finns flera metoder som du kan använda för att distribuera operativ system till Configuration Manager klient datorer.  

- **PXE-initierad distribution**: PXE-initierad distribution innebär att klientdatorerna begär distribution via nätverket. Med den här distributionsmetoden skickas operativsystemsavbildningen och en Windows PE-startavbildning till en distributionsplats som är konfigurerad att ta emot PXE-startbegäranden. Mer information finns i [använda PXE för att distribuera Windows via nätverket med Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

- **Göra operativsystem tillgängliga i Software Center**: Du kan distribuera ett operativsystem och göra det tillgängligt i Software Center. Configuration Manager-klienter kan starta installationen av operativ systemet från Software Center. Mer information finns i [ersätta en befintlig dator och överföra inställningar](../deploy-use/replace-an-existing-computer-and-transfer-settings.md).  

- **Multicast-distribution**: Multicast-distribution sparar nätverksbandbredd genom att data skickas samtidigt till flera klienter i stället för att en kopia av informationen skickas till varje klient via en separat anslutning. Med den här distributionsmetoden skickas operativsystemsavbildningen till en distributionsplats. Den distribuerar i sin tur avbildningen när klientdatorerna begär distribution. Mer information finns i [använda multicast för att distribuera Windows via nätverket](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

- **Distribution med startbara media**: Vid distribution med startbara media kan du distribuera operativsystemet när måldatorn startar. När måldatorn startas, tar den emot aktivitetssekvensen, operativsystemsavbildningen och allt övrigt innehåll som behövs från nätverket. Eftersom innehållet inte finns med på mediet, kan du uppdatera innehållet utan att behöva ta fram ett nytt medium. Mer information finns i [Skapa startbara media](../deploy-use/create-bootable-media.md).  

- **Fristående mediedistribution**: Med fristående mediedistribution kan du distribuera operativsystem under följande förhållanden:  

  - I miljöer där det inte är praktiskt att kopiera en operativsystemsavbildning eller andra stora paket via nätverket.  

  - I miljöer utan nätverksanslutning eller i nätverk med låg bandbredd.  

    Mer information finns i [skapa fristående media](../deploy-use/create-stand-alone-media.md).  

- **Distribution med förinstallerade media**: Vid distribution med förinstallerade media kan du distribuera ett operativsystem till en dator som inte är helt etablerad. Det förinstallerade mediet är en WIM-fil (Windows Imaging format) som kan installeras på en dator utan operativ system av tillverkaren eller till ett företag som inte är anslutet till Configuration Managers miljön.  

   Senare i Configuration Managers miljön startar datorn med hjälp av den Start avbildning som tillhandahålls av mediet och ansluter sedan till plats hanterings platsen för tillgängliga aktivitetssekvenser som slutför nedladdnings processen. Den här distributionsmetoden kan minska nätverkstrafiken, eftersom startavbildningen och operativsystemsavbildningen redan finns på måldatorn. Du kan ange vilka program, paket och drivrutinspaket som du vill ha med på förinstallerade media. Mer information finns i [skapa för beredda medier](../deploy-use/create-prestaged-media.md).  

##  <a name="boot-images"></a><a name="BKMK_BootImages"></a>Start avbildningar  
 En start avbildning i Configuration Manager är en Windows PE-avbildning (WinPE) som används under en operativ Systems distribution. Startavbildningar används för att starta en dator i WinPE, som är ett minimalt operativsystem med ett begränsat antal komponenter och tjänster som förbereder måldatorn för Windows-installationen. Configuration Manager tillhandahåller två start avbildningar: en som stöder x86-plattformar och en som stöder x64-plattformar. Dessa betraktas som standardstartavbildningar. Start avbildningar som du skapar och lägger till i Configuration Manager betraktas som anpassade avbildningar. Standard start avbildningar kan ersättas automatiskt när du uppdaterar Configuration Manager. Mer information om startavbildningar finns i [Hantera startavbildningar](../get-started/manage-boot-images.md).  

##  <a name="operating--system-images"></a><a name="BKMK_OSImages"></a>Operativ system avbildningar  
 Operativsystemavbildningar i Configuration Manager sparas i Windows Imaging-filformatet (WIM) och utgör en komprimerad samling med referensfiler och mappar som behövs för att installera och konfigurera ett operativsystem på en dator. Du måste välja en operativsystemavbildning för alla distributionsscenarier för operativsystem. Du kan använda operativsystemavbildningen som är standard eller skapa operativsystemavbildningen från en referensdator som du konfigurerar. Mer information finns i [Hantera operativ Systems avbildningar](../get-started/manage-operating-system-images.md).  

##  <a name="operating-system-upgrade-packages"></a><a name="BKMK_OSUpgradePackages"></a>Uppgraderings paket för operativ system  
 Uppgraderingspaket för operativsystem används för att uppgradera ett operativsystem och är påbörjade operativsystemsdistributioner. Du importerar uppgraderings paket för operativ system till Configuration Manager från en DVD eller monterad ISO-fil. Mer information finns i [Hantera uppgraderings paket för operativ system](../get-started/manage-operating-system-upgrade-packages.md).  

##  <a name="media-to-deploy-operating-systems"></a><a name="BKMK_OSDMedia"></a>Media för att distribuera operativ system  
 Du kan skapa flera olika typer av medier som kan användas för att distribuera operativsystem. Detta omfattar avbildningsmedier som används för att skapa operativsystemsavbildningar och fristående, förberedda och startbara medier som används för att distribuera ett operativsystem. Genom att använda medier kan du distribuera operativ system på datorer som inte har en nätverks anslutning eller som har en anslutning med låg bandbredd till din Configuration Manager plats. Mer information om hur du använder Media finns i [skapa media för aktivitetssekvens](../deploy-use/create-task-sequence-media.md).  

##  <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a>Enhets driv rutiner  
 Du kan installera enhetsdrivrutiner på måldatorer utan att inkludera dem i operativsystemsavbildningen som distribueras. Configuration Manager tillhandahåller en driv rutins katalog som innehåller referenser till alla enhets driv rutiner som du importerar till Configuration Manager. Drivrutinskatalogen finns i arbetsytan **Programvarubibliotek** och består av två noder: **Drivrutiner** och **Drivrutinspaket**. Noden **Drivrutiner** innehåller en lista med alla drivrutiner som du har importerat till drivrutinskatalogen. Du kan använda den för att se detaljer om varje importerad drivrutin, ändra vilket drivrutinspaket eller vilken startavbildning en drivrutin tillhör, aktivera eller inaktivera en drivrutin med mera. Mer information finns i [Hantera driv rutiner](../get-started/manage-drivers.md).  

##  <a name="save-and-restore-user-state"></a><a name="BKMK_OSDUserState"></a>Spara och återställa användar tillstånd  
 När du distribuerar operativsystem, kan du spara användartillståndet från måldatorn, distribuera operativsystemet och sedan återställa användartillståndet efter att operativsystemen har distribuerats. Den här processen används vanligt vis när du installerar operativ systemet på en Configuration Manager klient dator.  

 Informationen om användartillståndet samlas in och återställs med hjälp av aktivitetssekvenser. När informationen om användartillståndet samlas in, kan den lagras på ett av de följande sätten:  

- Du kan lagra användartillståndsdata genom att konfigurera en tillståndsmigreringsplats. Aktivitetssekvensen Avbilda gör att alla data skickas till tillståndsmigreringsplatsen. Efter att operativsystemet har distribuerats, hämtas alla data med hjälp av aktivitetssekvensen Återställ, och därigenom återställs användartillståndet på måldatorn.  

- Du kan lagra användartillståndsdata lokalt på en viss plats. I detta scenario kopieras användarens data till en specifik plats på måldatorn genom aktivitetssekvensen Avbilda. Efter att operativsystemet har distribuerats, hämtas alla användardata från den platsen med hjälp av aktivitetssekvensen Återställ.  

- Du kan ange hårda länkar som kan användas för att återställa alla användardata till den ursprungliga platsen. I detta scenario blir alla användartillståndsdata kvar på hårddisken när det gamla operativsystemet tas bort. Efter att operativsystemet har distribuerats, används de hårda länkarna för att återställa alla användartillståndsdata till den ursprungliga platsen med hjälp av aktivitetssekvensen Återställ.  

  Mer information [hanterar användar tillstånd](../get-started/manage-user-state.md).  

##  <a name="deploy-to-unknown-computers"></a><a name="BKMK_UnknownComputer"></a>Distribuera till okända datorer  
 Du kan distribuera ett operativ system till datorer som inte hanteras av Configuration Manager. Det finns ingen post för de här datorerna i Configuration Managers databasen. Dessa datorer kallas okända. Okända datorer är:  

- En dator där Configuration Manager-klienten inte är installerad  

- En dator som inte har importer ATS till Configuration Manager  

- En dator som inte har identifierats av Configuration Manager  

  Mer information finns i [förbereda för okända dator distributioner](../get-started/prepare-for-unknown-computer-deployments.md).  

##  <a name="associate-users-with-a-computer"></a><a name="BKMK_UDA"></a>Koppla användare till en dator  
 När du distribuerar ett operativsystem, kan du koppla användare till måldatorer för att stödja åtgärder för mappning mellan användare och enheter. När du kopplar en användare till en måldator, kan den administrativa användaren sedermera utföra åtgärder på den dator som är kopplad till den användaren, t.ex. distribuera ett program till en specifik användares dator. Men när du distribuerar ett operativsystem, kan du inte distribuera det till en specifik användares dator. Mer information finns i [associera användare med en måldator](../get-started/associate-users-with-a-destination-computer.md).  

##  <a name="use-task-sequences-to-automate-steps"></a><a name="BKMK_TaskSequences"></a>Automatisera steg med hjälp av aktivitetssekvenser  
 Du kan skapa aktivitetssekvenser för att utföra en rad olika uppgifter i din Configuration Managers miljö. Åtgärderna i en aktivitetssekvens definieras i de olika stegen i sekvensen. När en aktivitetssekvens körs utförs åtgärderna för varje steg på kommandoradsnivå utan inblandning av användaren. Du kan använda aktivitetssekvenser för följande:  

-   [Skapa en aktivitetssekvens för att installera ett operativsystem](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)  

-   [Skapa en aktivitetssekvens för annat än operativsystemsdistributioner](../deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)  

-   [Skapa en aktivitetssekvens för att avbilda ett operativsystem](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)  

-   [Skapa en aktivitetssekvens för att avbilda och återställa ett användartillstånd](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)  

-   [Skapa en anpassad aktivitetssekvens](../deploy-use/create-a-custom-task-sequence.md)  
