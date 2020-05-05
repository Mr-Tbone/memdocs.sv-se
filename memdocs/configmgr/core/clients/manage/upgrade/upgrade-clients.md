---
title: Uppgradera klienter
titleSuffix: Configuration Manager
description: Hämta information om hur du uppgraderar klienter i Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95e6ebf1544951b71ca2b60615e3e01b27cc0f3b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076687"
---
# <a name="upgrade-clients-in-configuration-manager"></a>Uppgradera klienter i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan använda olika metoder för att uppgradera Configuration Manager-klient program vara på Windows-datorer, UNIX-och Linux-servrar och Mac-datorer. Här är fördelarna och nack delarna med varje metod.  

> [!TIP]  
>  Om du uppgraderar serverinfrastrukturen från en tidigare Configuration Manager \(som Configuration Manager 2007 eller System Center 2012 Configuration Manager\) rekommenderar vi att du slutför serveruppgraderingarna och installerar alla uppdateringar av den aktuella grenen innan du uppgraderar Configuration Manager-klienterna. På så sätt har du också den senaste versionen av klient program varan.  

## <a name="group-policy-installation"></a>Grupprincipinstallation  
 **Klientplattform som stöds:** Windows  

#### <a name="advantages"></a>Fördelar  

- Datorer behöver inte ha identifierats innan klienten kan uppgraderas.  

- Kan användas för nya klientinstallationer eller för uppgraderingar.  

- Datorer kan läsa klientinstallationsegenskaper som har publicerats på Active Directory Domain Services.  

- Kräver inte att du konfigurerar och underhåller ett installationskonto för den avsedda klientdatorn.  

#### <a name="disadvantages"></a>Nackdelar  

- Kan orsaka hög nätverks trafik om du uppgraderar många klienter.  

- Om Active Directory-schemat inte har utökats för Configuration Manager måste du använda [Grupprincip inställningar](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP) för att lägga till klient installations egenskaper på datorerna på din plats.  


## <a name="logon-script-installation"></a>Installation av inloggningsskript  
 **Klientplattform som stöds:** Windows  

#### <a name="advantages"></a>Fördelar  

- Datorer behöver inte ha identifierats innan klienten kan installeras.  

- Kan användas för nya klientinstallationer eller för uppgraderingar.  

- Har stöd för kommandoradsegenskaper för CCMSetup.  

#### <a name="disadvantages"></a>Nackdelar  

- Kan orsaka hög nätverks trafik om du uppgraderar många klienter på kort tid.  

- Det kan ta lång tid att uppgradera alla klient datorer om användarna inte ofta loggar in på nätverket.  

  Mer information finns i [Installera Configuration Manager-klienter med hjälp av inloggningsskript](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  

## <a name="manual-installation"></a>Manuell installation  
 **Klientplattform som stöds:** Windows, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Fördelar  

- Datorer behöver inte ha identifierats innan klienten kan uppgraderas.  

- Kan vara användbart för testning.  

- Har stöd för kommandoradsegenskaper för CCMSetup.  

#### <a name="disadvantages"></a>Nackdelar  

- Ingen automatisering och är därför tidskrävande.  

  Mer information finns i följande avsnitt:  

- [Så här installerar du Configuration Manager-klienter manuellt](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

- [Uppgradera klienter för Linux-och UNIX-servrar](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

- [Uppgradera klienter på Mac-datorer](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>Uppgraderingsinstallation (programhantering)  
 **Klientplattform som stöds:** Windows  

> [!NOTE]  
>  Du kan inte uppgradera Configuration Manager 2007-klienter med den här metoden. I det här scenariot kan du distribuera Configuration Manager-klienten som ett paket från Configuration Manager 2007-platsen, eller så kan du använda automatisk klient uppgradering som automatiskt skapar och distribuerar ett paket som innehåller den senaste versionen av klienten.  

#### <a name="advantages"></a>Fördelar  

- Har stöd för kommandoradsegenskaper för CCMSetup.  

#### <a name="disadvantages"></a>Nackdelar  

- Kan orsaka hög nätverks trafik om du distribuerar klienten till stora samlingar.  

- Kan endast användas för att uppgradera klientprogramvaran på datorer som har identifierats och tilldelats till platsen.  

  Mer information finns i [Installera Configuration Manager-klienter genom att använda ett paket och programt](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp).  

## <a name="automatic-client-upgrade"></a>Automatisk klientuppgradering  

> [!NOTE]  
> Kan användas för att uppgradera Configuration Manager 2007-klienter till Configuration Manager aktuella filial klienter. En Configuration Manager 2007-klient kan tilldela till en Configuration Manager plats, men kan inte utföra några åtgärder förutom automatisk klient uppgradering.  

 **Klientplattform som stöds:** Windows  

#### <a name="advantages"></a>Fördelar  

- På grund av slumpmässigheten under den angivna perioden är bara automatisk uppgradering lämplig för storskaliga klient uppgraderingar. Andra metoder är antingen för långsamma vid stor skala eller har ingen slumpmässighet. 

    > [!Note]
    > Klient piloten är inte lämpad för stor skala eftersom den inte slumpare alls.  
- Kan användas för att automatiskt se till att klienterna på din plats är av den senaste versionen.  

- Kräver minimal administration.  

#### <a name="disadvantages"></a>Nackdelar  

- Kan endast användas för att uppdatera klientprogramvaran, inte för att installera en ny klient.  

- Gäller för alla klienter i hierarkin som är tilldelade till en plats. Kan inte begränsas per samling.  

- Begränsade möjligheter till schemaläggning.  

  Mer information finns i [Uppgradera klienter för Windows-datorer](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="client-testing"></a>Klienttest  
 **Klientplattform som stöds:** Windows  

#### <a name="advantages"></a>Fördelar  

- Kan användas för att testa nya klient versioner i en mindre för produktions samling.  

- När testningen är klar befordras klienter i för produktion till produktion och uppgraderas automatiskt på den Configuration Manager webbplatsen.  

#### <a name="disadvantages"></a>Nackdelar  

- Kan endast användas för att uppdatera klientprogramvaran, inte för att installera en ny klient.  

  [Testa klient uppgraderingar i en för produktions samling](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  
