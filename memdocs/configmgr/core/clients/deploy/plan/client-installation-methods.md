---
title: Installationsmetoder för klient
titleSuffix: Configuration Manager
description: Lär dig mer om metoderna för att installera Configuration Manager-klienten.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d5f238ddb0e2c28a51cdad8dc7347f872227535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713312"
---
# <a name="client-installation-methods-in-configuration-manager"></a>Klient installations metoder i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan använda olika metoder för att installera Configuration Manager-klient program varan. Använd en metod eller en kombination av metoder. I den här artikeln beskrivs varje metod så att du kan lära dig vilken som passar bäst för din organisation.  

## <a name="client-push-installation"></a>Push-installation av klient  

**Klient plattform som stöds**: Windows  

#### <a name="advantages"></a>Fördelar  

-   Kan användas för att installera klienten på en enstaka dator, en samling datorer eller resultaten av en fråga.  

-   Kan användas för att automatiskt installera klienten på alla identifierade datorer.  

-   Använder automatiskt de klientinstallationsegenskaper som definierats på fliken **Klient** i dialogrutan **Egenskaper för push-installation av klient**.  

#### <a name="disadvantages"></a>Nackdelar  

-   Kan orsaka hög belastning på nätverket vid push-installation till stora samlingar.  

-   Kan endast användas på datorer som har identifierats av Configuration Manager.  

-   Kan inte användas för att installera klienter i en arbets grupp.  

-   Ett konto för push-installation av klienter måste anges som har administratörsbehörighet till den avsedda klientdatorn.  

-   Windows-brandväggen måste konfigureras med undantag på klient datorer.   

-   Du kan inte avbryta push-installation av klienter. Configuration Manager försöker installera klienten på alla identifierade resurser. Det försöker igen om eventuella problem i upp till sju dagar.  

Mer information finns i [så här installerar du klienter med klient-push](../deploy-clients-to-windows-computers.md#BKMK_ClientPush).  



## <a name="software-update-point-based-installation"></a>Platsbaserad klientinstallation av programuppdateringar  

**Klient plattform som stöds**: Windows  

#### <a name="advantages"></a>Fördelar  

-   Kan använda din befintliga infrastruktur för programuppdateringar för att hantera klientprogramvaran.  

-   Om Windows Server Update Services (WSUS) och grup princip inställningar i Active Directory Domain Services har kon figurer ATS korrekt, kan klient program varan installeras automatiskt på nya datorer.  

-   Kräver inte att datorer identifieras innan klienten kan installeras.  

-   Datorer kan läsa klientinstallationsegenskaper som har publicerats på Active Directory Domain Services.  

-   Om klienten tas bort installerar den här metoden om den.  

-   Kräver inte att du konfigurerar och underhåller ett installations konto för den avsedda klient datorn.  

#### <a name="disadvantages"></a>Nackdelar  

-   Kräver en fungerade infrastruktur för programuppdatering som förutsättning.  

-   Måste använda samma server för klient installation och program uppdateringar. Den här servern måste finnas på en primär plats.  

-   Om du vill installera nya klienter måste du konfigurera ett grup princip objekt i Active Directory Domain Services med klientens aktiva program uppdaterings plats och port.  

-   Om Active Directory-schemat inte är utökat för Configuration Manager måste du använda grup princip inställningar för att etablera datorer med klient installations egenskaper.  

Mer information finns i [så här installerar du klienter med installation baserad på program uppdatering](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  



## <a name="group-policy-installation"></a>Grupprincipinstallation  

**Klient plattform som stöds**: Windows  

#### <a name="advantages"></a>Fördelar  

-   Kräver inte att datorer identifieras innan klienten kan installeras.  

-   Kan användas för nya klientinstallationer eller för uppgraderingar.  

-   Datorer kan läsa klientinstallationsegenskaper som har publicerats på Active Directory Domain Services.  

-   Kräver inte att du konfigurerar och underhåller ett installations konto för den avsedda klient datorn.  

#### <a name="disadvantages"></a>Nackdelar  

-   Om ett stort antal klienter installeras kan det orsaka hög nätverks trafik.  

-   Om Active Directory-schemat inte är utökat för Configuration Manager måste du använda grup princip inställningar för att lägga till klient installations egenskaper på datorerna på din plats.  

Mer information finns i [så här installerar du klienter med grup principer](../deploy-clients-to-windows-computers.md#BKMK_ClientGP).  



## <a name="logon-script-installation"></a>Installation av inloggningsskript  

**Klient plattform som stöds**: Windows  

#### <a name="advantages"></a>Fördelar  

-   Kräver inte att datorer identifieras innan klienten kan installeras.  

-   Har stöd för kommandoradsegenskaper för CCMSetup.  

#### <a name="disadvantages"></a>Nackdelar  

-   Om ett stort antal klienter installeras under en kort tids period kan det orsaka hög nätverks trafik.  

-   Om användarna inte ofta loggar in på nätverket kan det ta lång tid att installera på alla klient datorer.  

Mer information finns i [så här installerar du klienter med inloggnings skript](../deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  



## <a name="manual-installation"></a>Manuell installation  

**Klient plattform som stöds**: Windows, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Fördelar  

-   Kräver inte att datorer identifieras innan klienten kan installeras.  

-   Kan vara användbart för testning.  

-   Har stöd för kommandoradsegenskaper för CCMSetup.  

#### <a name="disadvantages"></a>Nackdelar  

-   Ingen automatisering och är därför tidskrävande.  

Mer information om hur du installerar klienten manuellt på varje plattform finns i följande artiklar:  

-   [Distribuera klienter på Windows-datorer](../deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [Distribuera klienter till UNIX- och Linux-servrar](../deploy-clients-to-unix-and-linux-servers.md)  

-   [Distribuera klienter på Mac-datorer](../deploy-clients-to-macs.md)  



## <a name="microsoft-intune-mdm-installation"></a>Microsoft Intune MDM-installation

**Klient plattformar som stöds**: Windows 10

#### <a name="advantages"></a>Fördelar  

-   Kräver inte att datorer identifieras innan klienten kan installeras.  

-   Kräver inte att du konfigurerar och underhåller ett installations konto för den avsedda klient datorn.  

-   Kan använda modern autentisering med Azure Active Directory.  

-   Kan installera och tilldela datorer på Internet.  

-   Kan automatiseras med Windows autopilot och Microsoft Intune för samhantering.  

#### <a name="disadvantages"></a>Nackdelar  

-   Kräver ytterligare tekniker utanför Configuration Manager.  

-   Kräver att enheten har åtkomst till Internet, även om den inte är Internet-baserad.  

Mer information finns i följande artiklar:  

-   [Så här installerar du klienter på Intune MDM-hanterade Windows-enheter](../deploy-clients-to-windows-computers.md#bkmk_mdm)  

-   [Installera och tilldela Configuration Manager Windows 10-klienter med Azure AD för autentisering](../deploy-clients-cmg-azure.md)  

