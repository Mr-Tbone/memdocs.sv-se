---
title: Funktioner i Technical Preview 1603
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1603.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f861b72-9f14-4d17-a512-4a79b660abe6
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 73e3e19df4ce545e4cbb36109da2710e848f1159
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076228"
---
# <a name="capabilities-in-technical-preview-1603-for-configuration-manager"></a>Funktioner i Technical Preview 1603 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1603. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. Alternativt, när du använder System Center Technical Preview 5, installeras den här versionen som en bas linje version av Configuration Manager Technical Preview. Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.  

 **Kända problem för den här tekniska för hands versionen:**  

- I den här versionen ingår uppdateringar för tidigare publicerade funktioner, men nya funktioner införs inte. Därför kommer sidan funktioner i uppdaterings guiden att vara tom om du tidigare har uppgraderat till 1602 och aktiverat alla funktioner som ingår i 1602.  

- Efter att plats servern har uppdaterats till Technical Preview 1603 kan klienterna inte använda några fjärr styrnings funktioner förrän de också uppdaterar till version 1603.  

  **Följande är nya funktioner som du kan prova med den här versionen.**  

##  <a name="improvements-to-software-center"></a><a name="BKMK_SC1603"></a>Förbättringar av Software Center  

### <a name="new-tiled-view-for-apps"></a>Ny sida i vyn för appar  
 Slutanvändare kan nu välja mellan en lista över appar eller en sida vid sida med appar på fliken **program** i Software Center.  

### <a name="select-multiple-updates-in-software-center"></a>Välj flera uppdateringar i Software Center  
 På fliken **uppdateringar** i Software Center kan du nu välja flera uppdateringar eller välja **Uppdatera alla** för att börja installera flera uppdateringar samtidigt.  

##  <a name="improvements-to-remote-control"></a><a name="BKMK_RC1603"></a>Förbättringar av fjärr styrning  

### <a name="limit-shared-clipboard-access-in-a-remote-control-session"></a>Begränsa delad urklipps åtkomst i en fjärrstyrningssession  
 Nu kan du aktivera den nya klient inställningen **uppmana användaren att ange behörighet för fil överföring i delat Urklipp** för att begränsa åtkomsten till det delade Urklippet i en fjärrstyrningssession.  

 När det här alternativet är aktiverat måste slutanvändaren som delar en fjärrsession ge behörighet till Viewer för den sessionen innan visnings programmet kan överföra filer från sessionen till den lokala datorn via det delade Urklippet.  

 Detta lägger till ett skydds lager för slutanvändaren som tidigare, om visnings programmet har beviljats fullständig kontroll över slutanvändarens dator, skulle de kunna använda det delade Urklippet för att överföra filer från sessionen till den lokala datorn på ett sätt som var helt transparent för slutanvändaren.  

##  <a name="customize-the-ramdisk-tftp-block-size-and-window-size-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a>Anpassa storleken på RamDisk TFTP-blocket och fönster storleken på PXE-aktiverade distributions platser  
 I 1603 Technical Preview kan du anpassa storleken på RamDisk TFTP-blocket och fönster storleken för PXE-aktiverade distributions platser. Om du har anpassat nätverket kan det orsaka att hämtningen av startavbildningen inte lyckas och att ett timeout-fel uppstår eftersom blockstorleken eller fönsterstorleken är för stor. Tack vare att du kan anpassa RamDisk TFTP-blockstorleken och fönsterstorleken kan du optimera TFTP-trafik när du använder PXE för att uppfylla dina specifika krav.   
Du behöver testa de anpassade inställningarna i din miljö för att avgöra vad som fungerar bäst.  

-   **TFTP-blockstorlek**: Blockstorleken är storleken på de datapaket som skickas från servern till klienten som hämtar filen (som beskrivs i RFC 2347). En större blockstorlek gör att servern kan skicka färre paket, så det finns färre fram-och-åter-förseningar mellan servern och klienten. Större blockstorlekar leder dock till fragmenterade paket som de flesta implementeringar av PXE-klienten inte har stöd för.  

-   **TFTP-fönsterstorlek**: TFTP kräver ett bekräftelsepaket (ACK) för varje datablock som skickas. Servern skickar inte nästa block i ordningsföljden förrän den tagit emot ACK-paketet för föregående block. I Windows Deployment Services finns en funktion för hantering av TFTP-fönster som gör att du kan ange hur många datablock som ska fylla ett fönster. Servern skickar datablock tills fönstret fylls och sedan skickar klienten ett ACK-paket. Om fönstret görs större minskar antalet fram-och-åter-förseningar mellan klienten och servern och den totala tiden som krävs för att hämta en startavbildning minskar.  

### <a name="try-it-out"></a>prova!  
 Försök att utföra följande uppgifter och Använd sedan feedback-informationen nära överst i det här avsnittet för att berätta för oss hur det fungerade:  

-   Jag kan anpassa RamDisk TFTP-fönstrets storlek på den PXE-aktiverade distributions platsen.  

-   Jag kan anpassa RamDisk TFTP-block storleken på den PXE-aktiverade distributions platsen.  

### <a name="to-modify-the-ramdisk-tftp-window-size"></a>Ändra storlek på RamDisk TFTP-fönstret  

- Lägg till följande registernyckel på PXE-aktiverade distributionsplatser för att anpassa RamDisk TFTP-fönsterstorleken:  

   **Plats**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  Namn: RamDiskTFTPWindowSize  

   **Typ**: REG_DWORD  

   **Värde**: &lt;anpassad fönster storlek\>  

  Standardvärdet är 1 (ett datablock fyller fönstret)  

### <a name="to-modify-the-ramdisk-tftp-block-size"></a>Ändra storlek på RamDisk TFTP-block  

- Lägg till följande registernyckel på PXE-aktiverade distributionsplatser för att anpassa RamDisk TFTP-fönsterstorleken:  

   **Plats**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  Namn: RamDiskTFTPBlockSize  

   **Typ**: REG_DWORD  

   **Värde**: &lt;anpassad block storlek\>  

  Standardvärdet är 4096 (4k).  
