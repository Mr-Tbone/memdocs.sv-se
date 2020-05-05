---
title: Gränser grupper för 1511, 1602 och 1606
titleSuffix: Configuration Manager
description: Använd gränser grupper med Configuration Manager versionerna 1511, 1602 och 1606.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dec1e0d7-5864-43a8-9f56-413923b3914e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 09c1b0613d36cd135ff3ac71ac7ec8472ad1e8c4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721110"
---
# <a name="boundary-groups-for-configuration-manager-version-1511-1602-and-1606"></a>Gränser grupper för Configuration Manager version 1511, 1602 och 1606

*Gäller för: Configuration Manager (aktuell gren)*
<!-- This topic drops from TOC with the release of version 1706 -->

Informationen i det här avsnittet är unik för användning av gränser grupper med version 1511, 1602 och 1606 av Configuration Manager.
Om du använder version 1610 eller senare, se [Konfigurera gränser grupper](boundary-groups.md) för information om hur du använder de omdesignade gränser grupperna.  


##  <a name="boundary-groups"></a><a name="BKMK_BoundaryGroups"></a>Gränser grupper  
 Du skapar gränsgrupper för att gruppera relaterade nätverksplatser (gränser) på ett logiskt sätt så att det blir enklare att hantera infrastrukturen. Innan du kan använda en gränsgrupp måste du tilldela den gränser. Klienterna använder gränsgruppskonfigurationen för:  

-   Automatisk platstilldelning  

-   Innehållsplats  

-   Prioriterade hanterings platser

    Om du ska använda önskade hanterings platser måste du aktivera det här alternativet för-hierarkin och inte inifrån konfigurationen för gränser gruppen. Se proceduren *för att aktivera användning av prioriterade hanterings platser* senare i det här avsnittet.  

När du konfigurerar gräns grupper lägger du till en eller flera gränser i gräns gruppen. Sedan kan du konfigurera ytterligare inställningar för användning av klienter som finns på dessa gränser.  

#### <a name="to-create-a-boundary-group"></a>Skapa en gränsgrupp  

1.  I Configuration Manager-konsolen väljer du**konfigurations** >  **gränser grupper**för **administrations** > hierarki.  

2.  På fliken **Start** går du till gruppen **skapa** och väljer **skapa en avgränsnings grupp**.  

3.  I dialog rutan **skapa gränser grupp** väljer du fliken **Allmänt** och anger sedan ett **namn** för den här gränser gruppen.  

4.  Spara den nya avgränsnings gruppen genom att välja **OK** .  

#### <a name="to-set-up-a-boundary-group"></a>Så här skapar du en avgränsnings grupp  

1.  I Configuration Manager-konsolen väljer du**konfigurations** >  **gränser grupper**för **administrations** > hierarki.  

2.  Välj den gränser grupp som du vill ändra.  

3.  På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  

4.  I dialog rutan **Egenskaper** för gräns gruppen väljer du fliken **Allmänt** för att ändra de gränser som är medlemmar i gräns gruppen:  

    -   Om du vill lägga till gränser väljer du **Lägg till**, markerar kryss rutan för en eller flera gränser och väljer sedan **OK**.  

    -   Om du vill ta bort gränser väljer du gränsen och väljer sedan **ta bort**.  

5.  Välj fliken **referenser** om du vill ändra platstilldelning och associerad plats system Server konfiguration:  

    -   Om du vill att den här gränser gruppen ska användas av klienter för platstilldelning markerar du kryss rutan för att **använda den här gränser gruppen för platstilldelning**och väljer sedan en plats i list rutan **tilldelad plats** .  

    -   Så här konfigurerar du de tillgängliga plats system servrar som är associerade med den här gränser gruppen:  

    1.  Välj **Lägg till**och markera sedan kryss rutan för en eller flera servrar. Servrarna läggs till som associerade platssystemservrar för gränsgruppen. Endast servrar som har en platssystemroll som stöds installerad är tillgängliga.  

        > [!NOTE]  
        >  Du kan välja valfri kombination av tillgängliga platssystem från alla platser i hierarkin. Valda platssystem visas på fliken **Platssystem** i egenskaperna för varje grupp som ingår i den aktuella gränsgruppen.  

    2.  Om du vill ta bort en server från den här gränser gruppen väljer du servern och väljer sedan **ta bort**.  

        > [!NOTE]  
        >  Om du vill sluta använda den här gränser gruppen för att associera plats system måste du ta bort alla servrar som är listade som associerade plats system servrar.  

    3.  Om du vill ändra nätverks anslutnings hastigheten för en plats system Server för den här gränser gruppen väljer du servern och väljer sedan **ändra anslutning**.  

         Som standard är anslutnings hastigheten för varje plats system **snabb**, men du kan ändra hastigheten till **långsam**. Kombinationen av nätverksanslutningens hastighet och inställningarna för en distribution avgör om en klient kan ladda ned innehåll från servern.  

6.  Välj **OK** för att stänga egenskaperna för kant linje gruppen och spara konfigurationen.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Associera en innehållsdistributionsserver eller hanteringsplats med en gränsgrupp  

1.  I Configuration Manager-konsolen väljer du**konfigurations** >  **gränser grupper**för **administrations** > hierarki.  

2.  Välj den gränser grupp som du vill ändra.  

3.  På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  

4.  I dialog rutan **Egenskaper** för gruppen gränser väljer du fliken **referenser** .  

5.  Under **Välj plats system servrar**väljer du **Lägg till**, markerar kryss rutan för de plats system servrar som du vill koppla till den här gränser gruppen och väljer sedan **OK**.  

6.  Välj **OK** för att stänga dialog rutan och spara konfigurationen för gränser gruppen.  

#### <a name="to-enable-use-of-preferred-management-points"></a>aktivera användningen av prioriterade hanteringsplatser  

1.  I Configuration Manager-konsolen väljer du **Administration** > **plats konfiguration** > **platser**och väljer sedan **Inställningar för hierarki**på fliken **Start** .  

2.  På fliken **Allmänt** i **Inställningar för hierarki**väljer **du klienter föredrar att använda hanterings platser som anges i gränser grupper**.  

3.  Välj **OK** för att stänga dialog rutan och spara konfigurationen.  

#### <a name="to-set-up-a-fallback-site-for-automatic-site-assignment"></a>Konfigurera en återställnings plats för automatisk platstilldelning  

1. I Configuration Manager-konsolen väljer du **Administration** > **plats konfiguration** >  **platser**.  

2. På fliken **Start** i gruppen **platser** väljer du **Inställningar för hierarkin**.  

3. Markera kryss rutan **Använd en återställnings plats**på fliken **Allmänt** och välj sedan en plats i list rutan **återställnings plats** .  

4. Spara konfigurationen genom att välja **OK** .  

   Följande avsnitt innehåller mer information om gränsgruppskonfigurationer.  

###  <a name="about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> Om platstilldelning  
 Du kan ställa in varje avgränsnings grupp med en tilldelad plats för klienter.  

-   En nyinstallerad klient som använder automatisk platstilldelning kommer att ansluta till den tilldelade platsen för en begränsande grupp som har klientens aktuella nätverks plats.  

-   En klient som är tilldelad till en plats ändrar inte sin platstilldelning när klienten ändrar sin nätverks plats. Om klienten till exempel växlar till en ny nätverks plats som representeras av en gräns i en gräns grupp som har en annan platstilldelning, ändras inte klientens tilldelade plats.  

-   Om Active Directory System Discovery identifierar en ny resurs, utvärderas nätverksinformation för den nya resursen gentemot gränserna i gränsgrupper. I processen associeras den nya resursen med en tilldelad plats genom metoden för klient-push-installation.  

-   När en avgränsning är medlem i flera gränser grupper som har olika tilldelade platser, väljer klienter slumpmässigt en av platserna.  

-   Ändringar av en begränsande grupps tilldelade plats gäller endast för nya platstilldelning. Klienter som tidigare har tilldelats en plats utvärderar inte sin platstilldelning igen baserat på ändringar i konfigurationen av en avgränsnings grupp (eller till en egen nätverks plats).  

Mer information om tilldelning av klient platser finns i [använda automatisk platstilldelning för datorer](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) i [så här tilldelar du klienter till en plats](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> Om innehållsplats  
 Du kan ställa in varje avgränsnings grupp med en eller flera distributions platser och platser för tillståndsmigrering, och du kan associera samma distributions platser och tillståndsmigrering med flera avgränsnings grupper.  

-   **Under programvarudistributionen**begär klienterna en plats för distributionsinnehåll. Configuration Manager skickar klienten en lista över distributions platser som är associerade med varje avgränsnings grupp som innehåller klientens aktuella nätverks plats.  

-   **Under operativ Systems distributionen**begär klienterna en plats för att skicka eller ta emot information om tillståndsmigrering. Configuration Manager skickar klienten en lista över tillståndsmigrering som är associerade med varje avgränsnings grupp som innehåller klientens aktuella nätverks plats.  

Detta gör att klienten kan välja den närmaste server från vilken informationen om innehållet eller tillståndsmigrering ska överföras.  

###  <a name="about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a>Om prioriterade hanterings platser  
 Prioriterade hanterings platser gör det möjligt för en klient att identifiera en hanterings plats som är kopplad till den aktuella nätverks platsen (gränsen).  

-   En klient försöker använda en önskad hanterings plats från sin tilldelade plats innan den använder en hanterings plats från den tilldelade platsen som inte har kon figurer ATS som önskad.  

-   Om du vill använda det här alternativet måste du aktivera det för hierarkin och konfigurera gräns grupper på enskilda primära platser för att inkludera de hanterings platser som ska kopplas till den gräns gruppens associerade gränser  

-   När önskade hanterings platser har kon figurer ATS och en klient ordnar sin lista över hanterings platser placerar klienten önskade hanterings platser längst upp i listan över tilldelade hanterings platser, som innehåller alla hanterings platser från klientens tilldelade plats.  

> [!NOTE]  
>  När en-klient växlar, t. ex. När en bärbar dator reser till en annan plats i nätverket och ändrar sin nätverks plats, kan den använda en hanterings plats (eller en hanterings plats för proxy) från den lokala platsen på den nya platsen innan den försöker använda en hanterings plats från dess tilldelade plats (som innehåller de prioriterade hanterings platserna).  Mer information finns i [förstå hur klienter hittar plats resurser och tjänster för Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) .  

###  <a name="about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> Om överlappande gränser  
 Configuration Manager stöder konfigurationer för överlappande gränser för innehålls platser:  

-   **När en klient begär innehåll**och klient nätverks platsen tillhör flera gränser grupper, skickar Configuration Manager klienten en lista över alla distributions platser som har innehållet.  

-   **När en klient begär en server för att skicka eller ta emot information om tillståndsmigrering**och klient nätverks platsen tillhör flera gränser grupper, skickar Configuration Manager klienten en lista över alla platser för tillståndsmigrering som är associerade med en avgränsnings grupp som innehåller klientens aktuella nätverks plats.  

Detta gör att klienten kan välja den närmaste server från vilken informationen om innehållet eller tillståndsmigrering ska överföras.  

###  <a name="about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a> Om hastighet för nätverksanslutning  
 Du kan ange nätverks anslutnings hastigheten för varje plats system server i en avgränsnings grupp. Den här inställningen gäller för klienter som ansluter till ett plats system baserat på den här gränser gruppens konfiguration. Samma platssystemserver kan ha olika anslutningshastigheter i olika gränsgrupper.  

 Nätverks anslutningens hastighet är som standard inställd på **snabb**, men du kan ändra den till **långsam**. Nätverks anslutningens hastighet och distributions konfigurationen kontrollerar om en klient kan ladda ned innehåll från en distributions plats när klienten finns i en tillhör ande avgränsnings grupp.  

 Mer information om hur konfigurationen av nätverks anslutnings hastigheten påverkar hur klienter hämtar innehåll finns i [scenarier för innehålls käll platser](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  
