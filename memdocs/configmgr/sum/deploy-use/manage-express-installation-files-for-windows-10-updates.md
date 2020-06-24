---
title: Hantera Windows 10 Express-uppdateringar
titleSuffix: Configuration Manager
description: Configuration Manager stöder installationsfiler för Windows 10, vilket ger mindre hämtnings tider och snabbare installations tider på klienter.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/02/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: ff018bc81ecdb3d11ebb71f1850804a5679c67f7
ms.sourcegitcommit: 7a099ff53668f50b37adab97ecd7ba98c5324676
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746586"
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>Hantera Express-installationsfiler för Windows 10-uppdateringar

Configuration Manager stöder installationsfiler för Windows 10-uppdateringar. Konfigurera klienten att bara hämta ändringarna mellan den aktuella månadens kumulativa Windows 10-uppdatering och den föregående månadens uppdatering. Utan Express-installationsfiler kan Configuration Manager-klienter Ladda ned den fullständiga kumulativa Windows 10-uppdateringen varje månad, inklusive alla uppdateringar från föregående månader. Med hjälp av Express-installationsfiler kan du få mindre hämtningar och snabbare installations tider på klienter.

Information om hur du använder Configuration Manager för att hantera uppdaterings innehåll för att hålla dig uppdaterad med Windows 10 finns i avsnittet [optimera leverans av Windows 10-uppdateringar](optimize-windows-10-update-delivery.md).  


> [!IMPORTANT]  
> OS-klientens support är tillgängligt i Windows 10, version 1607, med en uppdatering av Windows Update agenten. Uppdateringen ingår i de uppdateringar som publicerades den 11 april 2017. Mer information om de här uppdateringarna finns i [Support artikel 4015217](https://support.microsoft.com/kb/4015217). Framtida uppdateringar utnyttjar Express för mindre hämtningar. Tidigare versioner av Windows 10 och Windows 10 version 1607 utan den här uppdateringen stöder inte installationsfiler för Express installation.  


## <a name="enable-the-site-to-download-express-installation-files-for-windows-10-updates"></a>Aktivera platsen för att hämta installationsfiler för Windows 10-uppdateringar
Om du vill starta synkronisering av metadata för Windows 10 Express-installationsfiler aktiverar du den i egenskaperna för program uppdaterings platsen.  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .  

2. Välj den centrala administrations platsen eller den fristående primära platsen.  

3. I menyfliksområdet klickar du på **Konfigurera plats komponenter**och klickar sedan på **program uppdaterings plats**. Växla till fliken **uppdateringsfiler** och välj **Ladda ned både fullständiga filer för alla godkända uppdateringar och installationsfiler för Express installation för Windows 10**.

> [!NOTE]    
> Du kan inte konfigurera program uppdaterings plats komponenten så att den *bara* laddar ned Express uppdateringar.  Platsen laddar ned Express-installationsfiler utöver de fullständiga filerna. Detta ökar mängden innehåll som lagras i innehålls biblioteket och distribueras till och lagras på distributions platserna.

> [!Tip]  
> Om du vill fastställa det faktiska utrymmet som används på disken av filen kontrollerar du **storleken på** filens disk egenskap. Storleken på disk egenskapen bör vara betydligt mindre än värdet för storlek. Mer information finns i [vanliga frågor och svar för att optimera leverans av Windows 10-uppdateringar](optimize-windows-10-update-delivery.md#bkmk_faq).  


## <a name="enable-clients-to-download-and-install-express-installation-files"></a>Gör det möjligt för klienter att ladda ned och installera installationsfiler för Express
Om du vill aktivera stöd för Express-installationsfiler på-klienter aktiverar du Express-installationsfiler i **program uppdaterings** gruppen i klient inställningar. Den här inställningen skapar en ny HTTP-lyssnare som lyssnar efter begär Anden om att hämta installationsfiler för Express på den port som du anger.

> [!NOTE]    
> Det här är en lokal port som klienter använder för att lyssna efter begär Anden från leverans optimering eller Background Intelligent Transfer Service (BITS) för att hämta Express innehåll från distributions platsen. Du behöver inte öppna den här porten på brand väggar eftersom all trafik finns på den lokala datorn.  

När du har distribuerat klient inställningar för att aktivera den här funktionen på klienten försöker den Ladda ned delta mellan den kumulativa Windows 10-uppdateringen för den aktuella månaden och den föregående månadens uppdatering. Klienterna måste köra en version av Windows 10 som stöder installationsfiler för Express.  

1. Aktivera stöd för Express-installationsfiler i egenskaperna för program uppdaterings plats komponenten (föregående procedur).  

2. I Configuration Manager-konsolen går du till arbets ytan **Administration** och väljer **klient inställningar**.  

3. Välj lämpliga klient inställningar och klicka på **Egenskaper** i menyfliksområdet.  

4. Välj **program uppdaterings** gruppen. Konfigurera för **att** **aktivera installationen av Express uppdateringar på klienter**. Konfigurera **porten som används för att ladda ned innehåll för Express uppdateringar** med porten som används av http-lyssnaren på klienten.
    - I version 1902 har **installationen av Express uppdateringar på klienter** ändrats för att **tillåta att klienter laddar ned delta innehåll när det är tillgängligt**.
    - I version 1902 ändrades **porten som används för att ladda ned innehåll för Express uppdateringar** till **den port som klienter använder för att ta emot begär Anden om delta innehåll**.
    

## <a name="next-steps"></a>Nästa steg

[Distribuera programuppdateringar](deploy-software-updates.md)
