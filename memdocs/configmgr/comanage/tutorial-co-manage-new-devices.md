---
title: Självstudie&#58; aktivera samhantering för Internet enheter
titleSuffix: Configuration Manager
description: Lär dig hur du konfigurerar samhantering för nya Internet-baserade Windows 10-enheter med Configuration Manager och Microsoft Intune.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/12/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 7fb02a5c-e286-46b1-a972-6335c858429a
ms.openlocfilehash: 75016e8028dde29c83ae7e7f5a23a1f6dbb4417f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712717"
---
# <a name="tutorial-enable-co-management-for-new-internet-based-devices"></a>Självstudie: Aktivera samhantering för nya Internetbaserade enheter

Med samhantering kan du hålla väletablerade processer för att använda Configuration Manager för att hantera datorer i din organisation. Samtidigt ska du investera i molnet genom att använda Intune för säkerhet och modern etablering.

I den här självstudien ställer du in samhantering av Windows 10-enheter i en miljö där du använder både Azure Active Directory (AD) och en lokal AD, men inte har en [hybrid Azure Active Directory](/azure/active-directory/devices/concept-azure-ad-join-hybrid) (AD). Configuration Managers miljön innehåller en enda primär plats med alla plats system roller som finns på samma server, plats servern. Den här självstudien börjar med det lokala att dina Windows 10-enheter redan har registrerats med Intune. 

Om du har en hybrid Azure AD som ansluter till din lokala AD med Azure AD rekommenderar vi att du följer vår medföljande vägledning, [aktiverar samhantering för Configuration Manager klienter](tutorial-co-manage-clients.md).

Använd den här självstudien när:
  
- Du har Windows 10-enheter för att ta del av hantering. Dessa enheter kan ha etablerats via Windows autopilot eller direkt från din maskin vara OEM.
- Du har Windows 10-enheter på Internet som du för närvarande hanterar med Intune som du vill lägga till Configuration Manager-klienten på.

**I den här självstudien kommer du att:**  
> [!div class="checklist"]  
> * Granska krav för Azure och din lokala miljö
> * Begär ett offentligt SSL-certifikat för Cloud Management Gateway (CMG)
> * Aktivera Azure-tjänster i Configuration Manager
> * Distribuera och konfigurera en Cloud Management Gateway  
> * Konfigurera hanterings platsen och klienterna så att de använder CMG
> * Aktivera samhantering i Configuration Manager
> * Konfigurera Intune för att installera Configuration Manager-klienten

## <a name="prerequisites"></a>Krav  

### <a name="azure-services-and-environment"></a>Azure-tjänster och-miljö

- Azure-prenumeration ([kostnads fri utvärderings version](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Microsoft Intune-prenumeration
  > [!TIP]  
  > En prenumeration på Enterprise Mobility and Security (EMS) omfattar både Azure Active Directory Premium och Microsoft Intune. EMS-prenumeration ([kostnads fri utvärderings version](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

- Intune har kon figurer ATS för att [automatiskt registrera enheter](tutorial-co-manage-clients.md#configure-auto-enrollment-of-devices-to-intune)  

> [!TIP]
> Du behöver inte längre köpa och tilldela enskilda Intune-eller EMS-licenser till dina användare. Mer information finns i [vanliga frågor och svar om produkt och licensiering](../core/understand/product-and-licensing-faq.md#bkmk_mem).

### <a name="on-premises-infrastructure"></a>Lokal infrastruktur

- Configuration Manager aktuella grenen, version 1810 eller senare.
  
  Version 1810 introducerar [utökad http](../core/plan-design/hierarchy/enhanced-http.md), som används i den här självstudien för att undvika mer komplexa PKI-krav. Med hjälp av utökad HTTP måste den primära plats som du använder för att hantera klienter konfigureras för att använda Configuration Manager-genererade certifikat för HTTP-plats system.  

  Version 1810 innehåller också en enklare kommando rad för internetbaserad installation av Configuration Manager-klienten.

- MDM-utfärdaren måste vara inställd på Intune  

### <a name="external-certificates"></a>Externa certifikat

- Certifikat för CMG-serverautentisering. Det här certifikatet är ett SSL-certifikat från en offentlig och globalt betrodd certifikat leverantör. Till exempel, men inte begränsat till, DigiCert, Thawte eller VeriSign. Du kommer att exportera det här certifikatet som. PFX-fil med privat nyckel.  

- Senare i den här självstudien ger vi vägledning om hur du konfigurerar begäran för det här certifikatet.

### <a name="permissions"></a>Behörigheter

I den här självstudien använder du följande behörigheter för att slutföra aktiviteter:

- Ett konto som är en *Global administratör* för Azure Active Directory (Azure AD)
- Ett konto som är en *domän administratör* i din lokala infrastruktur  
- Ett konto som är en *Fullständig administratör* för *alla* scope i Configuration Manager

## <a name="request-a-public-certificate-for-the-cloud-management-gateway"></a>Begär ett offentligt certifikat för Cloud Management Gateway

När dina enheter är på Internet kräver samhantering Configuration Manager Cloud Management Gateway (CMG). CMG gör det möjligt för Internet-baserade Windows 10-enheter att kommunicera med din lokala Configuration Manager-distribution. CMG kräver ett SSL-certifikat för att upprätta ett förtroende mellan enheter och din Configuration Manager miljö.

I den här självstudien används ett offentligt certifikat som kallas **CMG för serverautentisering** som härleder auktoritet från en globalt betrodd certifikat leverantör. Även om det är möjligt att konfigurera samhantering med certifikat som härleder auktoritet från din lokala Microsoft-certifikatutfärdare, är användningen av självsignerade certifikat utanför den här självstudien.

**Certifikatet för CMG** används för att kryptera kommunikations trafiken mellan Configuration Manager-klienten och CMG. Certifikatet spårar tillbaka till en betrodd rot för att verifiera serverns identitet för klienten. Det offentliga certifikatet innehåller en betrodd rot som Windows-klienter redan litar på.

Om det här certifikatet: 

- Du kan identifiera ett unikt namn för din CMG-tjänst i Azure och sedan ange namnet i certifikat förfrågan.  
- Du genererar din certifikatbegäran på en enskild server och skickar sedan begäran till en offentlig certifikat leverantör för att hämta det nödvändiga SSL-certifikatet.  
- Du importerar till systemet som skapade begäran till det certifikat du får tillbaka från providern. Du använder samma dator för att exportera certifikatet för användning när du senare distribuerar CMG till Azure.  
- När CMG installeras skapas en CMG-tjänst i Azure med det namn som du angav i certifikatet.  

### <a name="identify-a-unique-name-for-your-cloud-management-gateway-in-azure"></a>Identifiera ett unikt namn för din Cloud Management Gateway i Azure

När du begär certifikatet för CMG, anger du vad som måste vara ett unikt namn för att identifiera din *moln tjänst (klassisk)* i Azure. Som standard använder det offentliga Azure-molnet *cloudapp.net*och CMG finns i cloudapp.net-domänen som * \<YourUniqueDnsName>. cloudapp.net*.  

> [!TIP]  
> I den här självstudien använder **certifikatet för CMG Server-autentisering** ett fullständigt domän namn som slutar på *contoso.com*.  När vi har skapat CMG konfigurerar vi en kanonisk namn post (CNAME) i vår organisations offentliga DNS. Den här posten skapar ett alias för den CMG som mappar till det namn som vi använder i det offentliga certifikatet.  

Innan du begär ditt offentliga certifikat kontrollerar du att det namn som du vill använda är tillgängligt i Azure. Du skapar inte tjänsten direkt i Azure. I stället används det namn som anges i det offentliga certifikatet som du begär i Configuration Manager för att skapa moln tjänsten när du installerar CMG.  

1. Logga in på [Microsoft Azure Portal](https://portal.azure.com/).  

2. Välj **skapa en resurs**, Välj **beräknings** kategori och välj sedan **moln tjänst**. Sidan moln tjänst (klassisk) öppnas.

3. I **DNS-namn**anger du prefixet för moln tjänsten som du kommer att använda. Det här prefixet måste vara samma som det du använder senare när du begär ett publicerings certifikat för certifikatet för CMG-serverautentisering. Vi använder *MyCSG*, som skapar namn området för *MyCSG.cloudapp.net*. Gränssnittet bekräftar om namnet är tillgängligt eller redan används av en annan tjänst.  
 När du har bekräftat att det namn som du vill använda är tillgängligt, är du redo att skicka begäran om certifikat signering (CSR).

### <a name="request-the-certificate"></a>Begär certifikatet

Använd följande information för att skicka en begäran om certifikat signering för din CMG till en offentlig certifikat leverantör. Ändra följande värden så att de är relevanta för din miljö.  

- *MyCMG* för att identifiera tjänst namnet för Cloud Management Gateway
- *Contoso* som företags namn
- *Contoso.com* som den offentliga domänen

Vi rekommenderar att du använder den primära plats servern för att skapa certifikat signerings förfrågningar (CSR). När du får certifikatet måste du registrera det på samma server som skapade CSR-servern eller så kan du inte exportera certifikatets privata nyckel, vilket krävs.  

Begär en version 2 nyckel leverantörs typ när du skapar en CSR. Endast version 2-certifikat stöds.  

> [!TIP]  
> När vi distribuerar CMG kommer vi även att installera en moln distributions plats (CDP) på samma gång. Som standard när du distribuerar en CMG kan alternativet **Tillåt att CMG fungerar som en moln distributions plats och hantera innehåll från Azure Storage** . Att samplacera CDP på servern med CMG tar bort behovet av separata certifikat och konfigurationer för att stödja CDP. Även om CDP inte krävs för att använda samhantering, är det användbart i de flesta miljöer.  
>
> Om du ska använda ytterligare moln distributions platser för samhantering måste du begära separata certifikat för varje ytterligare Server. Om du vill begära ett offentligt certifikat för CDP använder du samma information som för Cloud Management Gateway CSR. Du behöver bara ändra det egna namnet så att det är unikt för varje CDP.  

#### <a name="details-for-the-cloud-management-gateway-csr"></a>Information om Cloud Management Gateway CSR

- **Eget namn**: CloudServiceNameCMG.YourCompanyPubilcDomainName.com  
Exempel: MyCSG.contoso.com  
- **Alternativt namn för certifikat mottagare**: samma som nätverks namnet (CN)  
- **Organisation**: namnet på din organisation  
- **Avdelning**: per organisation  
- **Ort**: per organisation  
- **Tillstånd**: per organisation  
- **Land**: per organisation  
- **Nyckel storlek: 2048**  
- **Provider: Microsoft RSA SChannel Cryptographic Provider**  

### <a name="import-the-certificate"></a>Importera certifikatet

När du har fått det offentliga certifikatet importerar du det till det lokala certifikat arkivet på den dator som skapade CSR. Exportera sedan certifikatet som en. PFX-fil så att du kan använda den för din CMG i Azure.  

Offentliga certifikat leverantörer tillhandahåller vanligt vis instruktioner för att importera certifikatet. Processen för att importera certifikatet bör likna följande rikt linjer:  

1. Leta upp filen Certificate. pfx på den dator som certifikatet ska importeras till.  

2. Högerklicka på filen och välj sedan **Installera PFX**  

3. När guiden Importera certifikat startar väljer du **Nästa**.  

4. På sidan **fil som ska importeras** väljer du **Nästa**.

5. På sidan **lösen ord** anger du lösen ordet för den privata nyckeln i rutan lösen ord och väljer sedan **Nästa**.  
  
   Välj alternativet för att göra nyckeln exporter bar.

6. På **sidan certifikat Arkiv**väljer **du Välj certifikat Arkiv automatiskt baserat på certifikat typ**och välj sedan **Nästa**.  

7. Välj **Slutför**.

### <a name="export-the-certificate"></a>Exportera certifikatet

Exportera *certifikatet för CMG-serverautentisering* från servern. Genom att exportera certifikatet på nytt kan du använda den för din moln hanterings gateway i Azure.  

1. Öppna konsolen Certificate Manager genom att köra **certlm. msc** på den server där du importerade det offentliga SSL-certifikatet.  

2. I konsolen Certificate Manager väljer du **personliga > certifikat**. Högerklicka sedan på *certifikatet för CMG* som du registrerade i den föregående proceduren och välj sedan **alla aktiviteter > exportera**.  

3. I guiden Exportera certifikat väljer du **Nästa**, väljer **Ja, exportera den privata nyckeln**och klickar sedan på **Nästa**.  

4. På sidan fil format för export väljer du **personal information Exchange – PKCS #12 (. PFX)**, Välj **Nästa**och ange ett lösen ord. I fil namn anger du ett namn som **C:\ConfigMgrCloudMGServer**. Du refererar till den här filen när du skapar CMG i Azure.  

5. Välj **Nästa**och bekräfta sedan följande inställningar innan du väljer **Slutför** för att slutföra exporten:  

   - Exportera nycklar = Ja  
   - Ta med alla certifikat i certifierings Sök vägen = Ja  
   - Fil format = personal information Exchange (*. pfx)  

6. När du har slutfört exporten letar du upp. pfx-filen och placerar en kopia av den i **C:\Certs** på den Configuration Manager primära plats servern som ska hantera Internetbaserade klienter. Mappen med certifikat är en tillfällig mapp som ska användas vid flyttning av certifikat mellan servrar. Du kommer åt certifikat filen från den primära plats servern när du distribuerar Cloud Management Gateway till Azure.  

När du har kopierat certifikatet till den primära plats servern kan du ta bort certifikatet från det personliga certifikat arkivet på medlems servern.

## <a name="enable-azure-cloud-services-in-configuration-manager"></a>Aktivera Azure Cloud Services i Configuration Manager

Om du vill konfigurera Azure-tjänster inifrån Configuration Manager-konsolen använder du guiden Konfigurera Azure-tjänster och skapar två Azure Active Directory-appar (Azure AD).  

- **Server App** *– en WEBBAPP* i Azure AD  
- **Klient program** – en *inbyggd klient* app i Azure AD  

Kör följande procedur från den primära plats servern.  

1. Från den primära plats servern öppnar du Configuration Manager-konsolen och går till **administrations > Cloud Services > Azure-tjänster**och väljer **Konfigurera Azure-tjänster**.  

   På sidan Konfigurera Azure-tjänst anger du ett eget namn för den moln hanterings tjänst som du konfigurerar. Till exempel: *min moln hanterings tjänst*.

   Välj sedan **Cloud Management**och välj sedan **Nästa**.  

   > [!TIP]  
   > Mer information om de konfigurationer som du gör i guiden finns i [starta guiden Azure-tjänster](../core/servers/deploy/configure/Azure-services-wizard.md#start-the-azure-services-wizard)

2. På sidan **Egenskaper** **för webbapp**väljer du **Bläddra** för att öppna dialog rutan **Server App** och väljer sedan **skapa**. Konfigurera följande fält:

   - **Program namn**: Ange ett eget namn för appen, till exempel *Cloud Management Web App*.  

   - **Start sidans URL**: det här värdet används inte av Configuration Manager, men krävs av Azure AD. Som standard är `https://ConfigMgrService`det här värdet.  

   - **App-ID-URI**: det här värdet måste vara unikt i din Azure AD-klient. Den finns i åtkomsttoken som används av Configuration Manager-klienten för att begära åtkomst till tjänsten. Som standard är `https://ConfigMgrService`det här värdet.  

   Välj sedan logga in och ange ett globalt administratörs konto **för**Azure AD. Autentiseringsuppgifterna sparas inte av Configuration Manager. Den här personen behöver inte behörigheter i Configuration Manager och behöver inte vara samma konto som kör guiden Azure-tjänster.

   När du har loggat in visas resultatet. Välj **OK** för att stänga dialog rutan skapa serverprogram och gå tillbaka till sidan med egenskaper för appen.

3. För **ursprunglig klient-app**väljer du **Bläddra** för att öppna dialog rutan för **klientens app** .

4. Välj **skapa** för att öppna dialog rutan **skapa klient program** och konfigurera sedan följande fält:  

   - **Program namn**: Ange ett eget namn för appen, till exempel *Cloud Management Native Client app*.

   - **Svars-URL**: det här värdet används inte av Configuration Manager, men krävs av Azure AD. Som standard är `https://ConfigMgrClient`det här värdet.
   Välj sedan logga in och ange ett globalt administratörs konto **för**Azure AD. Precis som webbappen sparas inte dessa autentiseringsuppgifter och kräver inte behörigheter i Configuration Manager.

   När du har loggat in visas resultaten. Välj **OK** för att stänga dialog rutan skapa klient program och gå tillbaka till sidan med egenskaper för appen. Välj sedan **Nästa** för att fortsätta.

5. Markera kryss rutan **aktivera Azure Active Directory användar identifiering**på sidan **Konfigurera identifierings inställningar** , Välj **Nästa**och slutför sedan konfigurationen av identifierings dialog rutorna för din miljö.  

6. Fortsätt med sidorna Sammanfattning, förlopp och slut för ande och stäng sedan guiden.  

   Azure-tjänster för Azure AD-identifiering av användare har nu Aktiver ATS i Configuration Manager.  Låt konsolen vara öppen för tillfället.  

7. Öppna en webbläsare och logga in på [Azure Portal](https://portal.azure.com/).  

8. Välj **alla tjänster > Azure Active Directory > Appregistreringar**och sedan:

   1. Välj den webbapp som du skapade.

   2. Gå till **inställningar > nödvändiga behörigheter**, Välj **bevilja behörigheter**och välj sedan **Ja**.  

   3. Välj den inbyggda klient app som du skapade.

   4. Gå till **inställningar > nödvändiga behörigheter**, Välj **bevilja behörigheter**och välj sedan **Ja**.  

9. I Configuration Manager-konsolen går du till **Administration > översikt > Cloud Services > Azure-tjänster**och väljer din Azure-tjänst. Högerklicka på **Azure Active Directory användar identifiering** och välj **Kör fullständig identifiering nu**. Bekräfta åtgärden genom att välja **Ja** .  

10. På den primära plats servern öppnar du Configuration Manager **SMS_AZUREAD_DISCOVERY_AGENT. log** och letar efter följande post för att bekräfta att identifieringen fungerar: *har publicerat UDX för Azure Active Directory användare*  

    Som standard är logg filen i *% Program_Files% \ Microsoft Configuration Manager\Logs*.  

## <a name="create-the-cloud-services-in-azure"></a>Skapa moln tjänster i Azure

**I det här avsnittet av självstudien kommer du att**:

- Skapa moln tjänsten CMG  
- Skapa DNS CNAME-poster för båda tjänsterna  

### <a name="create-the-cmg"></a>Skapa CMG

Använd den här proceduren för att installera en Cloud Management Gateway som en tjänst i Azure. CMG installeras på platsen på den översta nivån i hierarkin. I den här självstudien fortsätter vi att använda den primära platsen där certifikat har registrerats och exporter ATS.

1. Öppna Configuration Manager-konsolen på den primära plats servern och gå till **Administration > översikt > Cloud Services > Cloud Management Gateway**och välj sedan **skapa Cloud Management Gateway**.  

2. På sidan **Allmänt**:  

   1. Välj din moln miljö för **Azure-miljön**. I den här självstudien används **AzurePublicCloud**.  

   2. Välj **Azure Resource Manager distribution**.  
  
   3. **Logga in** på din Azure-prenumeration. Configuration Manager fyller i ytterligare information baserat på den information som du konfigurerade när du aktiverade Azure Cloud Services för Configuration Manager.  

   Fortsätt genom att välja **Nästa**.  

3. På sidan **Inställningar** bläddrar du till och väljer den fil som heter **ConfigMgrCloudMGServer. pfx**, som är den fil som du exporterade efter att du importerat certifikatet för CMG-serverautentisering. När du har angett lösen ordet fylls **tjänst namnet** och **distributions namnet** i automatiskt baserat på informationen i. PFX-certifikat filen.

4. Ange din **region**.

5. För **resurs grupp**använder du en befintlig resurs grupp eller skapar en grupp med ett eget namn som inte använder blank steg som **CofigMgrCloudServices**. Om du väljer att skapa en grupp läggs gruppen till som en resurs grupp i Azure.  

6. Om du inte är redo att konfigurera vid skalning använder du en (1) för antalet **virtuella dator instanser**. Antalet virtuella dator instanser gör att en enda Cloud Management Gateway (CMG) moln tjänst kan skalas ut för att stödja fler klient anslutningar. Senare kan du använda Configuration Manager-konsolen för att returnera och redigera antalet virtuella dator instanser som du använder.  

7. Aktivera kryss rutan för **att verifiera åter kallelse av klient certifikat**.

8. Aktivera kryss rutan för **att tillåta att CMG fungerar som en moln distributions plats och hantera innehåll från Azure Storage** om du vill distribuera en moln distributions plats med CMG.

9. Fortsätt genom att välja **Nästa**.

10. Granska värdena på **aviserings** sidan och välj sedan **Nästa**.

11. Granska sidan **Sammanfattning** och klicka på **Nästa** för att skapa moln tjänsten Cloud Management Gateway. Välj **Stäng** för att slutföra guiden.  

12. I noden Cloud Management Gateway i Configuration Manager-konsolen kan du nu visa den nya tjänsten.  

### <a name="create-dns-cname-records"></a>Skapa DNS CNAME-poster

När du skapar en DNS-post för CMG kan du aktivera dina Windows 10-enheter både i och utanför företags nätverket för att använda namn matchning för att hitta CMG Cloud service i Azure.

Exemplet på en CNAME-post använder följande information:  

- Företags namnet är **contoso** med ett offentligt DNS-namnområde för ***contoso.com***.  

- CMG-tjänstens namn är **MyCMG**, som blir ***MyCMG.CloudApp.net*** i Azure.  

CNAME-post exempel: *MyCMG.contoso.com => My.cloudapp.net*

## <a name="configure-the-management-point-and-clients-to-use-the-cmg"></a>Konfigurera hanterings platsen och klienterna så att de använder CMG

Konfigurera inställningar som aktiverar lokala hanterings platser och klienter som använder Cloud Management Gateway.

Eftersom vi använder utökad HTTP för klient kommunikation behöver du inte använda en HTTPS-hanterings plats.  

### <a name="create-the-cmg-connection-point"></a>Skapa anslutnings punkten för CMG

Konfigurera platsen så att den stöder utökad HTTP.  

1. I Configuration Manager-konsolen går du till **Administration > översikt > plats konfiguration > platser**och öppnar egenskaperna för den primära platsen.  

2. På fliken **klient dator kommunikation** väljer du alternativet *https eller HTTP* för **Använd Configuration Manager-genererade certifikat för http-platssystem**och väljer sedan **OK** för att spara konfigurationen.

    > [!Note]
    > Från och med version 1906 kallas den här fliken **kommunikations säkerhet**.<!-- SCCMDocs#1645 -->  

3. Gå nu till **administrations > översikt > plats konfiguration > servrar och plats system roller** och välj servern med en hanterings plats där du vill installera anslutnings punkten för moln hanterings Gateway.  

4. Välj **Lägg till plats system roller**och **Nästa**> **Nästa**.  

5. Välj **Cloud Management Gateway-anslutningssträngen** och välj sedan **Nästa** för att fortsätta.  

6. Granska standard valen på sidan för **anslutning punkt för Cloud Management Gateway** och se till att rätt CMG är markerat. Om du har flera moln hanterings-gatewayer kan du använda List rutan för att ange en annan CMG. Du kan också ändra de CMG som används, efter installationen. Fortsätt genom att välja **Nästa**.

7. Välj **Nästa** för att starta installationen och Visa sedan resultaten på sidan slut för ande.  Välj **Stäng** för att slutföra installationen av anslutnings punkten.

8. Gå nu till **Administration > översikt > plats konfiguration > servrar och plats system roller** och öppna **egenskaperna** för hanterings platsen där du installerade anslutnings punkten. På fliken **Allmänt** markerar du kryss rutan **Tillåt Configuration Manager Cloud Management Gateway-trafik**och väljer sedan **OK** för att spara konfigurationen.
   > [!TIP]  
   > Även om det inte krävs för att aktivera samhantering, rekommenderar vi att du gör samma redigering för alla program uppdaterings platser.

### <a name="configure-client-settings-to-direct-clients-to-use-the-cmg"></a>Konfigurera klient inställningar för att dirigera klienter att använda CMG

Använd klient inställningar för att konfigurera Configuration Manager klienter att kommunicera med CMG.  

1. Öppna **Configuration Manager konsolen > Administration > översikt > klient inställningar**och redigera sedan **standard klient inställningarna**.  

2. Välj **Cloud Services**.

3. På sidan **standardinställningar** anger du följande inställningar till = **Ja**.  

   - **Registrera automatiskt nya Windows 10-domänanslutna enheter med Azure Active Directory**  

   - **Gör det möjligt för klienter att använda en Cloud Management Gateway**

   - **Tillåt åtkomst till moln distributions platsen**

4. På sidan **klient princip** anger du **Aktivera användar princip begär Anden från Internet klienter** = **Ja**.

5. Spara konfigurationen genom att välja **OK**.

## <a name="enable-co-management-in-configuration-manager"></a>Aktivera samhantering i Configuration Manager

Med Azure-konfiguration, plats system roller och klient inställningar på plats kan du konfigurera Configuration Manager att aktivera samhantering. Du behöver dock fortfarande göra några konfigurationer i Intune när du har aktiverat samhantering innan den här självstudien har slutförts. En av dessa aktiviteter är att konfigurera Intune för att distribuera Configuration Manager-klienten. Den uppgiften blir enklare genom att spara kommando raden för klient distribution som är tillgänglig i konfigurations guiden för samhantering. Därför aktiverar vi samhantering nu innan vi slutför konfigurationerna för Intune.

> [!TIP]
> - När du aktiverar samhantering tilldelar du en samling som en *pilot grupp*. Det här är en grupp som innehåller ett litet antal klienter för att testa konfigurationerna för samhantering. Vi rekommenderar att du skapar en lämplig samling innan du påbörjar proceduren. Sedan kan du välja samlingen utan att avsluta proceduren.
> - Från och med Configuration Manager version 1906 kan du behöva flera samlingar eftersom du kan tilldela en annan *pilot grupp* för varje arbets belastning.

### <a name="enable-co-management-starting-in-version-1906"></a>Aktivera samtidig hantering från och med version 1906

Om du vill aktivera samhantering från Configuration Manager version 1906 följer du anvisningarna nedan:

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>Aktivera samhantering i version 1902 och tidigare

Följ anvisningarna nedan om du vill aktivera samhantering för Configuration Manager version 1902 och tidigare:

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="use-intune-to-deploy-the-configuration-manager-client"></a>Använda Intune för att distribuera Configuration Manager-klienten

Du kan använda Intune för att installera Configuration Manager-klienten på Windows 10-enheter som för närvarande endast hanteras med Intune.  

Sedan, när en tidigare ohanterad Windows 10-enhet registreras med Intune, installerar den automatiskt den Configuration Manager klienten.

### <a name="create-an-intune-app-to-install-the-configuration-manager-client"></a>Skapa en Intune-App för att installera Configuration Manager-klienten

1. Från den primära plats servern loggar du in på [Azure Portal](https://portal.azure.com/) och går till Intune- **>-klientens appar > appar > Lägg till**.

2. För **typ av app**: Välj **branschspecifika appar**.

3. Välj **app Package-fil**och bläddra sedan till platsen för Configuration Manager filen **CCMSetup. msi**och välj sedan **Öppna > OK**.
Till exempel *C:\Program\Microsoft Configuration Manager\bin\i386\ccmsetup.msi*

4. Välj **app-information**och ange sedan följande information:
   - **Beskrivning**: Configuration Manager-klient  

   - **Utgivare**: Microsoft  

   - **Kommando rads argument**: * \<ange kommando raden **CCMSETUPCMD** . Du kan använda kommando raden som du sparade från* *sidan aktivering i konfigurations guiden för samhantering. Den här kommando raden innehåller namnen på moln tjänsten och ytterligare värden som gör det möjligt för enheter att installera Configuration Manager klient program varan. >*  

     Kommando rads strukturen bör likna det här exemplet endast med parametrarna CCMSETUPCMD och SMSSiteCode:  

     ``` Command
     CCMSETUPCMD="CCMHOSTNAME=<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/<GUID>" SMSSiteCode="<YourSiteCode>"  
     ```

     > [!TIP]  
     > Om du inte har kommando raden tillgänglig kan du visa egenskaperna för *CoMgmtSettingsProd* i Configuration Manager-konsolen för att få en kopia av kommando raden.

5. Välj **OK > Lägg till**.  Appen skapas och blir tillgänglig i Intune-konsolen. När appen är tillgänglig kan du använda följande avsnitt för att konfigurera Intune för att tilldela det till Windows 10-enheter.

### <a name="assign-the-intune-app-to-install-the-configuration-manager-client"></a>Tilldela Intune-appen för att installera Configuration Manager-klienten

Följande procedur distribuerar appen för att installera Configuration Manager-klienten som du skapade i föregående procedur.

1. Logga in på [Azure Portal](https://portal.azure.com/).  Välj **alla tjänster > Intune > klient program > appar**och välj sedan **Start programmet för klient installation för ConfigMgr**, den app som du skapade för att distribuera Configuration Manager klienten.  

2. Välj **tilldelningar > Lägg till grupp**.  Ange **tilldelnings typ** som **obligatorisk**och Använd sedan **inkluderade grupper** och **undantagna grupper** för att ange de Azure Active Directory (AD) grupper som har användare och enheter som du vill delta i samhantering.  

3. Välj **OK** och **Spara** konfigurationen.
Appen krävs nu av användare och enheter som du har tilldelat den till. När appen har installerat Configuration Manager-klienten på en enhet hanteras den av samhantering.

## <a name="summary"></a>Sammanfattning

När du har slutfört konfigurations stegen i den här självstudien kan du börja hantera dina enheter.

## <a name="next-steps"></a>Nästa steg

- Granska statusen för samhanterade enheter med [instrument panelen för samhantering](how-to-monitor.md)
- Använd [Windows autopilot](quickstart-autopilot.md) för att etablera nya enheter
- Använd [villkorlig åtkomst](quickstart-conditional-access.md) och Intune-efterlevnadsprinciper för att hantera användar åtkomst till företags resurser
