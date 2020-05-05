---
title: Funktioner i Technical Preview 1607
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1607.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bb69547-3370-4860-96b0-7fb600c56482
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 7ec5802a8931bc4397eaf302920f09d8597802fe
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721614"
---
# <a name="capabilities-in-technical-preview-1607-for-configuration-manager"></a>Funktioner i Technical Preview 1607 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1607. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats.      Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.    


**Följande är nya funktioner som du kan prova med den här versionen.**  

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a><a name="dmp_edition"></a>Förbättringar av versionsuppgraderingsprincipen för Windows 10

I den här versionen har följande förbättringar gjorts för den här principen:

* Nu kan du använda versions uppgraderings principen med Windows 10-datorer som kör Configuration Manager-klienten förutom Windows 10-datorer som har registrerats med Microsoft Intune.
* Du kan uppgradera från Windows 10 Professional till någon av plattformarna i guiden som är kompatibla med maskin varan.

[Läs mer om uppgraderings principen för Windows 10-versionen](../../compliance/deploy-use/upgrade-windows-version.md)

### <a name="try-it-out"></a>prova!

1. Använd informationen i [artikeln befintlig uppgraderings princip för utgåva](../../compliance/deploy-use/upgrade-windows-version.md) för att skapa en uppgraderings princip för utgåva.
2. Distribuera den här principen till en Windows 10-dator som kör Configuration Manager-klienten.
När principen når en riktad Windows-dator startas datorn om inom två timmar så att uppgraderingen verkställs. Du kan för närvarande inte ignorera den här omstarten. Se till att du informerar alla användare som du distribuerar principen till, eller Schemalägg principen så att den körs utanför användarnas arbets timmar.

### <a name="known-issue-with-this-release"></a>Kända problem med den här versionen
I Configuration Manager klient inställningar kan du se Inställningar för **uppgradering av utgåva**. I den här versionen fungerar inte de här inställningarna. Använd anvisningarna ovan för att uppgradera Windows 10 till en senare version.

## <a name="customizable-branding-for-software-center-dialogs"></a>Anpassningsbar profilering för Software Center-dialogrutor

Anpassad anpassning av Software Center introducerades i Configuration Manager version 1602. I teknisk för hands version 1607 är anpassningen nu utökad till alla associerade dialog rutor och aktivitets fälts meddelanden för att ge en mer konsekvent upplevelse för Software Center-användare.

### <a name="try-it-out"></a>prova!

Anpassad anpassning av Software Center tillämpas enligt följande regler:

1. Om plats Server rollen Programkatalog webbplats plats inte är installerad visar Software Center det organisations namn som anges i **dator agentens** klient inställning **organisations namn som visas i Software Center**. Instruktioner finns i [så här konfigurerar du klient inställningar](../../core/clients/deploy/configure-client-settings.md).

2. Om plats Server rollen Programkatalog webbplats plats är installerad visas organisationens namn och färg som anges i egenskaperna för plats Server rollen för webbplats platser Programkatalog i Software Center. Mer information finns i [konfigurations alternativ för programkatalog webbplats](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).

3. Om en Microsoft Intune-prenumeration har kon figurer ATS och är ansluten till Configuration Managers miljön visar Software Center organisationens namn, färg och företags logo typ som anges i prenumerations egenskaperna för Intune.

## <a name="use-the-same-network-adapter-for-multiple-pxe-initiated-deployments"></a>Använd samma nätverkskort för flera initierade PXE-distributioner
När du använder ett Ethernet-kort för att skapa flera enheter (till exempel ett USB-Ethernet-kort som du använder på flera enheter) i teknisk för hands version 1607, kan du aktivera en ny inställning som gör att du kan ange maskin varu identifierare för Ethernet-korten. Configuration Manager ignorerar maskinvaru-ID: n i listan när en PXE-installation utförs och för klient registrering.

Mer information om det här problemet finns i [bloggen Configuration Manager OSD support team](https://blogs.technet.microsoft.com/system_center_configuration_manager_operating_system_deployment_support_blog/2015/08/27/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in-system-center-configuration-manger-osd/).  

### <a name="enable-the-feature-to-manage-duplicate-hardware-identifiers"></a>Aktivera funktionen för att hantera dubbla maskin varu identifierare  
1. I Configuration Manager-konsolen går du till **Administration** > **Översikt** > **Cloud Services** > **uppdateringar och underhålls** > **funktioner**.
2. I visningsfönstret väljer du **Hantera dubbletter av maskin varu identifierare**.
3. På fliken **Start** går du till gruppen **funktioner** och klickar på **Aktivera**.

### <a name="add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Lägg till maskin varu identifierare för Configuration Manager att ignorera  
1. I Configuration Manager-konsolen går du till **Administration** > **Översikt** > **plats konfiguration** > **platser**.
2. På fliken **Start** går du till gruppen **Platser** och klickar på **Hierarkiinställningar**.
3. Gå till fliken **klient godkännande och poster i konflikt** .
4. Klicka på **Lägg till** i avsnittet **dubbletter av maskin varu identifierare** för att lägga till nya maskin varu identifierare.
