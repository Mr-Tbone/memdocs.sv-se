---
title: Konfigurera Wake on LAN
titleSuffix: Configuration Manager
description: Välj Wake On LAN inställningar i Configuration Manager.
ms.date: 08/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 33283b13bc28c7d102f014ac3cb4048681343ac2
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907855"
---
# <a name="how-to-configure-wake-on-lan-in-configuration-manager"></a>Så här konfigurerar du Wake on LAN i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Ange inställningar för Wake-on-LAN för Configuration Manager när du vill ta bort datorer från vilo läge.

## <a name="wake-on-lan-starting-in-version-1810"></a><a name="bkmk_wol-1810"></a> Wake on LAN som börjar i version 1810
<!--3607710-->
Från och med Configuration Manager 1810 är det ett nytt sätt att aktivera datorer i vilo läge. Du kan aktivera klienter från Configuration Manager-konsolen även om klienten inte finns i samma undernät som plats servern. Om du behöver utföra underhåll eller fråga enheter är du inte begränsad av fjärranslutna klienter som är i ström spar läge. Plats servern använder klient aviserings kanalen för att identifiera andra klienter som är aktiva på samma fjärrundernät och använder sedan dessa klienter för att skicka en Wake-on-LAN-begäran (Magic Packet). Genom att använda klienten meddelande kanal kan du undvika MAC-klaffar som kan orsaka att porten stängs av av routern. Den nya versionen av Wake on LAN kan aktive ras samtidigt som den [äldre versionen](#bkmk_wol-previous).

### <a name="prerequisites-and-limitations"></a>Krav och begränsningar
<!--7323898, 7363492-->
- Minst en klient i mål under nätet måste vara aktiv.
- Den här funktionen har inte stöd för följande nät verks tekniker:
   - IPv6
   - 802.1 x-nätverksautentisering
    >[!NOTE]
    > 802.1 x-nätverksautentisering kan fungera med ytterligare konfiguration beroende på maskin vara och dess konfiguration.
- Datorer som bara aktive ras när du meddelar dem genom **aktivering** av klient meddelanden.
    - För aktivering när ett tids gräns inträffar används den äldre versionen av Wake on LAN.
    -  Om den äldre versionen inte är aktive rad sker inte klient aktivering för distributioner som skapats med inställningarna **Använd Wake-on-LAN för att väcka klienter för nödvändiga distributioner** eller **Skicka väcknings paket**.  
- Varaktigheten för DHCP-lån får inte vara oändligt. <!--8018584-->
   - Du kan se att SleepAgent_ &lt; *domain* \> @SYSTEM_0.log -domänen blir mycket stor och eventuellt en sändning storm i miljöer där DHCP-lån är inställda på oändligt.  

### <a name="security-role-permissions"></a>Säkerhets roll behörigheter

- **Meddela resurs** under kategorin samling

### <a name="configure-the-clients-to-use-wake-on-lan-starting-in-version-1810"></a>Konfigurera klienterna så att de använder Wake on LAN från och med version 1810

Tidigare var du tvungen att manuellt aktivera klienten för Wake-on-LAN i egenskaperna för nätverkskortet. Configuration Manager 1810 innehåller en ny klient inställning som kallas **Tillåt nätverks aktivering**. Konfigurera och distribuera den här inställningen i stället för att ändra egenskaperna för nätverkskortet.

1. Under **Administration**, gå till **klient inställningar**.
1. Välj de klient inställningar som du vill redigera eller skapa nya anpassade klient inställningar som ska distribueras. Mer information finns i [så här konfigurerar du klient inställningar](configure-client-settings.md).
1. Under klient inställningarna för **energispar funktioner** väljer du **Aktivera** för inställningen **Tillåt nätverks aktivering** . Mer information om den här inställningen finns i [om klient inställningar](about-client-settings.md#power-management).

4. Från och med Configuration Manager 1902, gör den nya versionen av Wake-on-LAN den anpassade UDP-port som du anger för [klient inställningen](about-client-settings.md#power-management) **Wake on LAN port number (UDP)** . Den här inställningen delas av både den nya och äldre versionen av Wake on LAN.
 
<!--3605925-->

### <a name="wake-up-a-client-using-client-notification-starting-in-1810"></a>Aktivera en klient med hjälp av klient meddelanden från 1810
 
Du kan aktivera en enskild klient eller alla klienter i vilo läge i en samling. Ingen åtgärd vidtas för enheter som redan är aktiva i samlingen. Endast klienter som är i ström spar läge kommer att skickas till en Wake-on-LAN-begäran. Mer information om hur du meddelar en klient att aktivera finns i [klient meddelande](../manage/client-notification.md).

- **Så här aktiverar du en enskild klient:** Högerklicka på klienten, gå till **klient meddelande**och välj sedan **Aktivera**.

   ![Aktivera klient meddelanden i-konsolen](media/wol-wake-up-client-notification.png)

- **Så här aktiverar du alla klienter i vilo läge i en samling:** Högerklicka på enhets samlingen, gå till **klient meddelande**och välj sedan **Aktivera**.
   - Den här åtgärden kan inte köras på inbyggda samlingar.
   - När du har en blandning av ström-och aktiva klienter i en samling skickas endast klienter som är i ström spar läge till en Wake on LAN-begäran.
   - Från och med Configuration Manager 2002 är åtgärden tillgänglig från en konsol som är ansluten till en central administrations plats, en fristående plats eller en underordnad primär plats.
   - I version 1910 och tidigare är den här åtgärden endast aktiv när Configuration Manager-konsolen är ansluten till en fristående eller underordnad primär plats. Åtgärden är inte tillgänglig när du är ansluten till en central administrations plats.

### <a name="what-to-expect-when-only-the-new-version-of-wake-on-lan-is-enabled"></a>Vad som ska förväntas när endast den nya versionen av Wake-on-LAN är aktive rad

Om du bara har den nya versionen av Wake on LAN aktiverat, är det bara **aktiverings** klientens avisering aktive rad. Klienterna skickas inget meddelande när en tids gräns tas emot vid distributioner, till exempel aktivitetssekvenser, program varu distribution eller installation av program uppdateringar. När en vilande dator är online igen visas den i-konsolen när den checkar in med hanterings platsen.

Från och med Configuration Manager version 1902 kan du ange Wake-on-LAN-porten. Den här inställningen delas av både den nya och äldre versionen av Wake on LAN.

### <a name="what-to-expect-when-both-versions-of-wake-on-lan-are-enabled"></a>Vad som ska förväntas när båda versionerna av Wake on LAN är aktiverade

Om båda versionerna av Wake on LAN är aktiverade kan du använda meddelande om **aktivering** av klient och väckning på tids gränsen. Klient aviseringen fungerar lite annorlunda än traditionell Wake on LAN. En kort förklaring av hur klient aviseringen fungerar finns i avsnittet [Wake on LAN från och med version 1810](#bkmk_wol-1810) . Med den nya klient inställningen **Tillåt nätverks aktivering** ändras nätverkskortets egenskaper för att tillåta Wake on LAN. Du behöver inte längre ändra den manuellt för nya datorer som läggs till i din miljö. Alla andra funktioner i Wake on LAN har inte ändrats.

Från och med version 1902, meddelas den befintliga inställningen för **Wake on LAN port number (UDP)** i **aktiverings** klienten.


## <a name="wake-on-lan-for-version-1806-and-earlier"></a><a name="bkmk_wol-previous"></a>  Wake on LAN för version 1806 och tidigare

Ange inställningar för Wake-on-LAN för Configuration Manager när du vill att datorer ska vara i vilo läge för att installera nödvändig program vara, t. ex. program varu uppdateringar, program, aktivitetssekvenser och program.

Du kan komplettera Wake on LAN genom att använda klient inställningarna för Wake-up-proxy. Men om du vill använda Wake-up-proxy måste du först aktivera Wake on LAN för platsen och ange **Använd endast väcknings paket** och alternativet **unicast** för överförings metoden Wake on LAN. Den här aktiverings lösningen stöder även ad hoc-anslutningar, till exempel en fjärr skrivbords anslutning.

Använd den första proceduren för att konfigurera en primär plats för Wake on LAN. Använd sedan den andra proceduren för att konfigurera klient inställningarna för Wake-up-proxy. Den här andra proceduren konfigurerar standard klient inställningarna för inställningarna för Väcknings proxy som ska gälla för alla datorer i hierarkin. Om du vill att inställningarna bara ska gälla för valda datorer skapar du en anpassad enhets inställning och tilldelar den till en samling som innehåller de datorer som du vill konfigurera för Wake-up-proxy. Mer information om hur du skapar anpassade klient inställningar finns i [Konfigurera klient inställningar](../../../core/clients/deploy/configure-client-settings.md).

En dator som tar emot klient inställningarna för Wake-up-proxy kommer förmodligen att pausa sin nätverks anslutning i 1-3 sekunder. Detta inträffar eftersom klienten måste återställa nätverkskortet för att aktivera driv rutinen för Wake-up-proxy på den.

> [!WARNING]
> För att undvika oväntade avbrott i dina nätverks tjänster börjar du med att utvärdera aktiverings-proxyn på en isolerad och representativ nätverks infrastruktur. Använd sedan anpassade klient inställningar för att utöka testet till en vald grupp datorer på flera undernät. Mer information om hur Wake-up proxy fungerar finns i [Planera aktivering av klienter](../../../core/clients/deploy/plan/plan-wake-up-clients.md).


### <a name="to-configure-wake-on-lan-for-a-site-for-version-1806-and-earlier"></a>Konfigurera Wake on LAN för en plats för version 1806 och tidigare

 Om du vill använda Wake on LAN måste du aktivera det för varje plats i en hierarki.

1. I Configuration Manager-konsolen går du till **Administration > plats konfiguration > platser**.
2. Klicka på den primära plats som ska konfigureras och klicka sedan på **Egenskaper**.
3. Klicka på fliken **Wake on LAN** och konfigurera de alternativ som krävs för den här platsen. För att stödja Wake-up-proxy, se till att du väljer **Använd endast väcknings paket** och **unicast**. Mer information finns i [Planera aktivering av klienter](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. Klicka på **OK** och upprepa proceduren för alla primära platser i hierarkin.

![Aktivera Wake On LAN i plats egenskaperna](media/wol-site-properties.png)

### <a name="to-configure-wake-up-proxy-client-settings"></a>Konfigurera klient inställningar för Wake-up-proxy

1. I Configuration Manager-konsolen går du till **Administration > klient inställningar**.
2. Klicka på **Inställningar för standard klient**och klicka sedan på **Egenskaper**.
3. Välj **energispar funktioner** och välj sedan **Ja** för **Aktivera Wake-up-proxy**.
4. Granska och om det behövs kan du konfigurera de andra inställningarna för Wake-up-proxy. Mer information om de här inställningarna finns i [Inställningar för energispar funktioner](../../../core/clients/deploy/about-client-settings.md#power-management).
5. Klicka på **OK** för att stänga dialog rutan och klicka sedan på **OK** för att stänga dialog rutan inställningar för standard klient.

Du kan använda följande Wake On LAN rapporter för att övervaka installationen och konfigurationen av Wake-up-proxy:

- Sammanfattning av distributionstillståndet för aktiveringsproxy
- Information om distributionstillstånd för aktiveringsproxy

> [!TIP]
> Testa en anslutning till en dator i vilo läge för att testa om aktivering av proxyn fungerar. Du kan till exempel ansluta till en delad mapp på den datorn eller försöka ansluta till datorn med hjälp av fjärr skrivbord. Om du använder direkt åtkomst kontrollerar du att IPv6-prefixen fungerar genom att testa samma test för en dator som är i vilo läge och som finns på Internet.
