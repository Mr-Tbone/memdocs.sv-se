---
title: Läs mer om PowerShell-skript säkerhet
titleSuffix: Configuration Manager
description: Resurser som hjälper dig att lära dig mer om PowerShell-skript säkerhet.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6b519d60be094bb7c39f738d04322009b36a409f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075871"
---
# <a name="learn-more-about-powershell-script-security"></a>Läs mer om PowerShell-skript säkerhet

*Gäller för: Configuration Manager (aktuell gren)*

Det är administratörens ansvar att validera den föreslagna PowerShell-och PowerShell-parameter användningen i sin miljö. Här följer några användbara resurser som hjälper dig att utbilda administratörer om kraften hos PowerShell och potentiella risk ytor. Detta bidrar till att minska potentiella risk ytor och tillåta att säkra skript används.

## <a name="powershell-script-security"></a>Säkerhet för PowerShell-skript
Inbyggd i körnings skripten är en funktion för att visuellt granska och godkänna skript som har begärts att köras i miljön. Administratörer bör vara medvetna PowerShell-skript kan ha fördunklade-skript: skript som är skadlig och svår att identifiera med visuell granskning under skript godkännande processen. Vi rekommenderar att du använder vissa gransknings verktyg, i tillägg för att visuellt granska PowerShell-skript, för att identifiera misstänkta skript problem. De här verktygen kan inte alltid avgöra PowerShell-författarens avsikt så att det kan ta hänsyn till ett misstänkt skript. Verktygen kräver dock att administratören bedömer om den är skadlig eller avsiktlig syntax för skript.

## <a name="recommendations"></a>Rekommendationer
- Bekanta dig med metod tips för PowerShell-säkerhet med hjälp av de olika länkarna nedan.
- **Signera dina skript**: en annan metod för att skydda skript är att låta dem testats och sedan signeras innan de importeras för användning.
- Lagra inte hemligheter (till exempel lösen ord) i PowerShell-skript och lär dig mer om hur du hanterar hemligheter.


## <a name="general-information-about-powershell-security-best-practices"></a>Allmän information om metod tips för PowerShell-säkerhet

Den här samlingen länkar har valts för att ge Configuration Manager administratörer en utgångs punkt för att lära sig om metod tips för PowerShell-skript säkerhet.  

[Introduktion till metod tips för PowerShell-säkerhet](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ )

[Metod tips för PowerShell-säkerhet i PowerPoint](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[Skydda mot PowerShell-attacker, PowerShell-teamets blogg](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/)

[Försvara mot PowerShell-attacker Twitter, från en Microsoft PowerShell-och säkerhets rådgivare Pettersson Holmes](https://twitter.com/Lee_Holmes/status/922462821081694208)

[Skydda mot kod inmatning med skadlig kod](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/)

[PowerShell Blue-teamet, diskuterar djup skript Blocks loggning, skyddad händelse loggning, antivirus program mot skadlig kod, säkra API: er för kodgenerering](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

[För Windows 10 finns ett API för ett gränssnitt för genomsökning mot skadlig kod](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc)

## <a name="powershell-parameters-security"></a>Säkerhet för PowerShell-parametrar
Att skicka parametrar är ett sätt att ha flexibilitet i dina skript och skjuta upp beslut tills kör tid. Den öppnar också en annan risk yta. Metod tips för att förhindra skadliga parametrar eller skript inmatning är:

- Tillåt endast användning av fördefinierade parametrar.
- Använd funktionen reguljära uttryck för att validera parametrar som tillåts.
    - Exempel: om bara ett visst värde intervall är tillåtet använder du ett reguljärt uttryck för att kontrol lera om det bara är de tecken eller värden som kan vara i intervallet.
    - Validering av parametrar kan hjälpa till att förhindra att användare försöker använda vissa tecken som kan undantas, som citat tecken. Tänk på att det kan finnas flera typer av citat tecken, så att du kan använda reguljära uttryck för att validera vilka tecken som du har valt är ofta enklare än att försöka definiera alla indata som inte är tillåtna.
- Utnyttja PowerShell-modulen ["insprutning av Hunter"](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) i PowerShell-galleriet.
    - Det kan finnas falska positiva identifieringar, så leta efter avsikt när något är flaggat som misstänkt för att avgöra om det är ett problem eller inte. 
- Microsoft Visual Studio har en skript analys som kan hjälpa till med att kontrol lera PowerShell-syntax.
- Den här videon: "DEF CON 25-Pettersson Holmes-get $pwnd: angripa kampen mot Windows Server" ger en översikt över de typer av problem som du kan skydda mot (särskilt avsnitt 12:20 till 17:50):    <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## <a name="environment-recommendations"></a>Miljö rekommendationer
Allmänna rekommendationer för PowerShell-administratörer.
1. Distribuera den senaste versionen av PowerShell, till exempel version 5 eller senare, som är inbyggd i Windows 10. Alternativt kan du distribuera [Windows Management Framework](https://www.microsoft.com/download/details.aspx?id=54616). 
2. Aktivera och samla in PowerShell-loggar, om du vill, inklusive loggning av skyddade händelser. Inkludera dessa loggar i arbets flöden för signaturer, jakt och incident svar.
3. Implementera bara tillräckligt med administration på högvärdes system för att eliminera eller minska obegränsad administrativ åtkomst till dessa system.
4. Distribuera principer för Windows Defender-Programkontroll för att tillåta att förgodkända administrativa uppgifter använder den fullständiga funktionen hos PowerShell-språket, samtidigt som du begränsar interaktiv och ej godkänd användning till en begränsad del av PowerShell-språket.
5. Distribuera Windows 10 för att ge Antivirus leverantören fullständig åtkomst till allt innehåll (inklusive innehåll som genereras eller fördunklade vid körning) som bearbetas av Windows-skript värdar, inklusive PowerShell.
