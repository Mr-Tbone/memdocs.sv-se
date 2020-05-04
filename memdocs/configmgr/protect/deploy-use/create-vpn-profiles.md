---
title: Så här skapar du VPN-profiler
titleSuffix: Configuration Manager
description: Lär dig hur du skapar VPN-profiler i Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 17811d0bb0b72ebee6879d5dab90e165b439081b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713599"
---
# <a name="how-to-create-vpn-profiles-in-configuration-manager"></a>Så här skapar du VPN-profiler i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager stöder flera typer av VPN-anslutningar. Mer information om de anslutnings typer som är tillgängliga för de olika enhets plattformarna finns i [VPN-profiler](vpn-profiles.md).

För VPN-anslutningar från tredje part distribuerar du VPN-appen innan du distribuerar VPN-profilen. Om du inte distribuerar appen uppmanas användarna att göra det när de försöker ansluta till VPN-nätverket. Mer information finns i [distribuera program](../../apps/deploy-use/deploy-applications.md).

## <a name="create-a-vpn-profile"></a>Skapa en VPN-profil

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen **, expandera kompatibilitetsinställningar, expandera** **åtkomst till företags resurser**och välj noden **VPN-profiler** .

1. På fliken **Start** i menyfliksområdet väljer du **skapa VPN-profil**i gruppen **skapa** .

1. Ange följande information på sidan **Allmänt** i guiden Skapa VPN-profil:

    - **Namn**: Ange ett unikt namn för att identifiera VPN-profilen i-konsolen.

        > [!NOTE]
        > Använd inte följande tecken i VPN-profilens namn `\/:*?<>|; `:. Windows VPN-profilen har inte stöd för dessa specialtecken.

    - **Beskrivning**: du kan ange en beskrivning om du vill ange ytterligare information om VPN-profilen.

    - **VPN-profil typ**: Välj lämplig plattform.

        Om du väljer **Windows 8,1** -plattformen kan du också **Importera från en fil**. Den här åtgärden importerar VPN-profil information från en XML-fil. Om du väljer det här alternativet fören klar guiden resten av guiden till följande sidor: plattformar som **stöds** och **Importera VPN-profil**.

1. På sidan **plattformar som stöds** väljer du de OS-versioner som den här VPN-profilen stöder.

1. Ange följande information på sidan **anslutning** :

    - **Anslutnings typ**: Välj VPN-Anslutnings typ. Mer information om de typer som stöds finns i [VPN-profiler](vpn-profiles.md).

    - **Server lista**: Lägg till en ny server som ska användas för VPN-anslutningen. Beroende på anslutnings typen kan du lägga till en eller flera VPN-servrar och ange vilken server som är standard.

    - **Kringgå VPN vid anslutning till företagets nätverk**: Konfigurera klienter att inte använda VPN när de befinner sig i det interna nätverket. Om det behövs anger du ett anslutningsspecifikt DNS-namn.

1. På sidan **autentiseringsmetod** i guiden väljer du en metod som stöds av anslutnings typen. Inställningarna och de tillgängliga alternativen på den här sidan varierar beroende på vald Anslutnings typ. Mer information finns i [referens för autentiserings metoden](#bkmk_auth).

1. Om VPN använder en proxyserver på sidan **proxyinställningar** väljer du något av de alternativ som passar din miljö. Ange sedan konfigurations informationen för proxyservern.

1. Sidan **program** gäller endast för Windows 10-profiler. Lägg till Skriv bord och universella appar som automatiskt ansluter till den här VPN-anslutningen. Appens typ bestämmer appens identifierare:

    - För en *Skriv bords app*anger du appens fil Sök väg.

    - För en *universell app*anger du paket familje namnet (PFN). Information om hur du hittar PFN för en app finns i [hitta ett paket familje namn för per app-VPN](find-a-pfn-for-per-app-vpn.md).

    Du kan också konfigurera ett alternativ så att **endast apparna i listan kan använda det här VPN-nätverket**.

    > [!IMPORTANT]
    > Skydda alla listor över associerade appar som du kompilerar för att konfigurera en per app-VPN. Om en obehörig användare ändrar listan och du importerar den till listan per app-VPN-app, kan du tillåta VPN-åtkomst till appar som inte har åtkomst.

1. Sidan **gränser** gäller endast för Windows 10-profiler för att konfigurera VPN-gränser. Du kan lägga till följande alternativ:

    - **Regler för nätverks trafik**: Ange de protokoll, den lokala porten, den Fjärrport och de adress intervall som ska aktive ras för VPN-anslutningen.  

        > [!Note]
        > Om du inte skapar någon regel för nätverks trafik aktive ras alla protokoll, portar och adress intervall. När du har skapat en regel används bara de protokoll, portar och adress intervall som du anger i regeln eller i ytterligare regler som används av VPN-anslutningen.

    - **DNS-namn och servrar**: DNS-servrar som används av VPN-anslutningen när enheten upprättar anslutningen.

    - **Vägar**: nätverks vägar som använder VPN-anslutningen. Att skapa fler än 60 vägar kan leda till att principen Miss lyckas.

1. Slutför guiden.

Den nya VPN-profilen visas i noden **VPN-profiler** på arbetsytan **Tillgångar och efterlevnad** .

## <a name="authentication-method-reference"></a><a name="bkmk_auth"></a>Referens för autentiseringsmetod

Tillgängliga VPN-autentiseringsmetoder är beroende av anslutnings typen:

### <a name="certificates"></a>Certifikat

Om klient certifikatet autentiserar till en RADIUS-server, t. ex. en nätverks princip Server, anger du alternativt namn för certifikat mottagare i certifikatet till användarens huvud namn.

Anslutnings typer som stöds:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- Check Point Mobile VPN

### <a name="username-and-password"></a>Användarnamn och lösenord

Anslutnings typer som stöds:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- Check Point Mobile VPN

### <a name="microsoft-eap-ttls"></a>Microsoft EAP-TTLS

Anslutnings typer som stöds:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- PPTP
- IKEv2
- L2TP

### <a name="microsoft-protected-eap-peap"></a>Microsoft-skyddad EAP (PEAP

Anslutnings typer som stöds:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="microsoft-secured-password-eap-mschap-v2"></a>Microsoft-skyddat lösenord (EAP-MSCHAP v2)

Anslutnings typer som stöds:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="smart-card-or-other-certificate"></a>Smartkort eller annat certifikat

Anslutnings typer som stöds:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="mschap-v2"></a>MSCHAP v2

Anslutnings typer som stöds:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="use-machine-certificates"></a>Använd datorcertifikat

Anslutnings typer som stöds:

- IKEv2

### <a name="additional-authentication-options"></a>Ytterligare autentiseringsalternativ

När Windows-klienten har stöd för den är alternativet för att **Konfigurera** autentiseringsmetoden tillgängligt. Det här alternativet öppnar fönstret Windows-egenskaper för att konfigurera autentiseringsmetoden.

Beroende på vilka alternativ du väljer kan du bli ombedd att ange mer information, till exempel:

- **Spara autentiseringsuppgifterna för varje inloggning**: användarens autentiseringsuppgifter sparas så att användarna inte behöver ange dem varje gången de ansluter.  

- **Välj ett klient certifikat för klientautentisering**: Välj en tidigare skapad klient profil för SCEP-certifikat för att autentisera VPN-anslutningen. Mer information finns i [Skapa PFX-certifikat profiler](create-certificate-profiles.md).

## <a name="next-steps"></a>Nästa steg

- För VPN-anslutningar från tredje part distribuerar du VPN-appen innan du distribuerar VPN-profilen. Om du inte distribuerar appen uppmanas användarna att göra det när de försöker ansluta till VPN-nätverket. Mer information finns i [distribuera program](../../apps/deploy-use/deploy-applications.md).

- Distribuera VPN-profilen. Mer information finns i [så här distribuerar du profiler](deploy-wifi-vpn-email-cert-profiles.md).
