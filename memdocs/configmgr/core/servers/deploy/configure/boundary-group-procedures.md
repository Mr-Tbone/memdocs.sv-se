---
title: Procedurer för gränsgrupper
titleSuffix: Configuration Manager
description: Konfigurera gräns grupper för att logiskt organisera relaterade nätverks platser som kallas gränser.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1fe22d0-4695-4de0-8bf0-e3475b03cf0e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e8a47522cf59cc211f29c572010f9d3250659e1e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715797"
---
# <a name="how-to-configure-boundary-groups-for-configuration-manager"></a>Konfigurera gränser grupper för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln innehåller anvisningar om hur du konfigurerar gränser grupper. Innan du börjar bör du se till att du förstår begrepp för gränser-grupp. Mer information finns i [gränser grupper](boundary-groups.md).



## <a name="create-a-boundary-group"></a><a name="bkmk_create"></a>Skapa en avgränsnings grupp  

1.  I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **konfiguration av hierarki**och väljer noden **gränser grupper** .  

2.  På fliken **Start** går du till gruppen **skapa** och väljer **skapa en avgränsnings grupp**.  

3.  I dialog rutan **skapa gränser grupp** går du till fliken **Allmänt** och anger ett **namn** för den här gränser gruppen. Du kan också ta med en **Beskrivning**.  

4.  Välj **OK** för att spara den nya gränser gruppen eller Fortsätt till nästa avsnitt för att konfigurera gränser gruppen.  


## <a name="configure-a-boundary-group"></a><a name="bkmk_config"></a>Konfigurera en avgränsnings grupp  

1.  I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **konfiguration av hierarki**och väljer noden **gränser grupper** .  

2.  Välj den avgränsnings grupp som du vill ändra och välj **Egenskaper** i menyfliksområdet. Den här åtgärden öppnar gränser gruppen Fönstret Egenskaper.  

Konfigurera följande inställningar:  
- [Lägg till eller ta bort gränser](#bkmk_add)  
- [Konfigurera platstilldelning och välj plats system servrar](#bkmk_references)  
- [Konfigurera återställnings beteende](#bkmk_bg-fallback)  
- [Konfigurera alternativ för gränser grupp](#bkmk_options)  


### <a name="add-or-remove-boundaries"></a><a name="bkmk_add"></a>Lägg till eller ta bort gränser

I gräns gruppen Fönstret Egenskaper använder du fliken **Allmänt** för att ändra de gränser som är medlemmar i gräns gruppen:  

- Om du vill lägga till gränser väljer du **Lägg till**. I fönstret Lägg till gränser markerar du kryss rutan för en eller flera gränser och väljer **OK**.  

- Om du vill ta bort gränser markerar du gränsen i listan och väljer **ta bort**.  


### <a name="configure-site-assignment-and-select-site-system-servers"></a><a name="bkmk_references"></a>Konfigurera platstilldelning och välj plats system servrar

Om du vill ändra platstilldelning och associerad plats system Server konfiguration växlar du till fliken **referenser** i gränser gruppen fönstret Egenskaper.  

- Om du vill att den här gränser gruppen ska användas av klienter för platstilldelning väljer du **Använd den här ram gruppen för platstilldelning**. Välj sedan en plats i list rutan **tilldelad plats** . Mer information finns i [platstilldelning](boundary-groups.md#site-assignment).  

- Om du vill associera tillgängliga plats system servrar med den här gränser gruppen väljer du **Lägg till**. I fönstret Lägg till plats system visas endast servrar som har stöd för plats system roller som stöds. Markera kryss rutan för en eller flera servrar och välj **OK**. Den lägger till dem som associerade plats system servrar för den här gränser gruppen.  

    > [!NOTE]  
    >  Du kan välja valfri kombination av tillgängliga platssystem från alla platser i hierarkin. Valda plats system visas på fliken **plats system** i egenskaperna för varje bindning som är medlem i den här gränser gruppen.  

- Om du vill ta bort en server från den här gränser gruppen väljer du servern och väljer sedan **ta bort**.  

    > [!NOTE]  
    >  Om du vill sluta använda den här gränser gruppen för att associera plats system tar du bort alla servrar som anges som associerade plats system servrar.  


### <a name="configure-fallback-behavior"></a><a name="bkmk_bg-fallback"></a>Konfigurera återställnings beteende

Om du vill konfigurera återställnings beteende växlar du till fliken **relationer** i gränser gruppen fönstret Egenskaper.  

- Så här skapar du en relation med en annan avgränsnings grupp:  

  - Välj **Lägg till**. I fönstret återställnings gränser väljer du den gränser grupp som ska konfigureras.  

  - Ange en återställnings tid för följande plats system roller:  
    - Distributionsplats  
    - Programuppdateringsplats  
    - Hanteringsplats  

      > [!Note]  
      > Du kan till exempel öppna Fönstret Egenskaper för den begränsade gruppen för avdelnings kontor. I fönstret reserv gränser grupper väljer du huvud kontorets gränser grupp. Du ställer in återställnings tiden för `20`distributions platsen på. När du sparar den här konfigurationen börjar klienterna i den begränsade gruppen för lokal kontor att söka efter innehåll från distributions platserna i huvud kontorets gränser grupp efter 20 minuter.  

  - Om du vill förhindra återställningen till en angiven avgränsnings grupp väljer du gränser gruppen och väljer Återställ **aldrig** för typ av plats system roll. Den här åtgärden kan omfatta *standard platsens gränser grupp*.  

- Om du vill ändra konfigurationen för en befintlig relation väljer du den gränser gruppen i listan och väljer **ändra**. Den här åtgärden öppnar fönstret återställnings gränser för bara den här gränsen.  
 
- Om du vill ta bort en relation väljer du kant linje gruppen i listan och väljer **ta bort**.  

Mer information finns i [fallback](boundary-groups.md#fallback). 


### <a name="configure-boundary-group-options"></a><a name="bkmk_options"></a>Konfigurera alternativ för gränser grupp
<!--1356193-->
Från och med version 1806 kan du växla till fliken **alternativ** om du vill konfigurera ytterligare alternativ för klienter i den här gränser-gruppen. Mer information finns i [gränser grupp alternativ för peer-nedladdningar](boundary-groups.md#bkmk_bgoptions).

- **Tillåt nedladdning av peer-datorer i den här begränsnings gruppen**: det här alternativet är aktiverat som standard. Hanterings platsen ger klienterna en lista över innehålls platser som innehåller peer-källor.  

    - **Använd endast peer-datorer i samma undernät vid peer-hämtning**: den här inställningen är beroende av den ovan. Om du aktiverar det här alternativet innehåller hanterings platsen bara den innehålls plats i listan med peer-källor som finns i samma undernät som klienten.  


## <a name="configure-a-fallback-site-for-automatic-site-assignment"></a><a name="bkmk_site-fallback"></a>Konfigurera en återställnings plats för automatisk platstilldelning  

Om klienterna inte finns i en gränser grupp med en tilldelad plats tilldelar du dem till den här platsen när de är installerade.

1.  Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .  

2.  På fliken **Start** i menyfliksområdet i gruppen **platser** väljer du **Inställningar för hierarkin**.  

3.  På fliken **Allmänt** markerar du kryss rutan för att **använda en återställnings plats**. Välj sedan en plats i list rutan **återställnings plats** .  

4.  Välj **OK** för att spara konfigurationen.  

Mer information finns i [platstilldelning](boundary-groups.md#site-assignment).


## <a name="enable-use-of-preferred-management-points"></a><a name="bkmk_proc-prefer"></a>Aktivera användning av prioriterade hanterings platser  

Mer information finns i [prioriterade hanterings platser](boundary-groups.md#bkmk_preferred).

1.  Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .  

2. På fliken **Start** i menyfliksområdet i gruppen **platser** väljer du **Inställningar för hierarkin**.  

3. På fliken **Allmänt** väljer du **klienter föredrar att använda hanterings platser som anges i gränser grupper**.  

4. Välj **OK** för att spara konfigurationen.  

