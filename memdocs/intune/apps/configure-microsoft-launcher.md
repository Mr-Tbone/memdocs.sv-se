---
title: Konfigurera Microsoft Launcher för Android Enterprise med Intune
titleSuffix: ''
description: Använd Intune-konfigurationsprinciper med Microsoft Launcher.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/22/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ac4a9797df1ea64a5ffbceca3ea204bd9ed13a6f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075548"
---
# <a name="configure-microsoft-launcher"></a>Konfigurera Microsoft Launcher

Microsoft Launcher är en Android-app som gör att användare kan anpassa sin telefon, hålla ordning när de är på resa och gå över från att jobba via telefonen till datorn. 

På fullständigt hanterade Android Enterprise-enheter kan IT-företagsadministratörer anpassa startskärmen för hanterade enheter genom att välja bakgrundsbild, appar och ikonpositioner. Detta standardiserar utseendet för alla hanterade Android-enheter på olika OEM-enheter och systemversioner. 

## <a name="how-to-configure-the-microsoft-launcher-app"></a>Så här konfigurerar du Microsoft Launcher-appen 

När Microsoft Launcher-programmet har [lagts till i Intune](../apps/apps-add.md) går du till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och väljer **Appar** > **Appkonfigurationsprinciper**. Lägg till en konfigurationsprincip för **Hanterade enheter** som kör **Android** och välj **Microsoft Launcher** som den tillhörande appen. Klicka på **Konfigurationsinställningar** för att konfigurera de olika tillgängliga inställningarna för Microsoft Launcher. 

## <a name="choosing-a-configuration-settings-format"></a>Välja ett format för konfigurationsinställningar 

Det finns två metoder som du kan använda för att definiera konfigurationsinställningarna för Microsoft Launcher: 

- Med **Configuration Designer** kan du konfigurera inställningar med ett lättanvänt användargränssnitt som låter dig slå på och stänga av funktioner och ange värden. Det finns några inaktiverade konfigurationsnycklar med värdetyp BundleArray i den här metoden. Du kan endast konfigurera konfigurationsnycklarna genom att ange JSON-data. 

- Med **JSON-data** kan du definiera alla möjliga konfigurationsnycklar med ett JSON-skript. 

Om du lägger till egenskaper med **Configuration Designer** kan du automatiskt konvertera egenskaperna till JSON genom att välja **Ange JSON-data** på listrutan **Format för konfigurationsinställningar** enligt nedan.

   ![Format för konfigurationsinställningar – Använd Configuration Designer](./media/configure-microsoft-launcher/configure-microsoft-launcher-01.png)

   > [!NOTE]
   > När egenskaperna har konfigurerats via Configuration Designer kommer JSON-data också att uppdateras så att de endast återspeglar dessa egenskaper. Om du vill lägga till ytterligare konfigurationsnycklar i JSON-data använder du exemplet med [JSON-skript](../apps/configure-microsoft-launcher.md#microsoft-launcher-configuration-example) för att kopiera de rader som behövs för varje konfigurationsnyckel. 

Om komplexa egenskaper har konfigurerats, visas JSON-dataredigeraren i redigeringsprocessen när du redigerar tidigare skapade konfigurationsprinciper för appar. Alla tidigare konfigurerade inställningar kommer att bevaras och du kan växla till att använda konfigurationsverktyget för att ändra inställningar som stöds.

## <a name="using-configuration-designer"></a>Använda Configuration Designer

Med Configuration designer kan du välja förinställda inställningar och deras associerade värden.

   ![Format för konfigurationsinställningar – Ange JSON-data](./media/configure-microsoft-launcher/configure-microsoft-launcher-02.png)

I följande tabell visas tillgängliga konfigurationsnycklar, värdetyper, standardvärden och beskrivningar för Microsoft Launcher. Beskrivningen innehåller förväntat enhetsbeteende baserat på de valda värdena. Konfigurationsnycklar som är inaktiverade i Configuration Designer visas inte i tabellen.

|    Konfigurationsnyckel    |    Värdetyp    |    Standardvärde    |    Beskrivning     |
|---------------------------------------------------|------------------|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Typ av registrering    |    Sträng     |    Standardvärde    |    Gör att du kan ange den registreringstyp som den här principen ska gälla för. För närvarande refererar värdet **Default** (Standard) till **CorporateOwnedBuisnessOnly**. Det finns för närvarande inga andra registreringstyper som stöds.        JSON-nyckelnamn: management_mode_key        |
|    Användarändring av startskärmens appordning tillåts    |    Boolesk    |    Sant    |    Gör att du kan ange om inställningen för **appordning på startskärmen** kan ändras av slutanvändaren.<ul><li>Om den ställs in på **True** (Sant) tillämpas bara appordningen som definieras i principen för den första distributionen. Därefter kommer principen inte att tillämpas för att respektera ändringar som användaren har gjort.</li><li>Om den ställs in på **False** (Falskt) tillämpas appordningen vid varje synkronisering.</li></ul><br>**Obs:** Startskärmens appordning kan bara konfigureras via JSON-redigeraren.<br><br>JSON-nyckelnamn:<br>`com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed`    |
|    Ange storlek för rutnät    |    Sträng    |    Automatisk    |    Gör att du kan ange rutnätsstorlek för appar som ska placeras på startskärmen. Du kan ange antalet apprader och kolumner för att definiera rutnätets storlek i följande format: `columns;rows`. Om du definierar rutnätsstorleken ska det maximala antalet appar som visas på en rad på startskärmen vara antalet rader som du anger, och det maximala antalet appar som ska visas i en kolumn i startskärmen ska vara antalet kolumner som du anger.<br><br>        JSON-nyckelnamn:<br>`com.microsoft.launcher.HomeScreen.GridSize`    |
|    Ange enhetens bakgrundsbild    |    Sträng    |    Null    |    Gör att du kan ange en valfri bakgrundsbild genom att ange URL:en för den bild du vill ha som bakgrundsbild.<br><br>JSON-nyckelnamn:<br>`com.microsoft.launcher.Wallpaper.URL`    |
|    Användarändring för att ange enhetens bakgrundsbild tillåts    |    Bool    |    Sant    |    Gör att du kan ange om inställningen för att ange enhetens bakgrundsbild kan ändras av slutanvändaren.<ul><li>Om den ställs in på **True** (Sant) tillämpas bara bakgrundsbilden i principen för den första distributionen. Därefter kommer principen inte att tillämpas för att respektera ändringar som användaren har gjort.</li><li>Om den ställs in på **False** (Falskt) tillämpas bakgrundsbilden vid varje synkronisering.</li></ul><br>JSON-nyckelnamn:<br>`com.microsoft.launcher.Wallpaper.URL.UserChangeAllowed`        |
|    Aktivera feed    |    Boolesk    |    Sant    |    Gör att du kan aktivera startfeeden på enheten när användaren sveper åt höger på startskärmen.<ul><li>Om den ställs in på **True** (Sant) aktiveras feeden.</li><li>Om den ställs in på **False** (Falskt) inaktiveras feeden.</li></ul><br>JSON-nyckelnamn:<br>`com.microsoft.launcher.Feed.Enabled`    |
|    Användarändring för att aktivera feed tillåts    |    Boolesk    |    Sant    |     Gör att du kan ange om inställningen **Aktivera feed** kan ändras av slutanvändaren.<ul><li>Om den ställs in på **True** (Sant) tillämpas bara feeden för den första distributionen. Därefter kommer principen inte att tillämpas för att respektera ändringar som användaren har gjort.</li><li>Om den ställs in på **False** (Falskt) tillämpas feeden vid varje synkronisering.</li></ul><br>JSON-nyckelnamn:`com.microsoft.launcher.Feed.Enabled.UserChangeAllowed`    |
|    Placering av sökfältet   |    Sträng    |    Nedre    |  Gör att du kan ange **sökfältets placering** på startskärmen. <ul><li>Om värdet är inställt på **Nedre** finns sökfältet längst ned på startskärmen.</li><li>Om värdet är inställt på **Övre** finns sökfältet längst upp på startskärmen.</li><li>Om värdet är inställt på **Dölj** tas sökfältet bort från startskärmen.</li></ul><br>JSON-nyckelnamn:<br>`com.microsoft.launcher.Search.SearchBar.Placement`    |
|    Användarändring för sökfältets placering tillåts   |    Bool    |    Sant    |  Gör att du kan ange om inställningen för **sökfältets placering** kan ändras av slutanvändaren. <ul><li>Om den ställs in på **True** (Sant) framtvingas sökfältets placering enbart för den första distributionen. Därefter kommer principen inte att tillämpas för att respektera ändringar som användaren har gjort.</li><li>Om den ställs in på **False** (Falskt) framtvingas sökfältets placering vid varje synkronisering.</li></ul><br>JSON-nyckelnamn:<br>`com.microsoft.launcher.Search.SearchBar.Placement.UserChangeAllowed`    |
|    Dockningsläge  |    Sträng    |    Visa    | Gör att du kan aktivera dockan på enheten när användaren sveper åt höger på startskärmen.<ul><li>Om den ställs in på **Visa** aktiveras dockan.</li><li>Om den ställs in på **Dölj** döljs dockan från startskärmen, men användaren kan visa den vid behov.</li><li>Om den ställs in på **Inaktiverad** inaktiveras dockan.</li></ul><br>JSON-nyckelnamn:<br>`com.microsoft.launcher.Dock.Mode`    |
|   Användarändring för dockningsläge tillåts   |    Sträng    |    Sant    |  Gör att du kan ange om inställningen Dockningsläge kan ändras av slutanvändaren.<ul><li>Om den ställs in på **True** (Sant) framtvingas inställningen för dockningsläge bara för den första distributionen. Därefter kommer principen inte att tillämpas för att respektera ändringar som användaren har gjort.</li><li>Om den ställs in på **False** (Falskt) framtvingas inställningen för dockningsläge bara vid varje synkronisering.</li></ul><br>JSON-nyckelnamn:<br>`com.microsoft.launcher.Dock.Mode.UserChangeAllowed`    |

## <a name="enter-json-data"></a>Ange JSON-data

Ange JSON-data om du vill konfigurera alla tillgängliga inställningar för Microsoft Launcher samt de inställningar som är inaktiverade i **Configuration Designer**, enligt nedan.

   ![Configuration Designer – JSON-data](./media/configure-microsoft-launcher/configure-microsoft-launcher-03.png)

Förutom listan över konfigurerbara inställningar som anges i Configuration Designer-tabellen (ovan) innehåller följande tabell konfigurationsnycklar som du bara kan konfigurera via JSON-data.

|    Konfigurationsnyckel    |    Värdetyp    |    Standardvärde    |    Beskrivning     |
|----------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Ange tillåtna program<br>JSON-nyckel:`com.microsoft.launcher.HomeScreen.Applications`    |    BundleArray    | Se: [Ange tillåtna program](configure-microsoft-launcher.md#set-allow-listed-applications)</sup>    |    Gör att du kan definiera en uppsättning appar som ska visas på startskärmen bland apparna som är installerade på enheten. Du kan definiera appar genom att ange paketnamnet för de appar som du vill göra synliga. Till exempel skulle `com.android.settings` göra inställningar tillgängliga på startskärmen. Apparna som du godkänner i det här avsnittet bör vara installerade på enheten för att kunna visas på startskärmen.<p>Egenskaper:<ul><li>**Paket:** Namn på programpaketet</li><li>**Klass:** Programaktiviteten, som är specifik för en viss appsida. Den skulle använda standardappsidan om det här värdet är tomt.</li></ul>      |
|    Appordning på startskärmen<br>JSON-nyckel: `com.microsoft.launcher.HomeScreen.AppOrder`    |    BundleArray    |    Se: [Appordning på startskärmen](configure-microsoft-launcher.md#home-screen-app-order)      |    Gör att du kan ange appordningen på startskärmen.<p>Egenskaper:<br><ul><li>**Typ:** Om du vill ange platser för appar är den enda typ som stöds `application`. Om du vill ange platser för webblänkar är typen `weblink`.</li><li>**Position:** Anger programikonens placering på startskärmen. Det här börjar från position 1 högst upp till vänster och går från vänster till höger, uppifrån och ned.</li><li>**Paket:** Det här är programpaketets namn, som används för att ange apparnas ordning.</li><li>**Klass:** Det här är programaktiviteten, som är specifik för en viss appsida. Standardappsidan används om det här värdet är tomt. Den här egenskapen används för appen.</li><li>**Etikett:** Det här är programaktiviteten, som är specifik för en viss appsida. Standardappsidan används om det här värdet är tomt. Den här egenskapen används för appen.</li><li>**Länk:** URL:en som ska startas efter att slutanvändaren har klickat på webblänkikonen. Den här egenskapen används för webblänken.</li></ul>    |
|    Ställa in fästa webblänkar<br>JSON-nyckel: `com.microsoft.launcher.HomeScreen.WebLinks`    |    BundleArray    |    Se: [Ställa in fästa webblänkar](configure-microsoft-launcher.md#set-pinned-web-link)      |    Med den här nyckeln kan du fästa webbplatser på startskärmen som snabbstartsikoner. På så sätt kan du se till att slutanvändare får snabb och enkel åtkomst till viktiga webbplatser. Du kan ändra platsen för varje webblänkikon med inställningen ”Home Screen App Order” (appordning på startskärmen).<p>Egenskaper:<br><ul><li>**•  Etikett:** Webblänkrubriken som visas på startskärmen i MS Launcher.</li><li>**Länk:** URL:en som ska startas efter att slutanvändaren har klickat på webblänkikonen.</li></ul>    |


### <a name="set-allow-listed-applications"></a>Ange tillåtna program

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.Applications",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### <a name="home-screen-app-order"></a>Appordning på startskärmen

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "type",
                    "valueString": "application"
                },
                {
                    "key": "position",
                    "valueInteger": 0
                },
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### <a name="set-pinned-web-link"></a>Ställa in fästa webblänkar

```JSON
{ 
    "key": "com.microsoft.launcher.HomeScreen.WebLinks",  
    "valueBundleArray": [ 
        { 
            "managedProperty": [ 
                { 
                    "key": "label",
                    "valueString": "" 
                },  
                { 
                    "key": "link", 
                    "valueString": "" 
                } 
            ] 
        }
    ] 
},
{ 
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",  
    "valueBundleArray": [ 
        { 
            "managedProperty": [ 
                { 
                    "key": "type",  
                    "valueString": "" 
                },  
                { 
                    "key": "position",  
                    "valueInteger": 
                },  
                { 
                    "key": "label",  
                    "valueString": "" 
                },  
                { 
                    "key": "link",  
                    "valueString": "" 
                } 
            ] 
        }
    ] 
}
```



### <a name="microsoft-launcher-configuration-example"></a>Konfigurationsexempel för Microsoft Launcher

Här följer ett exempel på ett JSON-skript med alla tillgängliga konfigurationsnycklar:

```JSON
{
    "kind": "androidenterprise#managedConfiguration", 
    "productId": "app:com.microsoft.launcher", 
    "managedProperty": [
        {
            "key": "management_mode_key", 
            "valueString": "Default"
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable", 
            "valueBool": true
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url", 
            "valueBool": "http://www.contoso.com/wallpaper.png"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.GridSize", 
            "valueString": "5;5"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.Applications", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }
            ]
        }, 
        { 
            "key": "com.microsoft.launcher.HomeScreen.WebLinks",  
            "valueBundleArray": [ 
                { 
                    "managedProperty": [ 
                        { 
                            "key": "label",
                            "valueString": "News" 
                        },  
                        { 
                            "key": "link", 
                            "valueString": "https://www.bbc.com" 
                        } 
                    ] 
                }
            ] 
        },
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 17
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 18
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 19
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "weblink"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 20
                        }, 
                        {
                            "key": "label", 
                            "valueString": "News"
                        }, 
                        {
                            "key": "link", 
                            "valueString": "https://www.bbc.com"
                        }
                    ]
                }
            ]
        }
    ]
}

```

## <a name="next-steps"></a>Nästa steg

- Mer information om fullständigt hanterade Android Enterprise-enheter finns i [Konfigurera Intune-registrering av fullständigt hanterade Android Enterprise-enheter](../enrollment/android-fully-managed-enroll.md).
