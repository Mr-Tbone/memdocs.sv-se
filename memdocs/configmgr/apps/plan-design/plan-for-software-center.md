---
title: Planera för Software Center
titleSuffix: Configuration Manager
description: Bestäm hur du vill konfigurera och anpassa Software Center för att användare ska kunna interagera med Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15da90b12504fdaf7a4dd0a36704391eead877cd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709931"
---
# <a name="plan-for-software-center"></a>Planera för Software Center

*Gäller för: Configuration Manager (aktuell gren)*

Användare ändrar inställningar, söker efter program och installerar program från Software Center. När du installerar Configuration Manager-klienten på en Windows-enhet installeras även Software Center automatiskt.

Mer information om andra funktioner i Software Center finns i [användar handboken för Software Center](../../core/understand/software-center.md).  

## <a name="configure-software-center"></a><a name="bkmk_userex"></a>Konfigurera Software Center  

Uppdatera Configuration Manager-platser och-klienter till version 1906 eller senare för att dra nytta av de senaste förbättringarna.

Läs följande förbättringar av Software Center:

> [!Important]  
> De här iterativa förbättringarna av Software Center och hanterings platsen är att dra tillbaka program katalog rollerna.
>
> - Silverlight-användar upplevelsen stöds inte av den aktuella gren versionen 1806.
> - Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller.
> - Support upphör för program katalog rollerna med version 1910.  

### <a name="starting-in-version-1802"></a>Från och med version 1802

- Klient inställningen **Använd nya Software Center** i gruppen **dator agent** är aktive rad som standard. Den tidigare versionen av Software Center stöds inte längre. Mer information finns i [borttagna och föråldrade funktioner](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).  

- Användare kan söka efter och installera användar tillgängliga program på Azure Active Directory (Azure AD)-anslutna enheter. Mer information finns i [distribuera användar tillgängliga program på Azure AD-anslutna enheter](../deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices).  

### <a name="starting-in-version-1806"></a>Från och med version 1806

- Ange synlighet för länken till program katalogens webbplats på fliken **installations status** i Software Center. Mer information finns i klient inställningar för [Software Center](../../core/clients/deploy/about-client-settings.md#software-center) .  

- Program katalog roller krävs inte längre för att Visa användar tillgängliga program i Software Center. Den här ändringen hjälper dig att minska Server infrastrukturen som krävs för att leverera program till användare. Software Center använder nu hanterings platsen för att hämta den här informationen, vilket hjälper större miljöer att skala bättre genom att tilldela dem till [gräns grupper](../../core/servers/deploy/configure/boundary-groups.md#management-points).<!--1358309-->  

    > [!Note]  
    > Om du använder program katalogen för närvarande och uppdaterar Configuration Manager till version 1806 fortsätter den att fungera. Rollerna webbplats för program katalog och webb tjänst punkt *krävs*inte längre, men *stöds*fortfarande. **Användar upplevelsen för Silverlight** för program katalogens *webbplats* stöds inte längre. Mer information finns i [borttagna och föråldrade funktioner](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).
    >
    > Börja planera att ta bort program katalog rollerna från infrastrukturen i framtiden. Dra nytta av förbättringar av Software Center för att använda hanterings platsen och förenkla din Configuration Managers miljö.  

### <a name="starting-in-version-1902"></a>Från och med version 1902

- Konfigurera mappning mellan användare och enhet. Mer information finns i [Länka användare och enheter med mappning mellan användare och enhet](../deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="starting-in-version-1906"></a>Från och med version 1906

- Software Center kommunicerar nu med en hanterings plats för appar som är riktade till användare som tillgängliga. Den använder inte program katalogen längre. Den här ändringen gör det enklare för dig att ta bort program katalogen från webbplatsen.

- Tidigare valde Software Center den första hanterings platsen från listan över tillgängliga servrar. Från och med den här versionen använder den samma hanterings plats som klienten använder. Den här ändringen gör att Software Center kan använda samma hanterings plats från den tilldelade primära platsen som klienten.

- Hanterings platsen har Software Center-slutpunkter som stöder de här nya funktionerna. Nu kontrol leras hälsan för dessa slut punkter var femte minut. Den rapporterar eventuella problem via status meddelanden för SMS_MP_CONTROL_MANAGER plats komponenten.

- Du kan inte lägga till nya program katalog roller på platsen. Befintliga roller fortsätter att fungera. Endast befintliga klienter använder program katalogen för distributioner som är tillgängliga för användare. Uppdaterade klienter använder automatiskt hanterings platsen för alla distributioner.

- Du kan lägga till upp till 5 anpassade flikar i Software Center. Mer information finns i [klient inställningar för Software Center](../../core/clients/deploy/about-client-settings.md#software-center). <!--4063773-->

### <a name="summary-of-infrastructure-requirements-per-version"></a>Översikt över infrastruktur krav per version

Använd följande tabell för att få hjälp att förstå kraven för Software Center beroende på den särskilda versionen av Configuration Manager:

| Enhetstyp | Plats version | Infrastruktur |
|-----------------|--------------|----------------|
| Azure AD-ansluten enhet<br>(eller "molnbaserad domänanslutna") | 1802 eller 1806 | Hanterings plats för alla distributioner av appar |
| [Hybrid Azure AD-ansluten](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) enhet på Internet | 1802 eller 1806 | Cloud Management Gateway och hanterings plats för alla distributioner av appar |
| Lokal Active Directory domänanslutna enhet | 1802 | Program katalog krävs för appar som är tillgängliga för användare via Software Center |
| Lokal Active Directory domänanslutna enhet | 1806 | Hanterings plats för alla distributioner av appar |

> [!Important]  
> Om du vill dra nytta av nya Configuration Manager funktioner måste du först uppdatera klienter till den senaste versionen. När nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen, fungerar inte det fullständiga scenariot förrän klient versionen också är den senaste.


## <a name="replace-toast-notifications-with-dialog-window"></a><a name="bkmk_impact"></a>Ersätt popup-meddelanden med dialog fönster

<!--3555947-->
Användare ser ibland inte Windows popup-meddelanden om en omstart eller en nödvändig distribution. Sedan visas inte upplevelsen för att försätta påminnelsen i vilo läge. Det här beteendet kan leda till en låg användar upplevelse när klienten når en tids gräns.

Från och med version 1902, när [program varu ändringar krävs](#software-changes-are-required) eller distributioner [behöver startas om](#restart-required), kan du välja att använda en mer påträngande dialog ruta.

### <a name="software-changes-are-required"></a>Program varu ändringar krävs

När du [distribuerar ett program](../deploy-use/deploy-applications.md) som krävs med en tids gräns i framtiden väljer du följande alternativ för användar meddelande på sidan **användar upplevelse** i guiden distribuera program vara:

- **Visa i Software Center och Visa alla meddelanden**
- **När program varu ändringar krävs visar du ett dialog fönster för användaren i stället för ett popup-meddelande**

När du konfigurerar den här distributions inställningen ändras användar upplevelsen för det här scenariot.

Från följande popup-meddelande:

![Popup-meddelande om att program varu ändringar krävs](media/3555947-required-toast.png)  

I följande dialog fönster:

![Dialog fönster för nödvändiga program varu ändringar](media/3555947-required-dialog.png)


### <a name="restart-required"></a>Omstart krävs

I gruppen [dator omstart](../../core/clients/deploy/about-client-settings.md#computer-restart) av klient inställningar aktiverar du följande alternativ: **när en distribution kräver en omstart visar du ett dialog fönster för användaren i stället för ett popup-meddelande**.  

Om du konfigurerar den här klient inställningen ändras användar upplevelsen för alla nödvändiga distributioner som kräver en omstart av följande typer:

- [Program](../deploy-use/deploy-applications.md)
- [Aktivitetssekvens](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Program uppdatering](../../sum/deploy-use/deploy-software-updates.md)

Från följande popup-meddelande:

![Popup-meddelande som startas om krävs](media/3555947-restart-toast.png)  

I följande dialog fönster:

![Dialog ruta för att starta om datorn](media/3555947-restart-dialog.png)

> [!IMPORTANT]
> I Configuration Manager 1902, under vissa omständigheter, ersätter dialog rutan inte popup-meddelanden. Lös problemet genom att installera Samlad [uppdatering för Configuration Manager version 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="branding-software-center"></a>Anpassning av Software Center

Ändra utseendet på Software Center för att uppfylla organisationens anpassnings krav. Den här konfigurationen hjälper användare att lita på Software Center.

### <a name="configure-software-center-branding"></a>Konfigurera Software Center-anpassning

<!-- 1351224 -->
Anpassa utseendet för Software Center genom att lägga till organisationens anpassnings element och ange synlighet för flikarna.

Mer information finns i följande artiklar:

- [Software Center](../../core/clients/deploy/about-client-settings.md#software-center) -grupp för klient inställningar  
- [Konfigurera klientinställningar](../../core/clients/deploy/configure-client-settings.md)  

### <a name="branding-priorities"></a>Anpassnings prioriteter

Configuration Manager använder anpassad anpassning för Software Center enligt följande prioriteringar:  

1. Klient inställningar för **Software Center** . Mer information finns i [om klient inställningar](../../core/clients/deploy/about-client-settings.md#software-center).  

2. Klient inställning för **organisations namn** i **dator agent** grupp. Mer information finns i [om klient inställningar](../../core/clients/deploy/about-client-settings.md#computer-agent).  

#### <a name="application-catalog-branding-priorities"></a>Anpassnings prioritet för program katalog

> [!Important]
> Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  

Om du använder program katalogen följer anpassningen följande prioriteringar:  

1. Klient inställningar för **Software Center** . Mer information finns i [om klient inställningar](../../core/clients/deploy/about-client-settings.md#software-center).  

2. *Organisations namnet* och *färgen* som du anger i egenskaperna för webbplats platsen för program katalogen. Mer information finns i [konfigurations alternativ för webbplats för program katalog](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).  

3. Klient inställning för **organisations namn** i **dator agent** grupp. Mer information finns i [om klient inställningar](../../core/clients/deploy/about-client-settings.md#computer-agent).  


## <a name="see-also"></a>Se även

- [Användarhandbok för Software Center](../../core/understand/software-center.md)
- [Planera för och konfigurera programhantering](plan-for-and-configure-application-management.md)
