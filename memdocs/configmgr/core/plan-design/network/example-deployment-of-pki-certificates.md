---
title: Exempel på distribution av PKI-certifikat
titleSuffix: Configuration Manager
description: Följ ett steg-för-steg-exempel för att lära dig hur du skapar och distribuerar PKI-certifikat som Configuration Manager använder.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 994ee2916020ecc4e6d9d3c35f41fe24d5a31405
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718779"
---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-configuration-manager-windows-server-2008-certification-authority"></a>Steg för steg-distribution av PKI-certifikaten för Configuration Manager: Windows Server 2008-certifikat utfärdare

*Gäller för: Configuration Manager (aktuell gren)*

Den här steg-för-steg-exempel distributionen, som använder en Windows Server 2008-certifikat utfärdare (CA), har procedurer som visar hur du skapar och distribuerar de PKI-certifikat (Public Key Infrastructure) som Configuration Manager använder. I dessa procedurer används en utfärdare av företagscertifikat och certifikatmallar. Metoderna lämpar sig enbart för testnätverk, för att visa att det fungerar.  

Eftersom det inte finns någon distributions metod för de certifikat som krävs kan du läsa dokumentationen för PKI-distributionen för de nödvändiga procedurerna och metod tips för att distribuera de certifikat som krävs för en produktions miljö. Mer information om certifikat kraven finns i avsnittet [om krav för PKI-certifikat för Configuration Manager](pki-certificate-requirements.md).  

> [!TIP]
> Du kan anpassa instruktionerna i det här avsnittet för operativ system som inte är dokumenterade i avsnittet testa nätverks krav. Men om du kör den utfärdande certifikat utfärdaren på Windows Server 2012 behöver du inte ange versionen av certifikat mal len. Ange i stället detta på fliken **kompatibilitet** i mallens egenskaper:  
>
> - **Certifikatutfärdare**: **Windows Server 2003**  
>   - **Certifikatmottagare**: **Windows XP / Server 2003**  

## <a name="test-network-requirements"></a><a name="BKMK_testnetworkenvironment"></a>Testa nätverks krav

De detaljerade anvisningarna är förknippade med de följande kraven:  

- Testnätverket kör Active Directory Domain Services med Windows Server 2008, och det är installerat som en enda domän och en enda skog.  

- Du har en medlems server som kör Windows Server 2008 Enterprise Edition, som har rollen Active Directory certifikat tjänster installerad, och den har kon figurer ATS som företagets rot certifikat utfärdare (CA).  

- Du har en dator med Windows Server 2008 (Standard Edition eller Enterprise Edition, R2 eller senare) installerat på den, den datorn är avsedd som en medlems Server och Internet Information Services (IIS) installeras på den. Den här datorn kommer att vara den Configuration Manager plats system server som du ska konfigurera med ett fullständigt kvalificerat domän namn (FQDN) för intranätet som stöd för klient anslutningar på intranätet och ett Internet-FQDN om du måste stödja mobila enheter som har registrerats av Configuration Manager och klienter på Internet.  

- Du har en Windows Vista-klient med de senaste service pack installerade, och den här datorn är konfigurerad med ett dator namn som består av ASCII-tecken och är ansluten till domänen. Den här datorn är en Configuration Manager klient dator.  

- Du kan logga in med ett rot domän administratörs konto eller ett företags domän administratörs konto och använda det här kontot för alla procedurer i den här exempel distributionen.  

## <a name="overview-of-the-certificates"></a><a name="BKMK_overview2008"></a>Översikt över certifikaten

I följande tabell visas de typer av PKI-certifikat som kan krävas för Configuration Manager och beskriver hur de används.  

|Certifikatkrav|Beskrivning av certifikatet|  
|-----------------------------|-----------------------------|  
|Webbservercertifikat för platssystem som kör IIS|Det här certifikatet används för att kryptera data och autentisera servern för klienter. Den måste installeras externt från Configuration Manager på plats system servrar som kör Internet Information Services (IIS) och som har kon figurer ATS i Configuration Manager för att använda HTTPS.<br /><br /> Anvisningar om hur du konfigurerar och installerar det här certifikatet finns i [distribuera webb Server certifikatet för plats system som kör IIS](#BKMK_webserver2008_cm2012) i den här artikeln.|  
|Tjänstcertifikat för klienter som ansluter till molnbaserade distributionsplatser|Anvisningar om hur du konfigurerar och installerar det här certifikatet finns i [distribuera tjänst certifikatet för molnbaserade distributions platser](#BKMK_clouddp2008_cm2012) i den här artikeln.<br /><br /> **Viktigt:** Detta certifikat används tillsammans med Windows Azure-hanteringscertifikatet. Mer information om hanterings certifikatet finns i [så här skapar du ett hanterings certifikat](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#create-a-new-self-signed-certificate) och [hur du lägger till ett hanterings certifikat i en Windows Azure-prenumeration](https://docs.microsoft.com/azure/cloud-services/cloud-services-configure-ssl-certificate-portal#step-3-upload-a-certificate) i avsnittet Windows Azure-plattformen i MSDN-biblioteket.|  
|Klientcertifikat för Windows-datorer|Det här certifikatet används för att autentisera Configuration Manager klient datorer för plats system som har kon figurer ATS för att använda HTTPS. Den kan också användas för hanterings platser och tillståndsmigrering för att övervaka deras drift status när de har kon figurer ATS för att använda HTTPS. Den måste installeras externt från Configuration Manager på datorer.<br /><br /> Anvisningar för hur du konfigurerar och installerar det här certifikatet finns i [distribuera klient certifikatet för Windows-datorer](#BKMK_client2008_cm2012) i det här avsnittet.|  
|Klientcertifikat för distributionsplatser|Certifikatet har två syften:<br /><br /> Certifikatet används för att autentisera distributionsplatsen för en HTTPS-aktiverad hanteringsplats innan distributionsplatsen skickar statusmeddelanden.<br /><br /> När distributionsplatsalternativet **Aktivera PXE-stöd för klienter** är valt, skickas certifikatet till datorer som startas med PXE så att de kan ansluta till en HTTPS-aktiverad hanteringsplats då operativsystemet distribueras.<br /><br /> Anvisningar för hur du konfigurerar och installerar det här certifikatet finns i [distribuera klient certifikatet för distributions platser](#BKMK_clientdistributionpoint2008_cm2012) i den här artikeln.|  
|Registreringscertifikat för mobila enheter|Det här certifikatet används för att autentisera Configuration Manager mobila enhets klienter till plats system som är konfigurerade att använda HTTPS. Den måste installeras som en del av registreringen av mobila enheter i Configuration Manager och du väljer den konfigurerade certifikat mal len som en inställning för mobila enhets klienter.<br /><br /> Anvisningar för hur du konfigurerar det här certifikatet finns i [distribuera registrerings certifikatet för mobila enheter](#BKMK_mobiledevices2008_cm2012) i det här avsnittet.|  
|Klientcertifikat för Mac-datorer|Du kan begära och installera det här certifikatet från en Mac-dator när du använder Configuration Manager registrering och väljer den konfigurerade certifikat mal len som en inställning för mobila enhets klienter.<br /><br /> Anvisningar för hur du konfigurerar det här certifikatet finns i [distribuera klient certifikatet för Mac-datorer](#BKMK_MacClient_SP1) i den här artikeln.|  

## <a name="deploy-the-web-server-certificate-for-site-systems-that-run-iis"></a><a name="BKMK_webserver2008_cm2012"></a>Distribuera webb Server certifikatet för plats system som kör IIS

Den här certifikatdistributionen sker i följande steg:  

- Skapa och utfärda webb server certifikat mal len på certifikat utfärdaren  

- Begär webb Server certifikatet  

- Konfigurera IIS att använda webb Server certifikatet  

### <a name="create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_webserver22008"></a>Skapa och utfärda webb server certifikat mal len på certifikat utfärdaren

Den här proceduren skapar en certifikatmall för Configuration Manager plats system och lägger till den i certifikat utfärdaren.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>Skapa och utfärda webbservercertifikatmallen på certifikatutfärdaren

1.  Skapa en säkerhets grupp med namnet **CONFIGMGR IIS-servrar** som har medlems servrarna för att installera Configuration Manager-plats system som ska köra IIS.  

2.  På den medlems server där certifikat tjänster är installerat högerklickar du på **certifikatmallar** i konsolen certifikat utfärdare och väljer sedan **Hantera** för att läsa in konsolen **certifikatmallar** .  

3.  I resultat fönstret högerklickar du på posten som har **webb server** i kolumnen **mallens visnings namn** och väljer sedan **Duplicera mall**.  

4.  I dialog rutan **Duplicera mall** ser du till att **Windows 2003 Server, Enterprise Edition** är markerat och väljer sedan **OK**.  

    > [!IMPORTANT]  
    >  Välj inte **Windows 2008 Server, Enterprise Edition**.  

5.  I dialog rutan **Egenskaper för ny mall** går du till fliken **Allmänt** och anger ett Mallnamn, t. ex. **webb server certifikat för ConfigMgr**, för att generera de webb certifikat som ska användas på Configuration Manager plats system.  

6.  Välj fliken **ämnes namn** och kontrol lera att **Ange i begäran** är markerat.  

7.  Välj fliken **säkerhet** och ta bort behörigheten **Registrera** från säkerhets grupperna **domän administratörer** och **företags administratörer** .  

8.  Välj **Lägg till**, ange **ConfigMgr IIS-servrar** i text rutan och välj sedan **OK**.  

9. Välj behörigheten **Registrera** för gruppen och ta inte bort behörigheten **läsa** .  

10. Välj **OK**och Stäng **konsolen Certifikatmallar**.  

11. Högerklicka på **certifikatmallar**i konsolen certifikat utfärdare, Välj **ny**och välj sedan **certifikatmall som ska utfärdas**.  

12. I dialog rutan **Aktivera certifikatmallar** väljer du den nya mall som du nyss skapade, **ConfigMgr-webbserverns certifikat**och väljer sedan **OK**.  

13. Om du inte behöver skapa och utfärda fler certifikat stänger du **certifikat utfärdare**.  

###  <a name="request-the-web-server-certificate"></a><a name="BKMK_webserver32008"></a>Begär webb Server certifikatet  
 Med den här proceduren kan du ange de FQDN-värden för intranät och Internet som ska konfigureras i egenskaperna för plats system servern och sedan installera webb Server certifikatet på den medlems server som kör IIS.  

##### <a name="to-request-the-web-server-certificate"></a>Begära webbservercertifikatet  

1.  Starta om medlems servern som kör IIS för att se till att datorn har åtkomst till den certifikatmall som du skapade genom att använda behörigheterna **Läs** och **Registrera** som du konfigurerade.  

2.  Välj **Start**, Välj **Kör**och skriv sedan **MMC. exe.** Välj **Arkiv**i den tomma konsolen och välj sedan **Lägg till/ta bort snapin-modul**.  

3.  I dialog rutan **Lägg till eller ta bort snapin-moduler** väljer du **certifikat** i listan över **Tillgängliga snapin-moduler**och väljer sedan **Lägg till**.  

4.  I dialog rutan **snapin-modulen certifikat** väljer **du dator konto**och väljer sedan **Nästa**.  

5.  I dialog rutan **Välj dator** kontrollerar du att **lokal dator: (den dator den här konsolen körs på)** är markerad och väljer sedan **Slutför**.  

6.  I dialog rutan **Lägg till eller ta bort snapin-moduler** väljer du **OK**.  

7.  I-konsolen expanderar du **certifikat (lokal dator)** och väljer sedan **personligt**.  

8.  Högerklicka på **certifikat**, Välj **alla aktiviteter**och välj sedan **Begär nytt certifikat**.  

9. Välj **Nästa**på sidan **innan du börjar** .  

10. Om sidan **Välj princip för certifikat registrering** visas väljer du **Nästa**.  

11. På sidan **Begär certifikat** identifierar du **webb Server certifikatet för ConfigMgr** i listan över tillgängliga certifikat och väljer sedan **Mer information som krävs för att registrera det här certifikatet. Konfigurera inställningarna genom att klicka här**.  

12. I dialog rutan **certifikat egenskaper** går du inte till fliken **ämne** och ändrar namn på certifikat **mottagare**. Detta innebär att rutan **Värde** för avsnittet **Ämnesnamn** ska vara tom. I stället väljer du List rutan **typ** i avsnittet **Alternativt namn** och väljer sedan **DNS**.  

13. I rutan **värde** anger du de FQDN-värden som du ska ange i Configuration Manager plats system egenskaper. Välj sedan **OK** för att stänga dialog rutan **certifikat egenskaper** .  

     Exempel:  

    - Om plats systemet bara ska ta emot klient anslutningar från intranätet och plats Systems serverns FQDN för intranätet är **server1.Internal.contoso.com**anger du **server1.Internal.contoso.com**och väljer sedan **Lägg till**.  

    - Om plats systemet ska ta emot klient anslutningar från intranätet och Internet, och plats Systems serverns FQDN för intranätet är **server1.Internal.contoso.com** och plats system serverns Internet-fqdn är **Server.contoso.com**:  

        1.  Ange **server1.Internal.contoso.com**och välj sedan **Lägg till**.  

        2.  Ange **Server.contoso.com**och välj sedan **Lägg till**.  

        > [!NOTE]  
        >  Du kan ange de fullständiga domän namnen för Configuration Manager i vilken ordning som helst. Men kontrol lera att alla enheter som ska använda certifikatet, t. ex. mobila enheter och webb servrar, kan använda ett alternativt namn för certifikat mottagare (SAN) och flera värden i SAN. Om några enheter har begränsat stöd för SAN-värden i certifikat, kanske du kan behöva ändra ordningen på de fullständigt bestämda domännamnen eller använda värdet Ämne i stället.  

14. På sidan **begära certifikat** väljer du **ConfigMgr-webbserver certifikat** i listan över tillgängliga certifikat och väljer sedan **Registrera**.  

15. På sidan **certifikat installations resultat** väntar du tills certifikatet har installerats och väljer sedan **Slutför**.  

16. Stäng **Certifikat (lokal dator)**.  

###  <a name="configure-iis-to-use-the-web-server-certificate"></a><a name="BKMK_webserver42008"></a>Konfigurera IIS att använda webb Server certifikatet  
 Den här proceduren binder det installerade certifikatet till IIS **Standardwebbplats**.  

##### <a name="to-set-up-iis-to-use-the-web-server-certificate"></a>Konfigurera IIS att använda webb Server certifikatet  

1. På den medlems server där IIS är installerat väljer du **Start**, väljer **program**, väljer **administrations verktyg**och väljer sedan **Internet Information Services (IIS) Manager**.  

2. Expandera **platser**, högerklicka på **standard webbplats**och välj sedan **Redigera bindningar**.  

3. Välj **https** -posten och välj sedan **Redigera**.  

4. I dialog rutan **Redigera bindning för webbplats** väljer du det certifikat som du begärde med hjälp av mallen för webb server certifikat för ConfigMgr och väljer sedan **OK**.  

   > [!NOTE]  
   >  Om du inte är säker på vilket certifikat som är korrekt väljer du ett och sedan **Visa**. På så sätt kan du jämföra de valda certifikat uppgifterna med certifikaten i snapin-modulen certifikat. Till exempel visar snapin-modulen certifikat den certifikatmall som användes för att begära certifikatet. Du kan sedan jämföra tumavtryck för certifikatet som begärdes med hjälp av mallen för webb server certifikat för certifikat utfärdare för certifikatets tumavtryck för det certifikat som är markerat i dialog rutan **Redigera bindning för webbplats** .  

5. Välj **OK** i dialog rutan **Redigera bindning för webbplats** och välj sedan **Stäng**.  

6. Stäng **Internet Information Services (IIS) Manager**.  

   Medlems servern har nu kon figurer ATS med ett Configuration Manager webb server certifikat.  

> [!IMPORTANT]  
>  När du installerar Configuration Manager-plats system servern på den här datorn måste du kontrol lera att du anger samma FQDN i plats system egenskaperna som du angav när du begärde certifikatet.  

##  <a name="deploy-the-service-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddp2008_cm2012"></a>Distribuera tjänst certifikatet för molnbaserade distributions platser  

Den här certifikatdistributionen sker i följande steg:  

- [Skapa och utfärda en anpassad webb server certifikat mal len på certifikat utfärdaren](#BKMK_clouddpcreating2008)  

- [Begär det anpassade webb Server certifikatet](#BKMK_clouddprequesting2008)  

- [Exportera det anpassade webb Server certifikatet för molnbaserade distributions platser](#BKMK_clouddpexporting2008)  

###  <a name="create-and-issue-a-custom-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_clouddpcreating2008"></a>Skapa och utfärda en anpassad webb server certifikat mal len på certifikat utfärdaren  
 Den här proceduren skapar en anpassad certifikatmall som baseras på certifikat mal len webb server. Certifikatet är för Configuration Manager molnbaserade distributions platser och den privata nyckeln måste kunna exporteras. När certifikatmallen skapats läggs den till i certifikatutfärdaren.  

> [!NOTE]
>  Den här proceduren använder en annan certifikatmall från webb server certifikat mal len som du skapade för plats system som kör IIS. Även om båda certifikaten kräver serverautentisering, kräver certifikatet för molnbaserade distributions platser att du anger ett anpassat definierat värde för ämnes namnet och den privata nyckeln måste exporteras. Av säkerhets skäl bör du inte konfigurera certifikatmallar så att den privata nyckeln kan exporteras om inte denna konfiguration krävs. Den molnbaserade distributions platsen kräver den här konfigurationen eftersom du måste importera certifikatet som en fil, istället för att välja den från certifikat arkivet.  
> 
>  När du skapar en ny certifikatmall för det här certifikatet kan du begränsa vilka datorer som kan begära ett certifikat vars privata nyckel kan exporteras. I ett produktions nätverk kan du även överväga att lägga till följande ändringar för det här certifikatet:  
> 
> - Kräv godkännande för att installera certifikatet för ytterligare säkerhet.  
>   - Öka certifikatets giltighetsperiod. Eftersom du måste exportera och importera certifikatet varje gång innan det går ut, minskar giltighets perioden hur ofta du måste upprepa den här proceduren. En ökning av giltighets perioden minskar dock också säkerheten för certifikatet, eftersom det ger mer tid för en angripare att dekryptera den privata nyckeln och stjäla certifikatet.  
>   - Använd ett anpassat värde i certifikatets alternativa namn på certifikatmottagare (SAN) som hjälp att identifiera det här certifikatet bland standardwebbservercertifikat som du använder med IIS.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>Skapa och utfärda den anpassade webb server certifikat mal len på certifikat utfärdaren  

1.  Skapa en säkerhets grupp med namnet **ConfigMgr-plats servrar** som har medlems servrarna för att installera Configuration Manager primära plats servrar som ska hantera molnbaserade distributions platser.  

2.  På den medlems server som kör konsolen för certifikat utfärdare högerklickar du på **certifikatmallar**och väljer sedan **Hantera** för att läsa in hanterings konsolen för certifikatmallar.  

3.  I resultat fönstret högerklickar du på posten som har **webb server** i kolumnen **mallens visnings namn** och väljer sedan **Duplicera mall**.  

4.  I dialog rutan **Duplicera mall** ser du till att **Windows 2003 Server, Enterprise Edition** är markerat och väljer sedan **OK**.  

    > [!IMPORTANT]  
    >  Välj inte **Windows 2008 Server, Enterprise Edition**.  

5.  I dialog rutan **Egenskaper för ny mall** går du till fliken **Allmänt** och anger ett Mallnamn, t. ex. **certifikat för molnbaserad distributions plats för ConfigMgr**, för att generera webb Server certifikatet för molnbaserade distributions platser.  

6.  Välj fliken **hantering av begär Anden** och välj sedan **Tillåt att den privata nyckeln exporteras**.  

7.  Välj fliken **säkerhet** och ta bort behörigheten **Registrera** från säkerhets gruppen **företags administratörer** .  

8.  Välj **Lägg till**, ange **ConfigMgr-plats servrar** i text rutan och välj sedan **OK**.  

9. Välj behörigheten **Registrera** för gruppen och ta inte bort behörigheten **läsa** .  

10. Välj fliken **kryptografi** och se till att den **minsta nyckel storleken** har angetts till **2048**.

11. Välj **OK**och Stäng **konsolen Certifikatmallar**.  

12. Högerklicka på **certifikatmallar**i konsolen certifikat utfärdare, Välj **ny**och välj sedan **certifikatmall som ska utfärdas**.  

13. I dialog rutan **Aktivera certifikatmallar** väljer du den nya mall som du precis skapade, certifikat för **molnbaserad distributions plats för ConfigMgr**och väljer sedan **OK**.  

14. Om du inte behöver skapa och utfärda fler certifikat stänger du **certifikat utfärdare**.  

###  <a name="request-the-custom-web-server-certificate"></a><a name="BKMK_clouddprequesting2008"></a>Begär det anpassade webb Server certifikatet  
 Den här proceduren begär och installerar sedan det anpassade webb Server certifikatet på den medlems server som ska köra plats servern.  

##### <a name="to-request-the-custom-web-server-certificate"></a>Begära det anpassade webbservercertifikatet  

1.  Starta om medlems servern efter att du har skapat och konfigurerat säkerhets gruppen **ConfigMgr plats servrar** för att se till att datorn har åtkomst till den certifikatmall som du skapade genom att använda behörigheterna **Läs** och **Registrera** som du konfigurerade.  

2.  Välj **Start**, Välj **Kör**och ange sedan **MMC. exe.** Välj **Arkiv**i den tomma konsolen och välj sedan **Lägg till/ta bort snapin-modul**.  

3.  I dialog rutan **Lägg till eller ta bort snapin-moduler** väljer du **certifikat** i listan över **Tillgängliga snapin-moduler**och väljer sedan **Lägg till**.  

4.  I dialog rutan **snapin-modulen certifikat** väljer **du dator konto**och väljer sedan **Nästa**.  

5.  I dialog rutan **Välj dator** kontrollerar du att **lokal dator: (den dator den här konsolen körs på)** är markerad och väljer sedan **Slutför**.  

6.  I dialog rutan **Lägg till eller ta bort snapin-moduler** väljer du **OK**.  

7.  I-konsolen expanderar du **certifikat (lokal dator)** och väljer sedan **personligt**.  

8.  Högerklicka på **certifikat**, Välj **alla aktiviteter**och välj sedan **Begär nytt certifikat**.  

9. Välj **Nästa**på sidan **innan du börjar** .  

10. Om sidan **Välj princip för certifikat registrering** visas väljer du **Nästa**.  

11. På sidan **begära certifikat** identifierar du certifikatet för **molnbaserad distributions plats för ConfigMgr** i listan över tillgängliga certifikat och väljer sedan **Mer information som krävs för att registrera det här certifikatet. Konfigurera inställningarna genom att välja här**.  

12. I dialog rutan **certifikat egenskaper** går du till fliken **ämne** för **ämnes namnet**och väljer **eget namn** som **typ**.  

13. I rutan **Värde** anger du det du väljer som tjänstnamn och ditt domännamn med ett FQDN-format. Till exempel: **clouddp1.contoso.com**.  

    > [!NOTE]  
    >  Gör tjänst namnet unikt i ditt namn område. Du kommer att använda DNS för att skapa ett alias (CNAME-post) för att mappa det här tjänstnamnet till en automatiskt genererad identifierare (GUID) och en IP-adress från Windows Azure.  

14. Välj **Lägg till**och välj sedan **OK** för att stänga dialog rutan **certifikat egenskaper** .  

15. På sidan **begära certifikat** väljer du **certifikat för molnbaserad distributions plats för ConfigMgr** i listan över tillgängliga certifikat och väljer sedan **Registrera**.  

16. På sidan **certifikat installations resultat** väntar du tills certifikatet har installerats och väljer sedan **Slutför**.  

17. Stäng **Certifikat (lokal dator)**.  

###  <a name="export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddpexporting2008"></a>Exportera det anpassade webb Server certifikatet för molnbaserade distributions platser  
 Den här proceduren exporterar det anpassade webbservercertifikatet till en fil, så att det kan importeras när du skapar den molnbaserade distributionsplatsen.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>Exportera det anpassade webbservercertifikatet för molnbaserade distributionsplatser  

1. I konsolen **certifikat (lokal dator)** högerklickar du på det certifikat som du nyss installerade, väljer **alla uppgifter**och väljer sedan **Exportera**.  

2. I guiden Exportera certifikat väljer du **Nästa**.  

3. På sidan **Exportera privat nyckel** väljer du **Ja, exportera den privata nyckeln**och väljer sedan **Nästa**.  

   > [!NOTE]  
   >  Om detta alternativ inte är tillgängligt, har certifikatet skapats utan möjlighet att exportera den privata nyckeln. I så fall kan du inte exportera certifikatet i det format som krävs. Du måste konfigurera certifikat mal len så att den privata nyckeln kan exporteras och sedan begära certifikatet igen.  

4. På sidan **fil format för export** kontrollerar du att den **personliga informations Exchange-PKCS-#12 (. PFX)** är markerat.  

5. På sidan **lösen ord** anger du ett starkt lösen ord för att skydda det exporterade certifikatet med dess privata nyckel och väljer sedan **Nästa**.  

6. På sidan **fil som ska exporteras** anger du namnet på filen som du vill exportera och väljer sedan **Nästa**.  

7. Stäng guiden genom att välja **Slutför** i **guiden Exportera certifikat** och välj sedan **OK** i bekräftelse dialog rutan.  

8. Stäng **Certifikat (lokal dator)**.  

9. Lagra filen säkert och se till att du har åtkomst till den från Configuration Manager-konsolen.  

   Certifikatet är nu klart att importera när du skapar en molnbaserad distributionsplats.  

##  <a name="deploy-the-client-certificate-for-windows-computers"></a><a name="BKMK_client2008_cm2012"></a>Distribuera klient certifikatet för Windows-datorer  
 Den här certifikatdistributionen sker i följande steg:  

- Skapa och utfärda certifikat mal len för autentisering av arbets Station på certifikat utfärdaren  

- Konfigurera automatisk registrering av mallen för autentisering av arbets station med hjälp av grupprincip  

- Registrera certifikatet för autentisering av arbets Station automatiskt och verifiera installationen på datorer  

###  <a name="create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_client02008"></a>Skapa och utfärda certifikat mal len för autentisering av arbets Station på certifikat utfärdaren  
 Den här proceduren skapar en certifikatmall för Configuration Manager klient datorer och lägger till den i certifikat utfärdaren.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>Skapa och utfärda certifikatmallen för autentisering av arbetsstation på certifikatutfärdaren  

1.  På den medlems server som kör konsolen för certifikat utfärdare högerklickar du på **certifikatmallar**och väljer sedan **Hantera** för att läsa in hanterings konsolen för certifikatmallar.  

2.  I resultat fönstret högerklickar du på posten som har autentisering av **arbets Station** i kolumnen **mallens visnings namn** och väljer sedan **Duplicera mall**.  

3.  I dialog rutan **Duplicera mall** ser du till att **Windows 2003 Server, Enterprise Edition** är markerat och väljer sedan **OK**.  

    > [!IMPORTANT]  
    >  Välj inte **Windows 2008 Server, Enterprise Edition**.  

4.  I dialog rutan **Egenskaper för ny mall** går du till fliken **Allmänt** och anger ett Mallnamn, t. ex. **klient certifikat för ConfigMgr**, för att generera de klient certifikat som ska användas på Configuration Manager klient datorer.  

5.  Välj fliken **säkerhet** , Välj gruppen **domän datorer** och välj sedan de ytterligare behörigheterna **läsa** och **Registrera automatiskt**. Avmarkera inte **Registrera**.  

6.  Välj **OK**och Stäng **konsolen Certifikatmallar**.  

7.  Högerklicka på **certifikatmallar**i konsolen certifikat utfärdare, Välj **ny**och välj sedan **certifikatmall som ska utfärdas**.  

8.  I dialog rutan **Aktivera certifikatmallar** väljer du den nya mall som du nyss skapade, ConfigMgr- **klientcertifikat**och väljer sedan **OK**.  

9. Om du inte behöver skapa och utfärda fler certifikat stänger du **certifikat utfärdare**.  

###  <a name="configure-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a><a name="BKMK_client12008"></a>Konfigurera automatisk registrering av mallen för autentisering av arbets station med hjälp av grupprincip  
 Den här proceduren konfigurerar grupprincip att automatiskt registrera klient certifikatet på datorer.  

##### <a name="to-set-up-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>Konfigurera automatisk registrering av mallen för autentisering av arbets station genom att använda grupprincip  

1.  Välj **Start**på domänkontrollanten, Välj **administrations verktyg**och välj sedan **Grupprincip hantering**.  

2.  Gå till din domän, högerklicka på domänen och välj sedan **skapa ett grup princip objekt i den här domänen och länka det här**.  

    > [!NOTE]  
    >  Det här steget följer regelverket genom att skapa en ny grupprincip för anpassade inställningar, istället för att redigera den standarddomänprincip som installeras med Active Directory Domain Services. När du tilldelar den här grupprincip på domän nivå ska du tillämpa den på alla datorer i domänen. I en produktions miljö kan du begränsa den automatiska registreringen så att den bara registreras på valda datorer. Du kan tilldela grupprincip på en organisationsenhets nivå, eller så kan du filtrera domän grupprincip med en säkerhets grupp så att den endast gäller för datorerna i gruppen. Om du begränsar automatisk registrering måste du komma ihåg att ta med den server som har kon figurer ATS som hanterings plats.  

3.  I dialog rutan **nytt grup princip objekt** anger du ett namn, t. ex. **automatisk registrering av certifikat**, för den nya Grupprincip och väljer sedan **OK**.  

4.  I resultat fönstret går du till fliken **länkade Grupprincip objekt** , högerklickar på den nya Grupprincip och väljer sedan **Redigera**.  

5.  I **redigeraren Grupprinciphantering**, expanderar du **principer** under **dator konfiguration**och går sedan till **Windows-inställningar** / **säkerhets inställningar** / **principer för offentliga nycklar**.  

6.  Högerklicka på objekt typen **certifikat tjänst klienten-automatisk anmälan**och välj sedan **Egenskaper**.  

7.  I list rutan **konfigurations modell** väljer du **aktive rad**, Välj **förnya utgångna certifikat, uppdatera väntande certifikat, ta bort återkallade certifikat**, Välj **uppdatera certifikat som använder certifikatmallar**och välj sedan **OK**.  

8.  Stäng **Grupprincip hantering**.  

###  <a name="automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-computers"></a><a name="BKMK_client22008"></a>Registrera certifikatet för autentisering av arbets Station automatiskt och verifiera installationen på datorer  
 Den här proceduren installerar klientcertifikatet på datorer och verifierar installationen.  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>Registrera certifikatet för autentisering av arbets Station automatiskt och verifiera installationen på klient datorn  

1. Starta om arbets Stations datorn och vänta några minuter innan du loggar in.  

   > [!NOTE]  
   >  Att starta om datorn är det pålitligaste sättet att garantera att automatisk registrering av certifikat fungerar.  

2. Logga in med ett konto som har administratörs behörighet.  

3. I rutan Sök anger du **MMC. exe.** och trycker sedan på **RETUR**.  

4. I den tomma hanterings konsolen väljer du **fil**och sedan **Lägg till/ta bort snapin-modul**.  

5. I dialog rutan **Lägg till eller ta bort snapin-moduler** väljer du **certifikat** i listan över **Tillgängliga snapin-moduler**och väljer sedan **Lägg till**.  

6. I dialog rutan **snapin-modulen certifikat** väljer **du dator konto**och väljer sedan **Nästa**.  

7. I dialog rutan **Välj dator** kontrollerar du att **lokal dator: (den dator den här konsolen körs på)** är markerad och väljer sedan **Slutför**.  

8. I dialog rutan **Lägg till eller ta bort snapin-moduler** väljer du **OK**.  

9. I-konsolen expanderar du **certifikat (lokal dator)**, expanderar **personliga**och väljer sedan **certifikat**.  

10. I resultat fönstret bekräftar du att ett certifikat har **klientautentisering** i kolumnen **avsett syfte** och att **ConfigMgr-klientcertifikatet** finns i kolumnen **certifikatmall** .  

11. Stäng **Certifikat (lokal dator)**.  

12. Upprepa steg 1 till 11 för medlems servern för att kontrol lera att den server som ska konfigureras som hanterings plats också har ett klient certifikat.  

    Datorn har nu kon figurer ATS med ett Configuration Manager klient certifikat.  

##  <a name="deploy-the-client-certificate-for-distribution-points"></a><a name="BKMK_clientdistributionpoint2008_cm2012"></a>Distribuera klient certifikatet för distributions platser  

> [!NOTE]  
>  Det här certifikatet kan också användas för medieavbildningar som inte använder PXE-start, eftersom kraven på certifikaten är desamma.  

 Den här certifikatdistributionen sker i följande steg:  

- Skapa och utfärda en anpassad certifikatmall för autentisering av arbets Station på certifikat utfärdaren  

- Begär det anpassade certifikatet för autentisering av arbets Station  

- Exportera klient certifikatet för distributions platser  

###  <a name="create-and-issue-a-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_clientdistributionpoint02008"></a>Skapa och utfärda en anpassad certifikatmall för autentisering av arbets Station på certifikat utfärdaren  
 Den här proceduren skapar en anpassad certifikatmall för Configuration Manager distributions platser så att den privata nyckeln kan exporteras och lägger till certifikat mal len i certifikat utfärdaren.  

> [!NOTE]
>  Den här proceduren använder en annan certifikatmall än den certifikatmall som du skapade för klient datorer. Även om båda certifikaten kräver kapacitet för klientautentisering, kräver certifikatet för distributions platser att den privata nyckeln exporteras. Av säkerhets skäl bör du inte konfigurera certifikatmallar så att den privata nyckeln kan exporteras om inte denna konfiguration krävs. Distributions platsen kräver den här konfigurationen eftersom du måste importera certifikatet som en fil i stället för att välja den från certifikat arkivet.  
> 
>  När du skapar en ny certifikatmall för det här certifikatet kan du begränsa vilka datorer som kan begära ett certifikat vars privata nyckel kan exporteras. I vår exempel distribution kommer detta att vara den säkerhets grupp du tidigare skapade för Configuration Manager plats system servrar som kör IIS. I ett produktionsnätverk som distribuerar IIS-platssystemrollerna bör du överväga att skapa en ny säkerhetsgrupp för de servrar som kör distributionsplatser, så att du kan begränsa certifikatet till bara dessa platssystemservrar. Du kan även överväga att lägga till följande ändringar för det här certifikatet:  
> 
> - Kräv godkännande för att installera certifikatet för ytterligare säkerhet.  
>   - Öka certifikatets giltighetsperiod. Eftersom du måste exportera och importera certifikatet varje gång innan det går ut, minskar giltighets perioden hur ofta du måste upprepa den här proceduren. En ökning av giltighets perioden minskar dock också säkerheten för certifikatet, eftersom det ger mer tid för en angripare att dekryptera den privata nyckeln och stjäla certifikatet.  
>   - Använd ett anpassat värde i certifikatets ämnesfält eller fält för alternativt namn på certifikatmottagare (SAN) som hjälp att identifiera det här certifikatet bland standardklientcertifikaten. Detta kan vara till speciellt stor hjälp om du ska använda samma certifikat för flera distributionsplatser.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>Skapa och utfärda den anpassade certifikatmallen för autentisering av arbetsstation på certifikatutfärdaren  

1.  På den medlems server som kör konsolen för certifikat utfärdare högerklickar du på **certifikatmallar**och väljer sedan **Hantera** för att läsa in hanterings konsolen för certifikatmallar.  

2.  I resultat fönstret högerklickar du på posten som har autentisering av **arbets Station** i kolumnen **mallens visnings namn** och väljer sedan **Duplicera mall**.  

3.  I dialog rutan **Duplicera mall** ser du till att **Windows 2003 Server, Enterprise Edition** är markerat och väljer sedan **OK**.  

    > [!IMPORTANT]  
    >  Välj inte **Windows 2008 Server, Enterprise Edition**.  

4.  I dialog rutan **Egenskaper för ny mall** går du till fliken **Allmänt** och anger ett Mallnamn, t. ex. **certifikat för ConfigMgr-klientens distributions plats**, för att generera certifikatet för klientautentisering för distributions platser.  

5.  Välj fliken **hantering av begär Anden** och välj sedan **Tillåt att den privata nyckeln exporteras**.  

6.  Välj fliken **säkerhet** och ta bort behörigheten **Registrera** från säkerhets gruppen **företags administratörer** .  

7.  Välj **Lägg till**, ange **ConfigMgr IIS-servrar** i text rutan och välj sedan **OK**.  

8.  Välj behörigheten **Registrera** för gruppen och ta inte bort behörigheten **läsa** .  

9. Välj **OK**och Stäng **konsolen Certifikatmallar**.  

10. Högerklicka på **certifikatmallar**i konsolen certifikat utfärdare, Välj **ny**och välj sedan **certifikatmall som ska utfärdas**.  

11. I dialog rutan **Aktivera certifikatmallar** väljer du den nya mall som du precis skapade, certifikat för **ConfigMgr-klient distributions plats**och väljer sedan **OK**.  

12. Om du inte behöver skapa och utfärda fler certifikat stänger du **certifikat utfärdare**.  

###  <a name="request-the-custom-workstation-authentication-certificate"></a><a name="BKMK_clientdistributionpoint12008"></a>Begär det anpassade certifikatet för autentisering av arbets Station  
 Den här proceduren begär och installerar sedan det anpassade klient certifikatet på den medlems server som kör IIS och som ska konfigureras som en distributions plats.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>Begära det anpassade certifikatet för arbetsstationsautentisering  

1.  Välj **Start**, Välj **Kör**och ange sedan **MMC. exe.** Välj **Arkiv**i den tomma konsolen och välj sedan **Lägg till/ta bort snapin-modul**.  

2.  I dialog rutan **Lägg till eller ta bort snapin-moduler** väljer du **certifikat** i listan över **Tillgängliga snapin-moduler**och väljer sedan **Lägg till**.  

3.  I dialog rutan **snapin-modulen certifikat** väljer **du dator konto**och väljer sedan **Nästa**.  

4.  I dialog rutan **Välj dator** kontrollerar du att **lokal dator: (den dator den här konsolen körs på)** är markerad och väljer sedan **Slutför**.  

5.  I dialog rutan **Lägg till eller ta bort snapin-moduler** väljer du **OK**.  

6.  I-konsolen expanderar du **certifikat (lokal dator)** och väljer sedan **personligt**.  

7.  Högerklicka på **certifikat**, Välj **alla aktiviteter**och välj sedan **Begär nytt certifikat**.  

8.  Välj **Nästa**på sidan **innan du börjar** .  

9. Om sidan **Välj princip för certifikat registrering** visas väljer du **Nästa**.  

10. På sidan **begära certifikat** väljer du **certifikat för klient distributions plats för ConfigMgr** i listan över tillgängliga certifikat och väljer sedan **Registrera**.  

11. På sidan **certifikat installations resultat** väntar du tills certifikatet har installerats och väljer sedan **Slutför**.  

12. I resultat fönstret bekräftar du att ett certifikat har **klientautentisering** i kolumnen **avsett syfte** och att **certifikat för ConfigMgr-klientens distributions plats** finns i kolumnen **certifikatmall** .  

13. Stäng inte **Certifikat (lokal dator)**.  

###  <a name="export-the-client-certificate-for-distribution-points"></a><a name="BKMK_exportclientdistributionpoint22008"></a>Exportera klient certifikatet för distributions platser  
 Den här proceduren exporterar det anpassade certifikatet för autentisering av arbets station till en fil så att det kan importeras i egenskaperna för distributions platsen.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>Exportera klientcertifikatet för distributionsplatser  

1. I konsolen **certifikat (lokal dator)** högerklickar du på det certifikat som du nyss installerade, väljer **alla uppgifter**och väljer sedan **Exportera**.  

2. I guiden Exportera certifikat väljer du **Nästa**.  

3. På sidan **Exportera privat nyckel** väljer du **Ja, exportera den privata nyckeln**och väljer sedan **Nästa**.  

   > [!NOTE]  
   >  Om detta alternativ inte är tillgängligt, har certifikatet skapats utan möjlighet att exportera den privata nyckeln. I så fall kan du inte exportera certifikatet i det format som krävs. Du måste konfigurera certifikat mal len så att den privata nyckeln kan exporteras och sedan begära certifikatet igen.  

4. På sidan **fil format för export** kontrollerar du att den **personliga informations Exchange-PKCS-#12 (. PFX)** är markerat.  

5. På sidan **lösen ord** anger du ett starkt lösen ord för att skydda det exporterade certifikatet med dess privata nyckel och väljer sedan **Nästa**.  

6. På sidan **fil som ska exporteras** anger du namnet på filen som du vill exportera och väljer sedan **Nästa**.  

7. Stäng guiden genom att välja **Slutför** i **guiden Exportera certifikat** och välj **OK** i bekräftelse dialog rutan.  

8. Stäng **Certifikat (lokal dator)**.  

9. Lagra filen säkert och se till att du har åtkomst till den från Configuration Manager-konsolen.  

   Certifikatet är nu klart att importeras när du konfigurerar distributions platsen.  

> [!TIP]  
>  Du kan använda samma certifikat fil när du konfigurerar medie avbildningar för en operativ Systems distribution som inte använder PXE-start, och aktivitetssekvensen för att installera avbildningen måste kontakta en hanterings plats som kräver HTTPS-klientanslutningar.  

##  <a name="deploy-the-enrollment-certificate-for-mobile-devices"></a><a name="BKMK_mobiledevices2008_cm2012"></a>Distribuera registrerings certifikatet för mobila enheter  
 Den här certifikatdistributionen har en enda procedur för att skapa och utfärda en registreringscertifikatsmall på certifikatutfärdaren.  

### <a name="create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Skapa och utfärda registrerings certifikat mal len på certifikat utfärdaren  
 Den här proceduren skapar en registrerings certifikat mal len för Configuration Manager mobila enheter och lägger till den i certifikat utfärdaren.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Skapa och utfärda registreringscertifikatmallen på certifikatutfärdaren  

1. Skapa en säkerhets grupp som har användare som ska registrera mobila enheter i Configuration Manager.  

2. På den medlems server där certifikat tjänster är installerat högerklickar du på **certifikatmallar**i konsolen certifikat utfärdare och väljer sedan **Hantera** för att läsa in hanterings konsolen för certifikatmallar.  

3. I resultat fönstret högerklickar du på posten som har **Autentiserad session** i kolumnen **mallens visnings namn** och väljer sedan **Duplicera mall**.  

4. I dialog rutan **Duplicera mall** ser du till att **Windows 2003 Server, Enterprise Edition** är markerat och väljer sedan **OK**.  

   > [!IMPORTANT]  
   >  Välj inte **Windows 2008 Server, Enterprise Edition**.  

5. I dialog rutan **Egenskaper för ny mall** går du till fliken **Allmänt** och anger ett Mallnamn, t. ex. **registrerings certifikat för mobila**enheter i ConfigMgr, för att generera registrerings certifikaten för de mobila enheter som ska hanteras av Configuration Manager.  

6. Välj fliken **namn på certifikat mottagare** , se till att **skapa från den här Active Directory information** är markerat, Välj **eget namn** för **ämnes namnets format:** och ta sedan bort **användarens huvud namn (UPN)** från **ta med den här informationen i alternativt ämnes namn**.  

7. Välj fliken **säkerhet** , Välj säkerhets gruppen som har användare som har mobila enheter som ska registreras och välj sedan den ytterligare behörigheten **Registrera**. Avmarkera inte **Läsa**.  

8. Välj **OK**och Stäng **konsolen Certifikatmallar**.  

9. Högerklicka på **certifikatmallar**i konsolen certifikat utfärdare, Välj **ny**och välj sedan **certifikatmall som ska utfärdas**.  

10. I dialog rutan **Aktivera certifikatmallar** väljer du den nya mall som du nyss skapade, **registrerings certifikat för mobila enheter i ConfigMgr**och väljer sedan **OK**.  

11. Om du inte behöver skapa och utfärda fler certifikat stänger du konsolen certifikat utfärdare.  

    Certifikat mal len för registrering av mobila enheter är nu klar att väljas när du konfigurerar en profil för registrering av mobila enheter i klient inställningarna.  

##  <a name="deploy-the-client-certificate-for-mac-computers"></a><a name="BKMK_MacClient_SP1"></a>Distribuera klient certifikatet för Mac-datorer  

Den här certifikatdistributionen har en enda procedur för att skapa och utfärda en registreringscertifikatsmall på certifikatutfärdaren.  

###  <a name="create-and-issue-a-mac-client-certificate-template-on-the-certification-authority"></a><a name="BKMK_MacClient_CreatingIssuing"></a>Skapa och utfärda en Mac-certifikatmall på certifikat utfärdaren  
 Den här proceduren skapar en anpassad certifikatmall för Configuration Manager Mac-datorer och lägger till certifikat mal len i certifikat utfärdaren.  

> [!NOTE]  
>  Den här proceduren utnyttjar en annan certifikatmall än den som du kan ha skapat för Windows-klientdatorer eller för distributionsplatser.  
>   
>  När du skapar en ny certifikatmall för det här certifikatet kan du begränsa certifikatbegäran till behöriga användare.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>Skapa och utfärda certifikatmallen för Mac-klienter på certifikatutfärdaren  

1. Skapa en säkerhets grupp som har användar konton för administrativa användare som ska registrera certifikatet på Mac-datorn med hjälp av Configuration Manager.  

2. På den medlems server som kör konsolen för certifikat utfärdare högerklickar du på **certifikatmallar**och väljer sedan **Hantera** för att läsa in hanterings konsolen för certifikatmallar.  

3. I resultat fönstret högerklickar du på posten som visar **Autentiserad session** i kolumnen **mallens visnings namn** och väljer sedan **Duplicera mall**.  

4. I dialog rutan **Duplicera mall** ser du till att **Windows 2003 Server, Enterprise Edition** är markerat och väljer sedan **OK**.  

   > [!IMPORTANT]  
   >  Välj inte **Windows 2008 Server, Enterprise Edition**.  

5. I dialog rutan **Egenskaper för ny mall** går du till fliken **Allmänt** och anger ett Mallnamn, t. ex. **ConfigMgr Mac-klientcertifikat**, för att generera Mac-klientcertifikatet.  

6. Välj fliken **namn på certifikat mottagare** , se till att **skapa från den här Active Directory information** är markerat, Välj **eget namn** för **ämnes namnets format:** och ta sedan bort **användarens huvud namn (UPN)** från **ta med den här informationen i alternativt ämnes namn**.  

7. Välj fliken **säkerhet** och ta bort behörigheten **Registrera** från säkerhets grupperna **domän administratörer** och **företags administratörer** .  

8. Välj **Lägg till**, ange den säkerhets grupp du skapade i steg ett och välj sedan **OK**.  

9. Välj behörigheten **Registrera** för gruppen och ta inte bort behörigheten **läsa** .  

10. Välj **OK**och Stäng **konsolen Certifikatmallar**.  

11. Högerklicka på **certifikatmallar**i konsolen certifikat utfärdare, Välj **ny**och välj sedan **certifikatmall som ska utfärdas**.  

12. I dialog rutan **Aktivera certifikatmallar** väljer du den nya mall som du just har skapat, **ConfigMgr Mac-klientcertifikat**och väljer sedan **OK**.  

13. Om du inte behöver skapa och utfärda fler certifikat stänger du **certifikat utfärdare**.  

    Mac-klientens certifikatmall är nu klar att väljas när du konfigurerar klient inställningar för registrering.
