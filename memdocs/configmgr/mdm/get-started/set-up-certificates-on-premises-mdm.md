---
title: Certifikat för lokal MDM
titleSuffix: Configuration Manager
description: Konfigurera certifikat för betrodd kommunikation med lokal hantering av mobila enheter (MDM) i Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 2a7d7170-1933-40e9-96d6-74a6eb7278e2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc63a21970bb522407c86d027690b83894b3cb99
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721831"
---
# <a name="set-up-certificates-for-trusted-communications-with-on-premises-mdm"></a>Konfigurera certifikat för betrodd kommunikation med lokal MDM

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager lokal hantering av mobila enheter (MDM) kräver att du konfigurerar plats system roller för betrodd kommunikation med hanterade enheter. Du behöver två typer av certifikat:

- Ett **webb server certifikat** i IIS på de servrar som är värd för de nödvändiga plats system rollerna. Om en server är värd för flera plats system roller behöver du bara ett certifikat för den servern. Om varje roll finns på en separat server behöver varje server ett separat certifikat.

- Det **betrodda rot certifikatet** för den certifikat utfärdare (ca) som utfärdar webb server certifikaten. Installera det här rot certifikatet på alla enheter som måste ansluta till plats system rollerna.

Om du använder Active Directory certifikat tjänster för domänanslutna enheter, kan dessa certifikat installeras automatiskt på alla enheter. För icke-domänanslutna enheter installerar du det betrodda rot certifikatet på något annat sätt.

För Mass registrering av enheter kan du inkludera certifikatet i registrerings paketet. För användarregistrerade enheter måste du lägga till certifikatet via e-post, nedladdning från webben eller på något annat sätt.

Om du använder en välkänd offentlig certifikat utfärdare som VeriSign eller GoDaddy för att utfärda Server certifikat, kan du undvika att behöva installera det betrodda rot certifikatet manuellt på varje enhet. De flesta enheter litar internt på dessa offentliga myndigheter. Den här metoden är ett användbart alternativ för användar registrerade enheter, i stället för att installera certifikatet på annat sätt.

> [!IMPORTANT]  
> Det finns många sätt att ställa in certifikat för betrodd kommunikation mellan enheter och plats system servrar för lokal MDM. Informationen i den här artikeln är ett exempel på ett sätt att göra det. Den här metoden kräver Active Directory certifikat tjänster, med en certifikat utfärdare och webb registrerings rollen för certifikat utfärdare. Mer information finns i [Active Directory Certificate Services](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831740\(v=ws.11\)).

## <a name="publish-the-crl"></a><a name="bkmk_configCa"></a>Publicera CRL

Som standard använder Active Directory certifikat utfärdare (CA) LDAP-baserade listor över återkallade certifikat (CRL). Den tillåter anslutningar till listan över återkallade certifikat för domänanslutna enheter. Lägg till en HTTP-baserad CRL om du vill att icke-domänanslutna enheter ska kunna lita på certifikat som utfärdats från certifikat utfärdaren.

1. På den server som kör certifikat utfärdaren för platsen går du till **Start** -menyn, väljer **administrations verktyg**och väljer **certifikat utfärdare**.

1. I konsolen för certifikat utfärdare högerklickar du på **utfärdare**och väljer sedan **Egenskaper**.

1. I utfärdare-egenskaper växlar du till fliken **tillägg** . kontrol lera att **Select Extension** är inställt på **distributions punkt för CRL (CDP)**.

1. Välj `http://<ServerDNSName>/CertEnroll/<CAName><CRLNameSuffix><DeltaCRLAllowed>.crl`. Välj sedan följande alternativ:

    - **Ta med i listor över återkallade certifikat. klienter använder detta för att hitta platser för att delta**

    - **Ta med i CDP-tillägget för utgivna certifikat.**

    - **Ta med i IDP-tillägget i utfärdade listor över återkallade certifikat**

1. Växla till fliken **Avsluta modul** . Välj **Egenskaper**och välj sedan **Tillåt att certifikat publiceras till fil systemet**. Du ser ett meddelande om att starta om Active Directory Certificate Services.

1. Högerklicka på **återkallade certifikat**, Välj **alla aktiviteter**och välj sedan **publicera**.

1. I fönstret publicera CRL väljer du **endast delta-CRL**och väljer sedan **OK** för att stänga fönstret.

## <a name="create-the-certificate-template"></a><a name="bkmk_certTempl"></a>Skapa certifikat mal len

CA: n använder webb server certifikat mal len för att utfärda certifikat för de servrar som är värdar för plats system rollerna. Dessa servrar kommer att vara SSL-slutpunkter för betrodd kommunikation mellan plats system rollerna och registrerade enheter.

1. Skapa en domän säkerhets grupp med namnet **CONFIGMGR MDM-servrar**. Lägg till i gruppen dator kontona för plats system servrarna.

1. Högerklicka på **certifikatmallar**i konsolen certifikat utfärdare och välj **Hantera**. Den här åtgärden laddar konsolen Certifikatmallar.

1. I resultat fönstret högerklickar du på posten som visar **webb server** i kolumnen **mallens visnings namn** och väljer sedan **Duplicera mall**.

1. I fönstret **Duplicera mall** väljer du **Windows 2003 Server, Enterprise edition** eller **Windows 2008 Server, Enterprise Edition**och väljer sedan **OK**.

    > [!TIP]
    > Configuration Manager stöder mallar för Windows 2008 Server-certifikat, även kallat v3 eller kryptografi: Next Generation (CNG)-certifikat. Mer information finns i [Översikt över CNG-certifikat](../../core/plan-design/network/cng-certificates-overview.md).

    Om din certifikat utfärdare körs på Windows Server 2012 eller senare, visar det här fönstret inte alternativet för att välja version av certifikatmall. När du har duplicerat mallen väljer du versionen på fliken **kompatibilitet** för mallens egenskaper.

1. I fönstret **Egenskaper för ny mall** går du till fliken **Allmänt** och anger ett Mallnamn. CA: n använder det här namnet för att generera de webb certifikat som ska användas på Configuration Manager plats system. Skriv till exempel **CONFIGMGR MDM-webb server**.

1. Växla till fliken **namn på certifikat mottagare** och välj **build från Active Directory information**. För ämnes namnets format anger du **DNS-namn**. Om **användarens huvud namn (UPN)** är markerat inaktiverar du alternativet för alternativt ämnes namn.

1. Växla till fliken **säkerhet** .

    1. Ta bort behörigheten **Registrera** från säkerhets grupperna **domän administratörer** och **företags administratörer** .

    1. Välj **Lägg till**och ange namnet på din säkerhets grupp. Till exempel **CONFIGMGR MDM-servrar**. Välj **OK** för att stänga fönstret.

    1. Välj behörigheten **Registrera** för den här gruppen. Ta inte bort behörigheten **läsa** .

1. Välj **OK** för att spara ändringarna och Stäng konsolen Certifikatmallar.

1. Högerklicka på **certifikatmallar**i konsolen certifikat utfärdare, Välj **ny**och välj sedan **certifikatmall som ska utfärdas**.

1. I fönstret **Aktivera certifikatmallar** väljer du den nya mallen. Till exempel **webb server för CONFIGMGR MDM**. Välj **OK** för att spara och stänga fönstret.

## <a name="request-the-certificate"></a><a name="bkmk_requestCert"></a>Begär certifikatet

I den här processen beskrivs hur du begär webb Server certifikatet för IIS. Gör den här processen för varje plats system server som är värd för en av rollerna för lokal MDM.

1. Öppna en kommando tolk som administratör på den plats system server som är värd för en av rollerna. Ange `mmc` för att öppna en tom Microsoft Management-konsol.

1. I konsol fönstret går du till **Arkiv** -menyn och väljer **Lägg till/ta bort snapin-modul**.

    1. Välj **certifikat** i listan över tillgängliga snapin-moduler och välj **Lägg till**.

    1. I snapin-fönstret certifikat väljer du **dator konto**. Välj **Nästa**och välj sedan **Slutför** för att hantera den lokala datorn.

    1. Välj **OK** för att stänga fönstret Lägg till eller ta bort snapin-modul.

1. Expandera **certifikat (lokal dator)** och välj det **personliga** arkivet. Gå till **åtgärd** -menyn, Välj **alla aktiviteter**och välj **Begär nytt certifikat**. Den här åtgärden kommunicerar med Active Directory certifikat tjänster för att skapa ett nytt certifikat med hjälp av mallen som du skapade tidigare.

    1. Välj **Nästa**på sidan innan du börjar i guiden för certifikat registrering.

    1. På sidan Välj princip för certifikat registrering väljer du **Active Directory registrerings princip**och väljer sedan **Nästa**.

    1. Välj webb server certifikat mal len (**CONFIGMGR MDM-webbserver**) och välj sedan **Registrera**.

    1. När certifikatet har begärts väljer du **Slutför**.

Varje server behöver ett unikt webb server certifikat. Upprepa den här processen för varje server som är värd för en av de nödvändiga plats system rollerna. Om en server är värd för alla platssystemroller behöver du bara begära ett webbservercertifikat.

## <a name="bind-the-certificate"></a><a name="bkmk_bindCert"></a>Bind certifikatet

Nästa steg är att binda det nya certifikatet till webb servern. Följ den här processen för varje server som är värd för *registrerings platsen* och plats system roller för *proxyservern* . Om en server är värd för alla plats system roller behöver du bara utföra den här processen en gång.

> [!NOTE]
> Du behöver inte göra detta för plats system rollerna för distributions platsen och enhets hanterings platsen. De får automatiskt det begärda certifikatet under registreringen.

1. På den server som är värd för registrerings platsen eller proxyn för registrerings platsen går du till **Start** -menyn, väljer **administrations verktyg**och väljer **IIS-hanteraren**.

1. Välj **standard webbplatsen**i listan över anslutningar och välj sedan **Redigera bindningar**.

    1. I fönstret webbplats bindningar väljer du **https**och väljer sedan **Redigera**.

    1. I fönstret Redigera bindning för webbplats väljer du det nyligen registrerade certifikatet för **SSL-certifikatet**. Välj **OK** för att spara och välj sedan **Stäng**.

1. I konsolen IIS-hanteraren, i listan över anslutningar, väljer du webb servern. I Åtgärds panelen på höger sida väljer du **starta om**. Den här åtgärden startar om webb Server tjänsten.

## <a name="export-the-trusted-root-certificate"></a><a name="bkmk_exportCert"></a>Exportera det betrodda rot certifikatet

Active Directory Certificate Services installerar automatiskt det begärda certifikatet från certifikat utfärdaren på alla domänanslutna enheter. Om du vill hämta det certifikat som krävs för icke-domänanslutna enheter för att kommunicera med plats system rollerna kan du exportera det från certifikatet som är kopplat till webb servern.

1. I IIS-hanteraren väljer du **standard webbplatsen**. I Åtgärds panelen på höger sida väljer du **bindningar**.

1. Välj **https**i fönstret webbplats bindningar och välj sedan **Redigera**.

1. Välj webb server certifikat och välj **Visa**.

1. I egenskaperna för webb Server certifikatet växlar du till fliken **certifierings Sök väg** . Välj rot för certifierings Sök vägen och välj **Visa certifikat**.

1. I egenskaperna för rot certifikatet växlar du till fliken **information** och väljer sedan **Kopiera till fil**.

1. I guiden Exportera certifikat väljer du **Nästa**på sidan Välkommen.

1. Välj **der-kodad binär X. 509 (. CER)** som format och välj **Nästa**.

1. Ange en sökväg och ett fil namn för att identifiera det betrodda rot certifikatet. För fil namnet klickar du på **Bläddra...**, väljer en plats där du vill spara certifikat filen, namnger filen och väljer **Nästa**.

1. Granska inställningarna och välj **Slutför** för att exportera certifikatet till filen.

Beroende på din design för certifikat utfärdare kan du behöva exportera ytterligare underordnade certifikat utfärdares rot certifikat. Upprepa den här processen för att exportera de andra certifikaten i webb server certifikatets certifierings Sök väg.

## <a name="next-step"></a>Nästa steg

> [!div class="nextstepaction"]
> [Konfigurera registrering av enheter](set-up-device-enrollment-on-premises-mdm.md)
