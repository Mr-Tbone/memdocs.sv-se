---
title: Webbplatser för plats system
titleSuffix: Configuration Manager
description: Lär dig om standard webbplatser och anpassade webbplatser för plats system servrar i Configuration Manager.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 344ba7f6a6b0ee7683c3ac7661338f01be601a10
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718695"
---
# <a name="websites-for-site-system-servers-in-configuration-manager"></a>Webbplatser för plats system servrar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Flera Configuration Manager plats system roller kräver att Microsoft Internet Information Services (IIS) används och att standard webbplatsen för IIS används som värd för plats system tjänster. Om du måste köra andra webb program på samma server och inställningarna inte är kompatibla med Configuration Manager bör du överväga att använda en anpassad webbplats för Configuration Manager.  

> [!TIP]  
>  En säkerhets metod är att dedikera en server för de Configuration Manager plats system som kräver IIS. När du kör andra program på ett Configuration Manager-plats system ökar du datorns attack yta.  




##  <a name="what-to-know-before-choosing-to-use-custom-websites"></a><a name="BKMK_What2Know"></a>Vad du behöver veta innan du väljer att använda anpassade webbplatser  
 Som standard använder platssystemroller **standardwebbplatsen** i IIS. Detta konfigureras automatiskt när plats system rollen installeras. På primära platser kan du dock välja att använda anpassade webbplatser i stället. När du använder anpassade webbplatser:  

-   Anpassade webbplatser har Aktiver ATS för hela platsen i stället för enskilda plats system servrar eller roller.  

-   På primära platser måste varje dator som är värd för en tillämplig plats system roll konfigureras med en anpassad webbplats med namnet **SMSWEB**. Innan du skapar den här webbplatsen och konfigurerat plats system roller på den datorn för att använda den anpassade webbplatsen, kan det hända att klienterna inte kan kommunicera med plats system roller på den datorn.  

-   Eftersom sekundära platser konfigureras automatiskt så att de använder en anpassad webbplats när den primära överordnade platsen har kon figurer ATS att göra det, måste du också skapa anpassade webbplatser i IIS på varje sekundär plats system server som kräver IIS.  


  **Förutsättningar för att använda anpassade webbplatser:**  

 Innan du aktiverar alternativet att använda anpassade webbplatser på en plats måste du:  

-   Skapa en anpassad webbplats med namnet **SMSWEB** i IIS på varje platssystemserver som kräver IIS. Gör detta på den primära platsen och på alla underordnade sekundära platser.  

-   Konfigurera den anpassade webbplatsen att svara på samma port som du konfigurerade för Configuration Manager klient kommunikation (klient begär ande port).  

-   För varje anpassad eller standard webbplats som använder en anpassad mapp placerar du en kopia av den standard dokument typ som du använder i rotmappen som är värd för webbplatsen. Till exempel, på en Windows Server 2008 R2-dator med standardkonfigurationer, är **iisstart. htm** en av flera standard dokument typer som är tillgängliga. Du kan hitta filen i roten på standard webbplatsen och sedan placera en kopia av den här filen (eller en kopia av den standard dokument typ som du använder) i rotmappen som är värd för den anpassade webbplatsen för SMSWEB. Mer information om standard dokument typer finns i [standard dokument &lt;defaultDocument\> för IIS](https://www.iis.net/configreference/system.webserver/defaultdocument).  

**Om IIS-krav:**
**följande plats system roller kräver att IIS och en webbplats är värd för plats system tjänsterna:**  

-   Webbservicepunkt för programkatalog  

-   Webbplats för programkatalog  

-   Distributionsplats  

-   Registreringsplats  

-   Registreringsproxyplats  

-   Status för återställningsplats  

-   Hanteringsplats  

-   Programuppdateringsplats  

-   Plats för tillståndsmigrering  

Fler saker att ha i åtanke:  

-   När anpassade webbplatser har Aktiver ATS för en primär plats dirigeras klienter som är tilldelade till platsen att kommunicera med anpassade webbplatser i stället för standard webbplatser på tillämpliga plats system servrar  

-   Om du använder anpassade webbplatser för en primär plats bör du överväga anpassade webbplatser för alla primära platser i hierarkin för att se till att klienterna kan fungera i hierarkin. (Växling är när en klientdator flyttas till ett nytt nätverkssegment som hanteras av en annan plats. Nätverks växling kan påverka resurser som en klient har åtkomst till lokalt i stället för via en WAN-länk).  

-   Plats system roller som använder IIS men inte accepterar klient anslutningar, t. ex. repor ting Services-platsen, använder också SMSWEB-webbplatsen i stället för standard webbplatsen.  

-   Anpassade webbplatser kräver att du tilldelar port nummer som skiljer sig från de som datorns standard webbplats använder. En standardwebbplats och en anpassad webbplats kan inte köras samtidigt om båda platserna försöker använda samma TCP/IP-portar.  

-   De TCP/IP-portar som du konfigurerar i IIS för den anpassade webbplatsen måste matcha klient begär ande portarna för platsen.  

## <a name="switch-between-default-and-custom-websites"></a>Växla mellan standard webbplatser och anpassade webbplatser  
Även om du kan markera eller avmarkera kryss rutan för att använda anpassade webbplatser på en primär plats när som helst (rutan finns på fliken Allmänt i platsens egenskaper) bör du planera noggrant innan du gör den här ändringen. När den här konfigurationen ändras måste alla tillämpliga plats system roller på den primära platsen och underordnade sekundära platser avinstalleras och sedan installeras om:  

Följande roller **ominstalleras automatiskt**:  

-   Hanteringsplats  

-   Distributionsplats  

-   Programuppdateringsplats  

-   Status för återställningsplats  

-   Plats för tillståndsmigrering  

Följande roller måste **ominstalleras manuellt**:  

-   Webbservicepunkt för programkatalog  

-   Webbplats för programkatalog  

-   Registreringsplats  

-   Registreringsproxyplats  

Dessutom:  

-   När du byter från standard webbplatsen till att använda en anpassad webbplats tar Configuration Manager inte bort de gamla virtuella katalogerna. Om du vill ta bort filerna som Configuration Manager använt måste du manuellt ta bort de virtuella katalogerna som skapades under standard webbplatsen.  

-   Om du ändrar platsen för att använda anpassade webbplatser måste klienter som redan har tilldelats till platsen konfigureras om så att de använder de nya portarna för klient förfrågningar för de anpassade webbplatserna. Se [så här konfigurerar du klient kommunikations portar](../../../core/clients/deploy/configure-client-communication-ports.md).  

## <a name="set-up-custom-websites"></a>Konfigurera anpassade webbplatser  
Stegen för att skapa en anpassad webbplats varierar beroende på operativsystemversion. Läs därför dokumentationen för din version av operativsystemet för de specifika stegen, men använd följande information när så är tillämpligt:  

-   Webbplats namnet måste vara: **SMSWEB**.  

-   När du konfigurerar HTTPS måste du ange ett SSL-certifikat innan du kan spara konfigurationen.  

-   När du har skapat den anpassade webbplatsen tar du bort portarna för den anpassade webbplatsen som du använder från andra webbplatser i IIS:  

    1.  Redigera **bindningarna** för de andra webbplatserna för att ta bort portar som matchar de som har tilldelats **SMSWEB** -webbplatsen.  

    2.  Starta **SMSWEB** -webbplatsen.  

    3.  Starta om tjänsten **SMS_SITE_COMPONENT_MANAGER** på platsens platsserver.  
