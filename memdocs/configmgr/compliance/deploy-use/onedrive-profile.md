---
title: OneDrive för företag-profiler
titleSuffix: Configuration Manager
description: Omdirigera Windows-kända mappar till OneDrive för företag med hjälp av en OneDrive för företag-profil i Configuration Manager.
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: e217699a-28b2-471a-b421-8fbd1d1fd638
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d13d9dfd75abb656a765ce8c91ce6f177636cd3
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127179"
---
# <a name="onedrive-for-business-profiles"></a>OneDrive för företag-profiler

Från och med Configuration Manager version 1902 kan du skapa OneDrive för företag-profiler för att flytta Windows-kända mappar till OneDrive för företag. Dessa mappar innehåller Skriv bord, dokument och bilder. I varje profil kan du ange inställningar för att flytta de kända Windows-mapparna. Mer information om OneDrive för företag finns i [omdirigera och flytta Windows-kända mappar till OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders). <!--3556021-->

## <a name="prerequisites"></a>Förutsättningar

- [Hitta Microsoft 365 klient-ID](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id)  

- Distribuera version 18.111.0603.0004 eller senare av OneDrive sync-klient. Mer information finns i [distribuera OneDrive-appar med hjälp av Configuration Manager](https://docs.microsoft.com/onedrive/deploy-on-windows).  

## <a name="move-windows-known-folders-to-onedrive"></a><a name="bkmk_odfb"></a>Flytta Windows-kända mappar till OneDrive
<!--3556021-->
Använd Configuration Manager för att flytta Windows-kända mappar till OneDrive för företag. Dessa mappar innehåller Skriv bord, dokument och bilder. För att förenkla dina Windows 10-uppgraderingar distribuerar du inställningarna till Windows 7-klienter innan du distribuerar en aktivitetssekvens. 

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** , **expanderar kompatibilitetsinställningar och**väljer noden **OneDrive för företag-profiler** .  

   ![Noden för OneDrive för företag-profiler](media/onedrive-for-business-profiles-node.png)
2. I menyfliksområdet väljer du **skapa OneDrive för företag-profil**.  

3. Ange ett namn för att identifiera den här principen och välj **Nästa**.  

4. Välj de plattformar som ska tillhandahållas med OneDrive för företag-profilen. Klicka på **Nästa**när du är klar med att välja plattformarna.

    ![Välj plattformar för OneDrive för företag-profilen](media/onedrive-for-business-profile-select-platforms.png) 

5. På sidan **Inställningar** :

    1. Ange Microsoft 365 klient-ID.  

    2. Välj något av följande alternativ för att flytta de kända mapparna till OneDrive:  

        - **Uppmana användarna att flytta Windows-kända mappar till OneDrive**: med det här alternativet ser användaren en guide för att flytta sina filer. Om de väljer att skjuta upp eller avböja flyttningen av mappar, påminner OneDrive regelbundet om dem.  

        - **Flytta Windows-kända mappar i bakgrunden till OneDrive**: när den här principen tillämpas på enheten omdirigerar OneDrive-klienten automatiskt de kända mapparna till OneDrive för företag.  

            - **Visa meddelande till användare efter att mappar har omdirigerats**: om du aktiverar det här alternativet meddelar OneDrive-klienten användaren när den har flyttat mapparna.  

    3. **Förhindra att användare omdirigerar sina Windows-kända mappar tillbaka till sin dator**: inaktiverar alternativet i OneDrive för företag på klienten där användarna kan flytta tillbaka mapparna till enheten.  

       ![Inställningar för flytt av OneDrive för företag-kända mappar](media/onedrive-for-business-profile-move-folder-settings.png)

6. Slutför guiden och distribuera sedan principen.  


## <a name="deploy-the-onedrive-for-business-profile"></a>Distribuera OneDrive för företag-profilen

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** , **expanderar kompatibilitetsinställningar och**väljer noden **OneDrive för företag-profiler** .  


2. Välj profilen och välj sedan **distribuera** i menyfliksområdet.

3. Ange följande inställningar för distributionen:

   1. **Samling**: Klicka på **Bläddra...** och välj sedan den samling som du vill distribuera profilen för.  
   1. **Generera en avisering**:

      - **När kompatibiliteten är nedan**: lägsta procent andel av klientens kompatibilitet för att bibehålla en varning genereras.
      -  **Datum och tid**: datum aviseringarna först börjar genereras baserat på profilernas efterlevnad.
      - **Generera System Center Operations Manager avisering**: skicka en avisering om kompatibilitet till System Center Operations Manager.
   1. **Schema**:

      - **Enkelt schema**: som standard använder den här inställningen ett enkelt schema för att starta utvärderingen av efterlevnaden var sjunde dag.
      - **Anpassat schema**: definiera när utvärderingen av kompatibilitet ska köras. Start tiden baseras på den lokala tiden för den dator som kör Configuration Manager-konsolen vid den tidpunkt då du skapar schemat eller så kan du använda UTC.
 
      ![Distribuera OneDrive för företag-profil](media/onedrive-for-business-deploy-profile.png)

4. Klicka på **OK** för att distribuera OneDrive för företag-profilen.


## <a name="next-steps"></a>Nästa steg

[Skapa fjärranslutningsprofiler](create-remote-connection-profiles.md)
