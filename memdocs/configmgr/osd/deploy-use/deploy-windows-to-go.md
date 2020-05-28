---
title: Distribuera Windows To Go
titleSuffix: Configuration Manager
description: Lär dig hur du etablerar Windows To Go i Configuration Manager för att skapa en Windows To Go-arbetsyta som startar från en extern enhet.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8eed50f5-80a4-422e-8aa6-a7ccb2171475
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: add0d17205cc82b30f3a88558c690a813239b92a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906939"
---
# <a name="deploy-windows-to-go-with-configuration-manager"></a>Distribuera Windows To Go med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det här avsnittet innehåller anvisningar för hur du etablerar Windows To Go i Configuration Manager. Windows To Go är en företagsfunktion i Windows 8 som gör att du kan skapa en Windows To Go-arbetsyta som kan startas från ett USB-minne på datorer som uppfyller certifikatkraven för Windows 7 eller Windows 8, oavsett vilket operativsystem som körs på datorn. Windows To Go-arbetsytor kan använda samma avbildning som företag använder för sina skrivbordsdatorer och bärbara datorer, och kan hanteras på samma sätt.  

 Mer information om Windows To Go finns i [funktions översikt över Windows To Go](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh831833(v=ws.11)).  

## <a name="provision-windows-to-go"></a>Etablera Windows To Go  
 Windows To Go är ett operativsystem som är lagrat på ett USB-minne. Du kan etablera Windows To Go-enheten på ungefär samma sätt som du etablerar andra distributioner av operativsystem. Men eftersom Windows To Go är utformat som en användarorienterad och i hög grad mobil lösning måste du gå till väga på ett något annat sätt när du etablerar de här enheterna.  

 På hög nivå är Windows To Go en distribution i två faser som gör att du kan konfigurera Windows To Go-enheten och förinstallerat innehåll för operativsystemsdistributionen. Du kan uppnå detta med minimal påverkan på användaren och begränsa stillestånds tiden för användarens dator. När du har förberett datorn måste du slutföra hela etableringen för att säkerställa att datorn är klar för användaren. Etableringen går till på liknande sätt som den aktuella operativsystemsdistributionen. Här visas det allmänna arbetsflödet för att förinstallera innehåll och etablera Windows To Go:  

1.  [Krav för att etablera Windows To Go](#BKMK_Prereqs)  

2.  [Skapa förinstallerade media](#BKMK_CreatePrestagedMedia)  

3.  [Skapa ett Windows To Go Creator-paket](#BKMK_CreatePackage)  

4.  [Uppdatera aktivitetssekvensen för att aktivera BitLocker för Windows To Go](#BKMK_UpdateTaskSequence)  

5.  [Distribuera Windows To Go Creator-paketet och aktivitetssekvensen](#BKMK_Deployments)  

6.  [Användaren kör Windows To Go Creator](#BKMK_UserExperience)  

7.  [Configuration Manager konfigurerar och faser i Windows To Go-enheten](#BKMK_ConfigureStageDrive)  

8.  [Användaren loggar in på Windows 8](#BKMK_UserLogsIn)  

###  <a name="prerequisites-to-provision-windows-to-go"></a><a name="BKMK_Prereqs"></a> Krav för att etablera Windows To Go  
 Innan du etablerar Windows To Go måste du slutföra följande i Configuration Manager:  

-   **Distribuera en startavbildning till en distributionsplats**  

     Innan du skapar ett förberett medium måste du distribuera startavbildningen till en distributionsplats.  

    > [!NOTE]  
    >  Start avbildningar används för att installera operativ systemet på mål datorerna i din Configuration Managers miljö. Avbildningarna innehåller en Windows PE-version som installerar operativsystemet och andra enhetsdrivrutiner som krävs. Configuration Manager tillhandahåller två start avbildningar: en som stöder x86-plattformar och en som stöder x64-plattformar. Du kan också skapa egna startavbildningar. Mer information finns i [Hantera start avbildningar](../get-started/manage-boot-images.md).  

-   **Distribuera Windows 8-operativsystemavbildningen till en distributionsplats**  

     Innan du skapar ett förberett medium måste du distribuera Windows 8-operativsystemavbildningen till en distributionsplats.  

    > [!NOTE]  
    >  Operativsystemavbildningar är WIM-filer som representerar en komprimerad samling av referensfiler och mappar som behövs för att installera och konfigurera ett operativsystem på en dator. Mer information finns i [Hantera operativ Systems avbildningar](../get-started/manage-operating-system-images.md).  

-   **Skapa en aktivitetssekvens för att distribuera Windows 8**  

     Du måste skapa en aktivitetssekvens för en Windows 8-distribution som du sedan hänvisar till när du skapar ett förberett medium. Mer information finns i [Hantera aktivitetssekvenser för att automatisera uppgifter](manage-task-sequences-to-automate-tasks.md).  

###  <a name="create-prestaged-media"></a><a name="BKMK_CreatePrestagedMedia"></a>Skapa för beredda medier  
 Ett förberett medium innehåller den startavbildning som används för att starta måldatorn och den operativsystemavbildning som används på måldatorn. Den dator som du etablerar med förberedda medier kan startas med hjälp av startavbildningen. Datorn kan sedan köra en aktivitetssekvens för distribution av det befintliga operativsystemet för att installera en fullständig operativsystemdistribution. Den aktivitetssekvens som distribuerar operativsystemet ingår inte i mediet.  

 Du kan lägga till innehåll, till exempel program och enhetsdrivrutiner, förutom operativsystemavbildningen och startavbildningen under förberedelsefasen. På så vis går det snabbare att distribuera ett operativsystem och nätverkstrafiken minskar, eftersom innehållet redan finns på enheten.  

 Använd följande metod för att skapa förberedda medier.  

#### <a name="to-create-prestaged-media"></a>Skapa förberedda media  

1. I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

2. I arbets ytan **program bibliotek** expanderar du **operativ system**och klickar sedan på **aktivitetssekvenser**.  

3. På fliken **Start** går du till gruppen **Skapa** och klickar på **Skapa aktivitetssekvensmedium** för att starta guiden Skapa aktivitetssekvensmedium.  

4. På sidan **Välj medietyp** anger du följande information och klickar sedan på **Nästa**.  

   -   Välj **Förberett medium**.  

   -   Välj **Tillåt obevakad distribution av operativsystem** för att starta Windows To Go-distributionen utan användaråtgärder.  

       > [!IMPORTANT]  
       >  När du använder det här alternativet med den anpassade variabeln SMSTSPreferredAdvertID (anges senare i proceduren) krävs inga åtgärder från användaren och datorn startar automatiskt Windows To Go-distributionen när en Windows To Go-enhet upptäcks. Användaren tillfrågas dock om lösenord om mediet har konfigurerats med lösenordsskydd. Om du använder inställningen **Tillåt obevakad distribution av operativsystem** utan att ha konfigurerat variabeln SMSTSPreferredAdvertID, uppstår ett fel när du distribuerar aktivitetssekvensen.  

5. På sidan **Mediehantering** anger du följande information och klickar sedan på **Nästa**.  

   -   Välj **Dynamiskt medium** om du vill att en hanteringsplats ska kunna omdirigera mediet till en annan hanteringsplats, baserat på klientens plats i platsgränserna.  

   -   Välj **Platsbaserat medium** om du vill att mediet bara ska kontakta den angivna hanteringsplatsen.  

6. På sidan **Medieegenskaper**  anger du följande information och klickar sedan på **Nästa**.  

   -   **Skapad av**: Ange vem som skapade mediet.  

   -   **Version**: Ange mediets versionsnummer.  

   -   **Kommentar**: Ange en unik beskrivning av mediets avsedda användning.  

   -   **Mediefil**: Ange namn och sökväg för utdatafilerna. Guiden skriver utdatafilerna till den här platsen. Till exempel: ** \\ \servername\folder\outputfile.wim**  

7. På sidan **Säkerhet** anger du följande information och klickar sedan på **Nästa**.  

   -   Välj **Aktivera stöd för okända datorer** så att mediet kan distribuera ett operativ system till en dator som inte hanteras av Configuration Manager. Det finns ingen post för de här datorerna i Configuration Managers databasen. Okända datorer är:  

       -   En dator där Configuration Manager-klienten inte är installerad  

       -   En dator som inte har importer ATS till Configuration Manager  

       -   En dator som inte har identifierats av Configuration Manager  

   -   Välj **Skydda mediet med lösenord** och ange ett starkt lösenord för att skydda mediet från obehörig åtkomst. När du anger ett lösenord måste användaren ange lösenordet för att använda det förberedda mediet.  

       > [!IMPORTANT]  
       >  Som säkerhetsregel bör du alltid tilldela ett lösenord för att skydda det förberedda mediet.  

       > [!NOTE]  
       >  När du skyddar det förberedda mediet med ett lösenord måste användaren uppge lösenordet även när mediet är konfigurerat med inställningen **Tillåt obevakad distribution av operativsystem** .  

   -   För HTTP-kommunikation väljer du **Skapa självsignerat mediecertifikat**och anger sedan certifikatets start- och utgångsdatum.  

   -   För HTTPS-kommunikation väljer du **Importera PKI-certifikat**och anger sedan det certifikat som ska importeras och dess lösenord.  

        Mer information om det här klient certifikatet som används för start avbildningar finns i [krav för PKI-certifikat](../../core/plan-design/network/pki-certificate-requirements.md).  

   -   **Mappning mellan användare och enhet**: om du vill stödja den användarvänliga hanteringen i Configuration Manager anger du hur du vill att mediet ska koppla användare till mål datorn. Mer information om hur operativ Systems distributionen stöder mappning mellan användare och enhet finns i [associera användare med en måldator](../get-started/associate-users-with-a-destination-computer.md).  

       -   Ange **Tillåt mappning mellan användare och enhet med automatiskt godkännande** om du vill att mediet automatiskt ska koppla användare till måldatorn. Funktionen är baserad på åtgärderna för den aktivitetssekvens som distribuerar operativsystemet. I det här scenariot skapar aktivitetssekvensen en relation mellan de angivna användarna och måldatorn när operativsystemet distribueras till måldatorn.  

       -   Ange **Tillåt mappning mellan användare och enhet efter administratörs godkännande** om du vill att mediet ska koppla användare till måldatorn när godkännande har getts. Funktionen är baserad på omfånget för den aktivitetssekvens som distribuerar operativsystemet. I det här scenariot skapar aktivitetssekvensen en relation mellan de angivna användarna och måldatorn men väntar på godkännande från en administrativ användare innan operativsystemet distribueras.  

       -   Ange **Tillåt inte mappning mellan användare och enhet** om du inte vill att mediet ska koppla användare till måldatorn. I det här scenariot kopplas inga användare till måldatorn när aktivitetssekvensen distribuerar operativsystemet.  

8. På sidan **Aktivitetssekvens** anger du den Windows 8-aktivitetssekvens som du skapade i föregående avsnitt.  

9. På sidan **Startavbildning** anger du följande information och klickar sedan på **Nästa**.  

    > [!IMPORTANT]  
    >  Arkitekturen för den startavbildning som distribueras måste vara lämpad för måldatorns arkitektur. En x64-måldator kan exempelvis starta och köra en x86- eller x64-startavbildning. Men en x86-måldator kan bara starta och köra en x86-startavbildning. För Windows 8-certifierade datorer i EFI-läge måste du använda en x64-startavbildning.  

    -   **Startavbildning**: Ange den startavbildning som startar måldatorn.  

    -   **Distributionsplats**: Ange den distributionsplats som är värd för startavbildningen. Guiden hämtar startavbildningen från distributionsplatsen och skriver den till mediet.  

        > [!NOTE]  
        >  Den administrativa användaren måste ha behörigheten **Läs** för startavbildsinnehåll på distributionsplatsen. Mer information finns i [paket åtkomst konto](../../core/plan-design/hierarchy/accounts.md#package-access-account).  

    -   Om du valde **Platsbaserat medium** på sidan **Mediehantering** i guiden, anger du en hanteringsplats från en primär plats i rutan **Hanteringsplats** .  

    -   Om du valde **Dynamiskt medium** på sidan **Mediehantering** i guiden, anger du den primära platsens hanteringsplatser som ska användas och en prioritetsordning för den inledande kommunikationen i rutan **Associerade hanteringsplatser** .  

10. På sidan **Avbildningar** anger du följande information och klickar sedan på **Nästa**.  

    -   **Avbildningspaket**: Ange det paket som innehåller Windows 8-operativsystemavbildningen.  

    -   **Avbildningsindex**: Ange den avbildning som ska distribueras om paketet innehåller flera operativsystemavbildningar.  

    -   **Distributionsplats**: Ange den distributionsplats som är värd för operativsystemavbildningspaketet. Guiden hämtar operativsystemsavbildningen från distributionsplatsen och skriver den till media.  

        > [!NOTE]  
        >  Den administrativa användaren måste ha behörigheten **Läs** för operativsystemavbildsinnehåll på distributionsplatsen. Mer information finns i [paket åtkomst konto](../../core/plan-design/hierarchy/accounts.md#package-access-account).  

11. På sidan **Välj program** väljer du det programinnehåll som ska ingå i mediefilen. Klicka sedan på **Nästa**.  

12. På sidan **Välj paket** väljer du ytterligare paketinnehåll som ska ingå i mediefilen. Klicka sedan på **Nästa**.  

13. På sidan **Välj drivrutinspaket** väljer du det drivrutinspaketinnehåll som ska ingå i mediefilen. Klicka sedan på **Nästa**.  

14. På sidan **Distributionsplatser** väljer du en eller flera distributionsplatser som har det innehåll som begärs av aktivitetssekvensen. Klicka sedan på **Nästa**.  

15. På sidan **Anpassning** anger du följande information och klickar sedan på **Nästa**.  

    - **Variabler**: Ange de variabler som används av aktivitetssekvensen för att distribuera operativsystemet. För Windows To Go använder du variabeln SMSTSPreferredAdvertID för att automatiskt välja Windows To Go-distributionen med hjälp av följande format:  

       SMSTSPreferredAdvertID = {*DeploymentID*} där DeploymentID är det distributions-ID som är kopplat till den aktivitetssekvens du sedan använder för att slutföra etableringen av Windows To Go-enheten.  

      > [!TIP]  
      >  När du använder den här variabeln med en aktivitetssekvens som är inställd på att köras obevakad (vilket angetts tidigare i den här proceduren) krävs inga åtgärder från användaren och datorn startar automatiskt Windows To Go-distributionen när en Windows To Go-enhet upptäcks. Användaren tillfrågas dock om lösenord om mediet har konfigurerats med lösenordsskydd.  

    - **Förinläsningskommandon**: Ange eventuella förinläsningskommandon som ska köras innan aktivitetssekvensen körs. Förinläsningskommandon kan vara ett skript eller en körbar fil som kan användas av användaren i Windows PE innan aktivitetssekvensen körs för att installera operativsystemet. Konfigurera följande för Windows To Go-distributionen:  

      - **OSDBitLockerPIN**: BitLocker för Windows To Go kräver en lösenfras. Ange variabeln **OSDBitLockerPIN** i ett förinläsningskommando för att ange BitLocker-lösenfrasen för Windows To Go-enheten.  

        > [!WARNING]  
        >  När BitLocker har aktiverats för lösenfrasen måste användaren ange den lösenfrasen varje gång datorn startas med Windows To Go-enheten.  

      - **SMSTSUDAUsers**: Anger den primära användaren på måldatorn. Använd den här variabeln för att samla in användarnamnet vilket sedan kan användas för att koppla ihop användare och enhet Mer information finns i [associera användare med en måldator](../get-started/associate-users-with-a-destination-computer.md).  

        > [!TIP]  
        >  Du hämtar användarnamnet genom att skapa en indataruta i förinläsningskommandot och låta användaren uppge sitt användarnamn där. Ställ sedan in variabeln med värdet. Du kan till exempel lägga till följande rader i förinläsningskommandots skriptfil:  
        >   
        >  `UserID = inputbox("Enter Username" ,"Enter your username:","",400,0)`  
        >   
        >  `env("SMSTSUDAUsers") = UserID`  

        Mer information om hur du skapar en skript fil som ska användas som för inläsnings kommando finns i [för inläsnings kommandon för media för aktivitetssekvenser](../understand/prestart-commands-for-task-sequence-media.md).  

16. Slutför guiden.  

    > [!NOTE]  
    >  Det kan ta lång tid för guiden att skapa den förberedda mediefilen.  

###  <a name="create-a-windows-to-go-creator-package"></a><a name="BKMK_CreatePackage"></a>Skapa ett Windows To Go Creator-paket  
 Under distributionen av Windows To Go måste du skapa ett paket för att distribuera den förberedda mediefilen. Paketet måste innehålla verktyget som konfigurerar Windows To Go-enheten och extraherar det förberedda mediet till enheten. Skapa Windows To Go Creator-paketet på följande sätt.  

#### <a name="to-create-the-windows-to-go-creator-package"></a>Skapa Windows To Go Creator-paketet  

1. Skapa en målmapp för paketkällfilerna på den server som är värd för Windows To Go Creator-paketfilerna.  

   > [!NOTE]  
   >  Datorkontot på platsservern måste ha **läs** -behörighet för målmappen.  

2. Kopiera den förberedda mediefil som du skapade i avsnittet [Create prestaged media](#BKMK_CreatePrestagedMedia) till paketkällmappen.  

3. Kopiera Windows To Go Creator-verktyget (WTGCreator.exe) till paketkällmappen. Verktyget skapare är tillgängligt på valfri primär plats Server på följande plats: <*ConfigMgrInstallationFolder*> \OSD\Tools\WTG\Creator.  

4. Skapa ett paket och program med guiden Skapa paket och program.  

5. I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

6. I arbetsytan **Programbibliotek** expanderar du **Programhantering**och klickar sedan på **Paket**.  

7. Klicka på **Skapa paket** i gruppen **Skapa** på fliken **Start**.  

8. Ange ett namn på och en beskrivning av paketet på sidan **Paket** . Ange till exempel **Windows To Go** för paket namnet och ange **paket för att konfigurera en Windows To Go-enhet med hjälp av Configuration Manager** för paket beskrivningen.  

9. Välj **Det här paketet innehåller källfiler**, ange sökvägen till den paketkällmapp du skapade i steg 1 och klicka sedan på **Nästa**.  

10. På sidan **Programtyp** väljer du **Standardprogram**och klickar sedan på **Nästa**.  

11. På sidan **Standardprogram** anger du följande:  

    -   **Namn**: Ange namnet på programmet. Skriv till exempel **Creator** som programnamn.  

    -   **Kommandorad**: Skriv **WTGCreator.exe /wim:PrestageName.wim**där PrestageName är namnet på den förberedda fil du skapade och kopierade till paketkällmappen för Windows To Go Creator-paketet.  

         Du kan också lägga till följande alternativ:  

        -   **enableBootRedirect**: kommandoradsalternativ som ändrar Windows To Go-startalternativen så att startomdirigering tillåts. När du använder det här alternativet startar datorn från USB-minnet utan att startordningen behöver ändras i datorns inbyggda programvara eller att användaren behöver välja i en lista med startalternativ under starten. Om en Windows To Go-enhet identifieras startar datorn med den enheten.  

    -   **Kör**: Ange **Normal** för att köra programmet baserat på standardinställningarna för system och program.  

    -   **Programmet kan köra**: Ange om programmet bara kan köras när en användare är inloggad.  

    -   **Körningsläge**: Ange om programmet ska köras med de inloggade användarnas behörigheter eller med administrationsbehörigheter. För att köra Windows To Go Creator krävs förhöjd behörighet.  

    -   Välj **Tillåt att användare visar och interagerar med programinstallationen**och klicka sedan på **Nästa**.  

12. På kravsidan anger du följande:  

    - **Plattformskrav**: Välj lämpliga Windows 8-plattformar för att tillåta etablering.  

    - **Beräknat diskutrymme**: Ange storleken på paketkällmappen för Windows To Go Creator.  

    - **Tillåten maximal körningstid (minuter)**: Ange den maximala tid som programmet förväntas köras på klientdatorn. Som standard är det här värdet inställt på 120 minuter.  

      > [!IMPORTANT]  
      >  Om du använde underhållsfönster för den samling där programmet körs kan en konflikt uppstå om **Längsta tillåtna körningstid** är längre än det schemalagda underhållsfönstret. Om den längsta körningstiden är inställd på **Okänd**startar den under underhållsfönstret, men fortsätter att köras tills den har slutförts eller misslyckas när underhållsfönstret har stängts. Om du ställer in den maximala körningstiden på en viss period (inte på Okänd) som överskrider längden på ett eventuellt tillgängligt underhållsfönster, kommer det här programmet inte att köras.  

      > [!NOTE]  
      >  Om värdet är inställt på **Okänt**anger Configuration Manager den längsta tillåtna körnings tiden till 12 timmar (720 minuter).  

      > [!NOTE]  
      >  Om den längsta körnings tiden (oavsett om den har ställts in av användaren eller standardvärdet) överskrids, Configuration Manager stoppar programmet om alternativet **Kör med administrations behörighet** har valts och **Tillåt att användare visar och interagerar med programinstallationen** inte har valts på sidan **standard program** .  

      Klicka på **Nästa** och slutför guiden.  

###  <a name="update-the-task-sequence-to-enable-bitlocker-for-windows-to-go"></a><a name="BKMK_UpdateTaskSequence"></a>Uppdatera aktivitetssekvensen för att aktivera BitLocker för Windows To Go  
 Windows To Go aktiverar BitLocker på en extern startbar enhet utan att använda TPM-modulen. Du måste därför använda ett separat verktyg för att konfigurera BitLocker på Windows To Go-enheten. Om du vill aktivera BitLocker måste du lägga till en åtgärd i aktivitetssekvensen efter steget **Installera Windows och ConfigMgr** .  

> [!NOTE]  
>  BitLocker för Windows To Go kräver en lösenfras. I steget [Create prestaged media](#BKMK_CreatePrestagedMedia) ställer du in lösenfrasen som en del av ett förinläsningskommando med hjälp av variabeln OSDBitLockerPIN.  

 Använd följande procedur om du vill uppdatera Windows 8-aktivitetssekvensen för att aktivera BitLocker för Windows To Go.  

#### <a name="to-update-the-windows-8-task-sequence-to-enable-bitlocker"></a>Uppdatera Windows 8-aktivitetssekvensen för att aktivera BitLocker  

1.  I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

2.  I arbetsytan **Programbibliotek** expanderar du **Programhantering**och klickar sedan på **Paket**.  

3.  Klicka på **Skapa paket** i gruppen **Skapa** på fliken **Start**.  

4.  Ange ett namn på och en beskrivning av paketet på sidan **Paket** . Skriv till exempel **BitLocker for Windows To Go** för paketnamnet och **Package to update BitLocker for Windows To Go** som paketbeskrivningen.  

5.  Välj **Det här paketet innehåller källfiler**, ange platsen för verktyget BitLocker för Windows To Go och klicka sedan på **Nästa**. BitLocker-verktyget är tillgängligt på valfri Configuration Manager primär plats Server på följande plats: <*ConfigMgrInstallationFolder*> \OSD\Tools\WTG\BitLocker\  

6.  Välj **Skapa inget program** på sidan **Programtyp**.  

7.  Klicka på **Nästa** och slutför guiden.  

8.  I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

9. I arbets ytan **program bibliotek** expanderar du **operativ system**och klickar sedan på **aktivitetssekvenser**.  

10. Välj den Windows 8 aktivitetssekvens som du hänvisar till i det förinstallerade mediet.  

11. Klicka på **Redigera** i gruppen **Aktivitetssekvens** på fliken **Start**.  

12. Klicka på steget **Installera Windows och ConfigMgr** , klicka på **Lägg till**, klicka på **Allmänt**och klicka sedan på **Kör kommandorad**. Steget Kör kommandorad läggs till efter steget Installera Windows och ConfigMgr.  

13. Lägg till följande för steget **Kör kommandorad** på fliken **Egenskaper** :  

    1.  **Namn**: Ange ett namn för kommandoraden, t.ex. **Enable BitLocker for Windows To Go**.  

    2.  **Kommando rad**: i386 \ osdbitlocker_wtg. exe/Enable/pwd: < *ingen & #124; AD*>  

         Parametrar:  

        -   /PWD: <ingen&#124;AD> – ange återställnings läget för BitLocker-lösenordet. Den här parametern krävs om du använder parametern /Enable i kommandoraden.  

             Välj **AD** om du vill konfigurera BitLocker-diskkryptering för att säkerhetskopiera återställningsinformation för BitLocker-skyddade enheter till Active Directory-domäntjänsterna (AD DS). Att säkerhetskopiera återställningslösenorden för en BitLocker-skyddad enhet göra att administrativa användare kan återställa enheten om den är låst. Detta säkerställer att krypterade data som tillhör företaget alltid är tillgängliga för auktoriserade användare. Om du anger **Ingen**ansvarar användaren för att behålla en kopia av återställningslösenordet eller återställningsnyckeln. Om användaren förlorar den här informationen eller underlåter att av kryptera enheten innan personen lämna organisationen är det svårare för administrativa användare att få åtkomst till enheten.  

        -   /wait: <TRUE&#124;FALSe> – ange om aktivitetssekvensen ska vänta på att krypteringen ska slutföras innan den är klar.  

    3.  Välj **Paket**, och ange sedan det paket som du skapade i början av den här proceduren.  

    4.  Lägg till följande villkor på fliken **Alternativ** :  

        -   Villkor = aktivitetssekvensvariabel  

        -   Variabel = _SMSTSWTG  

        -   Villkor = lika med  

        -   Värde = Sant  

    > [!NOTE]  
    >  Steget **Aktivera BitLocker** , som är sannolikt efter det nya kommandoradssteget, används inte för att aktivera BitLocker för Windows To Go. Du kan dock behålla det här steget i den aktivitetssekvens som ska användas för Windows 8-distributioner där ingen Windows To Go-enhet används.  

###  <a name="deploy-the-windows-to-go-creator-package-and-task-sequence"></a><a name="BKMK_Deployments"></a> Distribuera Windows To Go Creator-paketet och aktivitetssekvensen  
 Windows To Go är en hybriddistributionsprocess. Därför måste du distribuera Windows To Go Creator-paketet och Windows 8-aktivitetssekvensen. Slutför distributionsprocessen med hjälp av följande procedurer:  

#### <a name="to-deploy-the-windows-to-go-creator-package"></a>Distribuera Windows To Go Creator-paketet  

1.  I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

2.  I arbetsytan **Programbibliotek** expanderar du **Programhantering**och klickar sedan på **Paket**.  

3.  Välj det Windows To Go-paket som du skapade i steget [Skapa ett Windows To Go Creator-paket](#BKMK_CreatePackage) .  

4.  På fliken **Start** går du till gruppen **Distribution** och klickar på **Distribuera**.  

5.  På sidan **Allmänt** anger du följande inställningar:  

    1.  **Programvara**: Kontrollera att Windows To Go-paketet har valts.  

    2.  **Samling**: Välj den samling som du vill distribuera Windows To Go-paketet till genom att klicka på **Bläddra** .  

    3.  **Använd standarddistributionsplatsgrupper som är associerade med samlingen**: Välj det här alternativet om du vill spara paketinnehållet i samlingens förvalda distributionsplatsgrupp. Om du inte har associerat den valda samlingen med en distributionsplatsgrupp kommer det här alternativet att vara otillgängligt.  

6.  Klicka på **Lägg till** på sidan **Innehåll** och välj sedan de distributionsplatser eller distributionsplatsgrupper som du vill distribuera det innehåll som är associerat med det här paketet och programmet till.  

7.  Välj **Tillgänglig** för distributionstypen på sidan **Distributionsinställningar** och klicka sedan på **Nästa**.  

8.  Konfigurera när det här paketet och programmet ska distribueras eller göras tillgängligt för klientenheter på sidan **Schemaläggning**.  

     Vilka alternativ som visas på sidan beror på om distributionsåtgärden **Tillgänglig** eller **Obligatorisk**har valts.  

9. Konfigurera följande inställningar på sidan **Schemaläggning**och klicka sedan på **Nästa**.  

    1.  **Schemalägg när distributionen ska vara tillgänglig**: Ange datum och tid då paketet och programmet ska vara tillgängliga för körning på måldatorn. Om du väljer **UTC**gör inställningen så att paketet och programmet blir tillgängligt för flera måldatorer samtidigt i stället för vid olika tidpunkter, enligt måldatorernas lokala tidsangivelse.  

    2.  **Schemalägg när distributionen ska upphöra att gälla**: Ange datum och tid då paketet och programmet ska upphöra att gälla på måldatorn. O du väljer **UTC**gör inställningen så att aktivitetssekvensen upphör att gälla på flera måldatorer samtidigt i stället för vid olika tidpunkter, enligt måldatorernas lokala tidsangivelse.  

10. Ange följande information på sidan **Användarupplevelse** i guiden:  

    -   **Programvaruinstallation**: Programvaran kan installeras utanför angivna underhållsperioder.  

    -   **Systemomstart (om det krävs för att slutföra installationen)**: En enhet kan starta om utanför de konfigurerade underhållsperioderna om detta krävs av programinstallationen.  

    -   **Inbäddade enheter**: Om du distribuerar paket och program till Windows Embedded-enheter som har aktiverade skrivfilter kan du ange att paketen och programmen ska installeras på det tillfälliga överlägget och spara ändringarna senare, eller spara ändringarna då installationens tidsgräns går ut eller under en underhållsperiod. När du gör ändringar vid installationens tidsgräns eller under en underhållsperiod krävs en omstart och ändringarna är kvar på enheten.  

11. Ange följande information på sidan **Distributionsplatser** :  

    -   **Distributionsalternativ:** Ange **Hämta innehållet från distributionsplatsen och kör lokalt**.  

    -   **Tillåt att klienter delar innehåll med andra klienter i samma undernät**: Välj det här alternativet om du vill minska belastningen på nätverket genom att tillåta att klienten laddar ned innehåll från andra klienter i nätverket som redan har laddat ned och cachelagrat innehållet. För det här alternativet används Windows BranchCache och det kan användas på datorer som kör Windows Vista SP2 och senare.  

    -   **Tillåt att klienter använder en återställningskällplats för innehåll**: Ange om klienterna ska få tillåtelse att återställas och använda en icke prioriterad distributionsplats som källplats för innehållet om innehållet inte är tillgängligt på en prioriterad distributionsplats.  

12. Slutför guiden.  

#### <a name="to-deploy-the-windows-8-task-sequence"></a>Distribuera Windows 8-aktivitetssekvensen  

1.  I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

2.  I arbets ytan **program bibliotek** expanderar du **operativ system**och klickar sedan på **aktivitetssekvenser**.  

3.  Välj den Windows 8-aktivitetssekvens som du skapade i steget [Prerequisites to provision Windows To Go](#BKMK_Prereqs) .  

4.  På fliken **Start** går du till gruppen **Distribution** och klickar på **Distribuera**.  

5.  På sidan **Allmänt** anger du följande inställningar:  

    1.  **Aktivitetssekvens**: Kontrollera att Windows 8-aktivitetssekvensen har valts.  

    2.  **Samling**: Klicka på **Bläddra** och välj den samling som innehåller alla enheter som en användare kan etablera Windows To Go för.  

        > [!IMPORTANT]  
        >  Om det förinstallerade medium som du skapade i avsnittet [Create prestaged media](#BKMK_CreatePrestagedMedia) använder variabeln SMSTSPreferredAdvertID kan du distribuera aktivitetssekvensen till samlingen **Alla system** och ange inställningen **Endast Windows PE (dolt)** på sidan **Innehåll** Eftersom den här aktivitetssekvensen är dold, kommer den enbart att vara tillgänglig för medier.  

    3.  **Använd standarddistributionsplatsgrupper som är associerade med samlingen**: Välj det här alternativet om du vill spara paketinnehållet i samlingens förvalda distributionsplatsgrupp. Om du inte har associerat den valda samlingen med en distributionsplatsgrupp kommer det här alternativet att vara otillgängligt.  

6.  Konfigurera följande inställningar på sidan **Distributionsinställningar** och klicka sedan på **Nästa**.  

    -   **Syfte**: Välj **Tillgänglig**. Om du distribuerar aktivitetssekvensen till en användare, ser användaren den publicerade aktivitetssekvensen i programkatalogen och kan begära den på begäran. Om du distribuerar aktivitetssekvensen till en enhet, ser användaren aktivitetssekvensen i Software Center och kan installera den på begäran.  

    -   **Gör tillgängligt för följande**: Ange om aktivitetssekvensen är tillgänglig för att Configuration Manager klienter, medier eller PXE.  

        > [!IMPORTANT]  
        >  Använd inställningen **Endast media och PXE (dolt)** för automatiserade aktivitetssekvensdistributioner. Välj **Tillåt obevakad distribution av operativsystem.** och ställ in variabeln SMSTSPreferredAdvertID som en del av det förinstallerade mediet för att få datorn att automatiskt starta till Windows To Go-distributionen utan interaktion med användaren när den identifierar en Windows To Go-enhet. Mer information om dessa inställningar för förinstallerade medier finns i avsnittet [Create prestaged media](#BKMK_CreatePrestagedMedia) .  

7.  Konfigurera följande inställning på sidan **Schemaläggning** och klicka sedan på **Nästa**.  

    1.  **Schemalägg när distributionen ska vara tillgänglig**: Ange datum och tid då aktivitetssekvensen är tillgänglig för körning på måldatorn. Om du väljer **UTC**gör den här inställningen att aktivitetssekvensen blir tillgänglig för flera måldatorer samtidigt i stället för vid olika tidpunkter, enligt den lokala tidsinställningen på måldatorerna.  

    2.  **Schemalägg när distributionen ska upphöra att gälla**: Ange datum och tid då aktivitetssekvensen upphör att gälla på måldatorn. O du väljer **UTC**gör inställningen så att aktivitetssekvensen upphör att gälla på flera måldatorer samtidigt i stället för vid olika tidpunkter, enligt måldatorernas lokala tidsangivelse.  

8.  Ange följande information på sidan **Användarupplevelse** :  

    -   **Visa förlopp för aktivitetssekvens**: Ange om den Configuration Manager klienten ska visa förloppet för aktivitetssekvensen.  

    -   **Programvaruinstallation**: Ange om användaren kan installera programvaran utanför en konfigurerad underhållsperiod efter den schemalagda tiden.  

    -   **Systemomstart (om det krävs för att slutföra installationen)**: En enhet kan starta om utanför de konfigurerade underhållsperioderna om detta krävs av programinstallationen.  

    -   **Inbäddade enheter**: Om du distribuerar paket och program till Windows Embedded-enheter som har aktiverade skrivfilter kan du ange att paketen och programmen ska installeras på det tillfälliga överlägget och spara ändringarna senare, eller spara ändringarna då installationens tidsgräns går ut eller under en underhållsperiod. När du gör ändringar vid installationens tidsgräns eller under en underhållsperiod krävs en omstart och ändringarna är kvar på enheten.  

    -   **Internetbaserade klienter**: Ange om aktivitetssekvensen kan köra på en Internetbaserad klient. Åtgärder som installerar programvara, exempelvis ett operativsystem, stöds inte med den här inställningen. Använd enbart det här alternativet för generiska skriptbaserade aktivitetssekvenser som utför åtgärder i standardoperativsystemet.  

9. På sidan **Aviseringar** anger du de aviseringsinställningar som du vill används för den har aktivitetssekvensdistributionen och klickar sedan på **Nästa**.  

10. På sidan **Distributionsplatser** anger du följande information och klickar sedan på **Nästa**.  

    -   **Distributionsalternativ**: Välj **Hämta allt innehåll lokalt vid behov genom att köra aktivitetssekvensen**.  

    -   **Använd en fjärrdistributionsplats om det inte finns några lokala distributionsplatser**: Ange om klienter kan använda distributionsplatser som finns i långsamma och otillförlitliga nätverk för att ladda ned det innehåll som krävs av aktivitetssekvensen.  

    -   **Tillåt att klienter använder en återställnings käll plats för innehåll**:
        - *Före version 1610*kan du markera kryss rutan Tillåt återställnings käll plats för innehåll för att tillåta att klienter utanför dessa begränsnings grupper återgår till och använder distributions platsen som en käll plats för innehåll när inga andra distributions platser är tillgängliga.
        - *Från och med version 1610*kan du inte längre konfigurera **Tillåt återställnings käll plats för innehåll**.  I stället konfigurerar du relationer mellan gränser grupper som avgör när en klient kan börja söka efter ytterligare avgränsnings grupper för en giltig innehålls käll plats. 

11. Slutför guiden.  

###  <a name="user-runs-the-windows-to-go-creator"></a><a name="BKMK_UserExperience"></a> Användaren kör Windows To Go Creator  
 När du har distribuerat Windows To Go-paketet och Windows 8-aktivitetssekvensen är Windows To Go Creator tillgängligt för användaren. Användaren kan gå till programkatalogen, eller till Software Center om Windows To Go Creator har distribuerats till enheterna, och köra Windows To Go Creator-programmet. När skaparpaketet har laddats ned visas en blinkande ikon i aktivitetsfältet. Om användaren klickar på ikonen visas en dialogruta där användaren kan välja Windows To Go-enheten för att etablera (om inte kommandoradsalternativet /drive används). Om enheten inte uppfyller kraven för Windows To Go eller om enheten inte har tillräckligt med ledigt diskutrymme för att installera avbildningen, visas ett felmeddelande i skaparprogrammet. Användaren kan kontrollera den enhet och avbildning som kommer att tillämpas från bekräftelsesidan. När skaparprogrammet konfigurerar och förinstallerar innehåll till Windows To Go-enheten visas en dialogruta som anger hur förloppet fortskrider. När förinstallationen är klar visar skaparprogrammet en uppmaning om att starta om datorn för att starta upp till Windows To Go-enheten.  

> [!NOTE]  
>  Om du inte har aktiverat startomdirigering som en del av kommandoraden för skaparprogrammet i avsnittet [Create a Windows To Go Creator package](#BKMK_CreatePackage) kan användaren behöva starta Windows To Go-enheten manuellt varje gång systemet startar om.  

###  <a name="configuration-manager-configures-and-stages-the-windows-to-go-drive"></a><a name="BKMK_ConfigureStageDrive"></a> Configuration Manager konfigurerar och skapar nivåer av Windows To Go-enheten  
 När datorn har startats om till Windows To Go-enheten, startar enheten upp till Windows PE och ansluter till hanteringsplatsen för att få principen att slutföra operativsystemsdistributionen. Configuration Manager konfigurerar och skapar en fas av enheten. När Configuration Manager stadier i enheten kan användaren starta om datorn för att slutföra etablerings processen (till exempel för att ansluta till en domän eller installera appar). Den här processen är densamma för alla förinstallerade medier.  

###  <a name="user-logs-in-to-windows-8"></a><a name="BKMK_UserLogsIn"></a>Användaren loggar in på Windows 8  
 När Configuration Manager har slutfört etablerings processen och lås skärmen för Windows 8 visas kan användaren logga in till operativ systemet.  
