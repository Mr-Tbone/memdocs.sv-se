---
title: Teknisk för hands version 1707
titleSuffix: Configuration Manager
description: Lär dig mer om de funktioner som finns i teknisk för hands version 1707 för Configuration Manager.
ms.date: 08/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ddae3e4c4cf31cb05376bfa437d722f16652fad
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721320"
---
# <a name="capabilities-in-technical-preview-1707-for-configuration-manager"></a>Funktioner i Technical Preview 1707 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1707. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. Innan du installerar den här versionen av Technical Preview kan du läsa [Technical Preview för Configuration Manager](../../core/get-started/technical-preview.md) för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Kända problem i den här tekniska för hands versionen:**
- **Det går inte att uppdatera till för hands version 1707 när du har en plats server i passivt läge**. När du kör för hands versionen av version 1706 och har en [primär plats server i passivt läge](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)måste du avinstallera plats servern för passivt läge innan du kan uppdatera för hands versions platsen till version 1707. Du kan installera om den passiva läges plats servern efter att platsen har kört version 1707.

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

## <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Stöd för klient-peer-cache för Express-installationsfiler för Windows 10 och Office 365
<!-- 1352486 -->
Från och med den här versionen stöder peer-cache distribution av installationsfiler för innehålls Express för Windows 10 och uppdaterings filer för Office 365. Inga ytterligare konfigurationer krävs.

## <a name="surface-device-dashboard"></a>Instrument panel för Surface-enheter
<!--1355788-->
På instrument panelen för Surface-enheter finns information om de Surface-enheter som finns i din miljö. I-konsolen går du till **övervakning** > av**Surface-enheter**. Du kan visa följande:
- procent av ytor
- procent av Surface-modeller
- de fem främsta operativ system versionerna

Klicka på en del av diagrammet **ytdiagram** för att visa en fullständig lista över enheterna.  

## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Konfigurera och distribuera Windows Defender Application Guard-principer
<!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) är en ny Windows-funktion som hjälper dig att skydda dina användare genom att öppna obetrodda webbplatser i en säker isolerad behållare som inte är tillgänglig för andra delar av operativ systemet. I den här tekniska för hands versionen har vi lagt till stöd för att konfigurera den här funktionen med Configuration Manager kompatibilitetsinställningar som du konfigurerar och sedan distribuera till en samling. Den här funktionen kommer att publiceras i för hands versionen för 64-bitars versionen av Windows 10 hösten Creators Update (kod objekt: RS3). Om du vill testa den här funktionen nu måste du använda en för hands version av den här uppdateringen.

### <a name="before-you-start"></a>Innan du börjar

För att kunna skapa och distribuera Windows Defender Application Guard-principer måste de Windows 10-enheter som du distribuerar principen till konfigureras med en princip för nätverks isolering. Mer information finns i [det här blogg inlägget](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Den här funktionen fungerar bara med de senaste Windows 10 Insider-versionerna. För att testa det måste dina klienter köra en ny Windows 10 Insider-version.

### <a name="try-it-out"></a>prova!

#### <a name="to-create-a-policy-and-to-browse-the-available-settings"></a>Så här skapar du en princip och bläddrar bland de tillgängliga inställningarna:

1. I Configuration Manager-konsolen väljer du **till gångar och efterlevnad**.
2. I arbets ytan **till gångar och efterlevnad** väljer du **Översikt** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. På fliken **Start** går du till gruppen **skapa** och klickar på **skapa Windows Defender Application Guard-princip**.
4. Med blogg inlägget som referens kan du bläddra bland och konfigurera de tillgängliga inställningarna för att testa funktionen.
5. I den här versionen har vi lagt till den nya **nätverks definitions** sidan i guiden. På den här sidan anger du företagets identitet och definierar företagets nätverks gränser.<br>Windows 10-datorer lagrar bara en lista över nätverks isolering på klienten. I den här versionen kan du skapa två olika typer av nätverks isolerings listor (en från Windows Information Protection och en från Windows Defender Application Guard) och distribuera dem till klienten. Om du distribuerar båda principerna måste dessa listor för nätverks isolering matcha. Om du distribuerar listor som inte matchar samma klient kommer distributionen att Miss Don.
Du hittar mer information om hur du anger nätverks definitioner i [Windows information Protection-dokumentationen](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. När du är klar slutför du guiden och distribuerar principen till en eller flera Windows 10-enheter.

### <a name="further-reading"></a>Mer information
Läs mer om Windows Defender Application Guard i [det här blogg inlägget](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Mer information om fristående läge för Windows Defender Application Guard finns i [det här blogg inlägget](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Lägg till parametrar när du distribuerar PowerShell-skript från Configuration Manager

<!-- 1236459 --->

I den senaste tekniska för hands versionen introducerade vi en ny funktion som gör att du kan [skapa och köra PowerShell-skript från Configuration Manager-konsolen](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console).
I den här tekniska för hands versionen har vi expanderat den här funktionen. Configuration Manager läser nu PowerShell-skriptet och visar alla parametrar i guiden skapa skript. Du kan ange ett värde för parametern i guiden som ska användas när skriptet körs. Du kan också lämna parametern tom. Om du gör det måste du ange ett värde för parametern när du kör skriptet.
I den här tekniska för hands versionen måste du ange alla parametrar som krävs av skriptet. I en senare version planerar vi att tillhandahålla skript parametrar valfria.

### <a name="try-it-out"></a>prova!

1. Följ instruktionerna för att [skapa och köra PowerShell-skript från Configuration Manager-konsolen](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console).
2. Välj en parameter på sidan nya **skript parametrar** i **guiden skapa skript**och klicka sedan på **Redigera**.
3. Ange ett parameter värde för den valda parametern och klicka sedan på **OK**.
4. Slutför guiden.

När skriptet körs använder det alla parameter värden som du har konfigurerat.
