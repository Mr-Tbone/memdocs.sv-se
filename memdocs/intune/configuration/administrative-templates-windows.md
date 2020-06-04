---
title: Använda mallar för Windows 10-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Använd Administrativa mallar i Microsoft Intune och Endpoint Manager för att skapa grupper med inställningar för Windows 10-enheter. Med de här inställningarna i en enhetskonfigurationsprofil kan du styra Office-program, Microsoft Edge, skydd för Internet Explorer, åtkomst till OneDrive, använda fjärrskrivbordet, aktivera automatisk uppspelning, ange energisparinställningar, använda HTTP-utskrifter, styra användarnas inloggning och ändra händelseloggens storlek.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 89635c9eb2849b4896ea3df85dd081d6e267627e
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990205"
---
# <a name="use-windows-10-templates-to-configure-group-policy-settings-in-microsoft-intune"></a>Använda Windows 10-mallar för att konfigurera grupprincipinställningar i Microsoft Intune

När du hanterar enheter i din organisation är det bra att skapa en grupp med inställningar som tillämpas på olika enhetsgrupper. Anta att du har flera enhetsgrupper. För grupp A vill du tilldela en viss uppsättning inställningar. För grupp B vill du tilldela en annan uppsättning inställningar. Du vill även ha en enkel vy över de inställningar du kan konfigurera.

Du kan slutföra den här uppgiften med **Administrativa mallar** i Microsoft Intune. De administrativa mallarna innehåller tusentals inställningar som styr funktionerna i bland annat Microsoft Edge version 77 och senare, Internet Explorer, Microsoft Office-program, fjärrskrivbord, OneDrive, lösenord och PIN-koder. Med de här inställningarna kan gruppadministratörer hantera grupprinciper i molnet.

Den här funktionen gäller för:

- Windows 10 och senare

Windows-inställningarna liknar inställningarna för grupprinciper (GPO) i Active Directory (AD). De här inställningarna är inbyggda i Windows och är [ADMX-baserade inställningar](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies) som använder XML. Office- och Microsoft Edge-inställningarna är ADMX-inmatade och använder ADMX-inställningarna i [Offices administrativa mallfiler](https://www.microsoft.com/download/details.aspx?id=49030) samt [Microsoft Edges administrativa mallfiler](https://www.microsoftedgeinsider.com/enterprise). Och Intune-mallarna är 100 % molnbaserade. De ger ett enkelt och rakt sätt att konfigurera inställningarna på, och hittar de inställningar du vill ha.

**Administrativa mallar** är inbyggda i Intune och kräver inga anpassningar, inklusive användning av OMA-URI. Som en del av din MDM-lösning (hantering av mobilenheter) använder du dessa mallinställningar som en heltäckande funktion för hantering av dina Windows 10-enheter.

Den här artikeln listar stegen för att skapa en mall för Windows 10-enheter och visar hur du filtrerar alla tillgängliga inställningar i Intune. När du skapar mallen skapar den en enhetskonfigurationsprofil. Du kan sedan tilldela eller distribuera profilen till Windows 10-enheter i din organisation.

## <a name="before-you-begin"></a>Innan du börjar

- Några av de här inställningarna är tillgängliga från och med Windows 10 version 1709 (RS2/version 15063). Vissa inställningar ingår inte i alla Windows-versioner. Vi rekommenderar att du använder Windows 10 Enterprise version 1903 (19H1/version 18362) och senare för bästa möjliga upplevelse.

- I Windows-inställningarna använder du [CSP:er för Windows-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies). CSP:er fungerar i olika utgåvor av Windows, till exempel Home, Professional, Enterprise och så vidare. Om du vill se om en CSP fungerar i en viss version går du till [CSP:er för Windows-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies).

## <a name="create-the-template"></a>Skapa mallen

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande egenskaper:

    - **Plattform**: Välj **Windows 10 och senare**.
    - **Profil**: Välj **Administrativa mallar**.

4. Välj **Skapa**.
5. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange ett beskrivande namn på profilen. Namnge dina profiler så att du enkelt kan identifiera dem senare. Ett användbart profilnamn är till exempel **Administratörsmall: Windows 10-administratörsmall som konfigurerar XYZ-inställningar i Microsoft Edge**.
    - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.

7. I **Konfigurationsinställningar** kan du välja **Alla inställningar** för att se en alfabetisk lista med alla inställningar. Eller konfigurationsinställningar som gäller för enheter (**Datorkonfiguration**) och inställningar som gäller för användare (**Användarkonfiguration**):

    > [!div class="mx-imgBorder"]
    > ![Använd inställningar för ADMX-mallar för användare och enheter i Microsoft Intune Endpoint Manager](./media/administrative-templates-windows/administrative-templates-choose-computer-user-configuration.png)

8. När du väljer **Alla inställningar** visas alla inställningar. Bläddra nedåt för att använda pilarna före och nästa för att se fler inställningar:

    > [!div class="mx-imgBorder"]
    > ![Se en lista exempellista över inställningar och använd föregående- och nästa-knapparna](./media/administrative-templates-windows/administrative-templates-sample-settings-list.png)

9. Välj en inställning. Filtrera exempelvis på **Office** och välj **Aktivera begränsad bläddring**. En detaljerad beskrivning av inställningen visas. Välj **Aktiverad**, **Inaktiverad** eller lämna inställningen som **Inte konfigurerad** (standard). Den detaljerade beskrivningen förklarar även vad som händer när du väljer **Aktiverad**, **Inaktiverad** eller **Inte konfigurerad**.

    > [!TIP]
    > Windows-inställningarna i Intune motsvarar den lokala grupprincipen sökväg som du ser i redigeraren för grupprincipobjekt (`gpedit`)

10. När du väljer **Datorkonfiguration** eller **Användarkonfiguration** visas inställningskategorierna. Du kan välja valfri kategori för att se de tillgängliga inställningarna.

    Välj till exempel **datorkonfiguration** > **Windows-komponenter** > **Internet Explorer** för att se alla enhetsinställningar som gäller för Internet Explorer:

    > [!div class="mx-imgBorder"]
    > ![Se alla enhetsinställningar som gäller för Internet Explorer i Microsoft Intune Endpoint Manager](./media/administrative-templates-windows/administrative-templates-all-internet-explorer-settings-device.png)

11. Klicka på **OK** för att spara ändringarna.

    Fortsätt gå igenom listan med inställningar och konfigurera de inställningar du vill använda i din miljö. Här följer några exempel:

    - Använd inställningen **Meddelandeinställningar för VBA-makro** till att hantera VBA-makron i andra Microsoft Office-program, till exempel Word and Excel.
    - Använd inställningen **Tillåt hämtning av filer** för att tillåta eller förhindra nedladdningar från Internet Explorer.
    - Använd **Kräv lösenord när en dator aktiveras (ansluts)** för att be användarna om ett lösenord när enheter aktiveras från viloläge.
    - Använd inställningen **Hämta osignerade ActiveX-kontroller** för att blockera användare från osignerade ActiveX-kontroller från Internet Explorer.
    - Använd inställningen **Inaktivera Systemåterställning** för att tillåta eller förhindra användare att köra en systemåterställning på enheten.
    - Använd inställningen **Tillåt import av favoriter** för att tillåta eller blockera användare från att importera favoriter från en annan webbläsare till Microsoft Edge.
    - Och mycket annat...

12. Välj **Nästa**.
13. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](..//fundamentals/scope-tags.md).

    Välj **Nästa**.

14. Under **Tilldelningar** väljer du de användare eller grupper som ska ta emot din profil. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](device-profile-assign.md).

    Om profilen är tilldelad till användargrupper gäller de konfigurerade ADMX-inställningarna för alla enheter som användaren registrerar och loggar in på. Om profilen är tilldelad till enhetsgrupper gäller de konfigurerade ADMX-inställningarna för alla användare som loggar in på den enheten. Den här tilldelningen sker om ADMX-inställningen är en datorkonfiguration (`HKEY_LOCAL_MACHINE`) eller en användarkonfiguration (`HKEY_CURRENT_USER`). Med vissa inställningar kan en datorinställning som tilldelas till en användare även påverka upplevelsen för andra användare på enheten.

    Mer information finns i [Användargrupper jämfört med enhetsgrupper](device-profile-assign.md#user-groups-vs-device-groups).

    Välj **Nästa**.

15. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

Nästa gången enheten söker efter konfigurationsuppdateringar tillämpas de inställningar som du har konfigurerat.

## <a name="find-some-settings"></a>Hitta några inställningar

Det finns tusentals inställningar tillgängliga i de här mallarna. För att göra det enklare att hitta specifika inställningar använder du de inbyggda funktionerna:

- I mallen markerar du kolumnerna **Inställningar**, **Tillstånd**, **Inställningstyp** eller **Sökväg** för att sortera listan. Du kan till exempel välja kolumnen **Sökväg** och klicka på pilen Nästa om du vill se alla inställningar för sökvägen `Microsoft Excel`.

- Använd rutan **Sök** i mallen för att hitta specifika inställningar. Du kan söka genom att ange inställning eller sökväg. Du kan till exempel välja **Alla inställningar** och söka efter `copy`. Alla inställningar med `copy` visas:

  > [!div class="mx-imgBorder"]
  > ![Sök efter kopia för att visa alla enhetsinställningar i administrativa mallar i Intune](./media/administrative-templates-windows/search-copy-settings.png) 

  I ett annat exempel söker du efter `microsoft word`. Du ser inställningarna du kan ange för Microsoft Word-programmet. Sök efter `explorer` om du vill se Internet Explorer-inställningar du kan lägga till i mallen.

- Du kan också smalna av sökningen genom att bara välja **Datorkonfiguration** eller **Användarkonfiguration**.

  Om du till exempel vill se alla tillgängliga användarinställningar för Internet Explorer väljer du **Användarkonfiguration** och söker efter `Internet Explorer`. Endast de IE-inställningar som gäller för användare visas:

  :::image type="content" source="./media/administrative-templates-windows/show-all-internet-explorer-settings-user-configuration.png" alt-text="Välj Användarkonfiguration i ADMX-mallen och sök eller filtrera efter Internet Explorer i Microsoft Intune.":::

## <a name="next-steps"></a>Nästa steg

Mallen har skapats, men den gör kanske inte något än. [Tilldela mallen (kallas även profil)](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Uppdatera [Office 365 med hjälp av administrativa mallar](administrative-templates-update-office.md).

[Självstudie: Använd molnet för att konfigurera grupprinciper på Windows 10-enheter med ADMX-mallar och Microsoft Intune](tutorial-walkthrough-administrative-templates.md)
