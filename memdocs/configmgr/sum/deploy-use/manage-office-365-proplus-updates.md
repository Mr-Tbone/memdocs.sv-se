---
title: Hantera uppdateringar till Microsoft 365-appar
titleSuffix: Configuration Manager
description: Configuration Manager synkroniserar Microsoft 365 appars klient uppdateringar från WSUS-katalogen till plats servern för att göra uppdateringar tillgängliga för distribution till klienter.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: d850e582b43e08743e5a61b17e6958ddc6084af1
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194148"
---
# <a name="manage-microsoft-365-apps-with-configuration-manager"></a>Hantera Microsoft 365 appar med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

> [!Note]
> Från och med den 21 april 2020 kommer Office 365 ProPlus att byta namn till **Microsoft 365 appar för företag**. Mer information finns i [namn ändring för Office 365 ProPlus](/deployoffice/name-change). Du kan fortfarande se referenser till det gamla namnet i Configuration Manager-konsolen och stöd dokumentationen medan-konsolen uppdateras.

Med Configuration Manager kan du hantera Microsoft 365 appar på följande sätt:

- [Distribuera Microsoft 365 appar](#bkmk_deploy): du kan starta installations programmet för Microsoft 365 Apps från [instrument panelen för Office 365-klient hantering](office-365-dashboard.md) för att göra det enklare att installera den inledande Microsoft 365 Apps. Med guiden kan du konfigurera installations inställningar för Microsoft 365 appar, ladda ned filer från Office Content Delivery Networks (CDN) och skapa och distribuera ett skript program med innehållet.

- [Distribuera uppdateringar för Microsoft 365 appar](#bkmk_update): du kan hantera klient uppdateringar för Microsoft 365 appar med hjälp av arbets flödet för program uppdaterings hantering. När Microsoft publicerar en ny uppdatering av Microsoft 365-appar till Office-Content Delivery Network (CDN) publicerar Microsoft även ett uppdaterings paket till Windows Server Update Services (WSUS). När Configuration Manager synkroniserar uppdateringar av Microsoft 365s appar från WSUS-katalogen till plats servern är uppdateringen tillgängliga för distribution till klienter.

   > [!NOTE]
   > Från och med Configuration Manager version 2002 kan du importera Microsoft 365 Apps-uppdateringar till frånkopplade miljöer. Mer information finns i [Synkronisera uppdateringar av Microsoft 365 appar från en frånkopplad program uppdaterings plats](../get-started/synchronize-office-updates-disconnected.md).   

- [Lägg till språk för Microsoft 365 appar uppdaterings nedladdningar](#bkmk_o365_lang): du kan lägga till stöd för Configuration Manager för att hämta uppdateringar för alla språk som stöds av Microsoft 365-appar. Det innebär att Configuration Manager inte behöver stödja språket så länge Microsoft 365 appar gör det. Innan Configuration Manager version 1610 måste du ladda ned och distribuera uppdateringar på samma språk som har kon figurer ATS på Microsoft 365 Apps-klienter.

- [Ändra uppdaterings kanalen](#bkmk_channel): du kan använda grup principer för att distribuera en ändring av register nyckel värden till Microsoft 365 appar klienter för att ändra uppdaterings kanalen.

Om du vill granska Microsoft 365 Apps-klient information och påbörja några av dessa hanterings åtgärder för Microsoft 365 appar använder du [instrument panelen för Office 365-klient hantering](office-365-dashboard.md).

## <a name="deploy-microsoft-365-apps"></a><a name="bkmk_deploy"></a> Distribuera Microsoft 365 appar
Starta installations programmet för Microsoft 365 Apps från instrument panelen för Office 365-klient hantering för den inledande Microsoft 365 Apps-installationen. Med guiden kan du konfigurera installations inställningar för Microsoft 365 appar, ladda ned filer från Office Content Delivery Network (CDN) och skapa och distribuera ett skript program för filerna. Innan Microsoft 365-appar har installerats på klienterna och [aktiviteten Microsoft 365 appar automatiska uppdateringar](/deployoffice/overview-update-process-microsoft-365-apps) inte är tillämpliga, är uppdateringar av Microsoft 365 program inte tillämpliga. I test syfte kan du köra uppdaterings aktiviteten manuellt.

För tidigare Configuration Manager-versioner måste du utföra följande steg för att installera Microsoft 365 appar för första gången på klienter:
- Hämta Office Deployment Tool (ODT)
- Ladda ned källfilerna för Microsoft 365 Apps-installationen, inklusive alla språk paket som du behöver.
- Generera Configuration.xml som anger rätt version och kanal för Microsoft 365 Apps.
- Skapa och distribuera antingen ett äldre paket eller ett skript program för att klienter ska kunna installera Microsoft 365 appar.

### <a name="requirements"></a>Krav
- Datorn som kör installations programmet måste ha Internet åtkomst.  
- Användaren som kör installations programmet måste ha **Läs** -och **Skriv** behörighet till den innehålls plats resurs som finns i guiden.
- Om du får ett fel meddelande om 404 hämtning kopierar du följande filer till mappen användare% Temp%:
  - [releasehistory.xml](https://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](https://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-microsoft-365-apps-using-configuration-manager-version-1806-or-higher"></a>Distribuera Microsoft 365 appar med Configuration Manager version 1806 eller senare: 
Från och med Configuration Manager 1806 är Office-anpassnings verktyget integrerat med installations programmet i Configuration Manager-konsolen. När du skapar en distribution för Microsoft 365 appar kan du konfigurera de senaste hanterings inställningarna dynamiskt. <!--1358149-->

1. I Configuration Manager-konsolen navigerar du till översikt över **program varu bibliotek**  >  **Overview**  >  **kontor 365-klient hantering**.
2. Klicka på **Office 365 installations program** i det övre högra fönstret. Installations guiden öppnas.
3. På sidan **program inställningar** anger du ett namn och en beskrivning för appen, anger nedladdnings platsen för filerna och klickar sedan på **Nästa**. Platsen måste anges som &#92;&#92;*server*&#92;*resurs*.
4. På sidan **Office-inställningar** klickar du på **gå till anpassnings verktyget för Office**. Då öppnas Office- [anpassnings verktyget för Klicka-och-kör](https://config.office.com).
5. Konfigurera önskade inställningar för installationen av Microsoft 365 Apps. Klicka på **Skicka** i det övre högra hörnet på sidan när du har slutfört konfigurationen. 
6. På sidan **distribution** bestämmer du om du vill distribuera nu eller vid ett senare tillfälle. Om du väljer att distribuera senare kan du hitta programmet i program **bibliotek**  >  **program hanterings**  >  **program**.  
7. Bekräfta inställningarna på sidan **Sammanfattning** . 
8. Klicka på **Nästa** och sedan på **Stäng** när guiden har slutförts. 

### <a name="deploy-microsoft-365-apps-using-configuration-manager-version-1802-and-prior"></a>Distribuera Microsoft 365 appar med Configuration Manager version 1802 och tidigare:

1. I Configuration Manager-konsolen navigerar du till översikt över **program varu bibliotek**  >  **Overview**  >  **kontor 365-klient hantering**.
2. Klicka på **Office 365 installations program** i det övre högra fönstret. Installations guiden öppnas.
3. På sidan **program inställningar** anger du ett namn och en beskrivning för appen, anger nedladdnings platsen för filerna och klickar sedan på **Nästa**. Platsen måste anges som &#92;&#92;*server*&#92;*resurs*.
4. På sidan **Importera klient inställningar** väljer du om du vill importera klient inställningarna för Microsoft 365 Apps från en befintlig XML-konfigurationsfil eller ange inställningarna manuellt. Klicka på **Nästa** när du är klar.  

    När du har en befintlig konfigurations fil anger du platsen för filen och hoppar till steg 7. Du måste ange platsen i formatet &#92;&#92;*server*&#92;*dela*&#92;*fil namn*. Fil.
    > [!IMPORTANT]    
    > XML-konfigurationsfilen får bara innehålla [språk som stöds av Office 2016](/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016).

5. På sidan **klient produkter** väljer du den Microsoft 365 Apps-svit som du använder. Välj de program som du vill inkludera. Välj ytterligare produkter som ska inkluderas och klicka sedan på **Nästa**.
6. På sidan **klient inställningar** väljer du de inställningar som ska inkluderas och klickar sedan på **Nästa**.
7. På sidan **distribution** väljer du om du vill distribuera programmet och klickar sedan på **Nästa**. <br/>Om du väljer att inte distribuera paketet i guiden går du vidare till steg 9.
8. Konfigurera resten av guide sidorna på samma sätt som för en typisk program distribution. Mer information finns i [skapa och distribuera ett program](../../apps/get-started/create-and-deploy-an-application.md).
9. Slutför guiden.
10. Du kan distribuera eller redigera programmet från program **bibliotek**  >  **Översikt**program  >  **hanterings**  >  **program**.

När du har skapat och distribuerat Microsoft 365 appar med hjälp av installations programmet hanterar Configuration Manager inte uppdateringar av Microsoft 365 appar som standard. Om du vill göra det möjligt för Microsoft 365 appar klienter att ta emot uppdateringar från Configuration Manager, se [distribuera uppdateringar för Microsoft 365 appar med Configuration Manager](#bkmk_update).

När du har distribuerat Microsoft 365 appar kan du skapa automatiska distributions regler för att underhålla apparna. Skapa en automatisk distributions regel för Microsoft 365 appar genom att klicka på **skapa en ADR** från [instrument panelen för Office 365-klient hantering](office-365-dashboard.md). Välj **Office 365-klient** när du väljer produkten. Mer information finns i [distribuera program uppdateringar automatiskt](automatically-deploy-software-updates.md).


## <a name="drill-through-required-microsoft-365-apps-updates"></a>Granska nödvändiga uppdateringar för Microsoft 365 appar
<!--4224414-->
*(Lanseras i version 1906)*

Du kan gå igenom efterlevnads statistik för att se vilka enheter som kräver en speciell Microsoft 365 program uppdatering av program vara. Om du vill visa enhets listan måste du ha behörighet att visa uppdateringar och de samlingar som enheterna tillhör. Så här ökar du detalj nivån i enhets listan:

1. Gå till **program varu bibliotek**  >  **kontor 365 klient hantering**  >  **Office 365 uppdateringar**.
1. Välj en uppdatering som krävs av minst en enhet.
1. Titta på fliken **Sammanfattning** och hitta cirkel diagrammet under  **statistik**.
1. Välj hyperlänken **vy som krävs** bredvid cirkel diagrammet för att öka detalj nivån i enhets listan.
1. Den här åtgärden tar dig till en tillfällig nod under **enheter** där du kan se vilka enheter som kräver uppdateringen. Du kan också utföra åtgärder för noden, till exempel skapa en ny samling från listan.


## <a name="deploy-microsoft-365-apps-updates"></a><a name="bkmk_update"></a> Distribuera uppdateringar för Microsoft 365 appar

Använd följande steg för att distribuera uppdateringar för Microsoft 365 appar med Configuration Manager:

1. [Kontrol lera kraven](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates) för att använda Configuration Manager för att hantera Microsoft 365 Apps-klient uppdateringar i avsnittet **krav för att använda Configuration Manager för att hantera Microsoft 365 Apps-klient uppdateringar** i artikeln.  

2. [Konfigurera program uppdaterings platser](../get-started/configure-classifications-and-products.md) för att synkronisera uppdateringarna för Microsoft 365 Apps-klienten. Ange **uppdateringar** för klassificeringen och välj **Office 365-klient** för produkten. Synkronisera program uppdateringar när du har konfigurerat program uppdaterings platserna att använda **uppdaterings** klassificeringen.
3. Aktivera Microsoft 365 appar klienterna ska ta emot uppdateringar från Configuration Manager. Använd Configuration Manager klient inställningar eller grup princip för att aktivera klienten.

    **Metod 1**: från och med Configuration Manager version 1606 kan du använda klient inställningen Configuration Manager för att hantera klient agenten för Microsoft 365-appar. När du har konfigurerat den här inställningen och distribuerat uppdateringar för Microsoft 365 appar kommunicerar Configuration Manager klient agenten med klient agenten för Microsoft 365-appar för att ladda ned uppdateringarna från en distributions plats och installera dem. Configuration Manager tar inventering av klient inställningar för Microsoft 365 Apps.    

      1. I Configuration Manager-konsolen klickar du på **Administration**  >  **Översikt**  >  **klient inställningar**.  

      2. Öppna lämpliga enhets inställningar för att aktivera klient agenten. Mer information om standard-och anpassade klient inställningar finns i [Konfigurera klient inställningar](../../core/clients/deploy/configure-client-settings.md).  

      3. Klicka på **program uppdateringar** och välj **Ja** för inställningen **aktivera hantering av klient agenten för Office 365** .  

    **Metod 2**:  [aktivera Microsoft 365 appar klienter att ta emot uppdateringar](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient) från Configuration Manager med hjälp av distributions verktyget för Office eller Grupprincip.  

4. [Distribuera uppdateringar för Microsoft 365-appar](deploy-software-updates.md) till klienter.

> [!NOTE]  
>
> Om Microsoft 365 appar installerades nyligen, och beroende på hur det har installerats, är det möjligt att uppdaterings kanalen inte har kon figurer ATS ännu. I så fall identifieras distribuerade uppdateringar som ej tillämpliga. Det finns en [schemalagd automatisk uppdaterings uppgift](/deployoffice/overview-of-the-update-process-for-office-365-proplus) som skapas när Microsoft 365 appar installeras. I den här situationen måste den här uppgiften köras minst en gång för att uppdaterings kanalen ska kunna konfigureras och uppdateringar identifieras som tillämpliga.
>
> Om Microsoft 365 appar har installerats nyligen och distribuerade uppdateringar inte identifieras, kan du i test syfte starta Office automatiska uppdateringar manuellt och sedan starta [utvärderings cykeln för program uppdaterings distribution](../understand/software-updates-introduction.md#scan-for-software-updates-compliance-process) på klienten. Instruktioner för hur du gör detta i en aktivitetssekvens finns i [uppdatera Microsoft 365 appar i en](manage-office-365-proplus-updates.md#bkmk_ts)aktivitetssekvens.

## <a name="restart-behavior-and-client-notifications-for-microsoft-365-apps-updates"></a>Omstarts beteende och klient meddelanden för uppdateringar av Microsoft 365 appar
När du distribuerar en uppdatering till en Microsoft 365 Apps-klient, är omstarts beteendet och klient meddelanden olika beroende på vilken version av Configuration Manager. Följande tabell innehåller information om slutanvändarens upplevelse när klienten får en uppdatering av Microsoft 365-appar:

|Configuration Manager version |Slutanvändarens upplevelse|  
|----------------|---------------------|
|1706, 1710|Klienten får popup-meddelanden och meddelanden i appen, samt en dialog ruta för nedräkning, innan du installerar uppdateringen.|
|1802| Klienten får popup-meddelanden och meddelanden i appen, samt en dialog ruta för nedräkning, innan du installerar uppdateringen. </br>Om några Microsoft 365 appar körs under en klient uppdatering tvingas Microsoft 365-apparna inte att stängas. I stället returneras uppdaterings installationen så att datorn måste startas om <!--510006-->|


> [!Important]
>
>Observera följande information i Configuration Manager version 1706:
>
>- En meddelande ikon visas i meddelande fältet i aktivitets fältet för obligatoriska appar där tids gränsen är inom 48 timmar i framtiden och uppdaterings innehållet har hämtats. 
>- En nedräknings dialog ruta visas för obligatoriska appar där tids gränsen är inom 7,5 timmar i framtiden och uppdateringen har laddats ned. Användaren kan skjuta upp nedräknings dialog rutan upp till tre gånger före tids gränsen. När den uppskjuts visas nedräkningen igen efter två timmar. Om den inte skjuts upp, finns det en slut för ande av 30 minuter och uppdatering installeras när nedräkningen går ut.
>- Ett popup-meddelande kanske inte visas förrän användaren klickar på ikonen i meddelande fältet. Om meddelande fältet har ett minimalt utrymme kan det hända att meddelande ikonen inte visas om användaren öppnar eller utökar meddelande området. 
>- Dialog rutan för meddelanden och nedräkning kan starta när användaren inte aktivt arbetar på enheten. Till exempel när enheten är låst över natten är det möjligt Microsoft 365 appar som körs på enheten kan tvingas att stängas för att installera uppdateringen. Innan du stänger appen sparar Office AppData för att förhindra data förlust. 
>- Om tids gränsen har passerats eller kon figurer ATS för att starta så snart som möjligt, kan körningen av Microsoft 365 appar tvingas stängas utan meddelanden. 
>- Om användaren installerar en uppdatering för Microsoft 365-appar före deadline, kontrollerar Configuration Manager att uppdateringen installeras när tids gränsen nås. Om uppdateringen inte identifieras på enheten installeras uppdateringen. 
>- Aviserings fältet i appen visas inte i en app som körs innan uppdateringen laddas ned. När uppdateringen har hämtats visas meddelandet i appen endast för nyligen öppnade appar.
>- För uppdateringar av Microsoft 365-appar som har utlösts av ett tjänst fönster eller som är schemalagda för icke-kontors tid kan det hända att Office-appar som körs kan tvingas att stängas för att installera uppdateringen utan meddelanden. 
>- Mer information finns i [meddelanden om slut användar uppdatering för Microsoft 365 appar](/deployoffice/end-user-update-notifications-microsoft-365-apps)


## <a name="add-languages-for-microsoft-365-apps-update-downloads"></a><a name="bkmk_o365_lang"></a> Lägg till språk för uppdaterings nedladdning för Microsoft 365-appar
Du kan lägga till stöd för Configuration Manager för att hämta uppdateringar för alla språk som stöds av Microsoft 365 appar.

### <a name="download-updates-for-additional-languages-in-version-1902"></a>Hämta uppdateringar för ytterligare språk i version 1902
<!--3555955-->

Från och med Configuration Manager version 1902 separerar uppdaterings arbets flödet 38-språken för **Windows Update** från de många ytterligare språken för **klient uppdatering för Office 365**.

Om du vill välja de språk som behövs använder du sidan **Val av språk** på följande platser:
- Guiden Skapa regel för automatisk distribution
- Guiden distribuera program uppdateringar
- Guiden Hämta program uppdateringar
- Egenskaper för automatisk distributions regel

På sidan **Val av språk** väljer du **Office 365-klient uppdatering**och klickar sedan på **Redigera**. Lägg till de språk som behövs för Microsoft 365 appar och klicka sedan på **OK**.

![Skärm bild som visar hur du lägger till ytterligare språk för Microsoft 365-appar](media/office-update-languages-selection.png)

### <a name="to-add-support-to-download-updates-for-additional-languages-in-version-1810-and-earlier"></a>För att lägga till stöd för att hämta uppdateringar för ytterligare språk i version 1810 och tidigare

Använd följande procedur på program uppdaterings platsen på den centrala administrations platsen eller den fristående primära platsen.

> [!IMPORTANT]  
> Konfiguration av ytterligare Microsoft 365-appar uppdaterings språk är en inställning för hela platsen. När du har lagt till språken med hjälp av följande procedur laddas alla uppdateringar för Microsoft 365-appar ned på dessa språk, samt de språk som du väljer på sidan **Val av språk** i guiden hämta program uppdateringar eller distribuera program uppdateringar.

1. Från en kommando tolk skriver du *WBEMTest* som en administrativ användare för att öppna Windows Management Instrumentation testaren.
2. Klicka på **Anslut**och skriv sedan *root\sms\ site_ &lt; siteCode &gt; *.
3. Klicka på **fråga**och kör sedan följande fråga: *välj &#42; från SMS_SCI_Component där componentname = "SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![WMI-fråga](../media/1-wmiquery.png)
4. I resultat fönstret dubbelklickar du på objektet med plats koden för den centrala administrations platsen eller den fristående primära platsen.
5. Välj egenskapen **Props** , klicka på **Redigera egenskap**och klicka sedan på **Visa inbäddade**.
   ![Egenskaps redigerare](../media/2-propeditor.png)
6. Börja med det första frågeresultatet och öppna varje objekt tills du hittar det med **AdditionalUpdateLanguagesForO365** för egenskapen **PropertyName** .
7. Välj **värde2** och klicka på **Redigera egenskap**.  
   ![Redigera egenskapen värde2](../media/3-queryresult.png)
8. Lägg till ytterligare språk i egenskapen **värde2** och klicka på **Spara egenskap**. <br/> Till exempel pt-pt (för portugisiska-Portugal), AF za (för Afrikaans-Sydafrika), nn-no (för norska (nynorsk)-Norge) osv. Du skulle skriva `pt-pt,af-za,nn-no` för exempel språken. Använd inte blank steg mellan språken.
 
   ![Lägg till språk i egenskaps redigeraren](../media/4-props.png)  
9. Klicka på **Stäng**, klicka på **Stäng**, klicka på **Spara egenskap**och klicka på **Spara objekt** (om du klickar på **Stäng** här ignoreras värdena). Klicka på **Stäng**och avsluta Windows Management Instrumentation testaren genom att klicka på **Avsluta** .
10. I Configuration Manager-konsolen går du till **Software Library**  >  **Översikt över**program bibliotek  >  **kontor 365 klient hantering**  >  **Office 365 uppdateringar**.
11. Nu när du hämtar uppdateringar för Microsoft 365 appar laddas uppdateringarna ned på de språk som du väljer i guiden och konfigureras i den här proceduren. För att kontrol lera att uppdateringarna laddas ned på rätt språk går du till paket källan för uppdateringen och letar efter filer med språk koden i fil namnet.  
    ![Fil namn med ytterligare språk](../media/5-verification.png)

## <a name="updating-microsoft-365-apps-in-a-task-sequence"></a><a name="bkmk_ts"></a> Uppdatera Microsoft 365 appar i en aktivitetssekvens
När du använder steget [installera program uppdateringar](../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates) för att installera uppdateringar av Microsoft 365 appar, är det möjligt att distribuerade uppdateringar identifieras som ej tillämpliga.  Detta kan inträffa om aktiviteten schemalagda Office automatiska uppdateringar inte körs minst en gång (se kommentaren i [distribuera uppdateringar för Microsoft 365 appar](manage-office-365-proplus-updates.md#bkmk_update)). Detta kan till exempel inträffa om Microsoft 365-appar har installerats direkt innan du kör det här steget.

För att se till att uppdaterings kanalen är inställd så att distribuerade uppdateringar identifieras korrekt, använder du någon av följande metoder:

**Metod 1:**
1. Öppna Schemaläggaren (taskschd. msc) på en dator med samma version av Microsoft 365-appar och identifiera aktiviteten Microsoft 365 Apps automatiska uppdateringar. Normalt finns den under Schemaläggaren- **bibliotek**  > **Microsoft** > **Office**.
2. Högerklicka på aktiviteten automatiska uppdateringar och välj **Egenskaper**.
3. Gå till fliken **åtgärder** och klicka på **Redigera**. Kopiera kommandot och eventuella argument. 
4. Redigera aktivitetssekvensen i Configuration Manager-konsolen.
5. Lägg till ett nytt **körnings kommando rads** steg innan steget **installera program uppdateringar** i aktivitetssekvensen. Om Microsoft 365 appar installeras som en del av samma aktivitetssekvens kontrollerar du att det här steget körs när Office har installerats.
6. Kopiera i kommandot och argumenten som du har samlat in från Office automatiska uppdateringar schemalagda aktiviteter. 
7. Klicka på **OK**. 

**Metod 2:**
1. Öppna Schemaläggaren (taskschd. msc) på en dator med samma version av Microsoft 365-appar och identifiera aktiviteten Microsoft 365 Apps automatiska uppdateringar. Normalt finns den under Schemaläggaren- **bibliotek**  > **Microsoft** > **Office**.
2. Redigera aktivitetssekvensen i Configuration Manager-konsolen.
3. Lägg till ett nytt **körnings kommando rads** steg innan steget **installera program uppdateringar** i aktivitetssekvensen. Om Microsoft 365 appar installeras som en del av samma aktivitetssekvens kontrollerar du att det här steget körs när Office har installerats.
4. I fältet kommando rad anger du den kommando rad som ska köra den schemalagda aktiviteten. Se exemplet nedan och se till att strängen i citat tecken matchar sökvägen och namnet på uppgiften som identifierades i steg 1.  

    Exempel: `schtasks /run /tn "\Microsoft\Office\Office Automatic Updates 2.0"`
5. Klicka på **OK**. 

## <a name="update-channels-for-microsoft-365-apps"></a><a name="bkmk_channel"></a> Uppdatera kanaler för Microsoft 365 appar
<!--6298093-->
När Office 365 ProPlus har bytt namn till **Microsoft 365 appar för företag**, ändrades även uppdaterings kanalernas namn. Om du använder en automatisk distributions regel (ADR) för att distribuera uppdateringar måste du göra ändringar i automatisk distribution om de är beroende av egenskapen **title** . Det beror på att namnet på uppdaterings paketen i Microsoft Updates katalogen ändras.

För närvarande börjar rubriken på ett uppdaterings paket för Office 365 ProPlus med "Office 365-klient uppdatering" som visas i följande exempel:

&nbsp;&nbsp;Office 365-klient uppdatering – halvårs kanal Version 1908 för x64-baserad utgåva (version 11929,20648)

För uppdaterings paket som släpps den 9 juni kommer rubriken att börja med "Microsoft 365 uppdatering av appar" som visas i följande exempel:

&nbsp;&nbsp;Uppdatering av Microsoft 365-appar – halvårs kanal Version 1908 för x64-baserad utgåva (version 11929,50000)
</br>
</br>

|Nytt kanal namn|Föregående kanal namn|
|--|--|
|Halvårs årlig företags kanal|Halvårskanal|
|Halvårs visare för företags kanal (för hands version)|Halvårskanal (riktad)|
|Månatlig företags kanal|NA|
|Aktuell kanal|Månads kanal|
|Aktuell kanal (förhands granskning)|Månads kanal (riktad)|
|Beta kanal|Insider|

Mer information om hur du ändrar din automatisk distribution finns i [distribuera program uppdateringar automatiskt](automatically-deploy-software-updates.md). Mer information om namn ändringen finns i [namn ändring för Office 365 ProPlus](/deployoffice/name-change).


## <a name="change-the-update-channel-after-you-enable-microsoft-365-apps-clients-to-receive-updates-from-configuration-manager"></a>Ändra uppdaterings kanalen när du har aktiverat Microsoft 365 Apps-klienter för att ta emot uppdateringar från Configuration Manager

När du har distribuerat Microsoft 365 appar kan du ändra uppdaterings kanalen med grupprincip eller Office Deployment Tool (ODT). Du kan till exempel flytta en enhet från halvårs kanal till halvårs kanal (riktad). När du byter kanal uppdateras Office automatiskt utan att du behöver installera om eller ladda ned den fullständiga versionen. Mer information finns i [ändra Microsoft 365 Apps uppdaterings kanal för enheter i din organisation](/deployoffice/change-update-channels).

## <a name="next-steps"></a>Nästa steg

Använd instrument panelen för Office 365-klient hantering i Configuration Manager om du vill granska Microsoft 365 Apps-klient information och distribuera Microsoft 365 appar. Mer information finns i [instrument panelen för Office 365-klient hantering](office-365-dashboard.md).