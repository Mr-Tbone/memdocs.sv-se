---
title: Definiera gränser
titleSuffix: Configuration Manager
description: Lär dig hur du definierar nätverks platser i intranätet som kan innehålla enheter som du vill hantera.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 41c0d08c5f445cd6d643542cfaa646bc2d89de76
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128434"
---
# <a name="define-network-locations-as-boundaries-for-configuration-manager"></a>Definiera nätverks platser som gränser för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager gränser är platser i nätverket som innehåller enheter som du vill hantera. Du kan skapa olika typer av gränser, till exempel en Active Directory webbplats eller nätverks-IP-adress. När Configuration Manager-klienten identifierar en liknande nätverks plats, är enheten en del av kanten.

Configuration Manager stöder följande typer av gränser:

- IP-undernät
- Active Directory-plats
- IPv6-prefix
- IP-adressintervall
- VPN (från och med version 2006)

Du kan skapa enskilda gränser manuellt eller använda [Active Directory skogs identifiering](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest). Den här identifierings metoden söker automatiskt efter och skapar gränser för IP-undernät och Active Directory platser. När Active Directory skogs identifiering identifierar en övernät för en Active Directory plats, konverterar Configuration Manager övernät till ett IP-adressintervall.

Om en enhet inte är inom gränsen som du förväntar dig, kan det bero på att du inte har definierat nätverks platsen som en gräns. När nätverks platsen för en enhet är tveksam använder du följande Windows-kommandon på enheten för att bekräfta:

- IP-adress:`ipconfig`
- Active Directory webbplats:`nltest /dsgetsite`
- Konfigurera`ipconfig /all`

## <a name="boundary-types"></a>Avgränsnings typer

### <a name="ip-subnet"></a>IP-undernät

IP-undernätets gränser typ kräver ett **Undernäts-ID**. Till exempel `169.254.0.0`. Om du anger värden för **nätverk** (standard-gateway) och **nätmask** , beräknar Configuration Manager automatiskt **under nätets ID**. När du sparar gränser sparas Configuration Manager bara under nätets ID-värde.

> [!NOTE]
> Configuration Manager har inte stöd för direkt inmatning av en övernät som en avgränsning. Använd gränstypen för IP-adressintervall i stället.

### <a name="active-directory-site"></a>Active Directory-plats

För **Active Directory platsens** kant linje typ anger du platsens namn. Du kan ange namnet eller bläddra i den lokala skogen på plats servern.

När du anger en Active Directory plats för en gränser, innehåller bindningen varje IP-undernät som är medlem av den Active Directory webbplatsen. Om Active Directory-platsens konfiguration ändras i Active Directory, ändras även de nätverksplatser som ingår i gränsen.  

Active Directory plats gränser fungerar inte för rena Azure Active Directory (Azure AD)-enheter, även kallade anslutna enheter i molnet. Om de använder roaming lokalt, och du bara skapar Active Directory plats typs gränser, så kommer dessa enheter inte att vara inom gränsen.

> [!TIP]
> Använd följande Windows-kommando om du vill se en enhets aktuella Active Directory webbplats: `nltest /dsgetsite` .
>
> Använd följande Windows-kommando för att avgöra om en klient är ansluten till en molnbaserad domän: `dsregcmd /status` . Mer information finns i [dsregcmd-kommando enhets tillstånd](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-device-dsregcmd).

### <a name="ipv6-prefix"></a>IPv6-prefix

Ange ett **prefix**för **IPv6-prefixets** gränser-typ. Till exempel `2001:1111:2222:3333`.

### <a name="ip-address-range"></a>IP-adressintervall

Ange den **första IP-adressen** och den **sista IP-adressen** för intervallet för intervallets typ av **IP-adressintervall** . Intervallet kan omfatta en del av ett IP-undernät eller flera IP-undernät. Använd en bindnings typ för IP-adressintervall för att stödja en övernät.

Du kan också använda den här typen för att definiera en gränser för en enskild IP-adress. Ange både start-och slut-IP-adresserna som samma värde. Den här konfigurationen kan vara användbar för unika enheter eller test miljöer.

### <a name="vpn"></a>VPN

<!--7020519-->

Från och med version 2006, för att förenkla hanteringen av fjärrklienter, skapar du en avgränsnings typ för VPN-nätverk. När en klient skickar en plats förfrågan innehåller den ytterligare information om nätverks konfigurationen. Baserat på den här informationen avgör servern om klienten finns på en VPN-server. För att Configuration Manager associera klienten i den här kanten ansluter du enheten till VPN-nätverket.

Du kan konfigurera en VPN-gränser på flera sätt:

- **Identifiera VPN automatiskt**: Configuration Manager identifierar alla VPN-lösningar som använder PPTP (Point-to-Point Tunneling Protocol). Använd något av de andra alternativen om den inte identifierar ditt VPN. Avgränsning svärdet i konsol listan är `Auto:On` .

- **Anslutnings namn**: Ange namnet på VPN-anslutningen på enheten. Det är namnet på nätverkskortet i Windows för VPN-anslutningen. Configuration Manager matchar de första 250 tecknen i strängen, men stöder inte jokertecken eller partiella strängar. Värdet i konsol listan kommer att vara `Name:<name>` , där `<name>` är det anslutnings namn som du anger.

  Du kan till exempel köra `ipconfig` kommandot på enheten, och något av avsnitten börjar med: `PPP adapter ContosoVPN:` . Använd strängen `ContosoVPN` som **anslutnings namn**. Den visas i listan som `Name:CONTOSOVPN` .

- **Anslutnings Beskrivning**: Ange en beskrivning av VPN-anslutningen. Configuration Manager matchar de första 243 tecknen i strängen, men stöder inte jokertecken eller partiella strängar. Värdet i konsol listan är `Description:<description>` , där `<description>` är den anslutnings beskrivning som du anger.

  Du kan till exempel köra `ipconfig /all` kommandot på enheten, och en av anslutningarna innehåller följande rad: `Description . . . . . . . . . . . : ContosoMainVPN` . Använd strängen `ContosoMainVPN` som **anslutnings Beskrivning**. Den visas i listan som `Description:CONTOSOMAINVPN` .

> [!IMPORTANT]
> För att dra full nytta av den här funktionen kan du, när du har uppdaterat platsen, även uppdatera klienter till den senaste versionen. Nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen. Det fullständiga scenariot fungerar inte förrän klient versionen också är den senaste.
>
> Om du vill använda VPN-gränser under en operativ Systems distribution, måste du också uppdatera start avbildningen så att den innehåller de senaste-klient binärfilerna.

## <a name="create-a-boundary"></a>Skapa en kant linje

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **konfiguration av hierarki**och väljer noden **gränser** .

1. På fliken **Start** i menyfliksområdet väljer du **skapa kant linje**i gruppen **skapa** .

1. Ange följande information på fliken **Allmänt** i fönstret **skapa gränser** :

    - **Beskrivning**: identifiera avgränsningen med ett eget namn eller en referens.

        > [!NOTE]
        > Configuration Manager automatiskt namnger gränsen baserat på dess typ och omfattning. Du kan inte ändra namnet.

    - **Typ**: Välj den typ av kant linje som ska skapas. Ange ytterligare information som krävs för typen. Mer information finns i [avgränsnings typer](#boundary-types).

1. Växla till fliken **gränser grupper** . Om du redan har begränsade grupper på platsen kan du omedelbart lägga till den här nya avgränsningen i en eller flera grupper.

1. Välj **OK** för att spara den nya avgränsningen.

## <a name="configure-a-boundary"></a>Konfigurera en kant linje

> [!TIP]
> När du skapar en begränsning Configuration Manager automatiskt namnet baserat på begränsningens typ och omfång. Du kan inte ändra det här namnet. Ange en beskrivning för att identifiera gränserna i Configuration Manager-konsolen.

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **konfiguration av hierarki**och väljer noden **gränser** .

1. Välj den gräns som du vill ändra. Välj **Egenskaper**i gruppen **Egenskaper** på fliken **Start** i menyfliksområdet.

1. I fönstret **Egenskaper** för gränsen går du till fliken **Allmänt** och konfigurerar följande inställningar:

    - Redigera **beskrivningen**
    - Ändra kant linje **typ**
    - Ändra omfattning för en begränsning genom att redigera dess nätverks platser. För till exempel en Active Directory-platsgräns kan du ange ett nytt Active Directory-platsnamn.

1. Om du vill visa de plats system som är associerade med den här gränser, byter du till fliken **plats system** . Du kan inte ändra den här konfigurationen från egenskaperna för en kant linje.

    > [!TIP]
    > För att en server ska visas som ett plats system för en gränser associerar du den som en plats system Server för minst en avgränsnings grupp som innehåller den här gränser. Gör den här konfigurationen på fliken **referenser** för en avgränsnings grupp. Mer information finns i [Konfigurera platstilldelning och välj plats system servrar](boundary-group-procedures.md#bkmk_references).

1. Om du vill ändra gränserna för gränserna för den här gränser väljer du fliken **gränser grupper** :

    - Välj **Lägg till**om du vill lägga till den här avgränsningen i en eller flera gränser grupper. Välj en eller flera avgränsnings grupper och välj sedan **OK**.

    - Om du vill ta bort den här kanten från en ram väljer du den och väljer sedan **ta bort**.

1. Välj **OK** för att stänga gränser-egenskaperna och spara konfigurationen.

## <a name="next-steps"></a>Nästa steg

Varje avgränsning är tillgänglig för alla platser i hierarkin. När du har skapat en kant linje lägger du till den i en eller flera [gränser grupper](boundary-groups.md).
