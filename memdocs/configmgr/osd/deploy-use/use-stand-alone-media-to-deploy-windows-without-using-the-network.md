---
title: Använd fristående media för att distribuera Windows
titleSuffix: Configuration Manager
description: Använd fristående media i Configuration Manager för att distribuera Windows där bandbredden är begränsad som ett alternativ för att uppdatera, installera eller uppgradera datorer.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a840636ae1be0d8d38819d0465be1211ff6d2f60
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724225"
---
# <a name="use-stand-alone-media-to-deploy-windows-without-using-the-network"></a>Använda fristående media för att distribuera Windows utan att använda nätverket

*Gäller för: Configuration Manager (aktuell gren)*

Fristående media i Configuration Manager innehåller allt som krävs för att distribuera ett operativ system på en dator. Detta omfattar startavbildningen, operativsystemavbildningen och aktivitetssekvensen för att installera operativsystemet, inklusive program, drivrutiner och så vidare. Med fristående mediedistribution kan du distribuera operativsystem under följande betingelser:  

-   I miljöer där det inte är praktiskt att kopiera en operativsystemsavbildning eller andra stora paket via nätverket.  

-   I miljöer utan nätverksanslutning eller i nätverk med låg bandbredd.  

Du kan använda fristående media i följande scenarier för operativsystemsdistribution:  

- [Uppdatera en befintlig dator med en ny version av Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Installera en ny version av Windows på en ny dator (utan operativsystem)](install-new-windows-version-new-computer-bare-metal.md)  

- [Uppgradera Windows till den senaste versionen](upgrade-windows-to-the-latest-version.md)  

  Utför stegen i ett av scenarierna för operativsystemsdistribution och använd sedan följande avsnitt för att förbereda för och skapa fristående media.  

## <a name="task-sequence-actions-not-supported-when-using-stand-alone-media"></a>Aktivitetssekvensåtgärderna stöds inte när du använder fristående media  
 Om du har utfört stegen i ett av de scenarier för operativsystemsdistribution som stöds, aktivitetssekvensen som ska distribueras eller uppgraderas, har operativsystemet skapats och allt tillhörande innehåll har distribuerats till en distributionsplats. När du använder fristående media stöds inte följande åtgärder i aktivitetssekvensen:  

-   Steget Använd drivrutiner automatiskt i aktivitetssekvensen. Automatisk tillämpning av enhetsdrivrutiner från drivrutinskatalogen stöds inte, men du kan välja steget Använd drivrutinspaket för att göra en angiven uppsättning drivrutiner tillgänglig för Windows-installationsprogrammet.  

-   Installera programuppdateringar.  

-   Installera programvara innan operativsystemet har distribuerats.  

-   Associera användare med måldatorn som stöd för mappning mellan användare och enhet.  

-   Dynamiska paket installerar via aktiviteten Installationspaket.  

-   Dynamiska program installerar via aktiviteten Installera program.  

> [!NOTE]  
>  Om aktivitetssekvensen för att distribuera ett operativsystem omfattar steget [Install Package](../understand/task-sequence-steps.md#BKMK_InstallPackage) och du skapar fristående media på en central administrationsplats kan ett fel uppstå. Den centrala administrationsplatsen har inte de nödvändiga klientkonfigurationsprinciper som krävs för att aktivera programdistributionsagenten under genomförandet av aktivitetssekvensen. Följande fel kan visas i filen CreateTsMedia.log:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>   
>  För fristående media som innefattar steget **Installera paket** måste du skapa fristående media på en primär plats som har programdistributionsagenten aktiverad eller lägga till steget [Run Command Line](../understand/task-sequence-steps.md#BKMK_RunCommandLine) efter steget [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) och före det första **Installera paket** -steget i aktivitetssekvensen. Steget **Kör kommandorad** kör ett WMIC-kommando för att aktivera programdistributionsagenten innan det första Installera paket-steget körs. Du kan använda följande i ditt aktivitetssekvenssteg **Kör kommandorad** :  
>   
>  **Kommandorad**: **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  

## <a name="configure-deployment-settings"></a>Konfigurera distributionsinställningar  
 När du använder fristående media för att starta operativsystemsdistributionen måste du konfigurera distributionen för att göra operativsystemet tillgängligt för media. Du kan konfigurera detta på sidan **Distributionsinställningar** i guiden Distribuera programvara eller på fliken **Distributionsinställningar** i egenskaperna för distributionen.  Konfigurera något av följande för inställningen **Gör tillgängligt för följande** :  

-   **Configuration Manager-klienter, media och PXE**  

-   **Endast media och PXE**  

-   **Endast media och PXE (dolt)**  

## <a name="create-the-stand-alone-media"></a>Skapa fristående media  
 Du kan ange om det fristående mediet är ett USB-minne eller en cd-/dvd-skiva. Den dator som startar mediet måste stödja alternativet som du väljer som startbar enhet. Mer information finns i [skapa fristående media](create-stand-alone-media.md).  

## <a name="install-the-operating-system-from-stand-alone-media"></a>Installera operativsystemet från fristående media  
 Infoga det fristående mediet i en startbar enhet på datorn och starta den sedan för att installera operativsystemet.  
