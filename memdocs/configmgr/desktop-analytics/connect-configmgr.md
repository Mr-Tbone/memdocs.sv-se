---
title: Ansluta Configuration Manager
titleSuffix: Configuration Manager
description: En instruktions guide för att ansluta Configuration Manager med Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: c7bb6d01a35ce42002207d57d27fc41c37646d15
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268869"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Så här ansluter du Configuration Manager med Desktop Analytics

Desktop Analytics är nära integrerat med Configuration Manager. Kontrol lera först att webbplatsen är uppdaterad så att den stöder de senaste funktionerna. Skapa sedan Skriv bords analys anslutningen i Configuration Manager. Övervaka slutligen hälso tillståndet för anslutningen.

## <a name="update-the-site"></a><a name="bkmk_hotfix"></a>Uppdatera platsen

Se först till att Configuration Managers platsen kör minst version 1902. Mer information finns i [Installera uppdateringar i konsolen](../core/servers/manage/install-in-console-updates.md).

Du måste också installera den samlade uppdateringen för version 1902 (4500571) för att stödja integrering med Desktop Analytics. Mer information om den här uppdateringen finns i samlad [uppdatering för Configuration Manager aktuella grenen, version 1902](https://support.microsoft.com/help/4500571).

1. Uppdatera platsen med den samlade uppdateringen för version 1902. Mer information finns i [Installera uppdateringar i konsolen](../core/servers/manage/install-in-console-updates.md).

2. Uppdatera klienter. Överväg att använda automatisk klient uppgradering för att förenkla den här processen. Mer information finns i [Uppgradera klienter](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).

## <a name="connect-to-the-service"></a><a name="bkmk_connect"></a>Anslut till tjänsten

> [!TIP]
> Innan du startar guiden skapar du mål samlingen som nämns i steg 8, eftersom du inte kan välja utanför guiden när du har startat den.

Använd den här proceduren för att ansluta Configuration Manager till Desktop Analytics och konfigurera enhets inställningar. Den här proceduren är en eng ång slö process för att koppla din hierarki till moln tjänsten.

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden **Azure-tjänster** . Välj **Konfigurera Azure-tjänster** i menyfliksområdet.

    > [!TIP]
    > Anslut till tjänsten direkt från noden för att **underhålla Skriv bords analys** . I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** och väljer noden **Skriv bords analys** . I rutan *nytt till Skriv bords analys?* väljer du den andra länken för att *ansluta Configuration Manager till Skriv bords analys tjänsten*.

2. Konfigurera följande inställningar på sidan **Azure-tjänster** i guiden Azure-tjänster:

    - Ange ett **namn** för objektet i Configuration Manager.

    - Ange en valfri **Beskrivning** som hjälper dig att identifiera tjänsten.

    - Välj **Skriv bords analys** i listan över tillgängliga tjänster.

   Välj **Nästa**.

3. På sidan **app** väljer du lämplig Azure- **miljö**. Välj sedan **Bläddra** efter webbappen.

4. Om du har en befintlig app som du vill använda för den här tjänsten väljer du den i listan och väljer **OK**.

5. I de flesta fall kan du skapa en app för Skriv bords analys anslutningen med den här guiden. Välj **Skapa**.<!-- 3572123 -->

    > [!TIP]
    > Om du inte kan skapa appen från den här guiden kan du skapa appen manuellt i Azure AD och sedan importera till Configuration Manager. Mer information finns i [skapa och importera app för Configuration Manager](troubleshooting.md#create-and-import-app-for-configuration-manager).

6. Konfigurera följande inställningar i fönstret **skapa serverprogram** :

    - **Program namn**: ett eget namn för appen i Azure AD.

    - **Start sidans URL**: det här värdet används inte av Configuration Manager, men krävs av Azure AD. Det här värdet är som standard `https://ConfigMgrService`.

    - **App-ID-URI**: det här värdet måste vara unikt i din Azure AD-klient. Den finns i åtkomsttoken som används av Configuration Manager-klienten för att begära åtkomst till tjänsten. Det här värdet är som standard `https://ConfigMgrService`.

    - **Giltighets period för hemlig nyckel**: Välj antingen **1 år** eller **2 år** i list rutan. Ett år är standardvärdet.

    Välj **Logga** in. När du har autentiserat till Azure visar sidan namnet på **Azure AD-klienten** för referensen.

    > [!NOTE]
    > Slutför det här steget som **Global administratör**. Autentiseringsuppgifterna sparas inte av Configuration Manager. Den här personen behöver inte behörigheter i Configuration Manager och behöver inte vara samma konto som kör guiden Azure-tjänster.

    Välj **OK** för att skapa webbappen i Azure AD och Stäng dialog rutan skapa serverprogram. I dialog rutan Server App väljer du **OK**. Välj sedan **Nästa** på sidan app i guiden Azure-tjänster.

7. Konfigurera följande inställningar på sidan **diagnostikdata** :

    - **Kommersiellt ID**: det här värdet ska automatiskt fyllas i med organisationens ID. Om den inte gör det kontrollerar du att proxyservern har kon figurer ATS för att tillåta alla nödvändiga [slut punkter](enable-data-sharing.md#endpoints) innan du fortsätter. Du kan också hämta ditt kommersiella ID manuellt från [Skriv bords analys portalen](monitor-connection-health.md#bkmk_ViewCommercialID).

    - **Windows 10-diagnostisk datanivå**: Välj minst **Basic**. Se [diagnostiska data nivåer](enable-data-sharing.md#diagnostic-data-levels)
  
    - **Tillåt enhets namn i diagnostikdata**: Välj **Aktivera**

        > [!NOTE]
        > Från och med Windows 10 version 1803 skickas inte enhets namnet till Microsoft som standard. Om du inte skickar enhets namnet visas det i Skriv bords analys som "okänt". Det här beteendet kan göra det svårt att identifiera och utvärdera enheter.

   Välj **Nästa**. Sidan **tillgängliga funktioner** visar de Skriv bords analys funktioner som är tillgängliga med inställningarna för diagnostikdata från föregående sida. Välj **Nästa** för att fortsätta eller **föregående** för att göra ändringar.

    ![Exempel sidan tillgängliga funktioner i guiden Azure-tjänster](media/available-functionality.png)

<a name="bkmk_Collections"></a>

8. Konfigurera följande inställningar på sidan **samlingar** :

    - **Visnings namn**: Skriv bords analys portalen visar den här Configuration Manager anslutningen med det här namnet. Använd den för att skilja mellan olika hierarkier och för att identifiera samlingar från separata hierarkier. Använd villkor för att enkelt skilja flera hierarkier i din miljö, till exempel: *test labb* eller *produktion*.

    - **Mål samling**: den här samlingen innehåller alla enheter som Configuration Manager konfigurerar med inställningarna för ditt handels-ID och diagnostikdata. Det är en fullständig uppsättning enheter som Configuration Manager ansluter till Skriv bords analys tjänsten.

    - **Enheter i mål samlingen använder en användar autentiserad proxy för utgående kommunikation**: som standard är det här värdet **Nej**. Ange till **Ja**om det behövs i din miljö.

    - **Välj specifika samlingar som ska synkroniseras med Desktop Analytics**: Välj **Lägg till** om du vill inkludera ytterligare samlingar från **mål samlingens** hierarki. Dessa samlingar är tillgängliga i Skriv bords analys portalen för gruppering med distributions planer. Se till att inkludera samlingar av pilot-och pilot undantags samlingar.  <!-- 4097528 -->

        > [!TIP]
        > I fönstret Välj samlingar visas endast de samlingar som är begränsade av **mål samlingen**.
        >
        > I följande exempel väljer du samla in som mål samling. När du lägger till ytterligare samlingar visas samla, CollectionB och CollectionC. Det går inte att lägga till samlingen.
        >
        > - Samla in: begränsat av samlingen **alla system**
        >     - CollectionB: begränsas av samling
        >         - CollectionC: begränsat av CollectionB
        > - Samling: begränsad av **alla system** samlingar
        >
        > Om du vill hantera samlingar som är tillgängliga i Skriv bords analys portalen för gruppering med distributions planer går du till arbets ytan **Administration** i Configuration Manager-konsolen, expanderar **Cloud Services**och väljer noden **Azure-tjänster** . Välj den post som är associerad med **Desktop Analytics** Azure-tjänsten och uppdatera inställningarna på sidan för **samling av Skriv bords analys** .

        > [!IMPORTANT]
        > De här samlingarna fortsätter att synkroniseras när deras medlemskap ändras. Mål samlingen använder till exempel en samling med en regel för Windows 7-medlemskap. När enheterna uppgraderas till Windows 10 och Configuration Manager utvärderar samlings medlemskapet, släpps de enheterna bort från samlingen och skriv bords analys.

9. Slutför guiden.

Configuration Manager skapar en inställnings princip för att konfigurera enheter i mål samlingen. Den här principen inkluderar inställningar för diagnostikdata för att göra det möjligt för enheter att skicka data till Microsoft. Som standard uppdaterar klienterna principer varje timme. När du har tagit emot de nya inställningarna kan det ta flera timmar innan data är tillgängliga i Skriv bords analys.

## <a name="monitor-connection-health"></a><a name="bkmk_monitor"></a>Övervaka anslutnings hälsa

Övervaka konfigurationen av dina enheter för Skriv bords analys. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera noden **Skriv bords analys** och välj instrument panelen för **hälso tillstånd för anslutning** .

Mer information finns i [övervaka anslutnings hälsa](monitor-connection-health.md).

Configuration Manager synkroniserar samlingarna inom 60 minuter när anslutningen upprättas. Gå till**Global pilot**i Skriv bords analys portalen och se Configuration Manager enhets samlingar.

> [!NOTE]
> Configuration Manager anslutningen till Skriv bords analys förlitar sig på tjänst anslutnings punkten. Eventuella ändringar av den här plats system rollen kan påverka synkroniseringen med moln tjänsten. Mer information finns i [om tjänst anslutnings punkten](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move).

## <a name="next-steps"></a>Nästa steg

Fortsätt till nästa artikel för att registrera enheter till Skriv bords analys.
> [!div class="nextstepaction"]
> [Registrera enheter](enroll-devices.md)
