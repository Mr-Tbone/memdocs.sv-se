---
title: Hantera VPP-appar från Microsoft Store för företag
titleSuffix: Microsoft Intune
description: Lär dig att synkronisera appar i Intune från Microsoft Store för företag.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2ed5d3f0-2749-45cd-b6bf-fd8c7c08bc1b
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seoapril2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: 02f90fc0cd249062f878b5a18481f6a6a73228af
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80323385"
---
# <a name="how-to-manage-volume-purchased-apps-from-the-microsoft-store-for-business-with-microsoft-intune"></a>Så här hanterar du volymköpta appar från Microsoft Store för företag med Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

I [Microsoft Store för företag](https://www.microsoft.com/business-store) kan du söka efter och köpa appar för din organisation, separat eller i volym. Genom att ansluta butiken till Microsoft Intune kan du hantera volyminköpta program från Azure-portalen. Exempel:

* Du kan synkronisera listan med appar som du har köpt (eller som är kostnadsfria) från butiken med Intune.
* Appar som är synkroniserade visas i administrationskonsolen för Intune. Du kan tilldela de här apparna på samma sätt som andra appar.
* Både online- och offline-licensierade versioner av appar synkroniseras till Intune. Appnamn kommer att läggas till med "online" eller "offline" i portalen.
* Du kan spåra hur många licenser som är tillgängliga och hur många som används i administrationskonsolen för Intune.
* Intune blockerar tilldelning och installation av appar om det inte finns tillräckligt många tillgängliga licenser.
* Appar som hanteras av Microsoft Store för företag återkallar automatiskt licenser när en användare lämnar företaget eller när administratören tar bort användaren och användarenheterna.

## <a name="before-you-start"></a>Innan du börjar

Granska följande information innan du börjar synkronisera och tilldela appar från Microsoft Store för företag:

- Konfigurera Intune som utfärdare för hantering av mobila enheter för din organisation.
- Du måste ha registrerat dig för ett konto i Microsoft Store för företag.
- När du har associerat ett konto i Microsoft Store för företag med Intune kan du inte ändra till något annat konto i framtiden.
- Appar som köpts från butiken kan inte manuellt läggas till i eller tas bort från Intune. De kan endast synkroniseras med Microsoft Store för företag.
- Både online- och offlinelicensierade appar som du har köpt från Microsoft Store för företag synkroniseras i Intune-portalen. Du kommer sedan att kunna distribuera apparna till enhetsgrupper eller användargrupper.
- Online-appinstallationer hanteras i butiken.
- Kostnadsfria offlineappar kan också synkroniseras till Intune. Dessa appar installeras av Intune och inte av butiken.
- För användning av den här funktionen måste enheterna vara anslutna till Active Directory Domain Services, Azure AD-anslutna eller arbetsplatsanslutna.
- Registrerade enheter måste använda 1511-versionen av Windows 10 eller senare.

> [!NOTE]
> Om du inaktiverar butiken på hanterade enheter (antingen manuellt eller via princip eller grupprincip) kommer onlinelicensierade appar inte att installeras.

## <a name="associate-your-microsoft-store-for-business-account-with-intune"></a>Koppla ditt konto för Microsoft Store för företag till Intune

Innan du aktiverar synkronisering i Intune-konsolen måste du konfigurera ditt Windows Store-konto för att använda Intune som ett hanteringsverktyg:

1. Se till att du loggar in i [Microsoft Store för företag](https://www.microsoft.com/business-store) med samma klientkonto som du använder för att logga in på Intune.
2. I Business Store väljer du fliken **Hantera** sedan **Inställningar**, och välj fliken **Distribuera**.
3. Om du inte specifikt har **Microsoft Intune** tillgängligt som ett verktyg för hantering av mobila enheter, väljer du **Lägg till hanteringsverktyget** för att lägga till **Microsoft Intune**. Om du inte har **Microsoft Intune** aktiverat som ditt verktyg för hantering av mobila enheter, klickar du på **Aktivera** bredvid **Microsoft Intune**. Observera att du bör aktivera **Microsoft Intune** snarare än **Microsoft Intune-registrering**.

> [!NOTE]
> Tidigare kunde du bara associera ett hanteringsverktyg för att tilldelning av appar med Microsoft Store för företag. Du kan nu koppla flera hanteringsverktyg till butiken, exempelvis Intune och Configuration Manager.

Du kan nu fortsätta och konfigurera synkronisering i Intune-konsolen.

## <a name="configure-synchronization"></a>Konfigurera synkronisering

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Administration av klientorganisation** > **Anslutningsappar och token** > **Microsoft Store för företag**.
3. Klicka på **Aktivera**.
4. Om du inte redan gjort det klickar du på länken för att registrera Microsoft Store för företag och kopplar kontot på det sätt som beskrivs tidigare.
5. I listrutan **Språk** väljer du det språk som ska användas vid visning av program från Microsoft Store för företag i Azure Portal. Apparna installeras i slutanvändarens språk om det är tillgängligt oavsett vilket språk de visas i.
6. Klicka på **Synkronisera** för att hämta appar som du har köpt från Microsoft Store i Intune.

## <a name="synchronize-apps"></a>Synkronisera appar

1. Välj **Administration av klientorganisation** > **Anslutningsappar och token** > **Microsoft Store för företag**.
2. Klicka på **Synkronisera** för att hämta appar som du har köpt från Microsoft Store i Intune.

> [!NOTE]
> Appar med krypterade appaket stöds inte för närvarande och kommer inte att synkroniseras med Intune.

## <a name="assign-apps"></a>Tilldela appar

Du kan tilldela appar från Windows Store på samma sätt som du tilldelar andra Intune-appar. Mer information finns i [Tilldela appar till grupper med Microsoft Intune](apps-deploy.md).

Offlineappar kan riktas till användargrupper, enhetsgrupper eller grupper med användare och enheter.
Offlineappar kan installeras för en viss användare av en enhet eller för alla användare av en enhet.

När du tilldelar en app från Microsoft Store för företag används en licens för varje användare som installerar appen. Om du använder alla tillgängliga licenser för en tilldelad app kommer du inte att kunna tilldela fler exemplar. Välj en av följande åtgärder:

* Avinstallera appen från vissa enheter.
* Minska omfånget för den aktuella tilldelningen för att bara fokusera på de användare som du har tillräckliga licenser för.
* Köpa fler kopior av appen från Microsoft Store för företag.

## <a name="remove-apps"></a>Ta bort appar

Om du vill ta bort en app som synkroniseras från Microsoft Store för företag måste du logga in i Microsoft Store för företag och gå igenom återbetalningsstegen för appen. Processen är samma oavsett om appen är kostnadsfri eller inte. För en kostnadsfri app återbetalar butiken 0 $. Exemplet nedan visar en återbetalning för en kostnadsfri app. 

![Skärmbild av information om appborttagning](./media/windows-store-for-business/microsoft-store-for-business-01.png)

> [!NOTE]
> Det räcker inte att ta bort en apps synlighet i den privata katalogen för att Intune ska sluta synkronisera appen. Du måste återbetala appen för att helt ta bort den.

## <a name="next-steps"></a>Nästa steg

* [Hantera volyminköpta appar och böcker med Microsoft Intune](vpp-apps.md)
