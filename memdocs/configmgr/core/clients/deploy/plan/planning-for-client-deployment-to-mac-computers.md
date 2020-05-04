---
title: Planera klient distribution till Mac-datorer
titleSuffix: Configuration Manager
description: Planera för klient distribution till Mac-datorer i Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f231e0681b2a202696b6c719966abf818a9c8e27
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713228"
---
# <a name="planning-for-client-deployment-to-mac-computers-in-configuration-manager"></a>Planera för klient distribution till Mac-datorer i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan installera Configuration Manager-klienten på Mac-datorer som kör operativ systemet Mac OS X och använda följande hanterings funktioner:  

- **Maskinvaruinventering**  

   Du kan använda Configuration Manager maskin varu inventering för att samla in information om maskin vara och installerade program på Mac-datorer. Den här informationen kan sedan visas i Resursläsaren i Configuration Manager-konsolen och användas för att skapa samlingar, frågor och rapporter. Mer information finns i [använda Resursläsaren för att Visa maskin varu inventering](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

   Configuration Manager samlar in följande maskin varu information från Mac-datorer:  

  -   Processor  

  -   Datorsystem  

  -   Disk enhet  

  -   Diskpartition  

  -   Nätverkskort  

  -   Operativsystem  

  -   Tjänst  

  -   Process  

  -   Installerad program vara  

  -   Dator System produkt  

  -   USB-styrenhet  

  -   USB-enhet  

  -   CDROM-enhet  

  -   Video styrenhet  

  -   Skriv bords skärm  

  -   Bärbart batteri  

  -   Fysiskt minne  

  -   Skrivare  

  > [!IMPORTANT]  
  >  Du kan inte utöka maskin varu informationen som samlas in från Mac-datorer under maskin varu inventeringen.  

- **Kompatibilitetsinställningar**  

   Du kan använda Configuration Manager kompatibilitetsinställningar för att visa efterlevnad av och reparera inställningarna för Mac OS X-inställningar (. plist). Du kan till exempel använda inställningar för start sidan i Safari-webbläsaren eller kontrol lera att Apple-brandväggen är aktive rad. Du kan också använda Shell-skript för att övervaka och åtgärda inställningarna i MAC OS X.  

- **Program hantering**  

   Configuration Manager kan distribuera program vara till Mac-datorer. Du kan distribuera följande program varu format till Mac-datorer:  

  -   Apple Disk Image (. DMG  

  -   Meta-paketfil (. MPKG)  

  -   Mac OS X Installer-paket (. FÖRP  

  -   Mac OS X-program (. MOBILAPPAR  

  När du installerar Configuration Manager-klienten på Mac-datorer kan du inte använda följande hanterings funktioner som stöds av Configuration Manager-klienten på Windows-baserade datorer:  

- Push-installation av klient  

- Distribution av operativsystem  

- Programuppdateringar  

  > [!NOTE]  
  >  Du kan använda Configuration Manager program hantering för att distribuera nödvändiga Mac OS X-program uppdateringar till Mac-datorer. Dessutom kan du använda kompatibilitetsinställningar för att kontrol lera att datorerna har nödvändiga program uppdateringar.  

- Underhållsfönster  

- Fjärrstyrning  

- Energisparfunktioner  

- Klientkontroll och reparation av klientstatus  

  Mer information om hur du installerar och konfigurerar Configuration Manager Mac-klienten finns i [Distribuera klienter till Mac-datorer](../../../../core/clients/deploy/deploy-clients-to-macs.md).
