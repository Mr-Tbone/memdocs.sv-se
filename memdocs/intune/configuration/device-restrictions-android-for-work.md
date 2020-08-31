---
title: Enhetsinställningar för Android Enterprise i Microsoft Intune – Azure | Microsoft Docs
description: Du kan begränsa enhetsinställningarna för Android Enterprise eller Android for Work, inklusive inställningar för att kopiera och klistra in, visa aviseringar, appbehörigheter, dela data, lösenordslängd, inloggningsfel, använda fingeravtryck för upplåsning, återanvändning av lösenord och aktivering av Bluetooth-delning för arbetskontakter. Konfigurera enheter som en särskild enhet för att köra en eller flera appar.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: chmaguir, chrisbal, priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b08d5f1395c30b646885470c95fed2c7a96d3f9
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88819617"
---
# <a name="android-enterprise-device-settings-to-allow-or-restrict-features-using-intune"></a>Enhetsinställningarna för Android Enterprise tillåter eller begränsar funktioner med hjälp av Intune

Den här artikeln beskriver de olika inställningar som du kan styra på Android Enterprise-enheter. Som en del av MDM-lösningen (hantering av mobilenheter) använder du de här inställningarna för att tillåta eller inaktivera funktioner, köra appar på dedikerade enheter, kontrollera säkerhet och mer.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en enhetskonfigurationsprofil](device-restrictions-configure.md).

## <a name="fully-managed-dedicated-and-corporate-owned-work-profile"></a>Fullständigt hanterad, dedikerad och företagsägd arbetsprofil

Dessa inställningar gäller för Android Enterprise-registreringstyper där Intune styr hela enheten, till exempel fullständigt hanterade Android Enterprise-enheter eller dedikerade Android Enterprise-enheter och företagsägda arbetsprofilenheter.

Vissa inställningar stöds inte av alla registreringstyper. Information om vilka inställningar som stöds av vilka registreringstyper finns i användargränssnittet. Varje inställning finns under en rubrik som anger vilka registreringstyper som kan använda den inställningen.

![Ange rubriker.](./media/device-restrictions-android-for-work/setting-headers.png)

Vissa inställningar gäller endast på arbetsprofilnivå för företagsägda enheter med en arbetsprofil. De här inställningarna gäller fortfarande hela enheten för fullständigt hanterade och dedikerade enheter. De här inställningarna markeras med beskrivningen *(arbetsprofilnivå)* i användargränssnittet.

![Ange rubriker.](./media/device-restrictions-android-for-work/work-profile-level.png)


### <a name="general"></a>Allmänt

- **Skärmdump**: **Blockera** förhindrar skärmbilder eller skärmdumpar på enheten. Förhindrar också att innehållet visas på visningsenheter som inte har en säker videoutgång. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användaren sparar skärminnehållet som en bild.
- **Kamera**: **Blockera** förhindrar åtkomst till enhetens kamera. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta åtkomst till kameran.

  Intune hanterar endast åtkomst till enhetens kamera. Intune har inte åtkomst till bilder eller videor.

- **Standardprincip för behörigheter**: Den här inställningen definierar standardbehörighetsprincipen vid begäranden om körningsbehörigheter. Alternativen är
  - **Standard för enheten**: Använd enhetens standardinställning.
  - **Fråga**: Användare uppmanas godkänna behörigheten.
  - **Bevilja automatiskt**: Behörigheter beviljas automatiskt.
  - **Neka automatiskt**: Behörigheter nekas automatiskt.
- **Datum- och tidsändringar**: **Blockera** förhindrar att användarna anger datum och tid manuellt. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att ange datum och tid på enheten.
- **Volymändringar**: **Blockera** hindrar användare från att ändra enhetens volym och stänger också av huvudvolymen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användning av volyminställningarna på enheten.
- **Fabriksåterställning**: **Blockera** förhindrar att användarna använder alternativet för fabriksåterställning i enhetens inställningar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att använda den här inställningen på enheten.
- **Säker start**: **Blockera** förhindrar att användarna startar om enheten i felsäkert läge. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att starta om enheten i felsäkert läge.
- **Statusfält**: **Blockera** förhindrar åtkomst till statusfältet, inklusive aviseringar och snabbinställningar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användarna får åtkomst till statusfältet.
- **Dataroaming**: **Blockera** förhindrar dataroaming i mobilnätet. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta dataroaming när enheten använder ett mobilnät.
- **Ändringar i Wi-Fi-inställning**: **Blockera** förhindrar att användarna ändrar Wi-Fi-inställningar som skapats av enhetsägaren. Användarna kan skapa sina egna Wi-Fi-konfigurationer. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att ändra Wi-Fi-inställningarna på enheten.
- **Konfiguration av Wi-Fi-åtkomstpunkt**: **Blockera** förhindrar att användarna skapar eller ändrar Wi-Fi-konfigurationer. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att ändra Wi-Fi-inställningarna på enheten.
- **Bluetooth-konfiguration**: **Blockera** förhindrar att användarna konfigurerar Bluetooth på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att Bluetooth används på enheten.
- **Internetdelning och åtkomst till surfpunkter**: **Blockera** förhindrar Internetdelning och åtkomst till bärbara surfpunkter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta Internetdelning och åtkomst till bärbara surfpunkter.
- **USB-lagring**: Välj **Tillåt** för åtkomst till USB-lagring på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard förhindra åtkomst till USB-lagring.
- **USB-filöverföring**: **Blockera** förhindrar överföring av filer via USB. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta överföring av filer.
- **Externa medier**: **Blockera** förhindrar användning av eller anslutning till externa medier på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta externa medier på enheten.
- **Överför data via NFC**: **Blockera** förhindrar användning av NFC-teknik (Near Field Communication) vid överföring av data från appar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användning av NFC för att dela data mellan enheter.
- **Felsökningsfunktioner**: Välj **Tillåt** för att tillåta att användarna använder felsökningsfunktioner på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard förhindra att användare använder felsökningsfunktioner på enheten.
- **Mikrofonjustering**: **Blockera** förhindrar att användarna slår på ljudet på mikrofonen och ändrar dess volym. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att använda och justera mikrofonvolymen på enheten.
- **E-post för skydd mot fabriksåterställning**: Välj **E-postadresser för Google-konto**. Ange e-postadresserna för enhetsadministratörer som kan låsa upp enheten när den har rensats. Se till att avgränsa e-postadresser med semikolon, till exempel `admin1@gmail.com;admin2@gmail.com`. Om en e-postadress inte anges kan vem som helst låsa upp enheten efter den har återställts till fabriksinställningarna. De här e-postadresserna gäller endast när fabriksåterställning har körts (inte av användaren), till exempel om en fabriksåterställning körs via återställningsmenyn.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

- **Nätverkshjälp**: **Aktivera** tillåter att användarna aktiverar funktionen för nätverkshjälp. Om en nätverksanslutning inte skapats när enheten startas kommer nätverkshjälpen tillfälligt be om att ansluta till ett nätverk och uppdatera enhetsprincipen. När principen har tillämpats glöms det tillfälliga nätverket och starten av enheten fortsätter. Funktionen ansluter enheten till ett nätverk om:
  - Den förra principen saknar ett lämpligt nätverk.
  - Enheten startar i en app i låsläget.
  - Användare inte kan nå enhetsinställningarna.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard förhindra att användare aktiverar funktionen nätverkshjälp på enheten.

- **Systemuppdatering**: Välj ett alternativ för att definiera hur enheten ska hantera trådlösa uppdateringar. Alternativen är
  - **Standard för enheten**: Använd enhetens standardinställning.
  - **Automatiskt**: Uppdateringar installeras automatiskt utan att användaren behöver göra något. Om du konfigurerar den här principen installeras väntande uppdateringar omedelbart.
  - **Uppskjuten**: Uppdateringar skjuts upp i 30 dagar. Mot slutet av 30-dagarsperioden uppmanar Android användarna att installera uppdateringen. Det är möjligt för enhetstillverkare eller operatörer att undanta viktiga säkerhetsuppdateringar från att skjutas upp. En undantagen uppdatering visar användarna ett systemmeddelande på enheten.
  - **Underhållsperiod**: Uppdateringar installeras automatiskt under en daglig underhållsperiod som du anger i Intune. Installationen gör ett försök dagligen under 30 dagar och kan misslyckas vid otillräckligt diskutrymme eller för låga batterinivåer. Efter 30 dagar uppmanar Android användarna att installera. Det här fönstret används också för att installera uppdateringar för Play-appar. Använd det här alternativet för dedikerade enheter såsom helskärmslägen, eftersom förgrundsappar för dedikerade enheter med enskild app kan uppdateras.

- **Meddelandefönster**: När **Inaktivera** har valts visas inte fönstermeddelanden, bland annat popup-fönster, inkommande samtal, utgående samtal, systemaviseringar och systemfel, på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard visa meddelanden.
- **Hoppa över tips vid första start**: Om du väljer **Aktivera** döljs eller utelämnas förslag från appar som går igenom självstudier eller tips när appen startar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard visa dessa förslag när appen startar.

### <a name="system-security"></a>Systemsäkerhet

- **Hotgenomsökning för appar**: Om du väljer **Kräv** (standard) kan Google Play Protect genomsöka appar före de installeras och efter de installerats. Om ett hot identifieras kan användarna varnas och uppmanas att ta bort appen från enheten. När detta anges till **Inte konfigurerad** ändrar eller uppdaterar Intune inte den här inställningen. Som standard kanske operativsystemet inte aktiverar eller kör Google Play Protect för genomsökning av appar.

### <a name="device-experience"></a>Enhetsmiljö

Använd de här inställningarna till att konfigurera en kioskmiljö på dina dedikerade enheter eller för att anpassa startskärmen på dina helt hanterade enheter. Du kan konfigurera enheter för att köra en app eller flera appar. När en enhet är inställd på helskärmsläge är det bara de appar du lägger till som är tillgängliga.

**Typ av registreringsprofil**: Välj en typ av registreringsprofil för att börja konfigurera Microsoft Launcher eller Microsoft Managed Home Screen på dina enheter. Alternativen är:

- **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen. Som standard kan användarna se enhetens standardstartskärm.
- **Dedikerade enheter**: Konfigurera en helskärmsmiljö på dina dedikerade enheter. Innan du konfigurerar de här inställningarna måste du [lägga till](../apps/apps-add-android-for-work.md) och [tilldela](../apps/apps-deploy.md) de appar du vill använda på enheterna.

  - **Helskärmsläge**: Välj om enheten ska köra en app eller flera appar. Alternativen är:

    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Enstaka app**: Användarna har bara åtkomst till en enda app på enheten. Endast den specifika appen startar när enheten startar. Användarna förhindras att öppna nya appar eller ändra appen som körs.

      - **Välj en app att använda i helskärmsläge**: Välj den hanterade Google Play-appen i listan.

      > [!IMPORTANT]
      > När du använder helskärmsläge kanske inte uppringnings-/telefonappar fungerar som de ska.
  
    - **Flera appar**: Användarna har åtkomst till en begränsad uppsättning appar på enheten. Endast de appar du lägger till startar när enheten startar. Du kan också lägga till webblänkar som användare kan öppna. När principen används ser användarna ikoner för tillåtna appar på startskärmen.

      > [!IMPORTANT]
      > För dedikerade enheter för flera appar gäller att [appen Hanterade startskärmar](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise) från Google Play **måste vara**:
      >   - [Tillagd i Intune](../apps/apps-add-android-for-work.md)
      >   - [Tilldelad till den enhetsgrupp](../apps/apps-deploy.md) som skapats för dina dedikerade enheter
      >
      > Appen **Managed Home Screen** måste inte finnas med i konfigurationsprofilen, men du måste lägga till den som app. När du lägger till appen **Managed Home Screen** visas övriga appar du lägger till i konfigurationsprofilen som ikoner i appen **Managed Home Screen**.
      >
      > När du använder helskärmsläge för flera appar kanske inte uppringnings-/telefonappar fungerar som de ska.
      >
      > Mer information om den hanterade startskärmen finns i [setup Microsoft Managed Home Screen on Dedicated devices in multi-app kiosk mode](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060) (konfigurera Microsofts hanterade startskärm på dedikerade enheter i helskärmsläge för flera appar).

      - **Lägg till**: Välj dina appar i listan.

        Om appen **Hanterad startskärm** inte visas kan du [lägga till den från Google Play](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise). Se till att [tilldela appen](../apps/apps-deploy.md) till den enhetsgrupp som skapats för dina dedikerade enheter.

        Du kan även lägga till andra [Android-appar](../apps/apps-add-android-for-work.md) och [webbappar](../apps/web-app.md) som skapats av din organisation till enheten. Se till att [tilldela appen till den enhetsgrupp som skapats för dina dedikerade enheter](../apps/apps-deploy.md).

      - **Mappikon**: Välj färg och form för mappikonen som visas på den hanterade startskärmen. Alternativen är:
        - Inte konfigurerat 
        - Mörkt tema, rektangel
        - Mörkt tema, cirkel
        - Ljust tema, rektangel
        - Ljust tema, cirkel
      - **Storlek på app- och mappsymbol**: Välj storleken på mappikonen som visas på den hanterade startskärmen. Alternativen är:
        - Inte konfigurerat 
        - Extra liten
        - Liten
        - Genomsnitt
        - Stor
        - Extra stor

          Beroende på storleken på skärmen kan den faktiska ikonstorleken vara annorlunda.

      - **Skärmorientering**: Välj i vilken riktning Hanterad startskärm ska visas på enheter. Alternativen är:
        - Inte konfigurerat
        - Stående
        - Landskap
        - Rotera automatiskt
      - **Appaviseringsbrickor**: **Aktivera** visar antalet nya och olästa meddelanden på appikoner. När detta anges till **Inte konfigurerad** ändrar eller uppdaterar Intune inte den här inställningen.
      - **Virtuell hemknapp**: En programstyrd knapp som tar användarna tillbaka till den hanterade startskärmen så att användarna kan växla mellan appar. Alternativen är:
        - **Inte konfigurerat** (standard): Hemknappen visas inte. Användarna måste använda knappen Bakåt för att växla mellan appar.
        - **Svep uppåt**: En hemknapp visas när en användare sveper uppåt på enheten.
        - **Flytande**: En beständig flytande hemknapp visas på enheten.

      - **Lämna helskärmsläge**: **Aktivera** tillåter att administratörer tillfälligt kan pausa helskärmsläget för att uppdatera enheten. Om du vill använda den här funktionen kan administratören:
  
        1. Fortsätta att välja bakåtknappen tills knappen **Avsluta helskärmsläge** visas. 
        2. Väljer knappen **Avsluta helskärmsläge** och anger PIN-koden för **Kod för att lämna helskärmsläge**.
        3. När du är klar väljer du den **hanterade hemskärmsappen**. Det här steget låser enheten i helskärmsläge för flera appar.

        När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard förhindra att administratörer pausar helskärmsläge. Om administratören fortsätter att välja bakåtknappen och väljer knappen **Avsluta helskärmsläge** visas ett meddelande om att ett lösenord krävs.

      - **Lämna kod för helskärmsläge**: Ange en numerisk PIN-kod på 4–6 siffror. Administratören använder den här PIN-koden för att tillfälligt pausa helskärmsläge.

      - **Ange anpassad URL-bakgrund**: Ange en URL för att anpassa bakgrundsskärmen på den dedikerade enheten. Ange till exempel `http://contoso.com/backgroundimage.jpg`.

        > [!NOTE]
        > I de flesta fall rekommenderar vi att du börjar med bilder med minst följande storlek:
        >
        > - Telefon: 1 080 x 1 920 bildpunkter
        > - Läsplatta: 1 920 x 1 080 bildpunkter
        >
        > För bästa möjliga upplevelse och detaljrikedom föreslår vi att du skapar bildresurser till enheternas respektive bildskärmsspecifikationer.
        >
        > Moderna bildskärmar har högre bildpunktsdensitet och kan visa bilder i 2K/4K.

      - **Genväg till inställningsmenyn**: **Inaktivera** döljer genvägen för hanterade inställningar på den hanterade startskärmen. Användarna kan fortfarande svepa nedåt för att få åtkomst till inställningarna. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard visas genvägen för hanterade inställningar på enheter. Användarna kan även svepa nedåt för att få åtkomst till inställningarna.

      - **Snabbåtkomst till felsökningsmeny**: Den här inställningen styr hur användare kommer åt felsökningsmenyn. Alternativen är:

        - **Aktivera**: Användare kan få åtkomst till felsökningsmenyn enklare. Mer specifikt kan de svepa nedåt eller använda genvägen för hanterade inställningar. Som vanligt kan de fortsätta att välja bakåtknappen 15 gånger.
        - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen. Som standard är enkel åtkomst till felsökningsmenyn avstängd. Användarna måste välja bakåtknappen 15 gånger för att öppna felsökningsmenyn.

        Med hjälp av felsökningsmenyn kan användare:

        - Se och ladda upp loggar för Hanterad startskärm
        - Öppna Googles Android Device Policy Manager-app
        - Öppna [Microsoft Intune-appen](https://play.google.com/store/apps/details?id=com.microsoft.intune)
        - Avsluta helskärmsläge

      - **Wi-Fi-konfiguration**: Om du väljer **Aktivera** visas Wi-Fi-kontrollen på den hanterade startskärmen och användarna kan ansluta enheten till olika Wi-Fi-nätverk. Om du aktiverar den här funktionen aktiveras också enhetsplats. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kanske som standard inte visar Wi-Fi-kontrollen på den hanterade startskärmen. Användare hindras från att ansluta till Wi-Fi-nätverk när den hanterade startskärmen används.

        - **Lista över tillåten Wi-Fi**: Skapa en lista med giltiga namn på trådlösa nätverk, även kallat SSID (Service Set Identifier). Användare av Hanterad startskärm kan bara ansluta till de SSID:n som du anger.

          När det är tomt varken ändrar eller uppdaterar Intune den här inställningen. Som standard är alla tillgängliga Wi-Fi-nätverk tillåtna.

          **Importera** en .csv-fil som innehåller en lista över giltiga SSID:n.

          **Exportera** din aktuella lista till en .csv-fil.

        - **SSID**: Du kan också ange de Wi-Fi-nätverksnamn (SSID) som Hanterad startskärm-användare kan ansluta till. Var noga med att ange giltiga SSID:n.

      - **Bluetooth-konfiguration**: Om du väljer **Aktivera** visas Bluetooth-kontrollen på den hanterade startskärmen och användarna kan koppla enheter över Bluetooth. Om du aktiverar den här funktionen aktiveras också enhetsplats. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kanske som standard inte visar Bluetooth-kontrollen på den hanterade startskärmen. Användare hindras från att konfigurera Bluetooth och para ihop enheter när den hanterade startskärmen används.

      - **Åtkomst till ficklampa**: Om du väljer **Aktivera** visas ficklampekontrollen på den hanterade startskärmen och användarna kan aktivera eller inaktivera ficklampan. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kanske som standard inte visar ficklampekontrollen på den hanterade startskärmen. Användare hindras från att använda ficklampan när den hanterade startskärmen används.

      - **Medievolymkontroll**: Om du väljer **Aktivera** visas medievolymkontrollen på den hanterade startskärmen och användarna kan justera enhetens medievolym med hjälp av ett skjutreglage. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kanske som standard inte visar medievolymkontrollen på den hanterade startskärmen. Användarna hindras från att justera enhetens medievolym på den hanterade startskärmen, om inte deras maskinvaruknappar stöder det.

      - **Snabbåtkomst till enhetsinformation**: **Aktivera** tillåter att användare sveper nedåt för att se enhetsinformationen på Hanterad startskärm, till exempel serienummer, märke och modellnummer och SDK-nivå. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kanske enhetsinformationen inte visas.

      - **Skärmsläckarläge**: Om du väljer **Aktivera** visas en skärmsläckare på den hanterade startskärmen när enheten är låst eller när tidsgränsen uppnås. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kanske som standard inte visar en skärmsläckare på den hanterade startskärmen.

        När läget är aktiverat konfigurerar du även:

        - **Ställ in anpassad skärmsläckarbild**: Ange URL:en till en anpassad PNG, JPG, JPEG, GIF, BMP, WebP eller ICOimage. Om du inte anger en URL används enhetens standardbild, om det finns en sådan.

          Ange till exempel:

          - `http://www.contoso.com/image.jpg`
          - `www.contoso.com/image.bmp`
          - `https://www.contoso.com/image.webp`

          > [!TIP]
          > Alla filresurs-URL:er som kan omvandlas till en bitmapp stöds.

        - **Antal sekunder som skärmsläckaren visas innan skärmen stängs av**: Välj hur länge skärmsläckaren ska visas på enheten. Ange ett värde mellan 0 och 9999999 sekunder. Standardvärdet är `0` sekunder. När värdet är tomt eller är inställt på noll (`0`) är skärmsläckaren aktiv tills en användare interagerar med enheten.
        - **Antal sekunder som enheten är inaktiv innan skärmsläckaren visas**: Välj hur länge enheten ska vara inaktiv innan skärmsläckaren visas. Ange ett värde mellan 1 och 9999999 sekunder. Standardvärdet är `30` sekunder. Du måste ange ett tal som är större än noll (`0`).
        - **Identifiera media innan skärmsläckaren startar**: Om du väljer **Aktivera** (standard) visas inte skärmsläckaren om ljud eller video spelas upp på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kanske som standard inte visar skärmsläckaren, även om ljud eller video spelas upp.

- **Helt hanterade**: Konfigurerar appen Microsoft Launcher på dina helt hanterade enheter.

  - **Gör Microsoft Launcher till standardstartprogram**: Med **Aktivera** anges Microsoft Launcher som standardstartprogram på startskärmen. Om du använder Launcher som standardprogram kan användarna inte använda något annat startprogram. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard måste inte Microsoft Launcher användas som standardstartprogram.
  - **Konfigurera anpassade skrivbordsunderlägg**: **Aktivera** gör att du kan använda din egen avbildning som skrivbordsunderlägg på startskärmen och välja om användarna ska kunna ändra bilden. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard behåller enheten det aktuella skrivbordsunderlägget.
    - **Ange URL till skrivbordsunderläggsbild**: Ange URL till skrivbordsunderläggsbilden. Den här bilden visas på enhetens startskärm. Ange till exempel `http://www.contoso.com/image.jpg`. 
    - **Tillåt användare att ändra skrivbordsunderlägg**: **Aktivera** tillåter att användarna ändrar skrivbordsunderläggsbilden. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard hindras användare från att ändra skrivbordsunderlägg.
  - **Aktivera startfeed**: **Aktivera** aktiverar startfeeden, som visar kalendrar, dokument och senaste aktiviteter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Denna feed visas som standard inte.
    - **Tillåt att användaren aktiverar/inaktiverar feed**: **Aktivera** tillåter att användare aktiverar eller inaktiverar startfeeden. **Aktivera** tvingar bara den här inställningen den första gången profilen tilldelas. Alla framtida profiltilldelningar tvingar inte den här inställningen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard hindras användare från att ändra inställningar för startfeeden.
  - **Docknärvaro**: Dockan ger användarna snabb åtkomst till sina appar och verktyg. Alternativen är:
    - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
    - **Visa**: Dockan visas på enheter.
    - **Dölj**: Dockan är dold. Användarna måste svepa upp för att få åtkomst till dockan.
    - **Inaktiverad**: Dockan visas inte på enheter och användare hindras från att visa den.

  - **Tillåt användaren att ändra dockans närvaro**: **Aktivera** tillåter användare att visa eller dölja dockan. **Aktivera** tvingar bara den här inställningen den första gången profilen tilldelas. Alla framtida profiltilldelningar tvingar inte den här inställningen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard tillåts inte användare att ändra konfigurationen för enhetsdockan.

  - **Ersättning av sökfältet**: Välj var sökfältet ska läggas till. Alternativen är:
    - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
    - **Överst**: Sökfältet visas längst upp på enheterna.
    - **Nedre**: Sökfältet visas längst ned på enheterna.
    - **Dölj**: Sökfältet är dolt.

<!-- MandiA (7.16.2020) The following settings may be in a future release. Per PM, we can leave it in GitHub, not live. Remove comment tags if/when it releases.
  - **Allow user to change search bar placement**: **Enable** allows users to change the location of the search bar. **Enable** only forces this setting the first time the profile is assigned. Any future profile assignments don't force this setting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, users are prevented from changing the location.
End of comment -->

### <a name="password"></a>lösenordsinställning

- **Inaktivera Lås skärm**: Välj **Inaktivera** om du vill hindra användarna från att använda låsskärmsfunktionen Keyguard på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att använda Keyguard-funktionerna.
- **Inaktiverade låsskärmsfunktioner**: När keyguard har aktiverats på enheten väljer du vilka funktioner som ska inaktiveras. När **Säker kamera** är markerad är till exempel kamerafunktionen inaktiverad på enheten. Funktioner som inte är markerade är aktiverade på enheten.

  Dessa funktioner är tillgängliga för användarna när enheten är låst. Användarna kommer inte att se eller få åtkomst till de funktioner som är markerade.

- **Lösenordstyp som krävs**: Anger den komplexitetsnivå som krävs för lösenordet och om biometriska enheter kan användas. Alternativen är:
  - **Standard för enheten**
  - **Lösenord krävs, inga begränsningar**
  - **Svag biometrik**: [Stark eller svag biometri](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (öppnar Androids webbplats)
  - **Numeriskt**: Lösenordet får bara innehålla siffror, till exempel `123456789`. Ange även:
    - **Minsta lösenordslängd**: Ange den minsta längd som lösenordet måste ha (mellan 4 och 16 tecken).
  - **Numeriskt avancerat**: Upprepade eller efterföljande siffror, till exempel ”1111” eller ”1234”, tillåts inte. Ange även:
    - **Minsta lösenordslängd**: Ange den minsta längd som lösenordet måste ha (mellan 4 och 16 tecken).
  - **Alfabetiskt**: Bokstäver i alfabetet måste anges. Siffror och symboler krävs inte. Ange även:
    - **Minsta lösenordslängd**: Ange den minsta längd som lösenordet måste ha (mellan 4 och 16 tecken).
  - **Alfanumeriskt**: Innehåller versaler, gemener och numeriska tecken. Ange även:
    - **Minsta lösenordslängd**: Ange den minsta längd som lösenordet måste ha (mellan 4 och 16 tecken).
  - **Alfanumeriskt med symboler**: Innehåller versaler, gemener, numeriska tecken, skiljetecken och symboler. Ange även:

    - **Minsta lösenordslängd**: Ange den minsta längd som lösenordet måste ha (mellan 4 och 16 tecken).
    - **Antal tecken som krävs**: Ange hur många tecken som lösenordet måste innehålla (mellan 0 och 16 tecken).
    - **Antal gemener som krävs**: Ange hur många gemener som lösenordet måste innehålla (mellan 0 och 16 tecken).
    - **Antal versaler som krävs**: Ange hur många versaler som lösenordet måste innehålla (mellan 0 och 16 tecken).
    - **Antal icke-bokstavstecken som krävs**: Ange hur många icke-bokstavstecken (bokstäver som inte ingår i alfabetet) som lösenordet måste innehålla (mellan 0 och 16 tecken).
    - **Antal numeriska tecken som krävs**: Ange hur många numeriska tecken (till exempel `1`, `2` eller `3`) som lösenordet måste innehålla (mellan 0 och 16 tecken).
    - **Antal symboltecken som krävs**: Ange hur många symboltecken (till exempel `&`, `#` eller `%`) som lösenordet måste innehålla (mellan 0 och 16 tecken).

- **Antal dagar tills lösenordet går ut**: Ange antalet dagar innan enhetslösenordet måste ändras (från 1 till 365 dagar). Ange till exempel `90` om lösenordet ska upphöra efter 90 dagar. När lösenordet upphör att gälla uppmanas användarna att skapa ett nytt lösenord. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.
- **Antal lösenord som krävs innan användaren kan återanvända ett lösenord**: Använd den här inställningen för att förhindra att användare återanvänder tidigare använda lösenord. Ange antal tidigare använda lösenord som inte får återanvändas, från 1–24. Ange till exempel `5` om användare inte ska kunna ange ett nytt lösenord till sina nuvarande lösenord eller något av de föregående fyra lösenorden. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.
- **Antal felaktiga inloggningar innan enheten rensas**: Ange antal tillåtna felaktiga lösenord innan enheten rensas (från 4 till 11). `0` (noll) kan inaktivera funktionen för rensning av enheten. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.

  > [!NOTE]
  > Fullständigt hanterade, dedikerade och företagsägda arbetsprofilenheter uppmanas inte att ange ett lösenord. Inställningarna tillämpas och du måste ange lösenordet manuellt. Principen som framtvingar detta rapporterar att åtgärden misslyckades tills du anger lösenordet som uppfyller dina krav.

### <a name="power-settings"></a>Energiinställningar

- **Tid innan skärmen låses**: Ange den längsta tid som en användare kan ange innan enheten låses. Om du till exempel anger `10 minutes` kan användarna ange en tid från 15 sekunder till 10 minuter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

- **Skärmen är tänd när enheten är ansluten**: Välj vilka strömkällor som innebär att enhetens skärm är tänd när den är ansluten.

### <a name="users-and-accounts"></a>Användare och konton

- **Lägg till nya användare**: **Blockera** förhindrar användare från att lägga till nya användare. Varje användare har ett personligt utrymme på enheten för anpassade startskärmar, konton, appar och inställningar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att lägga till andra användare på enheten.
- **Borttagning av användare**: **Blockera** förhindrar användarna från att ta bort användare. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att ta bort andra användare från enheten.
- **Kontoändringar** (endast dedikerade enheter): **Blockera** förhindrar att användarna ändrar konton. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användare att uppdatera användarkonton på enheten.

  > [!NOTE]
  > Den här inställningen gäller inte för fullständigt hanterade, dedikerade och företagsägda arbetsprofilenheter. Om du konfigurerar den här inställningen ignoreras inställningen och har ingen effekt.

- **Användaren kan ställa in autentiseringsuppgifter**: Om du väljer **Blockera** hindras användare från att konfigurera certifikat som har tilldelats till enheter. Det gäller även enheter som inte är associerade med ett användarkonto. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användare att konfigurera eller ändra sina autentiseringsuppgifter i nyckellagret.
- **Personliga Google-konton**: Om du väljer **Blockera** hindras användare från att lägga till privata Google-konton på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användare att lägga till sina personliga Google-konton.

### <a name="applications"></a>Program

- **Tillåt installation från okända källor**: **Tillåt** tillåter att användare aktiverar **Okända källor**. Den här inställningen gör att appar kan installeras från okända källor, inklusive andra källor än Google Play. Den gör att användare kan läsa in appar separat på enheten via andra kanaler än Google Play Store. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard förhindra att användarna aktiverar **Okända källor**.
- **Tillåt åtkomst till alla appar i Google Play-butiken**: När **Tillåt** har valts får användarna åtkomst till alla appar i Google Play. De får inte åtkomst till de appar som har blockerats av administratören i [Klientappar](../apps/apps-add-android-for-work.md).

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard:
  
  - Tvinga användarna att endast använda appar som administratören gjort tillgängliga i Google Play, eller appar som krävs i [Klientappar](../apps/apps-add-android-for-work.md). 
  - Automatiskt avinstallera alla appar som identifierats som installerade av användare utanför Google Play-butiken.

  Om du vill aktivera separat inläsning ställer du in alternativen **Tillåt installation från okända källor** och **Tillåt åtkomst till alla appar i Google Play Store** på **Tillåt**.

- **Automatiska appuppdateringar**: Enheter söker efter programuppdateringar dagligen. Välj när automatiska uppdateringar ska installeras. Alternativen är:
  - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
  - **Användarens val**: Operativsystemet kan vara inställt på det här alternativet som standard. Användarna kan ange sina inställningar i den hanterade Google Play-appen.
  - **Aldrig**: Uppdateringar installeras aldrig. Det här alternativet rekommenderas inte.
  - **Endast Wi-Fi**: Uppdateringar installeras bara när enheten är ansluten till ett Wi-Fi-nätverk.
  - **Alltid**: Uppdateringar installeras när de är tillgängliga.

### <a name="connectivity"></a>Anslutningar

- **Konstant VPN-anslutning**: **Aktivera** konfigurerar en konstant VPN-klient som automatiskt ansluter och återansluter till VPN. VPN-anslutningen Alltid på förblir ansluten. Eller ansluter direkt när användarna låser enheten, enheten startas om eller det trådlösa nätverket ändras.

  Välj **Inte konfigurerad** om du inte vill att VPN-anslutningarna alltid ska vara aktiva. Inställningen tillämpas på alla VPN-klienter.

  > [!IMPORTANT]
  > Var noga med att endast distribuera en princip för VPN som alltid är aktivt för en enskild enhet. Det går inte att distribuera flera principer av den här typen till en enskild enhet.

- **VPN-klient**: Välj en VPN-klient som har stöd för AlwaysOn. Alternativen är:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Anpassad
    - **Paket-ID**: Ange paket-ID:t för appen i Google Play Butik. Om URL:en för appen i Google Play Store exempelvis är `https://play.google.com/store/details?id=com.contosovpn.android.prod` är paket-ID:t `com.contosovpn.android.prod`.

  > [!IMPORTANT]
  > - Den VPN-klient som du väljer måste vara installerad på enheten och den måste ha stöd för ”per app-VPN” i arbetsprofiler. Annars uppstår ett fel. 
  > - Du måste godkänna VPN-klientappen i **den hanterade Google Play Store-butiken**, synkronisera appen till Intune och distribuera appen till enheten. När du har gjort det installeras appen i användarens arbetsprofil.
  > - Du måste fortfarande konfigurera VPN-klienten med en [VPN-profil](vpn-settings-android-enterprise.md) eller via en [appkonfigurationsprofil](../apps/app-configuration-policies-use-android.md).
  > - Det kan finnas kända problem när du använder per app-VPN med F5-åtkomst för Android 3.0.4. Du hittar mer information i [Viktig F5-information för F5-åtkomst i Android 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android).

- **Låst läge**: **Aktivera** om du vill tvinga all nätverkstrafik att använda VPN-tunneln. Om en anslutning till VPN inte upprättas har inte enheten åtkomst till nätverket. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att trafik flödar via VPN-tunneln eller det mobila nätverket.

- **Rekommenderad global proxy**: **Aktivera** lägger till en global proxy på enheterna. När inställningen är aktiverad kan HTTP- och HTTPS-trafik, inklusive vissa appar på enheten, använda den proxy som du anger. Den här proxyn är bara en rekommendation. Det är möjligt att vissa appar inte använder proxyn. Om du väljer **Inte konfigurerad** (standard) läggs inte en rekommenderad global proxy till.

  Mer information om den här funktionen finns i [setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)) (öppnar en Android-webbplats).

  När detta är aktiverat anger du även en **proxytyp**. Alternativen är:

  - **Direkt**: Ange information om proxyservern manuellt, inklusive:
    - **Värd**: Ange värdnamnet eller IP-adressen för proxyservern. Ange till exempel `proxy.contoso.com` eller `127.0.0.1`.
    - **Portnummer**: Ange TCP-portnumret som används av proxyservern. Ange till exempel `8080`.
    - **Undantagna värdar**: Ange en lista över värdnamn eller IP-adresser som inte ska använda proxyn. Den här listan kan innehålla en asterisk (`*`) som jokertecken och flera värdar avgränsade med semikolon (`;`) utan blanksteg. Ange till exempel `127.0.0.1;web.contoso.com;*.microsoft.com`.

  - **Automatisk konfigurerad proxy**: Ange en **PAC-webbadress** till ett skript för automatisk proxykonfiguration. Ange till exempel `https://proxy.contoso.com/proxy.pac`.

    Mer information om PAC-filer finns under [PAC-fil (Proxy Auto-Configuration)](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (öppnar en webbplats som inte tillhör Microsoft).

  Mer information om den här funktionen finns i [setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)) (öppnar en Android-webbplats).

## <a name="work-profile-only"></a>Endast arbetsprofil

Dessa inställningar gäller för Android Enterprise-registreringstyper där Intune bara styr arbetsprofilen, t. ex. Android Enterprise-arbetsprofilregistrering på en personlig enhet eller BYOD (Bring Your Own Device).

### <a name="work-profile-settings"></a>Inställningar för arbetsprofil

- **Kopiera och klistra in mellan arbetsprofiler och personliga profiler**: **Blockera** förhindrar att funktionen kopiera och klistra in fungerar mellan arbetsappar och personliga appar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användare att dela data med hjälp av kopiera och klistra in med appar i den personliga profilen.
- **Datadelning mellan arbetsprofiler och personliga profiler**: Välj om appar i arbetsprofilen ska kunna dela data med appar i den personliga profilen. Du kan till exempel styra delningsåtgärder i program, så som alternativet **Dela...** i Chrome-webbläsarappen. Den här inställningen gäller inte för kopierings- och inklistringsbeteendet i Urklipp. Alternativen är:
  - **Standard för enheten**: Enhetens standardbeteende för delning beror på Android-versionen.
    - På enheter som kör Android 6.0 och senare är delning från arbetsprofilen till den personliga profilen blockerad. Delning från den personliga profilen till arbetsprofilen är tillåten.
    - På enheter som kör Android 5.0 och äldre är delning mellan arbetsprofilen och den personliga profilen blockerad i båda riktningarna.
  - **Appar i arbetsprofilen kan hantera delningsförfrågningar från den personliga profilen**: Aktiverar den inbyggda Android-funktionen som tillåter delning från den personliga profilen till arbetsprofilen. När detta är aktiverat, kan en delningsbegäran från en app i den personliga profilen dela med appar i arbetsprofilen. Det här är standardinställningen för Android-enheter som kör tidigare versioner än 6.0.
  - **Inga delningsbegränsningar**: Aktiverar delning över arbetsprofilgränsen i bägge riktningarna. När du väljer den här inställningen så kommer appar i arbetsprofilen att kunna dela data med omärkta appar i den personliga profilen. Med den här inställningen kan hanterade appar i arbetsprofilen dela med appar på den ohanterade delen av enheten. Använd därför den här inställningen med försiktighet.

- **Arbetsprofilmeddelanden när enheten är låst**: **Blockera** förhindrar att fönstermeddelanden, bland annat popup-fönster, inkommande samtal, utgående samtal, systemaviseringar och systemfel visas på låsta enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard visa meddelanden.
- **Standardappbehörigheter**: Ange standardprincipen för behörighet för alla appar i arbetsprofilen. Från och med Android 6 måste användarna bevilja vissa behörigheter som krävs av appar när appen startas. Den här principinställningen låter dig välja om användare ombeds att bevilja behörigheter för alla appar i arbetsprofilen. Om du till exempel tilldelar en app i arbetsprofilen som kräver platsåtkomst. Normalt skulle den appen be användarna att godkänna eller neka platsåtkomst för appen. Använd den här principen för att automatiskt bevilja behörigheter utan att användarna tillfrågas, för att automatiskt neka behörigheter utan att användarna tillfrågas eller för att låta användarna bestämma. Alternativen är:
  - **Standard för enheten**
  - **Fråga**
  - **Bevilja automatiskt**
  - **Neka automatiskt**

  Du kan också använda en appkonfigurationsprincip för att bevilja behörigheter för enskilda appar (**Klientappar** > **Appkonfigurationsprinciper**).

- **Lägga till och ta bort konton**: **Blockera** förhindrar att användare kan lägga till eller ta bort konton manuellt i arbetsprofilen. När du till exempel distribuerar Gmail-appen till en Android-arbetsprofil kan du hindra användare från att lägga till eller ta bort konton i arbetsprofilen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att konton läggs till i arbetsprofilen.  

  > [!NOTE]
  > Google-konton kan inte läggas till i en arbetsprofil.

- **Kontaktdelning via Bluetooth**: **Aktivera** tillåter delning och åtkomst till arbetsprofilkontakter från en annan enhet, inklusive en bil, som paras ihop med Bluetooth. När den här inställningen är aktiverad kan vissa Bluetooth-enheter tillåtas att cachelagra arbetskontakter vid den första anslutningen. Att inaktiverar den här principen efter en inledande länkning/synkronisering kanske inte kan ta bort arbetskontakter från en bluetooth-enhet.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kanske som standard inte delar arbetskontakter.

  Den här inställningen gäller för:

  - Androids arbetsprofilenheter på Android OS v6.0 och senare

- **Skärmdump**: **Blockera** förhindrar skärmbilder eller skärmdumpar på enheten i arbetsprofilen. Förhindrar också att innehållet visas på visningsenheter som inte har en säker videoutgång. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att skärmdumpar tas.

- **Visa arbetskontaktens nummerpresentation i en personlig profil**: Med **Blockera** visas inte arbetskontaktens nummerpresentation i den personliga profilen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard visa information om arbetskontakter när de ringer upp.

  Den här inställningen gäller för:

  - Android OS v6.0 och nyare versioner

- **Sök arbetskontakter från en personlig profil**: **Blockera** förhindrar att användarna söker efter arbetskontakter i appar i den personliga profilen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta sökningar efter arbetskontakter i den personliga profilen.

- **Kamera**: **Blockera** förhindrar åtkomst till kameran på enheten i arbetsprofilen. Kameran på den personliga sidan påverkas inte av inställningen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta åtkomst till kameran.

- **Tillåt widgetar från arbetsprofilappar**: Om du väljer **Aktivera** kan användare placera widgetar som exponeras av appar på startskärmen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard inaktivera den här funktionen.

  Outlook är till exempel installerat i dina användares arbetsprofiler. När **Aktivera** har angetts kan användarna placera agendawidgeten på enhetens startsida.

- **Kräv lösenord för arbetsprofil**: Med **Kräv** framtvingas en lösenordsprincip som endast gäller för apparna i arbetsprofilen. Som standard kan användare använda de två separat definierade PIN-koderna. Eller så kan användarna kombinera PIN-koderna till den starkare av de två PIN-koderna. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att använda arbetsappar utan att behöva ange något lösenord.

  Den här inställningen gäller för:

  - Android 7.0 och senare med arbetsprofilen aktiverad

  Konfigurera också:

  - **Minsta lösenordslängd**: Ange den minsta längd som lösenordet måste ha (mellan 4 och 16 tecken).
  - **Maximalt antal minuter av inaktivitet innan arbetsprofilen låses**: Ange hur lång tid enheterna måste vara inaktiva innan skärmen låses automatiskt. Därefter måste användaren ange sina autentiseringsuppgifter för att få åtkomst igen. Ange till exempel `5` om du vill låsa enheten efter 5 minuters inaktivitet. Om värdet är tomt eller inställt på **Inte konfigurerad**, ändrar eller uppdaterar Intune inte inställningen.

    Användare kan inte ange ett tidsvärde på enheten som är större än den konfigurerade tiden i profilen. Användarna kan dock ange ett lägre tidsvärde. Om profilen t.ex. är inställd på `15` minuter, kan användare ange värdet till 5 minuter. Användarna kan inte ange värdet till 30 minuter.

  - **Antal felaktiga inloggningar innan enheten rensas**: Ange antal tillåtna felaktiga lösenord innan arbetsprofilen på enheten rensas, från 4 till 11. `0` (noll) kan inaktivera funktionen för rensning av enheten. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.

  - **Lösenordets giltighetstid (dagar)** : Ange antalet dagar innan användarlösenordet måste ändras (från **1**-**365**).
  - **Lösenordstyp som krävs**: Anger den komplexitetsnivå som krävs för lösenordet och om biometriska enheter kan användas. Alternativen är:
    - **Standard för enheten**
    - **Låg säkerhetsbiometri**: [Stark eller svag biometri](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (öppnar Androids webbplats)
    - **Obligatoriskt**
    - **Minst numeriskt**: Innehåller numeriska tecken, till exempel `123456789`.
    - **Numeriskt avancerat**: Upprepade eller efterföljande siffror, till exempel `1111` eller `1234`, tillåts inte.
    - **Minst alfabetiskt**: Innehåller bokstäver i alfabetet. Siffror och symboler krävs inte.
    - **Minst alfanumeriskt**: Innehåller versaler, gemener och numeriska tecken.
    - **Minst alfanumeriskt med symboler**: Innehåller versaler, gemener, numeriska tecken, skiljetecken och symboler.

  - **Förhindra återanvändning av tidigare lösenord**: Använd den här inställningen för att förhindra att användare återanvänder tidigare använda lösenord. Ange antal tidigare använda lösenord som inte får återanvändas, från 1–24. Ange till exempel `5` om användare inte ska kunna ange ett nytt lösenord till sina nuvarande lösenord eller något av de föregående fyra lösenorden. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.
  - **Ansiktsupplåsning**: **Blockera** förhindrar att användare använder enhetens ansiktsigenkänning för att låsa upp arbetsprofilen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att låsa upp enheten med hjälp av ansiktsigenkänning.
  - **Upplåsning med fingeravtryck**: **Blockera** förhindrar att användarna använder enhetens till att låsa upp arbetsprofilen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att låsa upp enheten med hjälp av fingeravtryck.
  - **Irisupplåsning**: **Blockera** förhindrar att användare använder enhetens irisscanner för att låsa upp arbetsprofilen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att låsa upp enheten med hjälp av irisscannern.
  - **Smart Lock och andra betrodda agenter**: **Blockera** förhindrar Smart Lock och andra betrodda agenter från att ändra låsskärmsinställningar på kompatibla enheter. Med den här funktionen, även kallad förtroendeagent, kan du inaktivera eller kringgå lösenordet för enhetens låsskärm om enheten finns på en betrodd plats. Du kan exempelvis kringgå lösenordet för arbetsprofilen när enheten är ansluten till en specifik Bluetooth-enhet eller när den är nära en NFC-tagg. Använd den här inställningen för att förhindra att användare konfigurerar Smart Lock.

    När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

### <a name="password"></a>lösenordsinställning

Lösenordsinställningarna gäller för personliga profiler på enheter som använder en arbetsprofil.

- **Minsta lösenordslängd**: Ange den minsta längd som lösenordet måste ha (mellan 4 och 16 tecken).
- **Maximalt antal minuter av inaktivitet innan skärmen låses**: Ange hur lång tid enheterna måste vara inaktiva innan skärmen låses automatiskt. Därefter måste användaren ange sina autentiseringsuppgifter för att få åtkomst igen. Ange till exempel `5` om du vill låsa enheten efter 5 minuters inaktivitet. Om värdet är tomt eller inställt på **Inte konfigurerad**, ändrar eller uppdaterar Intune inte inställningen.

  Användare kan inte ange ett tidsvärde på enheten som är större än den konfigurerade tiden i profilen. Användarna kan dock ange ett lägre tidsvärde. Om profilen t.ex. är inställd på `15` minuter, kan användare ange värdet till 5 minuter. Användarna kan inte ange värdet till 30 minuter.

- **Antal felaktiga inloggningar innan enheten rensas**: Ange antal tillåtna felaktiga lösenord innan arbetsprofilen på enheten rensas, från 4 till 11. `0` (noll) kan inaktivera funktionen för rensning av enheten. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.
- **Lösenordets giltighetstid (dagar)** : Ange antalet dagar innan enhetslösenordet måste ändras (från 1 till 365 dagar). Ange till exempel `90` om lösenordet ska upphöra efter 90 dagar. När lösenordet upphör att gälla uppmanas användarna att skapa ett nytt lösenord. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.
- **Lösenordstyp som krävs**: Anger den komplexitetsnivå som krävs för lösenordet och om biometriska enheter kan användas. Alternativen är:
  - **Standard för enheten**
  - **Låg säkerhetsbiometri**: [Stark eller svag biometri](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (öppnar Androids webbplats)
  - **Obligatoriskt**
  - **Minst numeriskt**: Innehåller numeriska tecken, till exempel `123456789`.
  - **Numeriskt avancerat**: Upprepade eller efterföljande siffror, till exempel `1111` eller `1234`, tillåts inte.
  - **Minst alfabetiskt**: Innehåller bokstäver i alfabetet. Siffror och symboler krävs inte.
  - **Minst alfanumeriskt**: Innehåller versaler, gemener och numeriska tecken.
  - **Minst alfanumeriskt med symboler**: Innehåller versaler, gemener, numeriska tecken, skiljetecken och symboler.

- **Förhindra återanvändning av tidigare lösenord**: Använd den här inställningen för att förhindra att användare återanvänder tidigare använda lösenord. Ange antal tidigare använda lösenord som inte får återanvändas, från 1–24. Ange till exempel `5` om användare inte ska kunna ange ett nytt lösenord till sina nuvarande lösenord eller något av de föregående fyra lösenorden. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.
- **Upplåsning med fingeravtryck**: **Blockera** förhindrar att användarna använder enhetens fingeravtrycksläsare till att låsa upp den. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att låsa upp enheten med hjälp av fingeravtryck.
- **Ansiktsupplåsning**: **Blockera** förhindrar att användare använder enhetens ansiktsigenkänning för att låsa upp enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att låsa upp enheten med hjälp av ansiktsigenkänning.
- **Irisupplåsning**: **Blockera** förhindrar att användare använder enhetens irisscanner för att låsa upp enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att låsa upp enheten med hjälp av irisscannern.
- **Smart Lock och andra betrodda agenter**: **Blockera** förhindrar Smart Lock och andra betrodda agenter från att ändra låsskärmsinställningar på kompatibla enheter. Med den här funktionen, även kallad förtroendeagent, kan du inaktivera eller kringgå lösenordet för enhetens låsskärm om enheten finns på en betrodd plats. Du kan exempelvis kringgå lösenordet för arbetsprofilen när enheten är ansluten till en specifik Bluetooth-enhet eller när den är nära en NFC-tagg. Använd den här inställningen för att förhindra att användare konfigurerar Smart Lock.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

### <a name="system-security"></a>Systemsäkerhet

- **Hotgenomsökning för appar**: **Kräv** innebär att inställningen **Verifiera appar** är aktiverad för arbetsprofiler och personliga profiler. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

  Den här inställningen gäller för:

  - Android 8 (Oreo) och senare

- **Hindra appinstallationer från okända källor i privat profil**: Android Enterprise-arbetsprofilenheter har utformats för att inte kunna installera appar från andra källor än Play Store. Med den här inställningen får administratörer större kontroll över appinstallationer från okända källor. Om du väljer **Blockera** går det inte att installera appar från andra källor än Google Play Store i den personliga profilen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta appinstallationer från okända källor i den personliga profilen. Arbetsprofilenheter har två profiler:

  - En arbetsprofil som hanteras med MDM.
  - En personlig profil som är isolerad från MDM-hantering.

### <a name="connectivity"></a>Anslutningar

- **Konstant VPN-anslutning**: **Aktivera** konfigurerar en konstant VPN-klient som automatiskt ansluter och återansluter till VPN. VPN-anslutningen Alltid på förblir ansluten. Eller ansluter direkt när användare låser enheten, enheten startas om eller det trådlösa nätverket ändras.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard inaktivera VPN-anslutningen Alltid på för alla VPN-klienter.

  > [!IMPORTANT]
  > Var noga med att endast distribuera en princip för VPN som alltid är aktivt för en enskild enhet. Det går inte att distribuera flera principer av den här typen till en enskild enhet.

- **VPN-klient**: Välj en VPN-klient som har stöd för AlwaysOn. Alternativen är:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Anpassad
    - **Paket-ID**: Ange paket-ID:t för appen i Google Play Butik. Om URL:en för appen i Google Play Store exempelvis är `https://play.google.com/store/details?id=com.contosovpn.android.prod` är paket-ID:t `com.contosovpn.android.prod`.

  > [!IMPORTANT]
  > - Den VPN-klient som du väljer måste vara installerad på enheten och den måste ha stöd för ”per app-VPN” i arbetsprofiler. Annars uppstår ett fel.
  > - Du måste godkänna VPN-klientappen i **den hanterade Google Play Store-butiken**, synkronisera appen till Intune och distribuera appen till enheten. När du har gjort det installeras appen i användarens arbetsprofil.
  > - Det kan finnas kända problem när du använder per app-VPN med F5-åtkomst för Android 3.0.4. Du hittar mer information i [Viktig F5-information för F5-åtkomst i Android 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android).

- **Låst läge**: **Aktivera** om du vill tvinga all nätverkstrafik att använda VPN-tunneln. Om en anslutning till VPN inte upprättas har inte enheten åtkomst till nätverket.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att trafik flödar via VPN-tunneln eller det mobila nätverket.

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Du kan även skapa helskärmslägesprofiler för dedikerade enheter för [Android](device-restrictions-android.md#kiosk)- och [Windows 10](kiosk-settings.md)-enheter.

[Konfigurera och felsöka Android Enterprise-enheter i Microsoft Intune](https://support.microsoft.com/help/4476974).
