---
title: Skapa uppdateringar
titleSuffix: Configuration Manager
description: Skapa och paketera program uppdateringar med System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 46a1a8ac-126c-4ee6-ae09-32dfbdb83368
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b2445158732f5adf21c43d73b13039f9e41610c8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723987"
---
# <a name="create--software-updates-and-update-bundles-with-updates-publisher"></a>Skapa program uppdateringar och uppdaterings paket med Updates Publisher

*Gäller för: System Center Updates Publisher*

Med Updates Publisher kan du använda guiden **skapa uppdatering** för att skapa egna uppdateringar och guiden **skapa paket** för att skapa paket uppdateringar.

Eftersom dessa två guider har ett liknande arbets flöde, refererar proceduren för att skapa ett uppdaterings paket till proceduren för att skapa uppdateringar, med enbart de relevanta skillnaderna som beskrivs.

## <a name="use-the-create-update-wizard"></a>Använda guiden skapa uppdatering
1. Gå till **arbets ytan uppdateringar**i-konsolen och välj sedan **Uppdatera** på fliken **Start** i menyfliksområdet i rutan **komma igång** . Då öppnas guiden **skapa uppdatering** .

2. På sidan **paket** använder du följande information som hjälp för att konfigurera uppdateringen:

   -   Välj **Bläddra** för att hitta det program uppdaterings paket som du vill använda som paket källa. Giltiga källor är. MSI,. MSP eller. EXE-filer. Updates Publisher kräver åtkomst till filen för att skapa en fil-hash. Hash-och fil namnet används sedan i uppdatera metadata för uppdateringen som du skapar.

   -   Ange käll platsen för innehållet för den här uppdateringen. Normalt är detta den plats där uppdateringen av binärfilen kommer att laddas ned från vid publicering till en WSUS-server.  Om alternativet **Använd en lokal källa för att publicera program uppdaterings innehåll** är markerat, krävs inte sökvägen.

       Senare, när uppdateringen publiceras på en WSUS-server, laddar Updates Publisher binärfilerna för uppdateringen från den angivna käll platsen.  Om ingen sökväg anges söker uppdaterings utgivare i den [lokala käll publicerings Sök vägen](updates-publisher-options.md#advanced) för den binära uppdateringen.

   -   Ange program uppdateringens **binära språk** .

   -   Ange **lyckade retur koder**och **lyckade start koder** för uppdateringen. Avgränsa flera retur koder med kommatecken. Du kan använda retur koder för att avgöra när installationen av uppdateringen lyckades och när omstarter krävdes.

       -   Windows Installer-filer och korrigeringsfiler (. MSI och. MSP-filer) anger värdena automatiskt och kan inte ändras.

       -   Söker. EXE-uppdateringar, standard koderna som definierats av. EXE-filen används om inga retur koder anges.

   -   Ange eventuella kommando rads argument som krävs för att installera program uppdateringen.

       -   Windows Installer-filer och korrigeringsfiler (. MSI och. MSP-filer) anger dessa värden automatiskt. För de här fil typerna måste argumenten anges som ** \[namn\]=\[värde\]**. Dessutom stöds inte alla alternativ som börjar med a **/** (som **/Qn**) för. MSI eller. MSP-programuppdateringar.

       -   Söker. EXE-uppdateringar, alla argument är giltiga.

3. På sidan **information** anger du information om uppdateringen som ingår när uppdateringen publiceras eller exporteras. Informationen innehåller lokaliserade egenskaper som namn på uppdateringar (rubrik) och beskrivning. Sedan kan du ange mer allmän information som klassificering, leverantör, produkt och var du vill veta mer om uppdateringen.

    __Lokaliserade egenskaper:__

   - **Språk**: Välj ett språk och ange sedan en rubrik och en beskrivning. Du kan sedan välja ytterligare språk, ett i taget, med varje språk som har stöd för en egen titel och beskrivning.

   - **Rubrik**: Ange namnet på uppdateringen. Det här namnet visas i arbets ytan uppdateringar i Updates Publisher-konsolen.

   - **Beskrivning**: en egen beskrivning av uppdateringen. Du kan inkludera vad uppdateringen installeras och varför eller när det ska användas.

   **Klassificering:** Här följer några vanliga beskrivningar av de olika klassificeringarna.

   - **Uppdatering**: en uppdatering av ett program eller en fil som är installerad för närvarande.

   - **Kritisk**: en brett utgiven uppdatering för ett särskilt problem som åtgärdar en kritisk bugg som inte är relaterad till säkerhet.

   - **Funktions paket**: nya produkt funktioner som distribueras utanför en produkt lansering och som vanligt vis ingår i nästa fullständiga produkt lansering.

   - **Säkerhet**: en brett utgiven uppdatering för ett produktspecifik problem som är relaterat till säkerhet.

   - **Samlad uppdatering**: en kumulativ uppsättning snabb korrigeringar som är paketerade tillsammans för enkel distribution. Snabbkorrigeringarna kan bland annat innehålla säkerhetsuppdateringar, kritiska uppdateringar och uppdateringar. En samlad uppdatering hanterar vanligt vis ett speciellt utrymme, till exempel säkerhet eller en produkt funktion.

   - **Service Pack**: en kumulativ uppsättning snabb korrigeringar som tillämpas på ett program. Snabbkorrigeringarna kan bland annat innehålla säkerhetsuppdateringar, kritiska uppdateringar och programuppdateringar.

   - **Verktyg**: anger ett verktyg eller en funktion som hjälper dig att slutföra en eller flera uppgifter.

   - **Driv rutin**: en uppdatering för driv rutins program vara.

   **Leverantör:** Ange en leverantör för uppdateringen. Du kan använda List rutan för att använda värden från uppdateringar som finns i lagrings platsen. När du anger en leverantör skapar guiden en mapp med det leverantörs namnet under **alla program uppdateringar** i **arbets ytan uppdateringar** om mappen inte redan finns. Följande är Windows Server Update Services (WSUS) reserverade namn som inte kan anges för uppdateringar som du skapar:
   - Microsoft Corporation
   - Microsoft
   - Uppdatera
   - Programuppdatering
   - Verktyg
   - Verktyg
   - Kritisk
   - Kritiska uppdateringar
   - Säkerhet
   - Säkerhetsuppdateringar
   - Funktions paket
   - Samlad uppdatering
   - Service Pack
   - Drivrutin
   - Driv rutins uppdatering
   - Paket
   - Paket uppdatering

   **Produkt**: ange vilken typ av produkt uppdateringen gäller. Du kan använda List rutan för att använda värden från uppdateringar som finns i lagrings platsen. Samma lista med reserverade WSUS-namn som inte kan användas för **leverantören**, kan inte användas för **produkten**.

   **Mer info-URL**: Ange URL: en där du hittar mer information om den här uppdateringen. Du måste använda gemena bokstäver för **https** eller **http** när du anger den här URL: en.

4. På sidan **valfri information** kan du konfigurera information som innehåller ytterligare information om uppdateringen.

   -   **Bulletin-ID**: Bulletin-ID: n är vanligt vis, men inte alltid, från uppdaterings leverantörer.

   -   **Artikel-ID**: om det finns en program uppdaterings artikel kan artikel-ID: t vara användbart för personer som vill ha ytterligare information om uppdateringen.

   -   **CVE-ID:** Visa en lista med en eller flera vanliga sårbarheter och CVE-identifierare som tillhandahåller säkerhets information om uppdateringen eller uppdaterings paketet. När fler än en lista visas använder du ett semikolon för att avgränsa CVEs som i det här exemplet: *CVE1; CVE2.*

   -   **Support-URL:** Ange den URL som innehåller supportinformation för den här uppdateringen, om den är tillgänglig. Du måste använda gemena bokstäver för **https** eller **http** när du anger den här URL: en.

   -   **Allvarlighets grad:** Ange allvarlighets grad för den här uppdateringen.

   -   **Påverkan:** Följande alternativ kan användas för att ange påverkan:
       -   **Normal –** Använd detta för att ange att uppdateringen kräver vanliga installations procedurer.
       -   **Mindre –** Använd detta för att ange att uppdateringen kräver minimala installations procedurer.
       -   **Kräver exklusiv hantering –** Använd detta för att ange att uppdateringen måste installeras separat, utan endast från andra uppdateringar.   <br /><br />

   -   **Omstarts beteende:** Använd detta för att ange information om beteendet vid omstart av uppdateringar. Den här inställningen påverkar inte det faktiska beteendet för installationen av uppdateringen.

       -   **Startar aldrig**om: datorn utför aldrig en omstart av systemet när program uppdateringen har installerats.
       -   **Kräv alltid omstart**: datorn utför alltid en omstart av systemet när program uppdateringen har installerats.
       -   **Kan begära omstart**: när program uppdateringen har installerats begär datorn en omstart av systemet endast om en omstart krävs. Användaren kan välja att skjuta upp omstarten. Detta är standardvärdet. <br /><br />

5. På sidan **krav** anger du de krav som måste vara installerade på en dator innan den här uppdateringen kan installeras. Krav kan vara **detectoids** eller andra uppdateringar. Detectoids är högnivå regler som en som kräver att datorerna CPU är en 64-bitars processor. Detectoids kan också ange vilka uppdateringar som måste installeras innan den här uppdateringen kan installeras.

   -   Du får bättre prestanda om du använder detectoids i stället för att skapa *installerbara* och *installerade regler* som utför samma kontroll eller åtgärd.

   Använd sökalternativet för **tillgängliga program uppdateringar och detectoids** som hjälper dig att hitta vissa uppdateringar eller detectoids. Sök till exempel efter **CPU** för att hitta detectoids som gör att du kan begränsa installationen utifrån en speciell CPU-arkitektur.

   Du kan välja ett eller flera objekt i taget för att lägga till som en förutsättning. När du lägger till nödvändiga komponenter läggs de valda detectoids till som en eller flera grupper. För att du ska kunna installera måste en dator uppfylla kravet på minst en medlem i varje grupp som du konfigurerar:

   -   När du klickar på **Lägg till förutsättning** läggs alla objekt som du har valt till i separata, enskilda grupper. För att du ska kunna kvalificera sig för den här uppdateringen måste en dator uppfylla kraven i den här gruppen och skicka krav för ytterligare grupper som är konfigurerade.

   -   När du klickar på **Lägg till grupp** läggs alla objekt som du har valt till i en enda grupp. För att kunna kvalificera sig för den här uppdateringen måste en dator uppfylla minst en av kraven i den här gruppen och skicka krav för ytterligare grupper som har kon figurer ATS.

6. På sidan **ersätta** anger du de uppdateringar som ersätts (ersatts) av den här uppdateringen. När den här uppdateringen har publicerats markerar Configuration Manager varje uppdatering som ersätts som **upphört att gälla**. Klienterna kommer sedan att installera den här uppdateringen i stället för de ersatta uppdateringarna.

7. På sidan **tillämpbar** använder du **regel redigeraren** för att definiera en uppsättning regler som avgör om en enhet behöver den här uppdateringen. (Den här sidan liknar den **installerade** sidan, som följer.)

   Om du vill lägga till en ny regel klickar du på ![Ny regel](media/newrule.png). Då öppnas Tillämplighets regel sidan där du kan konfigurera regler.

   Typer av regler som du kan skapa är:

   -   **Fil** – Använd den här regeln för att kräva att en enhet har en fil med egenskaper som uppfyller ett eller flera villkor som du anger innan uppdateringen kan tillämpas.

   -   **Register –** Använd den här typen för att ange register information som måste finnas innan en enhet kvalificerar sig för att installera den här uppdateringen.

   -   **System –** Den här regeln använder system information för att fastställa tillämplighet. Du kan välja mellan att definiera en Windows-version, ett Windows-språk, en processor arkitektur eller ange en WMI-fråga för att identifiera enheternas operativ system.

   -   **Windows Installer –** Använd den här regel typen för att fastställa tillämplighet baserat på en installerad. MSI eller Windows Installer korrigering (. MSP). Du kan också bestämma om vissa komponenter eller funktioner installeras som en del av kravet.

       > [!IMPORTANT]  
       > På hanterade enheter kan Windows Update-agenten inte identifiera Windows installations paket som är installerade per användare. När du använder den här regel typen konfigurerar du ytterligare tillämplighets regler, t. ex. fil versioner eller register nyckel värden, så att Windows Installer-paketet kan identifieras på rätt sätt oavsett per användare eller per system.

   -   **Sparad regel –** Med det här alternativet kan du hitta och använda regler som du har *skapat i arbets ytan regler*.

       När du har skapat en regel kan du använda de andra ikonerna för att ändra regeln och om det finns flera regler för att definiera relationer mellan dessa regler.

   När du är klar med att skapa och lägga till regler klickar du på **OK** i dialog rutan **Skapa regel uppsättning** för att spara uppsättningen. Du kan sedan skapa en **ny** regel och även lägga till den till uppsättningen.

   När du har flera regler eller regel uppsättningar som ska läggas till i en uppdatering kan du använda de logiska operatorerna i **regel redigeraren** för att fastställa villkor mellan reglerna och i vilken ordning de bearbetas.

8. På sidan **installerad** använder du **regel redigeraren för att** definiera en uppsättning regler som avgör om en enhet redan har installerat uppdateringen som du konfigurerar. (Den här sidan liknar sidan **tillämplighets** , som fortsätter med den här sidan.)

   Den här sidan i guiden har stöd för att konfigurera regler med samma alternativ och kriterier som **tillämplighets** sidan.

   När guiden slutförs läggs den nya uppdateringen till i en nod på **arbets ytan uppdateringar** som identifieras av **leverantören** och **produkt** namnet som du använde för uppdateringen.

## <a name="use-the-create-bundle-wizard"></a>Använda guiden Skapa paket
Eftersom den här guiden använder samma arbets flöde som [guiden skapa uppdatering](#use-the-create-update-wizard), använder du det arbets flödet, men Observera följande skillnad för paket:

1.  Starta guiden genom att gå till **arbets ytan uppdateringar**i-konsolen och sedan välja **Paketera** från fliken **Start** i menyfliksområdet.

2.  Till skillnad från guiden skapa uppdatering finns det ingen paket sida när du skapar ett paket.

3.  På sidan **information** anger du information om uppdaterings paketet som ingår när uppdateringen publiceras eller exporteras.

4.  På sidan **valfri information** kan du konfigurera information som innehåller ytterligare information om uppdaterings paketet. De tillgängliga alternativen är desamma som för att skapa en uppdatering. Dock är alternativen för effekter och omstarts beteende inte tillgängliga eftersom de inte gäller för paket.

5.  På sidan **krav** anger du de krav som måste vara installerade på en dator innan paketet kan installeras. De här reglerna är desamma som de som visas för enskilda uppdateringar.

6.  På sidan **ersätta** anger du de uppdateringar som ersätts (ersatts) av det här uppdaterings paketet. De här reglerna är desamma som de som visas för enskilda uppdateringar.

7.  På sidan **medlemmar** väljer du uppdateringar som ska läggas till i uppdaterings paketet. Endast uppdateringar som du har skapat eller importerat till Updates Publisher är tillgängliga.

När guiden slutförs läggs det nya uppdaterings paketet till i en nod på **arbets ytan uppdateringar** som identifieras av det **leverantörs** namn som du använde för uppdaterings paketet.
