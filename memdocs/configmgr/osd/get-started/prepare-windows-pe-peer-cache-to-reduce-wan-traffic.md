---
title: Förbereda peer-cache i Windows PE för att minska WAN-trafiken
titleSuffix: Configuration Manager
description: Peer-cache i Windows PE fungerar i Windows PE för att hämta innehåll från en lokal peer och minimera WAN-trafik när det inte finns någon lokal distributions plats.
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 6c64f276-b88c-4b1e-8073-331876a03038
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fd622c1a54c1dd3cd3b5071cc62d1b6860a118e3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724043"
---
# <a name="prepare-windows-pe-peer-cache-to-reduce-wan-traffic-in-configuration-manager"></a>Förbered peer-cache i Windows PE för att minska WAN-trafiken i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du distribuerar ett nytt operativ system i Configuration Manager kan datorer som kör aktivitetssekvensen använda peer-cache i Windows PE för att hämta innehåll från en lokal peer (en peer-cache-källa) i stället för att hämta innehåll från en distributions plats. Detta hjälper till att minimera WAN-trafik i filialscenarier där det inte finns någon lokal distributionsplats.  

 Peer-cache i Windows PE liknar [Windows BranchCache](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache), men fungerar i Windows Preinstallation Environment (Windows PE). Följande villkor används för att beskriva klienter som använder peer-cache i Windows PE:  

-   Ett **peer-cacheklient** är en dator som är konfigurerad för att använda Windows PE Peer-cache.  

-   A **peer-cachekälla** är en klient som är konfigurerad för peer-cache och som gör innehåll tillgängligt för andra peer-cacheklienter som begär innehållet.  

Använd följande avsnitt för att hantera peer-cache.

##  <a name="objects-stored-on-a-peer-cache-source"></a><a name="BKMK_PeerCacheObjects"></a>Objekt som är lagrade i en peer-cache-källa  
 En aktivitetssekvens som har konfigurerats för att använda peer-cache i Windows PE kan hämta följande innehållsobjekt när det körs i Windows PE:  

- Operativsystemavbildning  

- Drivrutinspaket  

- Paket och program (när klienten fortsätter att köra aktivitetssekvensen i det fullständiga operativ systemet hämtar klienten det här innehållet från en peer-cache-källa om aktivitetssekvensen ursprungligen konfigurerades för peer-cache vid körning i Windows PE.)  

- Ytterligare startavbildningar  

  Följande innehållsobjekt överförs aldrig med peer-cache. De överförs i stället från en distributionsplats eller via Windows BranchCache om du har konfigurerat Windows BranchCache i din miljö:  

- Program  

- Programuppdateringar  

##  <a name="how-does--windows-pe-peer-cache-work"></a><a name="BKMK_PeerCacheWork"></a>Hur fungerar peer-cache i Windows PE?  
 Tänk dig ett scenario med en filial som inte har en distributionsplats, men som har flera klienter som kan använda peer-cache i Windows PE. Du distribuerar aktivitetssekvensen som konfigurerats för att använda peer-cache på flera klienter som är konfigurerade för att vara en del av peer-cachekällan. Den första klienten som ska köra aktivitetssekvensen skickar en begäran om en peer med innehållet. Om det inte går att hitta någon hämtas innehållet från en distributionsplats via WAN. Klienten installerar den nya avbildningen och lagrar sedan innehållet i sin Configuration Manager klientcachen så att den kan fungera som en peer-cache-källa till andra klienter. När nästa klient kör aktivitetssekvensen skickar den en förfrågan på undernätet efter en peer-cachekälla, och den första klienten svarar och gör det cachelagrade innehållet tillgängligt.  

##  <a name="determine-what--clients-will-be-part-of-the-windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheDetermine"></a>Ta reda på vilka klienter som ska ingå i Windows PE peer cache-källan  
 När du ska avgöra vilka datorer du ska välja som peer-cachekälla i Windows PE finns det flera saker du bör tänka på:  

-   Peer-cachekällan i Windows PE bör vara en stationär dator som alltid är påslagen och tillgänglig för peer-cacheklienter.  

-   Peer-cache i Windows PE har en klientcachestorlek som räcker för att lagra avbildningarna.  

##  <a name="requirements-for-a-client-to-use-a--windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheRequirements"></a>Krav för en klient för användning av en peer-cache-källa i Windows PE  
 Klienter som ska använda en peer-cachekälla i Windows PE måste uppfylla följande krav:  

-   Den Configuration Manager klienten måste kunna kommunicera via följande portar i nätverket:  

    -   Porten för den första nätverkssändningen för att hitta en peer-cachekälla: Som standard är detta UDP-port 8004.  

    -   Port för att ladda ned innehåll från en peer-cache-källa (HTTP och HTTPS). Som standard är detta TCP-port 8003.  
    
        Mer information finns i [portar som används för anslutningar](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp).  

        > [!TIP]  
        >  Klienterna använder HTTPS för att ladda ned innehåll när det är tillgängligt. Samma portnummer används dock antingen för HTTP eller HTTPS.  

-   [Konfigurera klientcacheminnet för Configuration Manager-klienter](../../core/clients/manage/manage-clients.md#BKMK_ClientCache) på klienter för att se till att de har tillräckligt med utrymme för att hålla och lagra de avbildningar som du distribuerar. Peer-cache i Windows PE påverkar inte konfigurationen eller beteendet för klientens cacheminne.  

-   Distributionsalternativen för aktivitetssekvensdistributioner måste konfigureras för att ladda ned innehåll lokalt när aktivitetssekvensen behöver detta.  

##  <a name="configure-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigure"></a>Konfigurera peer-cache i Windows PE  
 Du kan använda följande metoder för att etablera en klient med peer-cacheinnehåll, så att den kan fungera som en peer-cachekälla:  

- En peer-cach-klient som inte kan hitta en peer-cachekälla med innehållet hämtar det från en distributionsplats.  Om klienten får klientinställningar som möjliggör peer-cache och aktivitetssekvensen är konfigurerad för att bevara cachelagrat innehåll, blir klienten en peer-cachekälla.  

- En peer-cache-klient kan hämta innehåll från en annan peer cache-klient (en peer-cache-källa).  Eftersom klienten har konfigurerats för peer-cache blir den en peer-cachekälla när den kör den aktivitetssekvens som har konfigurerats för att bevara det cachelagrade innehållet.  

- En klient kör en aktivitetssekvens med det valfria steget [Hämta paketinnehåll](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent), som används för att förbereda relevant innehåll som ingår i aktivitetssekvensen för peer-cache i Windows PE. När du använder den här metoden gäller följande:  

  -   Klienten behöver inte installera den avbildning som distribueras.  

  -   Förutom alternativet **Hämta paketinnehåll** måste aktivitetssekvensen även använda alternativet **Cache för Configuration Manager-klienten** . Du använder det här kommandot för att lagra innehållet i klientens cacheminne, så att klienten kan fungera som peer-cachekälla för andra peer-cacheklienter.  

  Följande procedurer hjälper dig att konfigurera peer-cache i Windows PE på klienter och konfigurera aktivitetssekvenser som stöder peer-cache.  

### <a name="to-configure-the-windows-pe-peer-cache-source-computers"></a>Konfigurera källdatorer för peer-cache i Windows PE  

1. I Configuration Manager-konsolen går du till **Administration** > **klient inställningar**och skapar sedan en ny **anpassad klienten hets inställningar** eller redigerar ett befintligt inställnings objekt. Du kan också konfigurera detta för objektet **Inställningar för standardklient** .  

   > [!TIP]  
   >  Använd ett objekt för anpassade inställningar för att hantera vilka klienter som får den här konfigurationen. Du kanske t.ex. inte vill konfigurera det här på bärbara datorer, med användare som ofta är på språng. Ett höggradigt mobilt system kan vara en dålig källa för att tillhandahålla innehåll till andra peer-cacheklienter.  
   >   
   >  Kom också ihåg att när du konfigurerar den här inställningen som en del av **Inställningar för standardklient**gäller konfigurationen för alla klienter i din miljö.  

2. Under **Inställningar för klient-cache**anger du **aktivera Configuration Manager-klienten i fullständigt operativ system för att dela innehåll** till **Ja**.  

   -   Som standard är endast HTTP aktiverat. Om du vill att klienter ska kunna ladda ned innehåll över HTTPS anger du **Aktivera HTTPS för klient-peer-kommunikation** till **Ja**.  

   -   Som standard är porten för sändning inställd till 8004 och porten för nedladdning av innehåll till 8003. Du kan ändra båda.  

3. Spara och distribuera klientinställningar för klienter som du väljer som peer-cachekälla.  

   När en enhet har konfigurerats med det här inställningsobjektet är enheten konfigurerad för att fungera som en peer-cachekälla. De här inställningarna ska distribueras till potentiella peer-cacheklienter för att konfigurera de portar och protokoll som krävs.  

###  <a name="configure-a-task-sequence-for-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigureTS"></a> Konfigurera en aktivitetssekvens för peer-cache i Windows PE  
 När du konfigurerar aktivitetssekvensen använder du följande aktivitetssekvensvariabler som samlingsvariabler i den samling där aktivitetssekvensen distribueras:  

- **SMSTSPeerDownload**  

   Värde: TRUE  

   Detta gör att klienten kan använda peer-cache i Windows PE.  

- **SMSTSPeerRequestPort**  

   Värde: <port nummer\>  

   När du inte använder standard porten som kon figurer ATS i klient inställningarna (8004) måste du konfigurera den här variabeln med ett anpassat värde för den nätverks port som ska användas för den första sändningen.  

- **SMSTSPreserveContent**  

   Värde: TRUE  

   Detta flaggar att innehållet i aktivitetssekvensen ska behållas i Configuration Manager-klientcachen efter distributionen. Detta skiljer sig från att använda SMSTSPersisContent, som endast bevarar innehållet under aktivitetssekvensen och använder cachen för aktivitetssekvensen, inte Configuration Manager-klientcachen.  

  Mer information finns i [variabler för aktivitetssekvens](../understand/task-sequence-variables.md).  

###  <a name="validate-the-success-of-using-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheValidate"></a>Verifiera att det går att använda peer-cache i Windows PE  
 När du använder peer-cache i Windows PE för att distribuera och installera en aktivitetssekvens kan du bekräfta att processen använt peer-cachen genom att visa **smsts.log** på den klient som körde aktivitetssekvensen.  

 Leta upp en post som liknar följande i loggen, där <*SourceServerName*> identifierar den dator som klienten hämtade innehållet från. Den här datorn ska vara en peer-cachekälla, inte en distributionsplatsserver. Övriga detaljer varierar beroende på lokal miljö och konfiguration.  

-   *<! [LOG [Downloaded File from http://<\>SourceServerName: 8003/SCCM_BranchCache $/SS10000C/SCCM?/install.wim till C\\: _SMSTaskSequence \packages\ss10000c\install.wim] log]! ><tid = "14:24:33.329 + 420" date = "06-26-2015" Component = "ApplyOperatingSystem" context = "" Type = "1" Thread = "1256" File = "downloadcontent. cpp: 1626" >*  
