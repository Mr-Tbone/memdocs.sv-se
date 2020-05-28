---
title: Schemautökningar
titleSuffix: Configuration Manager
description: Utöka Active Directory-schemat så att det stöder Configuration Manager.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1ace560130e43fd5675b51b6d507e84043c01407
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904076"
---
# <a name="schema-extensions-for-configuration-manager"></a>Schemautökningar för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan utöka Active Directory-schemat så att det stöder Configuration Manager. Detta redigerar en skogs Active Directory schema för att lägga till en ny behållare och flera attribut som Configuration Manager platser använder för att publicera viktig information i Active Directory där klienterna kan använda den på ett säkert sätt. Den här informationen kan förenkla distributionen och konfigurationen av klienter och hjälper klienterna att hitta plats resurser som servrar med distribuerat innehåll eller som tillhandahåller olika tjänster till klienter.  

-   Det är en bra idé att utöka Active Directory schema, men det är inte obligatoriskt.  

Innan du [utökar Active Directory-schemat](https://docs.microsoft.com/sccm/core/plan-design/network/extend-the-active-directory-schema) bör du vara bekant med Active Directory Domain Services och känna dig bekväm med att [ändra Active Directory-schemat](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc759402(v=ws.10)).  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>Att tänka på när du utökar Active Directory schema för Configuration Manager  

-   Active Directory schema utökningar för Configuration Manager är oförändrade från de som Configuration Manager 2007 och Configuration Manager 2012 använder. Om du redan har utökat schemat för endera version behöver du inte utöka schemat igen.  

-   Utökning av schemat är en skogs omfattande åtgärd som kan ångras.  

-   Endast en användare som är medlem i gruppen schema administratörer eller som har delegerats tillräckliga behörigheter för att ändra schemat kan utöka schemat.  

-   Även om du kan utöka schemat innan eller efter att du kör Configuration Manager-installationen, är det en bra idé att utöka schemat innan du börjar konfigurera dina platser och inställningar för hierarki. Detta kan underlätta många konfigurationssteg längre fram.  

-   När du har utökat schemat replikeras den Active Directory globala katalogen i skogen. Därför bör du planera att utöka schemat när replikeringstrafiken inte påverkar andra nätverks beroende processer:  

    -   I Windows 2000-skogar gör utökning av schemat en fullständig synkronisering av hela den globala katalogen.  

    -   Från och med Windows 2003-skogar replikeras endast de nyligen tillagda attributen.  

**Enheter och klienter som inte använder Active Directory-schemat:**  

-   Mobila enheter som hanteras av Exchange Server-anslutningsprogrammet  

-   Klienten för Mac-datorer  

-   Klienten för Linux- och UNIX-servrar  

-   Mobila enheter som har registrerats av Configuration Manager  

-   Mobila enheter som har registrerats av Microsoft Intune  

-   Gamla mobilenhetsklienter  

-   Windows-klienter som är konfigurerade för klient hantering endast på Internet  

-   Windows-klienter som identifieras av Configuration Manager som ska finnas på Internet  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>Funktioner som har nytta av en schemautökning  
**Installation av klient dator och platstilldelning** – när en Windows-dator installerar en ny klient söker klienten Active Directory Domain Services efter installations egenskaper.  

-   **Lösningar:** Om du inte utökar schemat kan du använda något av följande alternativ för att ange konfigurations information som datorer måste installera:  

    -   **Använd push-installation av klient**. Innan du använder en klient installations metod måste du kontrol lera att alla krav är uppfyllda. Mer information finns i avsnittet "installations metodens beroenden" i [krav för distribution av klienter till Windows-datorer](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md).  

    -   **Installera klienter manuellt** och ange klient installations egenskaper genom att använda kommando rads egenskaper för CCMSetup-installation. Detta måste innefatta följande:  

        -   Ange en hanterings plats eller käll Sök väg som datorn kan ladda ned installationsfilerna från med hjälp av CCMSetup-egenskapen **/MP: = &lt; hanterings plats namn \> dator namn** eller **/Source: &lt; \> sökväg till klientens källfiler** på CCMSetup-kommandoraden under klient installationen.  

        -   Ange en lista med inledande hanterings platser som klienten ska använda så att den kan tilldela dem till platsen och sedan ladda ned klient princip-och plats inställningar. Använd egenskapen CCMSetup Client.msi SMSMP för att göra detta.  

    -   **Publicera hanteringsplatsen i DNS eller WINS** och konfigurera klienter att använda den här metoden för att hitta platsen för en tjänst.  

**Port konfiguration för kommunikation mellan klient och Server** – när en klient installeras konfigureras den med portinformation som lagras i Active Directory. Om du senare ändrar kommunikations porten mellan klient och server för en plats kan en klient hämta den nya port inställningen från Active Directory Domain Services.  

-   **Provisoriska lösningar**: Om du inte utökar schemat måste du använda en av följande alternativ för att tillhandahålla nya portkonfigurationer till befintliga klienter:  

    -   **Installera om klienterna** med hjälp av alternativ som konfigurerar den nya porten.  

    -   **Distribuera ett skript till klienterna som uppdaterar portinformationen**. Om klienterna inte kan kommunicera med en plats på grund av en port ändring kan du inte använda Configuration Manager för att distribuera det här skriptet. Du kan till exempel använda grupprincip.  

**Scenarier för innehålls distribution** – när du skapar innehåll på en plats och sedan distribuerar innehållet till en annan plats i hierarkin måste den mottagande platsen kunna verifiera signaturen för signerade innehålls data. Det kräver tillgång till en offentliga nyckeln för den källplats där du skapade dessa data. När du utökar Active Directory-schemat för Configuration Manager är en plats offentliga nyckel tillgänglig för alla platser i hierarkin.  

-   **Provisorisk lösning**: Om du inte utökar Active Directory-schemat kan du använda underhållsverktyget för hierarkier, **preinst.exe**, för att utbyta säker nyckelinformation mellan platser.  

     Om du till exempel planerar att skapa innehåll på en primär plats och distribuerar innehållet till en sekundär plats under en annan primär plats måste du antingen utöka Active Directory-schemat för att den sekundära platsen ska kunna hämta den primära käll platsens offentliga nyckel eller använda Preinst. exe för att dela nycklar mellan de två platserna direkt.  

## <a name="active-directory-attributes-and-classes"></a>Active Directory attribut och klasser  
När du utökar schemat för Configuration Manager läggs följande klasser och attribut till i schemat och är tillgängliga för alla Configuration Manager platser i den Active Directory skogen.  

-   Attribut:  

    -   CN = mS-SMS-Assignment-site-Code  

    -   CN = mS-SMS-Capabilities  

    -   CN = MS-SMS-standard-MP  

    -   CN = mS-SMS-Device-Management-Point  

    -   CN = mS-SMS-hälso tillstånd  

    -   CN = MS-SMS-MP-Address  

    -   CN = MS-SMS-MP-Name  

    -   CN = MS-SMS-intervall-IP-High  

    -   CN = MS-SMS-intervall-IP-Low  

    -   CN = MS-SMS-roaming-gränser  
        på  

    -   CN = MS-SMS-site-gränser  

    -   CN = MS-SMS-plats-kod  

    -   CN = mS-SMS-source-skog  

    -   CN = mS-SMS-version  

-   Klasser:  

    -   CN = MS-SMS-Management-Point  

    -   CN = MS-SMS-roaming-gränser-intervall  

    -   CN = MS-SMS-server-Locator-Point  

    -   CN = MS-SMS-site  

> [!NOTE]
> 
>  Schema tilläggen kan innehålla attribut och klasser som överförs från tidigare versioner av produkten men som inte används av Configuration Manager. Ett exempel:  
> 
> 
> - Attribut: CN = MS-SMS-plats-gränser  
>   -   Klass: CN = MS-SMS-server-Locator-Point  

Du kan se till att föregående listor är aktuella genom att visa **ConfigMgr_ad_schema. LDF** -filen från mappen **\SMSSETUP\BIN\x64** på installations mediet för Configuration Manager.  
