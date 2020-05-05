---
title: Publicera och Active Directory schema
titleSuffix: Configuration Manager
description: Utöka Active Directory-schemat för Configuration Manager för att förenkla processen för att distribuera och konfigurera klienter.
ms.date: 09/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3595273d55bf01158691fb46587ac264af16bffa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718765"
---
# <a name="prepare-active-directory-for-site-publishing"></a>Förbereda Active Directory för webbplats publicering

*Gäller för: Configuration Manager (aktuell gren)*

När du utökar Active Directory-schemat för Configuration Manager, introducerar du nya strukturer för Active Directory som används av Configuration Manager platser för att publicera viktig information på en säker plats där klienter enkelt kan komma åt den.  

Det är en bra idé att använda Configuration Manager med ett utökat Active Directory schema när du hanterar lokala klienter. Ett utökat schema kan förenkla processen för att distribuera och konfigurera klienter. Ett utökat schema gör det också möjligt för klienter att effektivt hitta resurser som innehålls servrar och ytterligare tjänster som de olika Configuration Manager plats system rollerna tillhandahåller.  

-   Om du inte är bekant med det utökade schemat för en Configuration Manager distribution kan du läsa om [schema utökningar för Configuration Manager](../../../core/plan-design/network/schema-extensions.md) som hjälper dig att fatta det här beslutet.  

-   När du inte använder ett utökat schema kan du konfigurera andra metoder som DNS och WINS för att hitta tjänster och plats system servrar. Dessa metoder för tjänstlokalisering kräver ytterligare konfigurationer och är inte den bästa metoden för tjänstlokalisering av klienter. Läs mer i [förstå hur klienter hittar plats resurser och tjänster för Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   Om Active Directory-schemat har utökats för Configuration Manager 2007 eller System Center 2012 Configuration Manager behöver du inte göra mer. Schema tilläggen har inte ändrats och är redan på plats.  

Att utöka schemat är en engångs åtgärd för alla skogar. Följ dessa steg om du vill utöka och sedan använda det utökade Active Directory schemat:  

## <a name="step-1-extend-the-schema"></a>Steg 1. Utöka schemat  
Så här utökar du schemat för Configuration Manager:  

-   Använd ett konto som är medlem i säkerhets gruppen schema administratörer.  

-   Vara inloggad på schemats huvud domän kontroller.  

-   Kör verktyget **extadsch. exe** eller Använd kommando RADS verktyget ldifde med filen **ConfigMgr_ad_schema. ldf** . Både verktyget och filen finns i mappen **SMSSETUP\BIN\X64** på installations mediet för Configuration Manager.  

#### <a name="option-a-use-extadschexe"></a>Alternativ A: Använd Extadsch.exe  

1.  Kör **extadsch.exe** för att lägga till nya klasser och attribut i Active Directory-schemat.  

    > [!TIP]  
    >  Kör det här verktyget från en kommandorad för att visa feedback när det körs.  

2.  Kontrol lera att schema tillägget lyckades genom att granska extadsch. log i roten på system enheten.  

#### <a name="option-b-use-the-ldif-file"></a>Alternativ B: Använd LDIF-filen  

1.  Redigera **ConfigMgr_ad_schema. ldf** -filen för att definiera den Active Directory rot domän som du vill utöka:  

    -   Ersätt alla förekomster av texten, **DC = x**, i filen med det fullständiga namnet på den domän som ska utökas.  

    -   Om till exempel det fullständiga namnet på den domän som ska utökas heter widgets.microsoft.com, ändra alla instanser av DC = x i filen till **DC = widgetar, DC = Microsoft, DC = com**.  

2.  Använd kommando rads verktyget LDIFDE för att importera innehållet i filen **ConfigMgr_ad_schema. ldf** till Active Directory Domain Services:  

    -   Följande kommando rad importerar t. ex. schema tilläggen till Active Directory Domain Services, aktiverar utförlig loggning och skapar en loggfil under importen: **ldifde-i-f ConfigMgr_ad_schema. ldf-v-j &lt;plats för att lagra logg filen\>**.  

3.  Kontrol lera att schema tillägget lyckades genom att granska en loggfil som skapats av kommando raden som användes i föregående steg.  

## <a name="step-2--create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>Steg 2.  Skapa System Management-containern och bevilja platsbehörigheter till containern  
 När du har utökat schemat måste du skapa en behållare med namnet **System Management** i Active Directory Domain Services (AD DS):  

-   Du skapar den här behållaren en gången i varje domän som har en primär eller sekundär plats som ska publicera data till Active Directory.  

-   För varje behållare beviljar du behörigheter till dator kontot för varje primär och sekundär plats server som ska publicera data till den domänen. Varje konto måste ha **fullständig** behörighet till behållaren med den avancerade behörigheten, **tillämpa på**, lika med **det här objektet och alla underordnade objekt**.  

#### <a name="to-add-the-container"></a>Lägga till containern  

1.  Använd ett konto som har behörigheten **Skapa alla underordnade objekt** för **System**-containern i Active Directory Domain Services.  

2.  Kör **ADSI Edit** (adsiedit. msc) och Anslut till plats serverns domän.  

3.  Skapa containern:  

    -   Expandera **domän** &lt;datorns fullständigt kvalificerade domän\>namn, &lt;expandera unikt\>namn, högerklicka på **CN = System**, Välj **nytt**och välj sedan **objekt**.  

    -   I dialog rutan **skapa objekt** väljer du **behållare**och väljer sedan **Nästa**.  

    -   I rutan **värde** anger du **System Management**och väljer sedan **Nästa**.  

4.  Tilldela behörigheter:  

    > [!NOTE]  
    >  Om du vill kan du använda andra verktyg som administrations verktyget Active Directory-användare och datorer (DSA. msc) för att lägga till behörigheter till behållaren.  

    -   Högerklicka på **CN = System Management**och välj sedan **Egenskaper**.  

    -   Välj fliken **säkerhet** , Välj **Lägg till**och Lägg sedan till plats serverns dator konto med behörigheten **fullständig** behörighet.  

    -   Välj **Avancerat**, Välj plats serverns dator konto och välj sedan **Redigera**.  

    -   I listan **tillämpa på** väljer du **det här objektet och alla underordnade objekt**.  

5.  Välj **OK** för att stänga konsolen och spara konfigurationen.  

## <a name="step-3-set-up-sites-to-publish-to-active-directory-domain-services"></a>Steg 3. Konfigurera platser att publicera till Active Directory Domain Services  
 När behållaren har kon figurer ATS beviljas behörigheter och du har installerat en Configuration Manager primär plats, kan du konfigurera platsen för att publicera data till Active Directory.  

 Mer information om hur du publicerar finns i [publicera plats data för Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md).  
