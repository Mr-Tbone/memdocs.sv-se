---
title: Introduktion till apphantering
titleSuffix: Configuration Manager
description: Identifiera den grundläggande information som du behöver för att hantera och distribuera program i Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1b2fc0dfe37ad51ce1a549545c3eaa716395438d
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347121"
---
# <a name="introduction-to-application-management-in-configuration-manager"></a>Introduktion till program hantering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I den här artikeln lär du dig grunderna innan du börjar arbeta med Configuration Manager-program.  

> [!TIP]  
> Om du redan är bekant med hur du hanterar program i Configuration Manager kan du hoppa över den här artikeln. Gå vidare till skapa ett exempel program: [skapa och distribuera ett program](../get-started/create-and-deploy-an-application.md).  

## <a name="what-is-an-application"></a>Vad är ett program?

Även om *programmet* eller *appen* är en vanlig användnings period i Configuration Manager, betyder det något särskilt. Du kan tänka dig ett program som en låda. Den här rutan innehåller en eller flera uppsättningar installationsfiler för ett program varu paket (kallas en *distributions typ*) samt anvisningar för hur du distribuerar program varan.  

När du distribuerar programmet till enheter bestämmer **kraven** vilken distributions typ Configuration Manager installeras på enheten.  

Du kan göra många fler saker med ett program. Du lär dig mer om dessa saker när du läser den här guiden. I följande avsnitt introduceras några begrepp som du måste känna till innan du börjar att gå djupare:  

### <a name="deployment-type"></a>Distributions typ

Om *programmet* är Box, är *distributions typen* uppsättningen med innehåll i rutan. Ett program behöver minst en distributions typ, eftersom det avgör hur appen ska installeras. Använd fler än en distributions typ om du vill konfigurera olika innehålls-och installations program för samma program.

Företaget har till exempel ett branschspecifika program som kallas Astoria. Programutvecklare tillhandahåller följande sätt att installera appen:

- Windows Installer paket för fullständiga funktioner på Windows 10-enheter
- Ett App-V-paket som ska användas i Terminal server-servergruppen
- En webbapp för mobila användare  

Du skapar ett enskilt program för Astoria i Configuration Manager. Programmet definierar de övergripande metadata som gäller för den app som är gemensam för alla installations metoder och plattformar. Sedan skapar du tre distributions typer för de tillgängliga installations metoderna och distribuerar programmet till alla användare. Baserat på krav och andra konfigurationer för distributions typerna, anger Configuration Manager rätt metod i varje användnings fall.

Mer information finns i [skapa distributions typer för programmet](../deploy-use/create-applications.md#bkmk_create-dt).

### <a name="requirements"></a>Krav

I tidigare versioner av Configuration Manager skulle du skapa en samling enheter för att distribuera ett program till. Även om du fortfarande kan skapa en samling, använder du *krav* för att ange mer detaljerade villkor för en program distribution.

Ange till exempel att ett program endast kan installeras på enheter som kör Windows 10. När du distribuerar programmet till alla dina enheter installeras det bara på enheter som kör Windows 10.

Configuration Manager utvärderar kraven för att avgöra om den installerar ett program och någon av dess distributions typer. Den avgör sedan korrekt distributionstyp som ska användas för att installera ett program. Var sjunde dag utvärderar den Configuration Manager klienten krav regler för att fastställa kompatibiliteten enligt klient inställningen **Schemalägg omvärdering för distributioner**.

Mer information finns i [skapa och distribuera ett program](../get-started/create-and-deploy-an-application.md) och [distributions typ krav](../deploy-use/create-applications.md#bkmk_dt-require).

### <a name="global-conditions"></a>Globala villkor

När du använder krav med en viss distributions typ i ett enda program kan du även skapa *globala villkor*. Dessa villkor är ett bibliotek med fördefinierade krav som du kan använda med alla program och distributions typer. Configuration Manager innehåller en uppsättning inbyggda globala villkor, eller så kan du skapa en egen.

Mer information finns i [skapa globala villkor](../deploy-use/create-global-conditions.md).

### <a name="simulated-deployment"></a>Simulerad distribution

En *simulerad distribution* utvärderar krav, identifierings metod och beroenden för ett program. En klient rapporterar resultaten utan att faktiskt installera programmet.

Mer information finns i [simulera program distributioner](../deploy-use/simulate-application-deployments.md).  

### <a name="deployment-action"></a>Distributionsåtgärd

En *distributions åtgärd* anger om du vill installera eller avinstallera det program som ska distribueras. Alla distributions typer stöder inte avinstallations åtgärden.

Mer information finns i [distribuera program](../deploy-use/deploy-applications.md).  

### <a name="deployment-purpose"></a>Distributionssyfte

*Distributions syftet* anger om distributions programmet **krävs** eller **är tillgängligt**:  

- Klienten installerar automatiskt en *nödvändig* distribution enligt det schema som du anger. Om programmet inte är dolt kan en användare spåra distributionens status. De kan också använda Software Center för att installera programmet före tids gränsen.  

- Om du distribuerar programmet till en användare som *tillgängligt*visas det i Software Center och kan begära det på begäran.  

Mer information finns i [distribuera program](../deploy-use/deploy-applications.md).  

### <a name="revisions"></a>Versioner

När du gör *ändringar* i ett program eller en distributions typ skapar Configuration Manager en ny version av programmet. Vidta följande åtgärder i Configuration Manager-konsolen:

- Visa historiken för varje program revision
- Visa dess egenskaper
- Återställa en tidigare version av ett program
- Ta bort en gammal version

Mer information finns i [omarbeta program](../deploy-use/revise-and-supersede-applications.md#application-revisions).  

### <a name="detection-method"></a>Identifieringsmetod

Använd *identifierings metoder* för att identifiera om en enhet redan har installerat ett program. Om identifierings metoden visar att programmet är installerat försöker Configuration Manager inte installera det igen.

Mer information finns i [alternativ för identifiering av distributions typer](../deploy-use/create-applications.md#bkmk_dt-detect).

### <a name="dependencies"></a>Beroenden

*Beroenden* definierar en eller flera distributions typer från ett annat program som klienten måste installera innan den här distributions typen installeras.

Mer information finns i [distributions typ beroenden](../deploy-use/create-applications.md#bkmk_dt-depend).  

### <a name="supersedence"></a>Ersättande

Med Configuration Manager kan du uppgradera eller ersätta befintliga program med hjälp av en *ersättande* relation. När du ersätter ett program anger du en ny distributions typ som ersätter det ersatta programmets distributions typ. Du kan också bestämma om du vill uppgradera eller avinstallera det ersatta programmet innan klienten installerar det ersättande programmet.

Mer information finns i [program ersättning](../deploy-use/revise-and-supersede-applications.md#application-supersedence).  

### <a name="user-centric-management"></a>Användarcentrerad hantering

Configuration Manager program stöder *användarvänlig hantering*, vilket gör att du kan associera vissa användare med vissa enheter. I stället för att behöva komma ihåg namnet på en användares enhet kan du distribuera appar till användaren och enheten. Den här funktionen hjälper dig att se till att de viktigaste apparna alltid är tillgängliga på var och en av användarens enheter. Om en användare skaffar en ny dator installerar Configuration Manager automatiskt sina appar på enheten innan de loggar in.

Mer information finns i [Länka användare och enheter med mappning mellan användare och enhet](../deploy-use/link-users-and-devices-with-user-device-affinity.md).  

### <a name="application-group"></a>Program grupp

Från och med version 1906 skapar du en grupp av program som du kan skicka till en användar-eller enhets samling som en enskild distribution. Metadata som du anger om app-gruppen visas i Software Center som en enda enhet. Du kan beställa apparna i gruppen så att klienten installerar dem i en speciell ordning.

Mer information finns i [skapa program grupper](../deploy-use/create-app-groups.md).

## <a name="what-application-types-can-you-deploy"></a>Vilka programtyper kan du distribuera?

Med Configuration Manager kan du distribuera följande typer av appar:  

- Windows Installer (MSI)  

- Windows-appaket och app-paket (appx, appxbundle, msix, msixbundle)  

- Windows-appaket i Microsoft Store  

- Skript installations program för installations program och skript omslag från tredje part

- Microsoft App-V v4 och v5  

- macOS  

- En aktivitetssekvens som inte är en OS-distribution för komplexa appar

När du hanterar enheter via Configuration Manager [lokal enhets hantering](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)kan du dessutom hantera följande typer av appar:  

- Windows Phone app-paket (XAP)  

- Windows Phone app-paket i Microsoft Store  

- Windows Installer via MDM (MSI)  

- Webbprogram

## <a name="state-based-applications"></a>Tillståndsbaserade program  

Configuration Manager program använder State-baserad övervakning. Du kan spåra den senaste program distributions statusen för användare och enheter. Tillståndsmeddelandena visar information om enskilda enheter. Om du t. ex. distribuerar ett program till en samling användare kan du Visa kompatibilitetstillstånd för distributionen och distributions syftet i Configuration Manager-konsolen. Övervaka distributionen av all program vara från arbets ytan **övervakning** i Configuration Manager-konsolen. Mer information finns i [övervaka program](../deploy-use/monitor-applications-from-the-console.md).  

Configuration Manager-klienten utvärderar regelbundet program distributioner. Ett exempel:  

- En användare avinstallerar ett distribuerat program. Vid nästa utvärderings cykel upptäcker Configuration Manager att appen inte finns. Klienten installerar sedan om appen automatiskt.  

- Configuration Manager inte installerat något program på en enhet eftersom det inte uppfyllde kraven. Senare görs en ändring av enheten och den uppfyller nu kraven. Configuration Manager identifierar den här ändringen och klienten installerar programmet.  

Du kan ställa in omprövnings intervallet för program distributioner. Använd inställningen **Schemalägg omvärdering för distributioner** i **program distributions** gruppen. Mer information finns i [om klient inställningar](../../core/clients/deploy/about-client-settings.md#software-deployment).  

## <a name="get-started-creating-an-application"></a>Kom igång med att skapa ett program  

Om du vill gå direkt till och skapa ett program hittar du en genom gång i artikeln [skapa och distribuera en program](../get-started/create-and-deploy-an-application.md) .  

Om du är bekant med grunderna och vill ha mer detaljerad referensinformation om alla tillgängliga alternativ börjar du med att [skapa program](../deploy-use/create-applications.md).  

## <a name="software-center"></a>Software Center  

Software Center är ett Windows-program som installeras med Configuration Manager-klienten. Använd den för följande åtgärder:  

- Bläddra efter och begär program som distribuerats till enheten eller användaren
- Installera och schemalägga program varu installationer
- Visa installations status för program, program uppdateringar och operativ system
- Konfigurera fjärr styrnings inställningar
- Konfigurera energispar funktioner

Mer information finns i följande artiklar:  

- [Planera för och konfigurera programhantering](../plan-design/plan-for-and-configure-application-management.md)
- [Planera för Software Center](../plan-design/plan-for-software-center.md)
- [Användarhandbok för Software Center](../../core/understand/software-center.md)

> [!Note]  
> Support upphör för program katalog rollerna med version 1910. Mer information finns i [ta bort program katalogen](../plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

## <a name="packages-and-programs"></a>Paket och program  

Configuration Manager fortsätter att stödja paket och program som användes i tidigare versioner av produkten.

Mer information finns i [paket och program](../deploy-use/packages-and-programs.md).  

## <a name="next-steps"></a>Nästa steg

Nu när du förstår de grundläggande begreppen för program hantering i Configuration Manager kan du fortsätta till följande artiklar:

- [Skapa och distribuera ett exempel program](../get-started/create-and-deploy-an-application.md)
- [Planera för och konfigurera programhantering](../plan-design/plan-for-and-configure-application-management.md)
- [Skapa program](../deploy-use/create-applications.md)
