---
title: Felmeddelanden
titleSuffix: Configuration Manager
description: Lär dig mer om fel meddelanden från Package Conversion Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0d3cf6e1-b295-4b05-821d-e9f57c74ca14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4d4a2fa66dc1c4a8af3b3f7f16c67d58edebb5fa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709889"
---
# <a name="technical-reference-for-package-conversion-manager-error-messages"></a>Teknisk referens för fel meddelanden i Package Conversion Manager

*Gäller för: Configuration Manager (aktuell gren)*

<!--1357861-->

I den här artikeln beskrivs de fel meddelanden som visas i Package Conversion Manager. Det innehåller också möjliga orsaker till felet och metoder för att åtgärda felet. Package Conversion Manager loggar fel meddelanden i **PCMtrace. log**. Mer information, inklusive hur du styr detalj nivån finns i [loggfiler](troubleshoot-pcm.md#log-files).


#### <a name="application-creation-failed-with-the-following-exception"></a>Det gick inte att skapa program med följande undantag

Det angivna undantaget inträffade när programobjektet skulle skickas till Configuration Manager servern.

Kontrol lera dina behörigheter i Configuration Manager, verifiera din anslutning och försök sedan igen. Om dessa åtgärder inte löser problemet granskar du filen **PCMtrace. log** (utförlig nivå 4) och **SMSProv. log**.


#### <a name="conversion-error--applies-to-a-package-transform-status"></a>Konverterings fel – gäller PAKETets OMVANDLINGs STATUS

Ett allmänt undantag inträffade under konverteringen av paketet. Leta i filen **PCMtrace. log** (utförlig nivå 4).

Kontrol lera användar behörigheterna för nätverks resursen (paket data källa), kontrol lera anslutningen och försök sedan igen. Om dessa åtgärder inte löser problemet granskar du filen **PCMtrace. log** (utförlig nivå 4).


#### <a name="did-not-find-a-converted-package-and-its-resultant-application-in-the-workflow-outputs"></a>Det gick inte att hitta något konverterat paket och det resulterande programmet i arbets flödets utdata
Programmet (konverterat paket/program) har tagits bort.

Ändra det beroende paketet/programmet så att det beroende paketet/programmet finns.


#### <a name="objects-were-not-created-successfully"></a>Det gick inte att skapa objekt
Det finns flera möjliga orsaker.

Kontrol lera dina behörigheter i Configuration Manager, verifiera din anslutning och försök sedan igen. Om dessa åtgärder inte löser problemet granskar du filen **PCMtrace. log** (utförlig nivå 4) och filen **SMSProv. log** .


#### <a name="please-close-the-wizard-and-resolve-any-issues-with-the-selected-package-see-pcmtracelog-for-more-details"></a>Stäng guiden och Lös eventuella problem med det valda paketet. Mer information finns i PCMTrace. log
Det finns flera möjliga orsaker.

Kontrol lera dina behörigheter i Configuration Manager, verifiera din anslutning och försök sedan igen. Om dessa åtgärder inte löser problemet granskar du filen **PCMtrace. log** (utförlig nivå 4) och filen **SMSProv. log** .


#### <a name="some-deployment-types-are-missing-detection-methods-all-deployment-types-must-have-detection-methods"></a>Vissa distributions typer saknar identifierings metoder. Alla distributions typer måste ha identifierings metoder
Identifierings metoder saknas i programmet.

Lägg till en eller flera identifierings metoder under **korrigerings-och konverterings** processen.


#### <a name="there-was-an-error-preparing-the-package-for-conversion"></a>Ett fel uppstod vid förberedelse av paketet för konvertering
Det finns flera möjliga orsaker.

Kontrol lera dina behörigheter i Configuration Manager, verifiera din anslutning och försök sedan igen. Om dessa åtgärder inte löser problemet granskar du filen **PCMtrace. log** (utförlig nivå 4) och filen **SMSProv. log** .


