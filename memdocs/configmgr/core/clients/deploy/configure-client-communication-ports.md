---
title: Konfigurera klient kommunikations portar
titleSuffix: Configuration Manager
description: Ange klient kommunikations portar i Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 406bbdbf-ab4a-4121-a68b-154f96ea14ec
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 30b553bbe2a68ec97e4d5200644a88d09ee5967d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713116"
---
# <a name="how-to-configure-client-communication-ports-in-configuration-manager"></a>Konfigurera klient kommunikations portar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan ändra de port nummer för begäran som Configuration Manager klienter använder för att kommunicera med plats system som använder HTTP och HTTPS för kommunikation. Även om det är mer troligt att HTTP eller HTTPS redan har kon figurer ATS för brand väggar, kräver klient meddelanden som använder HTTP eller HTTPS mer processor användning och minne på hanterings plats datorn än om du använder ett anpassat port nummer. Du kan också ange det plats port nummer som ska användas om du aktiverar klienter med traditionella aktiverings paket.  

 När du anger HTTP-och HTTPS-begäranden kan du ange både ett standard port nummer och ett alternativt port nummer. Klienterna försöker automatiskt med den alternativa porten när kommunikationen Miss lyckas med standard porten. Du kan ange inställningar för HTTP-och HTTPS-datakommunikation.  

 Standardvärdena för klient begär ande portar är **80** för HTTP-trafik och **443** för HTTPS-trafik. Ändra dem endast om du inte vill använda dessa standardvärden. Ett typiskt scenario för att använda anpassade portar är när du använder en anpassad webbplats i IIS i stället för standard webbplatsen. Om du ändrar standard port numren för standard webbplatsen i IIS och andra program också använder standard webbplatsen, kommer de sannolikt att sluta fungera.  

> [!IMPORTANT]
>  Ändra inte port numren i Configuration Manager utan att förstå konsekvenserna. Exempel:  
> 
> - Om du ändrar port numren för klient begär ande tjänster som plats konfiguration och befintliga klienter inte konfigureras om för att använda de nya port numren, kommer dessa klienter att bli ohanterade.  
>   -   Innan du konfigurerar ett port nummer som inte är standard kontrollerar du att brand väggar och alla mellanliggande nätverks enheter har stöd för den här konfigurationen och konfigurerar om dem efter behov. Om du ska hantera klienter på Internet och ändra standard-HTTPS-portnumret på 443 kan routrar och brand väggar på Internet blockera den här kommunikationen.  

 För att se till att klienterna inte blir ohanterade när du har ändrat port numren för begäran måste klienterna konfigureras för att använda de nya port numren för begäran. När du ändrar begär ande portar på en primär plats ärver alla anslutna sekundära platser automatiskt samma port konfiguration. Använd proceduren i det här avsnittet för att konfigurera begär ande portar på den primära platsen.  

> [!NOTE]  
>  Information om hur du konfigurerar begär ande portar för klienter på datorer som kör Linux och UNIX finns i [Konfigurera begär ande portar för klienten för Linux och UNIX](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigLnUClientCommuincations).  

 När Configuration Manager webbplatsen publiceras till Active Directory Domain Services konfigureras nya och befintliga klienter som kan komma åt den här informationen automatiskt med plats port inställningarna och du behöver inte vidta ytterligare åtgärder. Klienter som inte har åtkomst till den här informationen som publiceras till Active Directory Domain Services omfatta arbets grupps klienter, klienter från en annan Active Directory skog, klienter som är konfigurerade för enbart Internet och klienter som för närvarande är anslutna till Internet. Om du ändrar standard port numren efter att de här klienterna har installerats, installerar du om dem och installerar nya klienter med någon av följande metoder:  

- Installera om klienterna med hjälp av guiden för push-installation av klienter. Push-installation av klienter konfigurerar automatiskt klienter med den aktuella plats port konfigurationen. Mer information om hur du använder guiden push-installation av klient finns i [så här installerar du Configuration Manager-klienter med push](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)-installation av klienter.  

- Installera om klienterna med hjälp av CCMSetup. exe och installations egenskaperna för Client. msi för CCMHTTPPORT och CCMHTTPSPORT. Mer information om dessa egenskaper finns i [om klient installations egenskaper](../../../core/clients/deploy/about-client-installation-properties.md).  

- Installera om klienterna med hjälp av en metod som söker Active Directory Domain Services efter Configuration Manager klient installations egenskaper. Mer information finns i [om klient installations egenskaper som publicerats till Active Directory Domain Services](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

  Om du vill konfigurera om Port numren för befintliga klienter kan du även använda skriptet PORTSWITCH. VBS som medföljer installations mediet i mappen SMSSETUP\Tools\PortConfiguration  

> [!IMPORTANT]  
>  För befintliga och nya klienter som för närvarande är anslutna till Internet, måste du konfigurera port nummer som inte är standard med hjälp av egenskaperna CCMSetup. exe client. msi för CCMHTTPPORT och CCMHTTPSPORT.  

 När du har ändrat portarna för begäran på platsen konfigureras nya klienter som installeras med hjälp av metoden för push-installation av hela platsen automatiskt med platsens aktuella port nummer.  

#### <a name="to-configure-the-client-communication-port-numbers-for-a-site"></a>Konfigurera port nummer för klient kommunikation för en plats  

1. Klicka på **Administration**i Configuration Manager-konsolen.  

2. I arbets ytan **Administration** expanderar du **plats konfiguration**, klickar på **platser**och väljer den primära plats som ska konfigureras.  

3. På fliken **Start** klickar du på **Egenskaper**och sedan på fliken **portar** .  

4. Välj något av objekten och klicka på ikonen Egenskaper för att Visa dialog rutan **port information** .  

5. I dialog rutan **port information** anger du Port numret och beskrivningen för objektet och klickar sedan på **OK**.  

6. Välj **Använd anpassad webbplats** om du vill använda det anpassade webbplats namnet för **SMSWEB** för plats system som kör IIS.  

7. Klicka på **OK** för att stänga egenskapsdialogrutan för platsen.  

   Upprepa den här proceduren för alla primära platser i hierarkin.
