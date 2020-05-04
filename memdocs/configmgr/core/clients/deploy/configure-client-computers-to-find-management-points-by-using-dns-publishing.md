---
title: Konfigurera klienter för att använda DNS-publicering
titleSuffix: Configuration Manager
description: Konfigurera Configuration Manager klient datorer för att hitta hanterings platser med hjälp av DNS-publicering.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d28a8a35f711dcef7e3f9adb6dccbabc4082ab28
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713102"
---
# <a name="configure-client-computers-to-find-management-points-by-using-dns-publishing"></a>Konfigurera klient datorer för att hitta hanterings platser med DNS-publicering

*Gäller för: Configuration Manager (aktuell gren)*

Klienter i Configuration Manager måste hitta en hanterings plats för att slutföra platstilldelning och som en pågående process för fortsatt hantering. Active Directory Domain Services är den säkraste metoden för klienter i intranätet att hitta hanteringsplatser. Om klienterna dock inte kan använda den här metoden för att hitta tjänster (om du till exempel inte har utökat Active Directory-schemat eller om klienterna kommer från en arbetsgrupp), använd DNS publicering som föredragen alternativ metod för att hitta platsen för en tjänst.  

> [!NOTE]  
>  När du installerar klienten för Linux och UNIX måste du specificera en hanteringsplats att använda som inledande kontaktpunkt. Information om hur du installerar-klienten för Linux och UNIX finns i [Distribuera klienter till UNIX-och Linux-servrar](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

 Innan du använder DNS-publicering för hanteringsplatser, kontrollera att DNS-servrarna på intranätet har resursposter för att hitta tjänster (SRV RR) och motsvarande värds (A eller AAA) resursposter för platsens hanteringsplatser. Resurs posterna för tjänst platsen kan skapas automatiskt av Configuration Manager eller manuellt av DNS-administratören som skapar posterna i DNS.  

 Mer information om DNS-publicering som en tjänst plats metod för Configuration Manager-klienter finns i [förstå hur klienter hittar plats resurser och tjänster för Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

 Som standard genomsöker klienterna DNS efter hanteringsplatser i DNS-domänen. Om inga hanterings platser har publicerats i klienternas domän måste du dock konfigurera klienterna manuellt med ett DNS-suffix för hanterings platsen. Du kan konfigurera det här DNS-suffixet på klienter antingen under eller efter klientinstallation:  

-   Om du ska konfigurera klienter för ett hanteringsplatssuffix under klientinstallation måste du konfigurera CCMSetup Client.msi-egenskaper.  

-   Om du ska konfigurera klienter för ett hanteringsplatssuffix efter klientinstallation måste du konfigurera **Egenskaper för Configuration Manager**i kontrollpanalen.  

#### <a name="to-configure-clients-for-a-management-point-suffix-during-client-installation"></a>Så här konfigurerar du klienter för ett hanteringsplatssuffix under klientinstallation  

- Installera klienten med följande CCMSetup Client.msi-egenskap:  

  - **DNSSUFFIX =** * &lt;hanterings plats domän\>*  

     Om platsen har fler än en hanteringsplats och de finns i fler än en domän, ange endast en domän. När klienter ansluter till en hanteringsplats i den här domänen hämtar de en lista över tillgängliga hanteringsplatser som inkluderar hanteringsplatserna från andra domäner.  

    Mer information om kommando rads egenskaperna för CCMSetup finns i [om klient installations egenskaper](../../../core/clients/deploy/about-client-installation-properties.md).  

#### <a name="to-configure-clients-for-a-management-point-suffix-after-client-installation"></a>Så här konfigurerar du klienter för ett hanteringsplatssuffix efter klientinstallation  

1.  Navigera till **Configuration Manager**i Kontrollpanelen på klientdatorn och dubbelklicka på **Egenskaper**.  

2.  På fliken **Plats** anger du DNS-suffix för en hanteringsplats och klickar på **OK**.  

     Om platsen har fler än en hanteringsplats och de finns i fler än en domän, ange endast en domän. När klienter ansluter till en hanteringsplats i den här domänen hämtar de en lista över tillgängliga hanteringsplatser som inkluderar hanteringsplatserna från andra domäner.
