---
title: Snabb start för Support Center
titleSuffix: Configuration Manager
description: Registrera snabbt status för en Configuration Manager-klient för fel sökning.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5cb41e2b-4c79-4da9-a432-ff869c0870f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c8c43fe1dbca9155bf9b554a2554c652b1482583
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723119"
---
# <a name="support-center-quickstart-guide"></a>Snabb starts guide för Support Center

*Gäller för: Configuration Manager (aktuell gren)*

Support Center har kraftfulla funktioner, inklusive fel sökning och logg visning i real tid. Det kan också användas på bara några minuter för att avbilda status för en Configuration Manager klient dator. Den här möjligheten inkluderar åtkomst till fjärrklienter.

Skapa en fullständig *fel söknings paket* fil (. zip) som fångar upp klientens tillstånd. Paketet innehåller inte bara loggfiler. Den kan innehålla andra typer av data, till exempel register inställningar och klientkonfigurationer. Ge paketet till en support tekniker som använder Support Center Viewer.



## <a name="prerequisites"></a>Krav

- Lokal administratörs behörighet till en Configuration Manager-klient  

- Installations programmet för Support Center. Den här filen finns på plats servern på `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`. Mer information finns i [Support Center-install](support-center.md#install).  



## <a name="step-1-create-a-data-bundle-on-a-local-client"></a>Steg 1: skapa ett data paket på en lokal klient

1.  Installera Support Center på Configuration Manager-klienten.  

2.  Gå till **Start** -menyn, i gruppen **Microsoft System Center** , väljer du **Support Center**.  

3.  På fliken Start i menyfliksområdet väljer du **samla in markerade data**. Som standard samlar Support Center endast in den minsta data uppsättningen: loggfiler, klient konfiguration och operativ system.  

4.  Spara fel söknings paket filen (. zip) i en mapp på datorn. Som standard liknar fil namnet följande exempel: `Support_c885cdfed3c7482bba4f9e662978ec07.zip`.  



## <a name="step-2-view-the-data-bundle-using-support-center-viewer"></a>Steg 2: Visa data paketet med Support Center Viewer

1.  Starta **Support Center Viewer**. Den här åtgärden kan inträffa på alla datorer där du installerar Support Center.  

2.  Välj **Öppna paket**, bläddra till paket filen och välj **Öppna**.  

3.  När Support Center Viewer bearbetar filen växlar du till fliken tillgänglig. Visa de typer av data som Support Center samlar in som standard:  

    - **Konfiguration**  

        - Configuration Manager klient konfiguration  

        - Operativsystem  

        - Dator  

        - Tjänster  

        - Nätverkskort  

    - **Loggar**: Välj en eller flera poster i listan och välj **Öppna**. Den här åtgärden öppnar de valda loggfilerna i logg visaren. Använd den här funktionen för att leta upp felkoder och använda avancerade filter för att snabbt analysera loggfiler.  



## <a name="collect-more-data"></a>Samla in mer data

Utöver de här grundläggande funktionerna kan Support Center också samla in en mängd andra klient tillstånds uppgifter. Öppna **Support Center** och välj **samla in alla data**. Den här processen varar vanligt vis flera minuter, även på nyare datorer. Support Center samlar in följande ytterligare data:

- **Princip**: Configuration Manager princip inställningar, inklusive både den begärda princip konfigurationen och den faktiska princip konfigurationen  

- **Certifikat**: information om offentlig nyckel för klient certifikat. Support Center samlar inte in certifikatets privata nycklar.  

- **Klient register**: samlar in klient konfigurations information från registret. Support Center samlar endast in Configuration Manager register information.  

- **Klient-WMI**: klient konfigurations information från WMI. Support Center samlar inte in klient principer.  

- **Fel sökning**: real tids fel söknings data som hjälper dig att diagnostisera vanliga klient problem med Active Directory, hanterings platser, nätverk, princip tilldelningar och registrering.  

- **Fel söknings dum par**: utför en fel söknings dumpning av klienten och relaterade processer. Fel söknings dum par kan vara stora. Aktivera bara det här alternativet när du felsöker problem med klient prestanda.  

