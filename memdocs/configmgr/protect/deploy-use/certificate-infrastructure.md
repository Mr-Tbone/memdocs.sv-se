---
title: Konfigurera infrastrukturen för certifikat
titleSuffix: Configuration Manager
description: Lär dig hur du konfigurerar certifikat registrering i Configuration Manager.
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 656cc80c929eb7e829dd06b642a83cb174d3b0c8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697253"
---
# <a name="configure-certificate-infrastructure"></a>Konfigurera infrastrukturen för certifikat

*Gäller för: Configuration Manager (aktuell gren)*

Lär dig hur du konfigurerar certifikat infrastruktur i Configuration Manager. Innan du börjar ska du kontrol lera om det finns krav som anges i [krav för certifikat profiler](../../protect/plan-design/prerequisites-for-certificate-profiles.md).  

Använd de här stegen för att konfigurera din infrastruktur för SCEP-eller PFX-certifikat.

## <a name="step-1---install-and-configure-the-network-device-enrollment-service-and-dependencies-for-scep-certificates-only"></a>Steg 1 – Installera och konfigurera registrerings tjänsten för nätverks enheter och beroenden (endast för SCEP-certifikat)

 Du måste installera och konfigurera rolltjänsten Registreringstjänsten för nätverksenheter för Active Directory-certifikattjänster (AD CS), ändra säkerhetsbehörigheterna för certifikatmallarna, distribuera ett PKI-klientautentiseringscertifikat (Public Key Infrastructure) och redigera registret för att öka standardgränsen för storleken på IIS-webbadressen (Internet Information Services). Om det behövs måste du också konfigurera den aktuella certifikatutfärdaren för att tillåta en anpassad giltighetstid.  

> [!IMPORTANT]  
>  Innan du konfigurerar Configuration Manager att arbeta med registrerings tjänsten för nätverks enheter kontrollerar du installationen och konfigurationen av registrerings tjänsten för nätverks enheter. Om dessa beroenden inte fungerar som de ska får du svårt att felsöka certifikat registreringen med hjälp av Configuration Manager.  

### <a name="to-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>Installera och konfigurera registreringstjänsten för nätverksenheter och beroenden  

1. Installera och konfigurera rolltjänsten Registreringstjänsten för nätverksenheter för serverrollen Active Directory-certifikattjänster på en server som kör Windows Server 2012 R2. Mer information finns i [rikt linjer för registrerings tjänsten för nätverks enheter](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498\(v=ws.11\)).

2. Kontrollera och, om det behövs, ändra säkerhetsbehörigheten för de certifikatmallar som används i registreringstjänsten för nätverksenheter.  

   -   För det konto som kör Configuration Manager-konsolen: **Läs** behörighet.  

        Den här behörigheten krävs för att du, när du kör guiden Skapa certifikatprofil, ska kunna bläddra och välja den certifikatmall du vill använda när du skapar en SCEP-inställningsprofil. När du väljer en certifikatmall fylls vissa inställningar i guiden i automatiskt vilket innebär att du får mindre att konfigurera och det är mindre risk att du väljer inställningar som inte är kompatibla med de certifikatmallar som används i registreringstjänsten för nätverksenheter.  

   -   För det SCEP-tjänstkonto som används i programpoolen för registreringstjänsten för nätverksenheter: behörigheterna **Läs** och **Registrera**.  

        Detta krav är inte bara för Configuration Manager men är en del av konfigurationen av registrerings tjänsten för nätverks enheter. Mer information finns i [rikt linjer för registrerings tjänsten för nätverks enheter](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498\(v=ws.11\)).  

   > [!TIP]  
   >  Du kan se vilka certifikatmallar som används i registreringstjänsten för nätverksenheter med hjälp av följande registernyckel på den server som kör registreringstjänsten för nätverksenheter: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP.  

   > [!NOTE]  
   >  De här är standardsäkerhetsbehörigheterna som lämpar sig för de flesta miljöer. Du kan också använda en alternativ säkerhetskonfiguration. Mer information finns i [Planera för certifikat mal len behörigheter för certifikat profiler](../../protect/plan-design/planning-for-certificate-template-permissions.md).  

3. Distribuera ett PKI-certifikat som har stöd för klientautentisering på den här servern. Du kanske redan har ett passande certifikat på datorn som du kan använda eller också måste du (eller föredrar du) att distribuera ett certifikat för just detta ändamål. Mer information om kraven för det här certifikatet finns i informationen om servrar som kör Configuration Manager-Principmodulen med roll tjänsten för registrerings tjänsten för nätverks enheter i avsnittet **PKI-certifikat för servrar** i avsnittet [PKI-certifikat krav för Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md) .  

   > [!TIP]
   >  Om du behöver hjälp med att distribuera det här certifikatet kan du använda anvisningarna för [att distribuera klient certifikatet för distributions platser](../../core/plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012), eftersom certifikat kraven är desamma, med ett undantag:  
   > 
   > - Markera inte kryssrutan **Tillåt att den privata nyckeln exporteras** på fliken **Hantering av begäranden** i egenskaperna för certifikatmallen.  
   > 
   >   Du behöver inte exportera det här certifikatet med den privata nyckeln eftersom du kommer att kunna bläddra till den lokala datorns Arkiv och välja det när du konfigurerar Configuration Manager-principmodulen.  

4. Leta upp det rotcertifikat som ingår i samma kedja som klientautentiseringscertifikatet. Exportera sedan rotcertifikatet till en certifikatfil (.cer). Spara filen på en skyddad plats som du kan nå på ett säkert sätt när du senare installerar och konfigurerar platssystemservern för certifikatregistreringsplatsen.  

5. På samma server använder du registereditorn för att öka standardstorleksgränsen för IIS-webbadressen genom att ange värden för registernyckeln DWORD i HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters:  

   - Ställ in nyckeln **MaxFieldLength** på **65534**.  

   - Ställ in nyckeln **MaxRequestBytes** på**16777216**.  

     Mer information finns i Microsoft Support artikel [820129: Http.sys register inställningar för Windows](https://support.microsoft.com/help/820129).

6. På samma server går du till IIS-hanteraren (Internet Information Services), ändrar begäransfiltreringsinställningarna för programmet /certsrv/mscep och startar sedan om datorn. I dialogrutan **Redigera inställningar för begärandefiltrering** ska inställningarna för **Begärandebegränsningar** vara följande:  

   - **Högsta tillåtna innehållslängd (byte)**: **30000000**  

   - **Maximal URL-längd (byte):**: **65534**  

   - **Maximal frågesträng (byte):**: **65534**  

     Mer information om de här inställningarna och hur du konfigurerar dem finns i [begränsningar för IIS-begäranden](/iis/configuration/system.webServer/security/requestFiltering/requestLimits/).

7. Om du vill kunna begära ett certifikat som har kortare giltighetstid än den certifikatmall som du använder: Den här konfigurationen är inaktiverad som standard för företagscertifikatutfärdare. Om du vill aktivera det här alternativet för företagscertifikatutfärdare använder du kommandoradsverktyget Certutil och stoppar och startar sedan om certifikattjänsten med följande kommandon:  

   1. **certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**  

   2. **net stop certsvc**  

   3. **net start certsvc**  

      Mer information finns i [verktyg och inställningar för certifikat tjänster](/previous-versions/windows/it-pro/windows-server-2003/cc780742\(v=ws.10\)).

8. Kontrol lera att registrerings tjänsten för nätverks enheter fungerar genom att använda följande länk som exempel: `https://server.contoso.com/certsrv/mscep/mscep.dll` . Nu bör den inbyggda webbsidan för registreringstjänsten för nätverksenheter visas. På den här webbsidan förklaras vad tjänsten är och hur nätverksenheter kan använda webbadressen för att skicka certifikatförfrågningar.  

   Nu när du har konfigurerat registreringstjänsten för nätverksenheter och beroenden är det dags att installera och konfigurera certifikatregistreringsplatsen.


## <a name="step-2---install-and-configure-the-certificate-registration-point"></a>Steg 2 – Installera och konfigurera certifikat registrerings platsen.

Du måste installera och konfigurera minst en certifikat registrerings plats i Configuration Manager hierarkin, och du kan installera den här plats system rollen på den centrala administrations platsen eller på en primär plats.  

> [!IMPORTANT]  
>  Innan du installerar certifikat registrerings platsen, se avsnittet **plats system krav** i [konfigurationer som stöds för Configuration Manager](../../core/plan-design/configs/supported-configurations.md) avsnittet för operativ system krav och beroenden för certifikat registrerings platsen.  

##### <a name="to-install-and-configure-the-certificate-registration-point"></a>Installera och konfigurera certifikatregisteringsplatsen  

1. Klicka på **Administration**i Configuration Manager-konsolen.  

2. I arbetsytan **Administration** expanderar du **Platskonfiguration**, klickar på **Systemroller för servrar och platser** och väljer sedan vilken server du vill använda för certifikatregistreringsplatsen.  

3. På fliken **Hem** går du till gruppen **Server** och klickar på **Lägg till platssystemroller**.  

4. På sidan **Allmänt** anger du allmänna inställningar för platssystemet och klickar sedan på **Nästa**.  

5. På sidan **Proxy** klickar du på **Next**. Certifikatregistreringsplatsen använder inte Internetproxyinställningar.  

6. På sidan **Urval för systemroll** väljer du **Certifikatregistreringsplats** i listan över tillgängliga roller. Klicka sedan på **Nästa**. 

7. På sidan **certifikat registrerings läge** väljer du om du vill att den här certifikat registrerings platsen ska **bearbeta SCEP-certifikat begär Anden**eller **bearbeta PFX-certifikat begär Anden**. En certifikat registrerings plats kan inte behandla båda typer av begär Anden, men du kan skapa flera certifikat registrerings platser om du arbetar med båda typerna av certifikat.

   Om du bearbetar PFX-certifikat måste du välja en certifikat utfärdare, antingen Microsoft eller Entrust.

8. Sidan **Inställningar för certifikat registrerings plats** varierar beroende på certifikat typen:
   - Om du har valt **bearbeta SCEP-certifikat begär Anden**konfigurerar du följande:
     -   **Webbplats namn**, **https-portnummer**och **virtuellt program namn** för certifikat registrerings platsen. Dessa fält fylls i automatiskt med standardvärden. 
     -   **URL för registrerings tjänsten för nätverks enheter och rotcertifikatutfärdarcertifikat** – Klicka på **Lägg till**och ange följande i dialog rutan **Lägg till URL och rot** certifikat för certifikat utfärdare:
         - **URL för registreringstjänsten för nätverksenheter**: Ange webbadressen i följande format: https://*<server_FQDN>*/certsrv/mscep/mscep.dll. Om det fullständiga domän namnet för den server som kör registrerings tjänsten för nätverks enheter till exempel är server1.contoso.com, skriver du `https://server1.contoso.com/certsrv/mscep/mscep.dll` .
         - **Rotcertifikatutfärdarcertifikat**: Bläddra till och välj certifikatfilen (.cer) som du skapade och sparade i **Steg 1: Installera och konfigurera registreringstjänsten för nätverksenheter och beroenden**. Det här rot certifikat utfärdarens certifikat tillåter certifikat registrerings platsen att verifiera det certifikat för klientautentisering som Configuration Manager-Principmodulen kommer att använda.  

   - Om du har valt **bearbeta PFX-certifikat begär Anden**, konfigurerar du anslutnings informationen och autentiseringsuppgifterna för den valda certifikat utfärdaren.

     - Om du vill använda Microsoft som certifikat utfärdare klickar du på **Lägg till** och anger följande i dialog rutan **Lägg till en certifikat utfärdare och ett konto** :
         - **Certifikat utfärdarens Server namn** – ange namnet på din server för certifikat utfärdare.
         - **Certifikat utfärdarens konto** – Klicka på **Ange** för att välja eller skapa kontot som har behörighet att registrera i mallar på certifikat utfärdaren.
         - **Anslutnings konto för certifikat registrerings plats** – Välj eller skapa kontot som ansluter certifikat registrerings platsen till Configuration Manager databasen. Alteratively kan du använda det lokala dator kontot för den dator som är värd för certifikat registrerings platsen.
         - **Active Directory certifikat publicerings konto** – Välj ett konto eller skapa ett nytt konto som ska användas för att publicera certifikat till användar objekt i Active Directory.

         - I **URL: en för dialog rutan nätverks enhets registrering och rotcertifikatutfärdarcertifikat** anger du följande och klickar sedan på **OK**:  

     - Ange följande om du vill använda Entrust som certifikat utfärdare:

       - **URL för MDM-webbtjänst**
       - Autentiseringsuppgifterna för användar namn och lösen ord för URL: en.

         När du använder MDM-API: et för att definiera URL: en för den Entrust-webbtjänsten, måste du använda minst version 9 av API: et, som visas i följande exempel:

         `https://entrust.contoso.com:19443/mdmws/services/AdminServiceV9`

         Tidigare versioner av API: t stöder inte Entrust.

9. Klicka på **Nästa** och slutför guiden.  

10. Vänta några minuter tills installationen är klar och kontrollera sedan på något av följande sätt att certifikatregistreringsplatsen har installerats:  

    -   I arbetsytan **Övervakning** expanderar du **Systemstatus**, klickar på **Komponentstatus** och letar efter statusmeddelanden från **SMS_CERTIFICATE_REGISTRATION_POINT**-komponenten.  

    -   På platssystemservern använder du filen *<ConfigMgr Installation Path\>* \Logs\crpsetup.log file och *<ConfigMgr Installation Path\>* \Logs\crpmsi.log file. Om installationen slutfördes utan problem returneras slutkoden 0.  

    -   Med hjälp av en webbläsare kontrollerar du att du kan ansluta till URL: en för certifikat registrerings platsen. Till exempel `https://server1.contoso.com/CMCertificateRegistration`. En **Serverfel**-sida med programnamnet bör nu visas, och en HTTP 404-beskrivning.  

11. Leta upp den exporterade certifikatfilen för den rotcertifikatutfärdare som certifikatregistreringsplatsen skapade automatiskt i följande mapp på den primära platsserverdatorn: *<ConfigMgr Installation Path\>* \inboxes\certmgr.box. Spara filen på en skyddad plats som du kan komma åt på ett säkert sätt när du senare installerar Configuration Manager-principmodulen på den server som kör registrerings tjänsten för nätverks enheter.  

    > [!TIP]  
    >  Certifikatet är inte omedelbart tillgängligt i mappen. Du kan behöva vänta ett tag (till exempel en halvtimme) innan Configuration Manager kopierar filen till den här platsen.  


## <a name="step-3----install-the-configuration-manager-policy-module-for-scep-certificates-only"></a>Steg 3 – installera Configuration Manager-Principmodulen (endast för SCEP-certifikat).

Du måste installera och konfigurera modulen Configuration Manager-princip på varje server som du angav i **steg 2: installera och konfigurera certifikat registrerings platsen** som **URL för registrerings tjänsten för nätverks enheter** i egenskaperna för certifikat registrerings platsen.  

##### <a name="to-install-the-policy-module"></a>Installera principmodulen  

1. Logga in som domän administratör på den server som kör registrerings tjänsten för nätverks enheter och kopiera följande filer från mappen <ConfigMgrInstallationMedia \> \SMSSETUP\POLICYMODULE\X64 på installations mediet för Configuration Manager till en tillfällig mapp:  

   -   PolicyModule.msi  

   -   PolicyModuleSetup.exe  

   Om det finns en språkpaketmapp på installationsmediet kopierar du även den mappen och dess innehåll.  

2. Kör PolicyModuleSetup.exe i den tillfälliga mappen för att starta installations guiden för Configuration Manager-principmodulen.  

3. Klicka på **Nästa** på den första sidan i guiden, godkänn licensavtalet och klicka sedan på **Nästa**.  

4. På sidan **Installationsmapp** godkänner du standardinstallationsmappen för principmodulen eller anger en annan mapp. Klicka sedan på **Nästa**.  

5. På sidan **Certifikatregistreringsplats** anger du webbadressen för certifikatregistreringsplatsen genom att använda den fullständiga domännamnet för platssystemservern och namnet på det virtuella program som står i egenskaperna för certifikatregistreringsplatsen. Standardnamnet för det virtuella programmet är CMCertificateRegistration. Om plats system servern till exempel har ett fullständigt domän namn för server1.contoso.com och du använde det virtuella standard program namnet anger du `https://server1.contoso.com/CMCertificateRegistration` .

6. Godkänn standardporten **443** eller ange det alternativa portnummer som används av certifikatregistreringsplatsen och klicka sedan på **Nästa**.  

7. På sidan **Klientcertifikat för principmodulen** bläddrar du till och anger det klientautentiseringscertifikat som du distribuerade i **Steg 1: Installera och konfigurera registreringstjänsten för nätverksenheter och beroenden**, och klickar sedan på **Nästa**.  

8. På sidan **Certifikat på certifikatregistreringsplatsen** klickar du på **Bläddra** och väljer den exporterade certifikatfilen för den rotcertifikatutfärdare som du letade upp och sparade i **Steg 2: Installera och konfigurera certifikatregistreringspunkten**.  

   > [!NOTE]  
   >  Om du inte sparade den här certifikatfilen tidigare finns den i <ConfigMgr Installation Path\>\inboxes\certmgr.box på platsserverdatorn.  

9. Klicka på **Nästa** och slutför guiden.  

   Om du vill avinstallera Configuration Manager-Principmodulen använder du **program och funktioner** på kontroll panelen. 

 
Nu när du har slutfört konfigurations stegen är du redo att distribuera certifikat till användare och enheter genom att skapa och distribuera certifikat profiler. Mer information om hur du skapar certifikat profiler finns i [så här skapar du certifikat profiler](../../protect/deploy-use/create-certificate-profiles.md).