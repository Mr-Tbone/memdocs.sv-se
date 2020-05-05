---
title: Mottagar distributions plats
titleSuffix: Configuration Manager
description: Lär dig mer om konfigurationer och begränsningar för att använda en mottagar distributions plats med Configuration Manager. "
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c243897a4c52eff04263325b998c4b23d6b3dde4
ms.sourcegitcommit: ad4b3e4874a797b755e774ff84429b5623f17c5c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/27/2020
ms.locfileid: "82166595"
---
# <a name="use-a-pull-distribution-point-with-configuration-manager"></a>Använd en mottagar distributions plats med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du distribuerar innehåll till en standard distributions plats i Configuration Manager-konsolen skickar plats servern innehållet till distributions platsen. En mottagar distributions plats hämtar innehåll genom att hämta det från en käll plats som en-klient.  

När du distribuerar innehåll till flera distributions platser bidrar mottagar distributions platser till att minska bearbetnings belastningen på plats servern. De kan också påskynda innehålls överföringen till varje server. Normalt skickar distributions hanterarens komponent på plats servern innehåll till varje distributions plats. I stället avlastar platsen överföringen av innehållet till mottagar distributions platserna.  

Du konfigurerar enskilda distributions platser som mottagar distributions platser. För varje mottagar distributions plats anger du en eller flera käll distributions platser som den kan hämta innehåll från. En mottagar distributions plats kan endast hämta innehåll från en distributions plats som du anger som käll distributions plats.

När du distribuerar innehåll till en mottagar distributions plats i-konsolen skickar plats servern den till en avisering. Mottagar distributions platsen hämtar sedan innehållet från en käll distributions plats. En mottagar distributions plats hanterar innehålls överföringen genom att ladda ned från en distributions plats som redan har en kopia av innehållet.  

Mottagar distributions platser har stöd för samma konfigurationer och funktioner som vanliga distributions platser. En mottagar distributions plats stöder till exempel:

- Multicast-och PXE-konfigurationer
- Innehålls validering
- Innehållsdistribution på begäran
- HTTP-eller HTTPS-kommunikation från klienter
- Samma certifikat alternativ som andra distributions platser
- Hantera individuellt eller som medlem i en distributions plats grupp  

Konfigurera en mottagar distributions plats när du installerar distributions platsen. När du har skapat en distributions plats konfigurerar du den som en mottagar distributions plats genom att redigera roll egenskaperna. Mer information om hur du aktiverar en distributions plats som en mottagar distributions plats finns i [mottagar distributions plats](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pull).  

Ta bort konfigurationen till en mottagar distributions plats genom att redigera egenskaperna för distributions platsen. När du tar bort konfigurationen som en mottagar distributions plats återgår den till normal drift. Plats servern hanterar framtida innehålls överföringar till distributions platsen.  

## <a name="distribution-process"></a>Distributions process

När du distribuerar innehåll till en mottagar distributions plats inträffar följande händelse ordning:

- När du distribuerar innehåll till en mottagar distributions plats i-konsolen, kontrollerar Package Transfer Manager-komponenten på plats servern plats databasen för att bekräfta om innehållet är tillgängligt på en käll distributions plats. Om det inte går att bekräfta att innehållet finns på en käll distributions plats för mottagar distributions platsen, upprepas kontrollen var 20: e minut tills innehållet är tillgängligt.  

- När Package Transfer Manager bekräftar att innehållet är tillgängligt meddelas mottagardistributionsplatsen att innehållet ska laddas ned. Om det här meddelandet Miss lyckas görs ett nytt försök baserat på **inställningarna** för komponenten för program varu distribution för mottagar distributions platser. När mottagar distributions platsen tar emot det här meddelandet försöker den Ladda ned innehållet från sina käll distributions platser.  

- När mottagar distributions platsen laddar ned innehållet, avsöker paket överförings hanteraren statusen baserat på status för program distributionens komponent **status avsöknings inställningar** för mottagar distributions platser.  När mottagar distributions platsen Slutför nedladdningen av innehåll skickas den här statusen till en hanterings plats.  

## <a name="configure-site-component-settings"></a>Konfigurera inställningar för plats komponent

När du använder en mottagar distributions plats granskar och konfigurerar du följande inställningar för plats komponenter:  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .  

2. Välj-platsen. I menyfliksområdet väljer du **Konfigurera plats komponenter**och välj **program varu distribution**.  

3. Växla till fliken **mottagar distributions plats** .  

4. Granska följande värden i gruppen **Inställningar för återförsök** :  

    - **Antal återförsök**: antalet gånger som Package Transfer Manager försöker meddela mottagar distributions platsen för att hämta innehållet. När det har försökt det här antalet gånger avbryter Package Transfer Manager överföringen. Värdet är 30 som standard.  

    - **Fördröjning före nytt försök (minuter)**: antalet minuter som paket överförings hanteraren väntar mellan försök. Värdet är 20 som standard.  

5. I gruppen **status avsöknings inställningar** granskar du följande värden:  

    - **Antal avsökningar**: antalet gånger som Package Transfer Manager kontaktar mottagar distributions platsen för att hämta jobb status. Om det försöker det här antalet gånger innan jobbet har slutförts, avbryter Package Transfer Manager överföringen. Värdet är 72 som standard.

    - **Fördröjning före nytt försök (minuter)**: antalet minuter som paket överförings hanteraren väntar mellan försök. Värdet är 60 som standard.

    > [!NOTE]  
    >  När Package Transfer Manager avbryter ett jobb eftersom det överskrider antalet avsöknings försök fortsätter mottagar distributions platsen att ladda ned innehållet. När den är klar skickar mottagar distributions platsen rätt status meddelande och konsolen visar den nya statusen.  

## <a name="limitations"></a>Begränsningar

- Du kan inte konfigurera en moln distributions plats som en mottagar distributions plats.  

- Du kan inte konfigurera distributions plats rollen på en plats server som en mottagar distributions plats.  

- Den förinstallerade innehållskonfigurationen åsidosätter konfigurationen av mottagardistributionsplatsen. Om du aktiverar alternativet för att **Aktivera den här distributions platsen för förinstallerat innehåll** på en mottagar distributions plats väntar det på innehållet. Det tar inte emot innehåll från käll distributions platsen. Precis som en standard distributions plats som är aktive rad för förinstallerat innehåll, tar den inte emot innehåll från plats servern. Mer information finns i [förinstallerat innehåll](manage-network-bandwidth.md#BKMK_PrestagingContent).  

- En mottagar distributions plats använder inte scheman för schema eller hastighets gränser. När du konfigurerar en tidigare installerad distributions plats som en mottagar distributions plats sparas konfigurationer för schema-och hastighets begränsningar, men används inte. Om du senare tar bort konfigurationen av mottagar distributions platsen implementeras schema-och hastighets begränsnings konfigurationerna som tidigare konfigurerade.  

    > [!NOTE]  
    >  Flikarna **schema** och **hastighets begränsningar** visas inte i egenskaperna för distributions platsen.  

- Mottagar distributions platser använder inte inställningarna på fliken **Allmänt** i **komponent egenskaperna för program varu distribution** för varje plats. De här inställningarna omfattar **samtidig distribution** och **multicast-försök**.  

- Om du vill överföra innehåll från en käll distributions plats i en fjärran sluten skog installerar du Configuration Manager-klienten på mottagar distributions platsen. Konfigurera också ett konto för nätverks åtkomst som kan komma åt käll distributions platsen. Om du aktiverar alternativet plats för att **använda Configuration Manager-genererade certifikat för HTTP-plats system**behöver du inte något konto för nätverks åtkomst.<!--1358228-->  

- Om mottagar distributions platsen också är en Configuration Manager-klient, måste klient versionen vara samma som den Configuration Manager plats som installerar mottagar distributions platsen. Mottagar distributions platsen använder den CCMFramework som är gemensam för både mottagar distributions platsen och den Configuration Manager klienten.  

## <a name="about-source-distribution-points"></a>Om källdistributionsplatser  

När du konfigurerar mottagar distributions platsen anger du en eller flera käll distributions platser:  

- Guiden visar endast distributions platser som är kvalificerade för att vara käll distributions platser.  

- En mottagardistributionsplats kan anges som en källdistributionsplats för en annan mottagardistributionsplats.  

- Endast distributions platser som stöder HTTP kan anges som käll distributions platser när du använder Configuration Manager-konsolen.  

- Använd Configuration Manager SDK för att ange en käll distributions plats som är konfigurerad för HTTPS. Om du vill använda en käll distributions plats som är konfigurerad för HTTPS installerar du Configuration Manager-klienten på mottagar distributions platsen.  

- Om dina fjärranslutna kontor har en bättre anslutning till Internet, eller om du vill minska belastningen på WAN-länkarna, använder du en [moln distributions plats](use-a-cloud-based-distribution-point.md) i Microsoft Azure som källa. Mottagar distributions platsen måste ha Internet åtkomst för att kunna kommunicera med Microsoft Azure. Innehållet måste distribueras till käll moln distributions platsen.<!--1321554-->  

    > [!Note]  
    > Den här funktionen debiterar din Azure-prenumeration för data lagring och utgående nätverk. Mer information finns i [kostnaden för att använda en moln distributions plats](use-a-cloud-based-distribution-point.md#bkmk_cost).  

> [!Tip]  
> När en mottagardistributionsplats laddar ned innehåll från en källdistributionsplats räknas den mottagardistributionsplatsen som en klient i kolumnen **Använd klient (unik)** i rapporten **Användningsöversikt för distributionsplats** .  

### <a name="source-priorities"></a>Käll prioriteringar

- Tilldela en separat prioritet till varje käll distributions plats eller tilldela flera käll distributions platser till samma prioritet.  

- Prioriteten anger i vilken ordning som mottagar distributions platsen begär innehåll från sina käll distributions platser.  

- Mottagardistributionsplatser kontaktar först en källdistributionsplats med det lägsta värdet för prioritet. Om det finns flera käll distributions platser med samma prioritet väljer mottagar distributions platsen slumpmässigt en av källorna med den prioriteten.  

- Om innehållet inte är tillgängligt på en vald källa försöker mottagar distributions platsen Ladda ned innehållet från en annan distributions plats med samma prioritet.  

- Om ingen av distributions platserna med en viss prioritet har innehållet, försöker mottagar distributions platsen Ladda ned innehållet från en käll distributions plats med nästa prioritets nivå. Den här sökningen fortsätter tills innehållet har hittats.

- Om ingen av de tilldelade käll distributions platserna har innehållet väntar mottagar distributions platsen i 30 minuter och startar sedan processen igen.  

## <a name="inside-the-pull-distribution-point"></a>Inuti mottagar distributions platsen

- För att hantera överföringen av innehåll använder mottagar distributions platser **CCMFramework** -komponenten. Den Configuration Manager klienten innehåller den här komponenten.  

- När du aktiverar mottagar distributions platsen installerar platsen **pulldp. msi**. Den här installations programmet lägger också till CCMFramework-komponenten. Ramverket kräver inte Configuration Manager-klienten.  

- När mottagar distributions platsen har installerats använder den främst tjänsten **ccmexec** för att fungera.  

- När mottagar distributions platsen överför innehåll använder den **Background Intelligent Transfer Service** (bitar) som är inbyggd i Windows. En mottagar distributions plats kräver inte att du installerar BITS-tillägget för IIS-servern.<!--sms.503672 -Clarified BITS use-->

- För drift information, se följande loggfiler på mottagar distributions platsen:  

  - **DataTransferService.log**
  - **PullDP.log**

> [!TIP]
> Om du ser HTTP 403-fel i loggfilerna när du har lagt till en mottagar distributions plats, gör du följande ändring:
>
> 1. Ange följande register värde på käll distributions platsen:`HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL, ClientAuthTrustMode = 2 (REG_DWORD)`
> 1. Starta om käll distributions plats servern.
>
> Sedan ska mottagar distributions platsen börja hämta innehåll från källan. Mer information om den här register nyckeln finns i [Översikt över TLS-SSL (Schannel SSP)](https://docs.microsoft.com/windows-server/security/tls/what-s-new-in-tls-ssl-schannel-ssp-overview).<!-- SCCMDocs#1973 -->

## <a name="see-also"></a>Se även  

[Grundläggande begrepp för innehållshantering](fundamental-concepts-for-content-management.md)
