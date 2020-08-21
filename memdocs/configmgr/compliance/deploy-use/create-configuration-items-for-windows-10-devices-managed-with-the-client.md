---
title: Skapa konfigurations objekt för Windows 10
titleSuffix: Configuration Manager
description: Använd konfigurations objekt för Windows 10 för att hantera inställningar för Windows 10-datorer som hanteras av Configuration Manager-klienten.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 9589b9e542c9d323ab7a23af169725c1a54bfb70
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694771"
---
# <a name="create-configuration-items-for-windows-10-devices"></a>Skapa konfigurationsobjekt för Windows 10-enheter

Använd Configuration Manager konfigurations objekt för **Windows 10** för att hantera inställningar för Windows 10-datorer som hanteras av Configuration Manager-klienten.  
  
> [!IMPORTANT]  
>  Om du i den här versionen har skapat en **lösen ords** inställning som en del av ett konfigurations objekt av typen **Windows 10** (för en enhet som hanteras med Configuration Manager-klienten) bör du vara medveten om följande problem. Om inställningen inte redan finns eller inte har kon figurer ATS på Windows 10-enheten, kommer den felaktigt att utvärderas som kompatibel.  
>   
>  För att komma runt detta när du skapar en inställning för dessa enheter ser du till att **Reparera inkompatibla inställningar** är valt på inställningssidorna i guiden Skapa konfigurationsobjekt. När du distribuerar en konfigurations bas linje som innehåller ett konfigurations objekt för Windows 10 som innehåller lösen ords inställningar väljer du dessutom **Reparera inkompatibla regler när det stöds**. Du gör det här valet i dialog rutan distribuera konfigurations bas linjer. Genom att använda den här lösningen övervakas inställningen och åtgärdas om den inte är kompatibel. Efter reparationen rapporteras inställningen korrekt som **kompatibel** (om inte ett problem uppstår, vilket innebär att den rapporterar **fel**).  
  
### <a name="to-create-a-windows-10-configuration-item"></a>Så här skapar du ett Windows 10-konfigurationsobjekt  
  
1. I Configuration Manager-konsolen väljer du **till gångar och efterlevnad**.  
  
2. I arbets ytan **till gångar och efterlevnad** expanderar du **kompatibilitetsinställningar**och väljer sedan **konfigurations objekt**.  
  
3. På fliken **Start** går du till gruppen **skapa** och väljer **skapa konfigurations objekt**.  
  
4. På sidan **Allmänt** i guiden **skapa konfigurations objekt** anger du ett namn och en valfri beskrivning för konfigurationsobjektet.  
  
5. Välj **Windows 10**under **Ange typen av konfigurationsobjekt som du vill skapa**.  
  
6. Om du skapar och tilldelar kategorier som hjälper dig att söka efter och filtrera konfigurations objekt i Configuration Manager-konsolen väljer du **Kategorier**.  
  
7. På sidan **Plattformar som stöds** i guiden väljer du de Windows 10-plattformar som ska utvärdera konfigurationsobjektet.  
  
8. På sidan **Enhetsinställningar** i guiden väljer du den inställningsgrupp som du vill konfigurera. (Mer information finns i [inställnings referens för konfigurations objekt i Windows 10](#BKMK_Ref) i den här artikeln.) Välj sedan **Nästa**.  
  
   > [!TIP]  
   >  Om den inställning som du vill använda inte visas i listan markerar du **kryss rutan konfigurera ytterligare inställningar som inte finns med i standardinställnings grupperna**.  
  
9. På varje inställnings sida konfigurerar du de inställningar du behöver, och om du vill åtgärda dem när de inte är kompatibla på enheter (när det stöds).  
  
10. För varje inställnings grupp kan du också konfigurera allvarlighets graden som rapporteras när ett konfigurations objekt inte är kompatibelt:  
  
    -   **Ingen**: enheter som inte uppfyller den här regeln rapporterar inte allvarlighets grad för Configuration Manager rapporter.  
  
    -   **Information**: enheter som inte uppfyller den här regeln rapporterar allvarlighets graden **information** för Configuration Manager rapporter.  
  
    -   **Varning**! enheter som inte uppfyller den här regeln rapporterar allvarlighets graden **Varning** för Configuration Manager rapporter.  
  
    -   **Kritisk**: enheter som inte uppfyller den här regeln rapporterar allvarlighets graden **kritisk** för Configuration Manager rapporter.  
  
    -   **Kritisk med händelse**: enheter som inte uppfyller den här regeln rapporterar allvarlighets graden **kritisk** för Configuration Manager rapporter. Allvarlighetsgraden registreras även som en Windows-händelse i programhändelseloggen.  
  
11. På sidan **plattforms tillämplighet** i guiden granskar du alla inställningar som inte är kompatibla med de plattformar som du valde tidigare. Du kan gå tillbaka och ta bort inställningarna, eller fortsätta.  
  
    > [!TIP]  
    >  Kompatibiliteten utvärderas inte för inställningar som inte stöds.  
  
12. Slutför guiden.  
  
    Du kan visa det nya konfigurationsobjektet i noden **Konfigurationsobjekt** på arbetsytan **Tillgångar och efterlevnad** .  
  
## <a name="windows-10-configuration-item-settings-reference"></a><a name="BKMK_Ref"></a> Windows 10 configuration item settings reference  
  
### <a name="password"></a>lösenordsinställning  
  
|Inställningen|Information|  
|-------------|-------------|  
|**Kräv lösenordsinställningar på enheter**|Kräver ett lösen ord på enheter som stöds.|  
|**Minsta längd på lösenord (tecken)**|Den minsta längden i antal tecken för lösenordet.|  
|**Lösenordets giltighetstid, i dagar**|Antal dagar innan lösenordet måste ändras.|  
|**Antal lagrade lösenord**|Förhindrar återanvändning av tidigare lösen ord.|  
|**Antal misslyckade inloggningsförsök innan en enhet rensas.**|Rensar enheten om inloggningen Miss lyckas det här antalet gånger.|  
|**Inaktivitetstid innan enheten låses**|Anger hur många minuter enheten måste vara inaktiv innan den låses automatiskt.|  
|**Lösenordskomplexitet**|Välj om du kan ange en PIN-kod, till exempel "1234", eller om du måste ange ett starkt lösen ord.|
|**Antal avancerade teckenuppsättningar som krävs i lösen ord**|Om du har valt ett **starkt** lösen ord använder du den här inställningen för att konfigurera antalet avancerade teckenuppsättningar som krävs. För ett starkt lösen ord ska den här inställningen anges till minst **3**, vilket innebär att både bokstäver och siffror måste anges. Välj **4** om du vill framtvinga ett lösen ord som kräver särskilda tecken, till exempel **(% $**.<br>(Endast Windows 10)  |
  
###  <a name="device"></a>Enhet  
  
|Inställningsnamn|Information|  
|------------------|-------------|  
|**Bluetooth**|Tillåter användningen av Bluetooth-funktioner på enheten.|  
  
### <a name="cloud"></a>Moln  
  
|Inställningsnamn|Information|  
|------------------|-------------|  
|**Synkronisering av inställningar**|Tillåt synkronisering av inställningar mellan enheter.|  
|**Synkronisering av autentiseringsuppgifter**|Tillåter synkronisering av inloggningsuppgifter mellan enheter.|  
|**Inställningssynkronisering över anslutningar med datapriser**|Tillåter att inställningar synkroniseras när Internet anslutningen mäts.|  
  
### <a name="roaming"></a>Nätverksväxling  
  
|Inställningsnamn|Information|  
|------------------|-------------|  
|**Data nätverks växling**|Tillåter nätverks växling mellan nätverk vid åtkomst till data.|  
  
### <a name="encryption"></a>Kryptering  
  
|Inställningsnamn|Information|  
|------------------|-------------|  
|**Filkryptering på enhet**|Kräver att filer på enheten krypteras.|  
  
### <a name="system-security"></a>Systemsäkerhet  
  
|Inställningsnamn|Information|  
|------------------|-------------|  
|**User Account Control**|Konfigurerar hur Kontroll av användarkonto i Windows fungerar på enheten.<br />Du kan till exempel inaktivera funktionen eller ange på vilken nivå den ska meddela dig.|  
|**Nätverksbrandvägg**|Aktiverar eller inaktiverar Windows-brandväggen.|  
|**SmartScreen**|Aktiverar eller inaktiverar Windows SmartScreen.|  
|**Virusskydd**|Kräver att antivirusprogramvara installeras och konfigureras.|  
|**Virusskyddets signaturer är uppdaterade**|Kräver att signaturfiler för antivirus programmet på enheten måste vara uppdaterade.|  
  
### <a name="windows-information-protection"></a>Windows informationsskydd

Med ökningen av anställdas ägda enheter i företaget finns det också en ökande risk för oavsiktliga data läckor via appar och tjänster, t. ex. e-post, sociala medier och det offentliga molnet. De är utanför organisationens kontroll. Exempel är när en anställd:

- Skickar de senaste teknik bilderna från sitt personliga e-postkonto.
- Kopierar och klistrar in produkt information i en tweet.
- Sparar en pågående försäljnings rapport till sin offentliga moln lagring.

Windows Information Protection (Pia, tidigare företags data skydd) hjälper till att skydda mot potentiell data läckage utan att störa medarbetarnas upplevelse. Pia hjälper också till att skydda företags program och data mot oavsiktliga data läckor på företagsägda enheter och personliga enheter som anställda arbetar med. RIA kräver inte ändringar i din miljö eller andra appar.

Configuration Manager konfigurations objekt för Windows Information Protection hantera följande:

- Listan över appar som skyddas av RIA
- Företags nätverks platser
- Skydds nivå
- Krypteringsinställningar
  
Information om hur du konfigurerar Pia med Configuration Manager finns i:

- [Skydda dina företags data med Windows Information Protection (Pia)](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Skapa och distribuera en princip för Windows Information Protection (Pia) med Configuration Manager](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)
- [Begränsningar när du använder Windows-Information Protection (Pia)](/windows/security/information-protection/windows-information-protection/limitations-with-wip)

## <a name="see-also"></a>Se även  
[Konfigurations objekt för enheter som hanteras med Configuration Manager-klienten](../../compliance/deploy-use/create-configuration-items.md)