---
title: Publicera platsdata
titleSuffix: Configuration Manager
description: Lär dig hur du publicerar Configuration Manager-platser till Active Directory Domain Services.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 77ca6711f86250f4a6f937d919893cf95e022567
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718366"
---
# <a name="publish-site-data-for-configuration-manager"></a>Publicera plats data för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du har utökat Active Directory-schemat för Configuration Manager kan du publicera Configuration Manager platser till Active Directory Domain Services (AD DS). Detta gör att Active Directory datorer säkert kan hämta plats information från en betrodd källa. Även om det inte krävs att publicera plats information till AD DS för grundläggande Configuration Manager-funktioner, kan det minska det administrativa arbetet.  

-   **När en plats konfigureras att publicera till AD DS**kan Configuration Manager klienter automatiskt hitta hanterings platser genom Active Directory publicering. De använder en LDAP-fråga till en global katalog server.  

-   **När en plats inte publicerar till AD DS**måste klienter ha ett annat sätt att hitta sin standardhanteringsplats.  

Information om hur klienter hittar en hanterings plats finns i [förstå hur klienter hittar plats resurser och tjänster för Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="configure-sites-to-publish-to-ad-ds"></a>Konfigurera platser för publicering till AD DS  
 Följande är de övergripande stegen:  

-   Du måste [utöka Active Directory-schemat för Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) i varje skog där du ska publicera plats data. Se också till att **System Management** -behållaren finns.  

-   Du måste ge dator kontot för varje primär plats som ska publicera data **fullständig behörighet** till **System Management** -behållaren och alla dess underordnade objekt.  

### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>Så här aktiverar du en Configuration Manager webbplats för att publicera plats information till Active Directory skog

1.  Klicka på **Administration**i Configuration Manager-konsolen.  

2.  I arbets ytan **Administration** expanderar du **plats konfiguration**och klickar på **platser**. Välj den plats som du vill publicera plats data för. Klicka sedan på **Egenskaper**i gruppen **Egenskaper** på fliken **Start** .  

3.  På fliken **publicering** i platsens egenskaper väljer du de skogar som platsen ska publicera plats data på.  

4.  Spara ändringarna genom att klicka på **OK**.  

### <a name="to-set-up-active-directory-forests-for-publishing"></a>Konfigurera Active Directory-skogar för publicering  

1.  Klicka på **Administration**i Configuration Manager-konsolen.  

2.  I arbets ytan **Administration** expanderar du **konfiguration av hierarki**och klickar på **Active Directory skogar**. Om Identifiering av Active Directory-skogar har körts tidigare, visas alla skogar som har identifierats i resultatfönstret. Den lokala skogen och eventuella betrodda skogar identifieras när Identifiering av Active Directory-skogar körs. Det är bara obetrodda skogar som behöver läggas till manuellt.  

    -   Om du vill konfigurera en tidigare identifierad skog väljer du skogen i resultat fönstret. På fliken **Start** går du till gruppen **Egenskaper** och klickar på **Egenskaper** för att öppna skogs egenskaperna. Fortsätt med steg 3.  

    -   Om du vill konfigurera en ny skog som inte finns med i listan klickar du på **Lägg till skog** i gruppen **skapa** på fliken **Start** . dialog rutan **Lägg till skogar** öppnas. Fortsätt med steg 3.  

3.  På fliken **Allmänt** fyller du i konfigurationer för den skog som du vill identifiera och anger **Active Directory skogs konto**.  

    > [!NOTE]  
    >  Active Directory-skogskontot måste vara ett globalt konto om det ska gå att identifiera och publicera i skogar som inte är betrodda. Om du inte använder platsserverns datorkonto kan du välja ett globalt konto.  

4.  Om du tänker tillåta att platser publicerar platsdata i den här skogen, måste du ange konfigurationen för publicering i den här skogen på fliken **Publicering** .  

    > [!NOTE]  
    >  Om du gör det möjligt för platser att publicera till en skog måste du utöka Active Directory schemat för den skogen för Configuration Manager. Active Directory skogs kontot måste ha fullständig behörighet till system behållaren i den skogen.  

5.  Klicka på **OK** för att spara konfigurationen när du är klar med konfigurationen av den här skogen så att den går att använda av Identifiering av Active Directory-skogar.  
