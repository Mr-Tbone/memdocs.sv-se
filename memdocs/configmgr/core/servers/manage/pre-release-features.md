---
title: Förhandsfunktioner
titleSuffix: Configuration Manager
description: För hands versions funktioner är funktioner som finns i den aktuella grenen för tidig testning i en produktions miljö.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e341fab9f76ab6994f051dbd5e2333c3f521b4d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720158"
---
# <a name="pre-release-features-in-configuration-manager"></a>För hands versions funktioner i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

För hands versions funktioner är funktioner som finns i den aktuella grenen för tidig testning i en produktions miljö. Dessa funktioner stöds fullt ut, men fortfarande i aktiv utveckling. De kan få ändringar tills de flyttas ut från för hands versions kategorin.

## <a name="give-consent"></a>Ge medgivande  

Innan du använder för hands versions funktioner kan du ge tillåtelse att använda för hands versions funktioner. Att ge tillåtelse är en engångs åtgärd per hierarki som du inte kan ångra. Innan du ger ditt medgivande kan du inte aktivera nya för hands versions funktioner som ingår i uppdateringarna. När du har aktiverat en för hands versions funktion kan du inte inaktivera den.

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .  

2. Klicka på **Inställningar för hierarki** i menyfliksområdet.  

3. På fliken **Allmänt** i egenskaper för hierarkiska inställningar aktiverar du alternativet att **använda för hands versions funktioner**. Klicka på **OK**.  

## <a name="enable-pre-release-features"></a>Aktivera för hands versions funktioner

När du installerar en uppdatering som innehåller för hands versions funktioner visas dessa funktioner i guiden uppdateringar och underhåll med de vanliga funktionerna som ingår i uppdateringen.

### <a name="if-you-have-given-consent"></a>Om du har gett samtycke

Aktivera för hands versions funktioner i guiden uppdateringar och underhåll. Välj för hands versions funktionerna på samma sätt som med andra funktioner.

Du kan också vänta med att aktivera för hands versions funktioner senare från noden **funktioner** under **uppdateringar och underhåll** i arbets ytan **Administration** . Välj en funktion och klicka sedan på **Aktivera** i menyfliksområdet. Det här alternativet är inte tillgängligt för användning förrän du har gett ditt medgivande.

### <a name="if-you-havent-given-consent"></a>Om du inte har gett ditt medgivande

I guiden uppdateringar och underhåll visas för hands versions funktioner, men du kan inte aktivera dem. När uppdateringen har installerats visas dessa funktioner i noden **funktioner** . Du kan dock inte aktivera dem förrän du ger ditt medgivande.

> [!IMPORTANT]  
> I en hierarki med flera platser kan du bara aktivera valfria eller för hands versions funktioner från den centrala administrations platsen. Det här beteendet garanterar att det inte finns några konflikter i hierarkin. <!--507197-->  
>
> Om du har gett medgivande på en fristående primär plats och sedan expanderar hierarkin genom att installera en ny central administrations plats måste du ge ditt medgivande igen på den centrala administrations webbplatsen.  

När du aktiverar en för hands versions funktion måste Configuration Manager Hierarchy Manager (HMAN) bearbeta ändringen innan funktionen blir tillgänglig. Bearbetningen av ändringen är ofta omedelbar. Beroende på bearbetnings cykeln för HMAN kan det ta upp till 30 minuter att slutföra. När ändringen har bearbetats startar du om-konsolen innan du använder funktionen.

## <a name="list-of-pre-release-features"></a><a name="bkmk_table"></a>Lista över för hands versions funktioner

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](pre-release-features.md).  

> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](pre-release-features.md). Beginning with version 1906, it's no longer a pre-release feature.  

-->

<!-- With each current branch release, to help purge this list a bit, remove any entries that were added as a full feature in a version that's no longer supported -->
| Funktion          | Tillagt som för hands version | Tillagt som en fullständig funktion |
|------------------|----------------------|-------------------------|
| [Orkestreringsgrupper](../../../sum/deploy-use/orchestration-groups.md) <!--3098816--> | Version 2002 | ![Inte ännu](media/red_x.png) |
| [Distributions typ för aktivitetssekvens](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt) <!--3555953--> | Version 2002 | ![Inte ännu](media/red_x.png) |
| [Ta bort den centrala administrations platsen](../deploy/install/remove-central-administration-site.md) <!-- 3607277 --> | Version 2002 | ![Inte ännu](media/red_x.png) |
| [Fel sökare för aktivitetssekvens](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71--> | Version 1906 | ![Inte ännu](media/red_x.png) |
| [Program grupper](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D--> | Version 1906 | ![Inte ännu](media/red_x.png) |
| [Azure Active Directory användar grupp identifiering](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->| Version 1906 | Version 2002 |
| [Synkronisera samlings medlemskaps resultat till Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->| Version 1906| Version 2002 |
| [Fristående CMPivot](cmpivot.md#bkmk_standalone) <!--3555890/4692885,no GUID--> | Version 1906 | Version 2002 |
| [Administrations tjänst för SMS-provider](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service) <!--1359052--> | Version 1810 | Version 1906 |
| [Förbättrat HTTP-platssystem](../../plan-design/hierarchy/enhanced-http.md) <!--1356889,1358228--> | Version 1806 | Version 1810 |
| [Klient program för samhanterade enheter](../../../comanage/workloads.md#client-apps) <br/> (tidigare kallade *mobilappar för samhanterade enheter*) <!--1357892/3600959,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C--> | Version 1806 | Version 2002 |
| [Paket konverterings hanterare](../../../apps/pcm/package-conversion-manager.md) <!--1357861--> | Version 1806 | Version 1810 |
| [Fasindelade distributioner](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) <!--1356837--> | Version 1802 | Version 1806 |
| [Hantering av Windows Defender-programreglering](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) <!--3600958 (fka 1355092 & 1319346)--> | Version 1702 | Version 1906 |
| [Underhålla en kluster medveten samling (Server grupper)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697--> | Version 1602 | ![Inte ännu](media/red_x.png) |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!TIP]  
> Mer information om icke-för hands versions funktioner som du måste aktivera först finns i [Aktivera valfria funktioner från uppdateringar](install-in-console-updates.md#bkmk_options).  
>
> Mer information om funktioner som endast är tillgängliga i den tekniska för hands versionen finns i [Technical Preview](../../get-started/technical-preview.md).  
