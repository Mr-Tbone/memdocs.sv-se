---
title: Uppgradera klienter i Windows
titleSuffix: Configuration Manager
description: Uppgradera klienter på Windows-datorer i Configuration Manager.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7476f27c050a7870cd8f860f2e1b6bfa3d68a7e9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715027"
---
# <a name="how-to-upgrade-clients-for-windows-computers-in-configuration-manager"></a>Uppgradera klienter för Windows-datorer i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Uppgradera Configuration Manager-klienten på Windows-datorer med hjälp av klient installations metoder eller automatiska funktioner för klient uppgradering. Följande klientinstallationsmetoder är giltiga sätt att uppgradera klientprogramvara på Windows-datorer:  

- Grupprincipinstallation  

- Installation av inloggningsskript  

- Manuell installation  

- Installation av uppgradering  

Mer information finns i [Distribuera klienter till Windows-datorer](../../deploy/deploy-clients-to-windows-computers.md).

Undanta klienter från uppgradering genom att ange en undantags samling. Mer information finns i [så här utesluter du klienter från uppgradering](exclude-clients-windows.md). Exkluderade klienter laddar fortfarande ned och kör CCMSETUP, men uppgraderar inte.

> [!TIP]  
> Om du uppgraderar Server infrastrukturen från en tidigare version av Configuration Manager slutför du Server uppgraderingar innan du uppgraderar Configuration Manager-klienterna. I den här processen ingår att installera alla aktuella gren uppdateringar. Den senaste uppdateringen av den aktuella grenen innehåller den senaste versionen av klienten. Uppgradera klienter när du har installerat alla Configuration Manager-uppdateringar.

> [!NOTE]
> Om du planerar att omtilldela platsen för klienterna under uppgraderingen anger du den nya platsen med `SMSSITECODE` client. msi-egenskapen. Om du använder värdet `AUTO` för för `SMSSITECODE`, anger `SITEREASSIGN=TRUE`du även. Den här egenskapen tillåter automatisk omtilldelning av platser under uppgraderingen. Mer information finns i [Egenskaper för klient installation – SMSSITECODE](../../deploy/about-client-installation-properties.md#smssitecode).

## <a name="about-automatic-client-upgrade"></a><a name="bkmk_autoupdate"></a>Om automatisk klient uppgradering

Konfigurera platsen för att automatiskt uppgradera klienter till den senaste versionen av Configuration Manager. När Configuration Manager identifierar en tilldelad klients version är tidigare än hierarkins version, uppgraderas klienten automatiskt. I det här scenariot ingår uppgradering av klienten till den senaste versionen när den försöker tilldela till en Configuration Manager-plats.  

En klient kan uppgradera automatiskt i följande scenarier:  

- Klient versionen är tidigare än den version som används i hierarkin.  

- Klienten på den centrala administrations platsen (CAS) har ett språk paket installerat och den befintliga klienten är inte det.  

- Ett klientkrav i hierarkin har en annan version än den som är installerad på klienten.  

- En eller flera av klientinstallationsfilerna har en annan version.  

> [!NOTE]  
> Om du vill identifiera olika versioner av Configuration Manager-klienten i din hierarki använder du rapport **antalet Configuration Manager klienter efter klient versioner** i mappen rapportmapp **-klient information**.  

Configuration Manager skapar ett uppgraderings paket som standard. Paketet skickas automatiskt till alla distributions platser i hierarkin. Om du gör ändringar i klient paketet på certifikat utfärdarna, Configuration Manager automatiskt uppdatera paketet och distribuera det igen. Ett exempel är att ändra när du lägger till ett klient språk paket. Om du aktiverar automatisk klient uppgradering installerar varje klient automatiskt det nya klient språk paketet.

> [!NOTE]  
> Configuration Manager skickar inte klient uppgraderings paketet automatiskt till Configuration Manager molnbaserade distributions platser.  

Aktivera automatisk klient uppgradering i hela hierarkin. Den här konfigurationen håller dina klienter uppdaterade med mindre ansträngning.  

Om du också hanterar dina Configuration Manager plats system som klienter bör du bestämma om du vill ta med dem som en del av den automatiska uppgraderings processen. Du kan undanta alla servrar eller en speciell samling från klient uppgraderingen. Vissa Configuration Manager plats roller delar klient ramverket. Till exempel hanterings platsen och mottagar distributions platsen. De här rollerna uppgraderas när du uppdaterar platsen, så klient versionen på de här servrarna uppdateras på samma gång.

## <a name="configure-automatic-client-upgrade"></a><a name="bkmk_configure"></a>Konfigurera automatisk klient uppgradering

Använd följande procedur för att konfigurera automatisk klient uppgradering på CAS. Den här konfigurationen gäller för alla klienter i hierarkin.  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .  

1. På fliken **Start** i menyfliksområdet i gruppen **platser** väljer du **Inställningar för hierarkin**.  

1. Växla till fliken **klient uppgradering** . granska versionen och datumet för produktions klienten. Kontrol lera att det är den version som du vill använda för att uppgradera klienterna. Om det inte är den klient version som du förväntar dig kan du behöva uppgradera för produktions klienten till produktion. Mer information finns i [så här testar du klient uppgraderingar i en för produktions samling](test-client-upgrades.md).  

1. Välj **Uppgradera alla klienter i hierarkin med produktions klienten**. Välj **Ja** för att bekräfta.  

1. Om du inte vill att klient uppgraderingar ska tillämpas på servrar väljer du **Uppgradera inte servrar**.  

1. Ange hur många dagar som enheterna måste uppgradera klienten. När enheten har tagit emot en princip uppgraderas klienten till ett slumpmässigt intervall inom det här antalet dagar. Det här beteendet förhindrar att ett stort antal klienter uppgraderas samtidigt.

    > [!NOTE]
    > En dator måste vara igång för att klienten ska kunna uppgraderas. Om en dator inte körs när den är schemalagd att ta emot uppgraderingen sker inte uppgraderingen. När datorn aktive ras och den tar emot en princip, schemaläggs uppgraderingen för en slumpmässig tid inom det tillåtna antalet dagar. Om detta inträffar när antalet dagar som uppgraderingen har upphört att gälla, schemaläggs uppgraderingen vid en slumpmässig tidpunkt inom 24 timmar efter att datorn aktiverades.
    >
    > På grund av det här problemet kan det ta längre tid för datorer som stängs av att uppgraderas än förväntat om den slumpmässigt schemalagda uppgraderings tiden inte ligger inom den normala arbets tiden.

1. Om du vill undanta klienter från uppgradering väljer du **undanta angivna klienter från uppgradering**och anger den samling som ska undantas. Mer information finns i [undanta klienter från uppgradering](exclude-clients-windows.md).

1. Om du vill att platsen ska kopiera klient installations paketet till distributions platser som du har aktiverat för [förinstallerat innehåll](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent)väljer du alternativet för att **automatiskt distribuera klient installations paket till distributions platser som är aktiverade för förinstallerat innehåll**.  

1. Välj **OK** för att spara inställningarna och stänga egenskaper för hierarkiska inställningar.

Klienterna tar emot dessa inställningar nästa gång de hämtar principer.

> [!NOTE]
> Klient uppgraderingar följer alla Configuration Manager underhålls fönster som du har konfigurerat.

## <a name="next-steps"></a>Nästa steg

Alternativa metoder för att uppgradera klienter finns i [Distribuera klienter till Windows-datorer](../../deploy/deploy-clients-to-windows-computers.md).

Undanta vissa klienter från automatisk uppgradering. Mer information finns i [så här utesluter du klienter från uppgradering](exclude-clients-windows.md).
