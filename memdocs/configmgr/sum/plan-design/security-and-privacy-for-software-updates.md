---
title: Säkerhet och sekretess för programuppdateringar
titleSuffix: Configuration Manager
description: Följ dessa metod tips för säkerhet för program uppdateringar och lär dig mer om hur Configuration Manager hanterar sekretess information.
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 41d6d5d8-ba84-4efb-b105-4d1eed239824
author: mestew
ms.author: mstewart
ms.openlocfilehash: 5c7a1ac5e88aa669ae1d5e6bb9333e1f54fb5980
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724008"
---
# <a name="security-and-privacy-for-software-updates-in-configuration-manager"></a>Säkerhet och sekretess för program uppdateringar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det här avsnittet innehåller information om säkerhet och sekretess för program uppdateringar i Configuration Manager.  

##  <a name="security-best-practices-for-software-updates"></a><a name="BKMK_Security_HardwareInventory"></a> Rekommenderade säkerhetsmetoder för programuppdateringar  
 Använd följande rekommenderade säkerhetsmetoder när du distribuerar programvaruuppdateringar till klienter:  

-   Ändra inte standardbehörigheterna för programuppdateringspaketen.  

     Som standard är programuppdateringspaketen inställda på att ge administratörer **Fullständig behörighet** och användare **Läs** -behörighet. Om du ändrar behörigheteran kan det göra det möjligt för en angripare att lägga till, ta bort eller radera programuppdateringar.  

-   Kontrollera åtkomsten till nedladdningsplatsen för programuppdateringar.  

     Datorkontona för SMS-providern, platsservern och den administrativa användaren som laddar ner programuppdateringarna till nedladdningsplatsen kräver **Skriv** -behörighet till nedladdningsplatsen. Begränsa åtkomsten till nedladdningsplatsen för att minska risken för att angripare manipulerar programuppdateringskällfilerna där.  

     Om du dessutom använder en UNC-resurs för nedladdningsplatsen, säkra nätverkskanalen genom att använda IPsec- eller SMB-signering för att undvika manipulering av programuppdateringskällfilerna när de överförs via nätverket.  

-   Använd UTC för att utvärdera distributionstider.  

     Om du använder lokal tid istället för UTC kan användarna möjligen fördröja installationen av programuppdateringar genom att ändra tidszonen på sina datorer  

-   Aktivera SSL på WSUS och följ rekommenderade metoder för att säkra Windows Server Update Services (WSUS).  

     Identifiera och följ rekommenderade säkerhets metoder för den version av WSUS som du använder med Configuration Manager.  

    > [!IMPORTANT]  
    >  Om du konfigurera programuppdateringsplatsen att aktivera SSL-kommunikation för WSUS-servern måste du konfigurera virtuella rötter för SSL på WSUS-servern.  

-   Aktivera CRL-kontroll.  

     Som standard kontrollerar Configuration Manager inte listan över återkallade certifikat (CRL) för att verifiera signaturen på program uppdateringar innan de distribueras till datorer. Att kontrollera CRL-listan vid varje certifikatanvändning ger högre säkerhet än att använda ett certifikat som har återkallats, men ger även upphov till att anslutningen blir långsammare och att belastningen ökar på den dator där CRL-kontrollen utförs.  

     Mer information om hur du aktiverar CRL-kontroll för program uppdateringar finns i [Aktivera CRL-kontroll för program uppdateringar](../get-started/manage-settings-for-software-updates.md#crl-checking-for-software-updates).  

-   Konfigurera WSUS att använda en anpassad webbplats.  

     När du installerar WSUS på programuppdateringsplatsen kan du välja att använda den befintliga IIS-standardwebbplatsen eller att skapa en anpassad WSUS-webbplats. Skapa en anpassad webbplats för WSUS så att IIS är värd för WSUS-tjänsterna på en dedikerad virtuell webbplats istället för att dela samma webbplats som används av de andra Configuration Manager-plats systemen eller andra program.  

     Mer information finns i avsnittet [Configure WSUS to use a custom web site](plan-for-software-updates.md#BKMK_CustomWebSite).  

##  <a name="privacy-information-for-software-updates"></a><a name="BKMK_Privacy_HardwareInventory"></a>Sekretess information för program uppdateringar  
 Programuppdateringar söker igenom dina klientdatorer för att avgöra vilka programuppdateringar du behöver och skickar sedan tillbaka informationen till platsdatabasen. Under program uppdaterings processen kan Configuration Manager överföra information mellan klienter och servrar som identifierar datorn och inloggnings konton.  

 Configuration Manager underhåller statusinformation om program distributions processen. Statusinformationen är inte krypterad under överföring eller lagring. Tillståndsinformation lagras i Configuration Manager-databasen och tas bort av databasens underhålls aktiviteter. Ingen statusinformation skickas till Microsoft.  

 Användning av Configuration Manager program uppdateringar för att installera program uppdateringar på klient datorer kan omfattas av licens villkor för program vara för dessa uppdateringar, som är åtskilda från licens villkoren för program vara för Configuration Manager. Läs alltid igenom och godkänn licens villkoren för program vara innan du installerar program uppdateringarna med hjälp av Configuration Manager.  

 Configuration Manager implementerar inte program uppdateringar som standard och kräver flera konfigurations steg innan information samlas in.  

 Innan du konfigurerar programuppdateringar bör du tänka igenom dina sekretesskrav.  
