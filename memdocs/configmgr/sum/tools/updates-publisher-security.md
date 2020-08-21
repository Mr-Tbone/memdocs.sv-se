---
title: Certifikat och skydd
titleSuffix: Configuration Manager
description: Hantera certifikat och säkerhet för System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: a7f91e63-4750-402e-9970-dd14be7f76a3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dc8e31245212136cd67f6f8cac062723c2cabefb
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696012"
---
# <a name="manage-certificates-and-security-for-updates-publisher"></a>Hantera certifikat och säkerhet för Updates Publisher

*Gäller för: Configuration Manager (aktuell gren)*

Följande procedurer kan hjälpa dig att konfigurera certifikat arkivet på uppdaterings servern, konfigurera ett självsignerande certifikat på klient datorn och konfigurera grupprincip att tillåta att Windows Update-agenten på datorer söker efter publicerade uppdateringar.

## <a name="configure-the-certificate-store-on-the-update-server"></a>Konfigurera certifikat arkivet på uppdaterings servern
 Updates Publisher använder ett digitalt certifikat för att signera uppdateringarna i de kataloger som publiceras. Innan en katalog kan publiceras på uppdaterings servern måste certifikatet finnas i certifikat arkivet på uppdaterings servern och i certifikat arkivet för Updates Publisher-datorn om datorn är fjärran sluten till uppdaterings servern.

Följande procedur är en av flera olika metoder för att lägga till certifikatet i certifikat arkivet på uppdaterings servern.

### <a name="to-configure-the-certificate-store"></a>Konfigurera certifikat arkivet
1.  På en dator som har åtkomst till både Updates Publisher-datorn och uppdaterings servern klickar du på **Start**, klicka på **Kör**, Skriv **MMC** i text rutan och klicka sedan på **OK** för att öppna Microsoft Management Console (MMC).

2.  Klicka på **Arkiv**, klicka på **Lägg till/ta bort snapin-modul**, klicka på **Lägg till**, klicka på **certifikat**, klicka på **Lägg till**, Välj **dator konto**och klicka sedan på **Nästa**.

3.  Välj **en annan dator**, ange namnet på uppdaterings servern eller klicka på **Bläddra** för att hitta uppdaterings serverns dator, klicka på **Slutför**, klicka på **Stäng**och klicka sedan på **OK**.

4.  Expandera **certifikat (*uppdaterings serverns namn*)**, expandera **WSUS**och klicka sedan på **certifikat**.

5.  Högerklicka på önskat certifikat i resultat fönstret, klicka på **alla aktiviteter**och klicka sedan på **Exportera**.

6.  I guiden Exportera certifikat använder du standardinställningarna för att skapa en export fil med namnet och platsen som anges i guiden. Den här filen måste vara tillgänglig för uppdaterings servern innan du fortsätter till nästa steg.

7.  Högerklicka på **Betrodda utgivare**, klicka på **alla uppgifter**och klicka sedan på **Importera**. Slutför guiden Importera certifikat med hjälp av den exporterade filen från steg 6.

8.  Om ett självsignerat certifikat används, till exempel **själv signerade WSUS-utgivare**, högerklickar du på **betrodda rot certifikat utfärdare**, klickar på **alla uppgifter**och klickar sedan på **Importera**. Slutför guiden Importera certifikat med hjälp av den exporterade filen från steg 6.

9.  Högerklicka på **certifikat (*uppdaterings Server namn*)**, klicka på **Anslut till en annan dator**, ange dator namnet för Updates Publisher-datorn och klicka på **OK**.

10. Om Updates Publisher är fjärran sluten till uppdaterings servern upprepar du steg 7 till och med 9 för att importera certifikatet till certifikat arkivet på den Updates Publisher-datorn.



## <a name="configure-a-self-signing-certificate-on-client-computers"></a>Konfigurera ett självsignerat certifikat på klient datorer
På klient datorer genomsöker Windows Update Agent (WUA) efter uppdateringarna från katalogen. Den här processen kommer inte att kunna installera uppdateringar om agenten inte kan hitta det digitala certifikatet i arkivet Betrodda utgivare på den lokala datorn. Om ett självsignerat certifikat har använts för att publicera uppdaterings katalogen, t. ex. **själv signerade WSUS-utgivare**, måste certifikatet också finnas i certifikat arkivet Betrodda rot certifikat utfärdare på den lokala datorn så att agenten kan verifiera certifikatets giltighet.

Du kan använda en av flera metoder för att konfigurera certifikat på klient datorer, t. ex. genom att använda grupprincip och **guiden Importera certifikat** eller med hjälp av Certutil-verktyget och program distribution.

Följande finns som ett exempel på hur du konfigurerar signerings certifikatet på klient datorer.

### <a name="to-configure-a-self-signing-certificate-on-client-computers"></a>Konfigurera ett självsignerat certifikat på klient datorer
1. Klicka på **Start**på en dator med åtkomst till uppdaterings servern, klicka på **Kör**, Skriv **MMC** i text rutan och klicka sedan på **OK** för att öppna Microsoft Management Console (MMC).

2. Klicka på **Arkiv**, klicka på **Lägg till/ta bort snapin-modul**, klicka på **Lägg till**, klicka på **certifikat**, klicka på **Lägg till**, Välj **dator konto**och klicka sedan på **Nästa**.

3. Välj **en annan dator**, ange namnet på uppdaterings servern eller klicka på **Bläddra** för att hitta uppdaterings serverns dator, klicka på **Slutför**, klicka på **Stäng**och klicka sedan på **OK**.

4. Expandera **certifikat (*uppdaterings serverns namn*)**, expandera **WSUS**och klicka sedan på **certifikat**.

5. Högerklicka på certifikatet i resultat fönstret, klicka på **alla aktiviteter**och klicka sedan på **Exportera**. Slutför **guiden Exportera certifikat** med hjälp av standardinställningarna för att skapa en export certifikat fil med det namn och den plats som anges i guiden.

6. Använd någon av följande metoder för att lägga till certifikatet som används för att signera uppdaterings katalogen på varje klient dator som ska använda WUA för att söka efter uppdateringar i katalogen. Lägg till certifikatet på klient datorn enligt följande:

   -   För självsignerade certifikat: Lägg till certifikatet i certifikat Arkiv för **betrodda rot certifikat utfärdare** och **Betrodda utgivare** .

   -   För certifikat utfärdare (CA) utfärdade certifikat: Lägg till certifikatet i certifikat arkivet **Betrodda utgivare** .

   > [!NOTE]
   > WUA kontrollerar också om inställningen **Tillåt signerat innehåll från tjänsten Microsoft Update på intranätet** Grupprincip är aktive rad på den lokala datorn. Denna principinställning måste aktiveras för att Windows Update-agenten ska söka efter de uppdateringar som har skapats och publicerats med Updates Publisher. Mer information om hur du aktiverar den här grupprincip inställningen finns i [så här konfigurerar du Grupprincip på klient datorer](/previous-versions/bb530967(v=technet.10)).



## <a name="configuring-group-policy-to-allow-wuaon-computers-to-scan-for-published-updates"></a>Konfigurera grupprincip för att tillåta WUA på datorer att söka efter publicerade uppdateringar
Innan Windows Update Agent (WUA) på datorer söker efter uppdateringar som har skapats och publicerats med Updates Publisher, måste en princip inställning aktive ras för att tillåta signerat innehåll från en Microsoft-uppdateringstjänst på intranätet. När den här inställningen är aktive rad accepterar WUA uppdateringar som tas emot via en intranät plats om uppdateringarna är signerade i certifikat arkivet **Betrodda utgivare** på den lokala datorn. Det finns flera metoder för att konfigurera grupprincip på datorer i miljön.

För datorer som inte finns i domänen kan en register nyckel inställning konfigureras som tillåter signerat innehåll från ett intranät Microsoft Update tjänstens plats.

Följande procedurer innehåller grundläggande steg som kan användas för att konfigurera grupprincip för datorer i domänen och ett register nyckel värde på datorer som inte finns i domänen.

### <a name="to-configure-group-policy-to-allow-wua-to-scan-for-published-updates"></a>Så här konfigurerar du grupprincip så att WUA kan söka efter publicerade uppdateringar
1.  Öppna snapin-modulen Redigeraren för grupprincipobjekt Microsoft Management Console (MMC) med en användare som har rätt behörighet för att konfigurera grupprincip.

2.  Klicka på **Bläddra** och välj den domän, organisationsenhet eller de grup princip objekt som är länkade till den plats där den konfigurerade Grupprincip kommer att spridas till önskade klient datorer. Klicka på **OK**, klicka på **Slutför**, klicka på **Stäng**och klicka sedan på **OK**.

3.  Expandera den valda princip inställningen i konsol trädet, expandera **dator konfiguration**, expandera **administrativa mallar**, expandera **Windows-komponenter**och klicka sedan på **Windows Update**.

4.  I resultat fönstret högerklickar du på **Tillåt signerat innehåll från tjänsten Microsoft Update på intranätet**, klickar på **Egenskaper**, klicka på **aktive rad**och sedan på **OK**.