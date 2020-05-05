---
title: Definiera gränser
titleSuffix: Configuration Manager
description: Lär dig hur du definierar nätverks platser i intranätet som kan innehålla enheter som du vill hantera.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f53088843e0bf42a93c1d959255c7885b07dfe35
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721117"
---
# <a name="define-network-locations-as-boundaries-for-configuration-manager"></a>Definiera nätverks platser som gränser för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager gränser är platser i nätverket som innehåller enheter som du vill hantera. Den gränser som en enhet är på motsvarar den Active Directory platsen eller nätverks-IP-adressen som identifieras av Configuration Manager-klienten som är installerad på enheten.
- Du kan skapa enskilda gränser manuellt. Configuration Manager har dock inte stöd för direkt registrering av en övernät som en avgränsning. Använd gränstypen för IP-adressintervall i stället.
- Du kan konfigurera [identifierings metoden för Active Directory skogar](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) för att automatiskt identifiera och skapa gränser för varje IP-undernät och Active Directory plats som identifieras. När Active Directory skogs identifiering identifierar en övernät som är tilldelad en Active Directory plats Configuration Manager konverteras övernät till ett IP-adressintervall.  

Det är inte ovanligt att en enhet använder en IP-adress som Configuration Managers administratören inte känner till. När nätverks platsen för en enhet är tveksam kontrollerar du vad enheten rapporterar som sin plats med hjälp av kommandot **ipconfig** på enheten.  

När du konfigurerar en gräns tilldelas den automatiskt ett namn som baseras på gränsens typ och omfattning. Du kan inte ändra namnet. I stället kan du ange en beskrivning som hjälper dig att identifiera gränserna i Configuration Manager-konsolen.  

Varje avgränsning är tillgänglig för alla platser i hierarkin. När en gränsen har skapats kan du ändra dess egenskaper för att göra följande:  
- Lägga till gränsen i en eller flera gränsgrupper.  
- Ändra gränsens typ eller omfattning.  
- Visa fliken **Platssystem** för gränserna för att se vilka platssystemservrar (distributionsplatser, tillståndsmigreringsplatser och hanteringsplatser) som är associerade med gränsen.  

## <a name="to-create-a-boundary"></a>Skapa en gräns  

1.  I Configuration Manager-konsolen klickar du på**konfigurations** > **gränser** för **administrations** > hierarki  

2.  På fliken **Start** går du till gruppen **Skapa** och klickar på **Skapa Boundary**.  

3.  På fliken **Allmänt** i dialogrutan Skapa gräns kan du i rutan **Beskrivning** ange en lämplig beskrivning som gör det lätt att urskilja gränsen.  

4.  I **Typ** väljer du en gränstyp:  

    - Om du väljer **IP-undernät**måste du ange undernätets ID i **Undernät-ID** .  
      > [!TIP]  
      > Du kan ange information i **Nätverk** och **Nätmask** så fylls **Undernät-ID** i automatiskt. När du sparar gränsen, sparas endast undernät-ID:t.  

    - Om du väljer **Active Directory-plats**måste du ange eller navigera till (genom att välja **Bläddra** ) en Active Directory-plats i platsserverns lokala skog.  
        
      - Om du anger en Active Directory-plats för en gräns, inkluderas alla IP-undernät som ingår i den angivna Active Directory-platsen. Om Active Directory-platsens konfiguration ändras i Active Directory, ändras även de nätverksplatser som ingår i gränsen.  

      - Active Directory plats gränser fungerar inte för rena AzureAD-klienter. Om de roamas lokalt kommer de inte att hamna i någon gräns om de bara definieras med AD-platser.

    - Om du väljer **IPv6-prefix**måste du i **Prefix** ange ett prefix i rätt format för IPv6.  

    - Om du väljer **IP-adressintervall**måste du, genom att ange värden i **Inledande IP-adress** och **Avslutande IP-adress** , ange ett intervall som innehåller en del av ett IP-undernät eller flera IP-undernät.    

5.  Spara den nya gränsen genom att klicka på **OK** .  

## <a name="to-configure-a-boundary"></a>Konfigurera en gräns  

1.  I Configuration Manager-konsolen klickar du på**konfigurations** > **gränser** för **administrations** > hierarki  

2.  Välj den gräns som du vill ändra.  

3.  På fliken **Start** går du till gruppen **Egenskaper** och klickar på **Egenskaper**.  

4.  Om du vill redigera **Beskrivning** eller **Typ** väljer du fliken **Allmänt** i dialogrutan **Egenskaper** . Du kan även ändra en gräns omfattning genom att ändra gränsens nätverksplatser. För till exempel en Active Directory-platsgräns kan du ange ett nytt Active Directory-platsnamn.  

5.  Välj fliken **Platssystem** för att visa de platssystem som är associerade med gränsen. Det går inte att ändra konfigurationen i gränsens egenskaper.  

    > [!TIP]  
    > Om en platssystemserver ska visas som platssystem för en gräns, måste platssystemservern associeras som platssystemserver för minst en gränsgrupp där gränsen ingår. Detta konfigureras på fliken **Referenser** för en gränsgrupp.  

6.  Klicka på fliken **Begränsningsgrupper** om du vill byta gränsgrupp för den aktuella gränsen:  

    - Vill du lägga till gränsen i en eller flera gränsgrupper, klickar du på **Lägg till**, markerar kryssrutan för en eller flera gränsgrupper och klickar sedan på **OK**.  

    - Vill du ta bort gränsen från en gränsgrupp, markerar du gränsgruppen och klickar på **Ta bort**.  

7.  Stäng gränsegenskaperna och spara konfigurationen genom att klicka på **OK** .  
