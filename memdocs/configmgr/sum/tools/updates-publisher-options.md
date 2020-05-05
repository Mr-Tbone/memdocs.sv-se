---
title: Konfigurera alternativ
titleSuffix: Configuration Manager
description: Konfigurera alternativ för att använda System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8b6578e32d5ae5a003c485960b556f3b87e8d557
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717729"
---
# <a name="configure-options-for-updates-publisher"></a>Konfigurera alternativ för Updates Publisher

*Gäller för: System Center Updates Publisher*

Granska och konfigurera alternativen och de relaterade inställningarna som påverkar driften av Updates Publisher.

Du kommer åt alternativen för uppdaterings utgivare i det övre vänstra hörnet i konsolen genom att klicka på fliken **Updates Publisher** - **Egenskaper** och sedan välja **alternativ**.

![Alternativ](media/properties1.png)   


Alternativen är indelade i följande:

-     -uppdateringsserver
-   ConfigMgr-Server
-   Proxyinställningar
-   Betrodda utgivare
-   Avancerat
-   Uppdateringar
-   Loggning

## <a name="update-server"></a>  -uppdateringsserver
Du måste konfigurera Updates Publisher för att fungera med uppdaterings servern som Windows Server Update Services (WSUS) innan du kan [publicera uppdateringar](manage-updates-with-updates-publisher.md#publish-updates-and-bundles-from-the-updates-workspace). Detta inkluderar att ange servern, metoder för att ansluta till den servern när den är fjärran sluten till-konsolen och ett certifikat som används för att digitalt signera uppdateringar som du publicerar.

- **Konfigurera en uppdaterings Server**. När du konfigurerar en uppdaterings server väljer du den översta WSUS-servern (uppdaterings Server) i Configuration Manager-hierarkin så att alla underordnade platser har åtkomst till de uppdateringar som du publicerar.

  Om din uppdaterings Server är fjärran sluten från din Updates Publisher-server anger du det fullständigt kvalificerade domän namnet (FQDN) för servern och om du ska ansluta via SSL. När du ansluter via SSL ändras standard porten från 8530 till 8531. Se till att den port du anger matchar det som används av uppdaterings servern.

  > [!TIP]  
  > Om du inte konfigurerar en uppdaterings Server kan du fortfarande använda Updates Publisher för att redigera program uppdateringar.

- **Konfigurera signerings certifikatet**. Du måste konfigurera och ansluta till en uppdaterings server innan du kan konfigurera signerings certifikatet.

  Updates Publisher använder signerings certifikatet för att signera program uppdateringar som publiceras på uppdaterings servern. Publiceringen Miss lyckas om det digitala certifikatet inte är tillgängligt i certifikat arkivet på uppdaterings servern eller på den dator som kör Updates Publisher.

  Mer information om hur du lägger till certifikatet i certifikat arkivet finns i [certifikat och säkerhet för Updates Publisher](updates-publisher-security.md).

  Om ett digitalt certifikat inte identifieras automatiskt för uppdaterings servern väljer du något av följande:

  -   **Bläddra**: Bläddra är bara tillgänglig när uppdaterings servern är installerad på den server där du kör-konsolen. När du har valt ett certifikat måste du välja **skapa** för att lägga till certifikatet i WSUS-certifikatarkivet på uppdaterings servern. Du måste ange **. pfx** -filens lösen ord för certifikat som du väljer med den här metoden.

  -   **Skapa:** Använd det här alternativet om du vill skapa ett nytt certifikat. Detta lägger också till certifikatet i WSUS-certifikat arkivet på uppdaterings servern.

  **Om du skapar ett eget signerings certifikat konfigurerar du**följande:

  -   Aktivera alternativet **Tillåt att den privata nyckeln exporteras** .

  -   Ange **nyckel användning** till digital signatur.

  -   Ange den **minsta nyckel storleken** till ett värde som är lika med eller större än 2048 bitar.

  Använd alternativet **ta bort** om du vill ta bort ett certifikat från WSUS-certifikatarkivet. Det här alternativet är tillgängligt när uppdaterings servern är lokal i den Updates Publisher-konsol som du använder, eller när du använde **SSL** för att ansluta till en fjärruppdaterings Server.

## <a name="configmgr-server"></a>ConfigMgr-Server
Använd de här alternativen när du använder Configuration Manager med Updates Publisher.

-   **Ange Configuration Manager Server:** När du har aktiverat stöd för Configuration Manager anger du platsen för plats servern på den översta nivån från din Configuration Manager hierarki. Om den servern är fjärran sluten till installations programmet för uppdateringar anger du FQDN för plats servern. Välj **Testa anslutning** för att se till att du kan ansluta till plats servern.

-   **Konfigurera tröskelvärden:** Tröskelvärden används när du publicerar uppdateringar med en publikationstyp av typen automatisk. Tröskelvärdena hjälper till att avgöra när det fullständiga innehållet för en uppdatering publiceras i stället för endast metadata. Mer information om publikationstyper finns i [tilldela uppdateringar till en publikation](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication)

    Du kan välja ett eller båda av följande tröskelvärden:

    -   **Tröskelvärde för begärt antal klienter:** Detta definierar hur många klienter som måste begära en uppdatering innan uppdaterings utgivare kan publicera hela uppsättningen innehåll för uppdateringen automatiskt. Tills det angivna antalet klienter begär uppdateringen publiceras endast uppdateringarnas metadata.

    -   **Storleks tröskel för paket källa (MB):** Detta förhindrar automatisk publicering av uppdateringar som överskrider den storlek som du anger. Om uppdaterings storleken överskrider det här värdet publiceras bara metadata. Uppdateringar som är mindre än den angivna storleken kan ha sitt fullständiga innehåll publicerat.

## <a name="proxy-settings"></a>Proxyinställningar
Updates Publisher använder proxyinställningarna när du importerar program varu kataloger från Internet eller publicerar uppdateringar på Internet.

-   Ange FQDN eller IP-adress för en proxyserver. Har stöd för IPv4 och IPv6.

-   Om proxyservern autentiserar användare för Internet åtkomst måste du ange Windows-namnet. Det finns inte stöd för ett UPN (Universal Principal Name).

## <a name="trusted-publishers"></a>Betrodda utgivare
När du importerar en uppdaterings katalog läggs källan till katalogen (baserat på dess certifikat) till som en betrodd utgivare. På samma sätt läggs källan till uppdaterings certifikatet till som en betrodd utgivare när du publicerar en uppdatering.

Du kan Visa certifikat information för varje utgivare och ta bort en utgivare från listan över betrodda utgivare.

Innehåll från utgivare som inte är betrodda kan potentiellt skada klient datorer när klienten söker efter uppdateringar. Du bör endast acceptera innehåll från utgivare som du litar på.

## <a name="advanced"></a>Avancerat
Avancerade alternativ inkluderar följande:

-   **Plats för databas:** Visa och ändra plats för databas filen, **Scupdb. SDF**. Den här filen är lagrings platsen för Updates Publisher.

-   **Tidsstämpel:** När den är aktive rad läggs en tidsstämpel till i de uppdateringar du loggar som identifierar när den signerades. En uppdatering som signerades medan ett certifikat var giltig kan användas efter det att signerings certifikatet upphör att gälla. Som standard går det inte att distribuera program uppdateringar när deras signerings certifikat upphör att gälla.

-   **Sök efter uppdateringar av prenumererade kataloger:** Varje uppdatering av Publisher startar kan den automatiskt söka efter uppdateringar av kataloger som du prenumererar på. När en katalog uppdatering hittas, tillhandahålls information som de **senaste aviseringarna** i **översikts** fönstret i **arbets ytan uppdateringar**.

-   **Certifikat återkallning:** Välj det här alternativet för att aktivera kontroller av återkallade certifikat.

-   **Lokal käll publicering:** Updates Publisher kan använda en lokal kopia av en uppdatering som du publicerar innan du hämtar uppdateringen från Internet. Platsen måste vara en mapp på den dator som kör Updates Publisher. Som standard är den här platsen **min Documents\LocalSourcePublishing.** Använd det här när du tidigare har laddat ned en eller flera uppdateringar eller har gjort ändringar i en uppdatering som du vill distribuera.

-   **Guiden rensning av program uppdateringar:** Starta guiden Rensa uppdateringar. Guiden upphör att gälla uppdateringar som finns på uppdaterings servern, men inte i uppdaterings utgivarens lagrings plats. Se [Expires-uppdateringar som inte refererats](#expire-unreferenced-software-updates) för mer information.

## <a name="updates"></a>Uppdateringar
 Updates Publisher kan automatiskt söka efter nya uppdateringar varje gången den öppnas. Du kan också välja att ta emot för hands versioner av Updates Publisher.

Om du vill söka efter uppdateringar manuellt klickar du på ![egenskaper i Updates Publisher-konsolen](media/properties2.png)  
öppna egenskaperna för **Updates Publisher**och välj sedan **Sök efter uppdatering**.

När Updates Publisher hittar en ny uppdatering visas fönstret **uppdatering tillgänglig** och du kan välja att installera det. Om du väljer att inte installera uppdateringen erbjuds den nästa gången du öppnar konsolen.

## <a name="logging"></a>Loggning
Updates Publisher loggar grundläggande information om Updates Publisher till **%windir%\Temp\UpdatesPublisher.log**.

Använd anteckningar eller **CMTrace** för att visa loggen. CMTrace är Configuration Manager logg fils verktyget och finns i mappen **\SMSSetup\Tools** på käll mediet för Configuration Manager.

Du kan ändra storleken på loggen och dess detalj nivå.

När du aktiverar databas loggning inkluderas information om de frågor som körs mot Updates Publisher-databasen. Användningen av databas loggning kan leda till minskad prestanda hos Updates Publisher-datorn.

Om du vill visa logg filen går du till-konsolen ![och](media/properties2.png) klickar på Egenskaper för att öppna **egenskaperna för Updates Publisher**och väljer sedan **Visa loggfil**.

## <a name="expire-unreferenced-software-updates"></a>Förfallna program uppdateringar som inte refererats
Du kan köra **Guiden rensning av program uppdatering** för att upphöra att gälla uppdateringar som finns på din uppdaterings Server, men inte i Updates Publisher-lagringsplatsen. Detta meddelar Configuration Manager som sedan tar bort uppdateringarna från framtida distributioner.

Det går inte att ångra en uppdaterings åtgärd. Utför bara den här uppgiften när du är säker på att de program uppdateringar du väljer inte längre krävs av din organisation.

### <a name="to-remove-expired-software-updates"></a>Ta bort program uppdateringar som har upphört att gälla
1.  I Updates Publisher-konsolen klickar du på ![egenskaper](media/properties2.png) för att öppna **egenskaperna för Updates Publisher**och väljer sedan **alternativ**.

2.  Välj **Avancerat**och gå sedan till **guiden Rensa program uppdatering** och välj **Starta**.

3.  Välj de program uppdateringar som du vill upphör att gälla och välj sedan **Nästa**.

4.  När du har granskat dina val väljer du **Nästa** för att godkänna valen och förfaller uppdateringarna.

5.  När guiden har slutförts väljer du **Stäng** för att slutföra guiden.
