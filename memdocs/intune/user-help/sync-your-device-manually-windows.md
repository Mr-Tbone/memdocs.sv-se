---
title: Synkronisera Windows-enheten manuellt | Microsoft Docs
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/20/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: priyar
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ba2f9d2e3f9e89d37b1dc8361cd80451155a6869
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820688"
---
# <a name="sync-your-windows-device-manually"></a>Synkronisera Windows-enheten manuellt

När appinstallationens hastighet är lägre än idealet påbörjar du en manuell enhetssynkronisering. Manuella synkroniseringar tvingar din enhet att ansluta med Intune för de senaste uppdateringarna och kommunikationerna. Installationshastigheten kan öka när enhetssynkroniseringen är klar.

Intune stöder manuell synkronisering från företagsportalappen, aktivitetsfältet på skrivbordet eller Start-menyn samt från enhetens inställningsapp. Företagsportalappens funktioner har stöd på Windows 10-enheter som kör Creators uppdatering (1703) eller senare. 

Alla Windows-enheter kan synkroniseras från enhetens inställningsapp, inklusive:

* [Windows 10 Desktop](#windows-10-desktop)  
* [Microsoft HoloLens](#microsoft-hololens)   

## <a name="sync-directly-from-company-portal-app-for-windows"></a>Synkronisera direkt från företagsportalappen för Windows
Följ stegen för att manuellt synkronisera alla Windows 10-enheter som kör Creators uppdatering (version 1709) eller senare.

1. Öppna företagsportalappen på din enhet.

2. Välj **Inställningar** > **Synkronisering**.

    ![Skärmbild av startsidan i företagsportalappen, Inställningar markerat](./media/RS1_homePage_settings_04.png)  
    
    ![Skärmbild av inställningssidan för företagsportalappen, Synkroniseringsknappen markerad](./media/RS1_settingspage_sync05.png)  

## <a name="sync-from-device-taskbar-or-start-menu"></a>Synkronisera från enhetens aktivitetsfält eller Start-meny   

Du kan även använda synkroniseringskontrollen utanför appen, från enhetens skrivbord. Det här sättet är användbart om du har fäst appen direkt på aktivitetsfältet eller Start-menyn och vill synkronisera snabbt.  

1. Leta upp ikonen för företagsportalappen i aktivitetsfältet eller på Start-menyn.  
2. Högerklicka på appikonen så visas menyn (kallas även en snabblista).  

    ![Skärmbild av Windows-aktivitetsfältet på en enhets skrivbord. Ikonen för företagsportalappen har valts och visar en meny med alternativen ”Fäst i verktygsfältet, ”Stäng fönster” och ”Synkronisera den här enheten”.](./media/sync-device-from-start-menu-1807.png)  

3. Välj **Synkronisera den här enheten**. Företagsportalappen öppnas till sidan **Inställningar** och initierar synkroniseringen.  

## <a name="sync-from-settings-app"></a>Synkronisera från Inställningsappen 
Följ stegen för att synkronisera dina Microsoft HoloLens-, Windows 10 desktop-enheter från inställningsappen manuellt.  

### <a name="windows-10-desktop"></a>Windows 10 desktop
1. På enheten, välj **Start** > **Inställningar**.

2. Välj **Konton**.

    ![Välj konton på sidan Inställningar](./media/win10pc-sync-2-settings-accounts.png)  

3. Det finns flera versioner av Windows 10 för stationära datorer. Jämför din skärm med skärmbilderna nedan för att avgöra vilken uppsättning steg du ska följa. 

    * Om skärmen visar **Åtkomst till arbetsplats eller skola**, går du vidare till stegen i [Åtkomst till arbetsplats eller skola](#access-work-or-school-steps).

    ![Alternativet Åtkomst till arbetsplats eller skola i inställningsappen](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

    * Om skärmen visar **Åtkomst till arbetsplats**, går du vidare till stegen under [Åtkomst till arbetsplats](#work-access-steps).  

    ![Välj arbetsåtkomst som kontotyp](./media/win10pc-sync-3-work-access.png)

### <a name="microsoft-hololens"></a>Microsoft HoloLens  
Dessa anvisningar gäller HoloLens-enheter som kör Windows 10 Anniversary-uppdateringen (även kallad RS1).  

1. Öppna inställningsappen på enheten.  

2. Välj **Konton** > **Åtkomst till arbetsplats**.  

    ![Skärmbild på HoloLens-inställningsappen, kontolänken markerad](./media/RS1_holoLens_SettingsRS1_Accounts_06.png)  

3. Välj ditt anslutna konto > **Synkronisera**.  

    ![Skärmbild på HoloLens-inställningsapp, synkroniseringsknappen markerad](./media/RS1_holoLens_SyncRS1_Sync_08.png)   

#### <a name="access-work-or-school-steps"></a>Stegen för Åtkomst till arbetsplats eller skola  

1. Välj **Åtkomst till arbete eller skola**.

    ![Skärmbild som visar alternativet Åtkomst till arbetsplats eller skola](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

2. Välj det konto som har en portfölj-ikon bredvid sig. Om du inte ser det här kontot alls, kan ditt företag ha konfigurerat inställningarna på ett annat sätt. Klicka då på det konto som har en Microsoft-logotyp bredvid sig.

     ![Välj namnet på ditt konto bredvid portföljikonen eller Microsoft-logotypen](./media/win10pc-rs1-sync-info-button.png)

3. Välj **Info**. 

4. Välj **Synkronisera**. 

#### <a name="work-access-steps"></a>Steg för Åtkomst till arbetsplats

1. Väj **Åtkomst till arbetsplats**.

    ![Välj arbetsåtkomst som kontotyp](./media/win10pc-sync-3-work-access.png)

2. Under **Registrera dig för enhetshantering**, välj namnet på ditt företag.

    ![Välj företagsnamnet för enhetshantering](./media/win10pc-sync-4-tap-com-name.png)

3. Välj **Synkronisera**. Knappen är inaktiverad tills synkroniseringen är klar.

    ![Välj knappen Synkronisera](./media/win10pc-sync-5-tap-sync.png)  
    
## <a name="next-steps"></a>Nästa steg  

Behöver du fortfarande hjälp? Kontakta företagssupporten. Titta efter IT-administratörens kontaktuppgifter på [företagsportalens webbplats](https://go.microsoft.com/fwlink/?linkid=2010980).
