---
title: Anpassa självbetjäningsportalen
titleSuffix: Configuration Manager
description: Lägg till anpassad organisationsinformation till självbetjänings portalen för BitLocker-hantering
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 6bc26e36-9914-4606-ae8d-f7b23218942f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 220ebb558a0e01f701cab621381ad951a8fd0738
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88123909"
---
# <a name="customize-the-self-service-portal"></a>Anpassa självbetjäningsportalen

*Gäller för: Configuration Manager (aktuell gren)*

<!--3601034-->

När du har [installerat själv service portal för BitLocker](setup-websites.md)kan du anpassa den för din organisation. Lägg till ett anpassat meddelande, ditt organisations namn och annan leverantörsspecifik information.

## <a name="branding"></a>Anpassning

Anpassa självbetjänings portalen med organisationens namn, supportavdelningen och meddelande texten.

1. Logga in som administratör på webb servern som är värd för självbetjänings portalen.

1. Starta **Internet Information Services (IIS)-hanteraren** (kör **inetmgr.exe**).

1. Expandera **platser**, expandera **standard webbplats**och välj noden **självbetjänings** . I informations fönstret, **ASP.net** -grupp, öppnar du **program inställningar**.

    [![Exempel skärm bild av självbetjänings program inställningar i IIS-hanteraren](media/bitlocker-self-service-iis-app-settings.png)](media/bitlocker-self-service-iis-app-settings.png#lightbox)

1. Välj det objekt som du vill ändra och i fönstret **åtgärder** väljer du **Redigera**. Ändra **värdet** till det nya namn som du vill använda.

    > [!CAUTION]
    > Ändra inte **namn** värden. Ändra till exempel inte `CompanyName` , ändra `Contoso IT` . Om du ändrar **namn** värden slutar självbetjänings portalen att fungera.

Ändringarna börjar gälla omedelbart.

### <a name="supported-branding-values"></a>Anpassnings värden som stöds

De värden som du kan ange finns i följande tabell:

|Name|Beskrivning|Standardvärde &nbsp;|
|--- |--- |--- |
|CompanyName|Organisations namnet som självbetjänings portalen visar som rubrik överst på varje sida.|`Contoso IT`|
|DisplayNotice|Visa ett inledande meddelande om att användaren måste bekräfta.|`true`|
|HelpdeskText|Strängen i den högra rutan under "för alla andra relaterade problem"|`Contact Helpdesk or IT Department`|
|HelpdeskUrl|Länken för HelpdeskText-strängen.|saknas|
|NoticeTextPath|Texten för det inledande meddelande som användaren måste bekräfta. Som standard är den fullständiga sökvägen på webb servern `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt` . Redigera och spara filen i en oformaterad text redigerare. Värdet för den här sökvägen är i förhållande till självbetjänings-programmet.|`Notice.txt`|

<!-- Not sure if we support changing these values. At a minimum need a description.
|ClientValidationEnabled||`true`|
|UnobtrusiveJavaScriptEnabled||`true`|
-->

En skärm bild av självbetjänings portalen som är standard finns i [själv service portal för BitLocker](self-service-portal.md).

> [!TIP]
> Om det behövs kan du lokalisera vissa av strängarna så att de visas på olika språk. Mer information finns i [lokalisering](#bkmk_localize).

## <a name="session-time-out"></a>Tids gräns för session

Om du vill att användarens session ska upphöra att gälla efter en angiven period av inaktivitet, kan du ändra timeout-inställningen för sessionen för självbetjänings portalen.

1. Logga in som administratör på webb servern som är värd för självbetjänings portalen.

1. Starta **Internet Information Services (IIS)-hanteraren** (kör **inetmgr.exe**).

1. Expandera **platser**, expandera **standard webbplats**och välj noden **självbetjänings** . I informations fönstret, **ASP.net** -grupp, öppnar du **sessionstillstånd**.

1. I gruppen **cookie-inställningar** ändrar du värdet för **timeout (i minuter)** . Det är det antal minuter som användarens session upphör att gälla. Standardvärdet är `5`. Om du vill inaktivera inställningen, så att det inte finns någon tids gräns, ställer du in värdet på `0` .

1. I fönstret **åtgärder** väljer du **tillämpa**.

## <a name="localize-helpdesk-text-and-url"></a><a name="bkmk_localize"></a>Lokalisera supportavdelningen-text och webb adress

Du kan konfigurera lokaliserade versioner av självbetjänings portalens `HelpdeskText` instruktion och `HelpdeskUrl` länk. Den här strängen informerar användarna om hur de får ytterligare hjälp när de använder portalen. Om du konfigurerar lokaliserad text visar portalen den lokaliserade versionen för webbläsare på det språket. Om ingen lokaliserad version hittas visas standardvärdet i `HelpdeskText` `HelpdeskUrl` inställningarna och.

1. Logga in som administratör på webb servern som är värd för självbetjänings portalen.

1. Starta **Internet Information Services (IIS)-hanteraren** (kör **inetmgr.exe**).

1. Expandera **platser**, expandera **standard webbplats**och välj noden **självbetjänings** . I informations fönstret, **ASP.net** -grupp, öppnar du **program inställningar**.

1. I fönstret **åtgärder** väljer du **Lägg till**.

1. I fönstret **Lägg till program inställning** konfigurerar du följande värden:

    - **Namn**: ange `HelpdeskText_<language>` , där `<language>` är språk koden för texten.

      Om du till exempel vill skapa en lokaliserad `HelpdeskText` instruktion i spanska (Spanien) är namnet `HelpdeskText_es-es` .

    - **Värde**: den lokaliserade strängen som ska visas i den högra rutan i självbetjänings portalen nedan för alla andra relaterade problem.

1. Välj **OK** för att spara den nya inställningen.

1. Upprepa processen för att lägga till en ny program inställning för `HelpdeskUrl_<language>` som matchar den associerade `HelpdeskText_<language>` inställningen.

Upprepa processen för att lägga till ett par inställningar för alla språk som du har stöd för i din organisation.

## <a name="localize-the-notice-file"></a>Lokalisera meddelande filen

Du kan konfigurera lokaliserade versioner av det första meddelandet som användaren måste bekräfta i självbetjänings portalen. Som standard är den fullständiga sökvägen på webb servern `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt` .

Skapa en lokaliserad notice.txt-fil om du vill visa lokaliserad meddelande text. Spara det sedan i en specifik språkmapp. Till exempel: `Self Service Website\es-es\Notice.txt` för spanska (Spanien).

Självbetjänings portalen visar meddelande texten baserat på följande regler:

- Om standard meddelande filen saknas visar portalen ett meddelande om att standard filen saknas.

- Om du skapar en lokaliserad meddelande fil i lämplig språkmapp visas den lokaliserade meddelande texten.

- Om webb servern inte hittar en lokaliserad version av meddelande filen visas standard meddelandet.

- Om användaren anger sin webbläsare till ett språk som inte har ett lokalt meddelande visas standard meddelandet i portalen.

### <a name="create-a-localized-notice-file"></a>Skapa en lokaliserad meddelande fil

1. Logga in som administratör på webb servern som är värd för självbetjänings portalen.

1. Skapa en `<language>` mapp för varje språk som stöds i `Self Service Website` program Sök vägen. Till exempel `es-es` för spanska (Spanien). Den fullständiga sökvägen är som standard `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es` .

    En lista över giltiga språk koder som du kan använda finns i [API-referens för National language support (NLS)](https://docs.microsoft.com/windows/win32/intl/locale-identifiers#predefined-locale-identifiers).

    > [!TIP]
    > Namnet på språkmappen kan också vara det språk oberoende namnet. Till exempel **es** för spanska, i stället för **es-es** för spanska (Spanien) och **es-p.a.** för spanska (Argentina). Om användaren anger sina webbläsare till **es**och den språkmappen inte finns, kontrollerar webb servern rekursivt den överordnade mappen (**es**). (De överordnade språken definieras i .NET.) Till exempel `Self Service Website\es\Notice.txt` . Den här rekursiva återställningen imiterar reglerna för .NET-resurs inläsning.

1. Skapa en kopia av din standard meddelande fil med den lokaliserade texten. Spara den i mappen för språk koden. Till exempel för spanska (Spanien) är den fullständiga sökvägen som standard `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es\Notice.txt` .

Upprepa den här processen till en lokaliserad meddelande fil för alla språk som du har stöd för i din organisation.

## <a name="next-steps"></a>Nästa steg

Nu när du har installerat och anpassat självbetjänings portalen kan du prova! Mer information finns i [självbetjänings portalen för BitLocker](self-service-portal.md).
