---
title: Fjärråtgärder med samhantering
titleSuffix: Configuration Manager
description: Köra fjärråtgärder från Intune för samhanterade enheter
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ca37a4e15f5da63ed743b541eeabc43708b0be1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075327"
---
# <a name="remote-actions-with-co-management"></a>Fjärråtgärder med samhantering

Du måste se till att alla enheter som du hanterar är nåbara, oavsett var de är, oavsett var de ansluter. Du måste också förse varje användare med allt de behöver för att vara produktiv, samtidigt som du skyddar appar och data. Med de enhets åtgärder som stöds av Intune kan du fjärrmatcha dessa kritiska funktioner.

I följande video, huvudsakliga program hanteraren Heidi Cheng och erfarna program hanteraren Danny Guillory diskutera och demo fjärråtgärder med samhantering:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>Fördelar

Med åtgärder för fjärran sluten enhet får du hanterings kontroller på enheten utan att störa personliga data. Med dessa åtgärder för fjär renhet kan du: 
- Ta bort företags data på borttappade eller stulna enheter  
- Byta namn på en enhet  
- Starta om en enhet  
- Granska enhets inventering  
- Fjärr styrning av en enhet  
- Rensa förinstallerade OEM-appar med en ny start omstart  
- Gör en fabriks återställning på en Windows 10-enhet  

Dessa funktioner är ett viktigt och enkelt sätt att skydda företags data som lagras på dessa enheter, oavsett om de finns i e-post eller OneDrive.

Mer information om de här åtgärderna finns i [tillgängliga fjärråtgärder](#available-remote-actions). 



## <a name="case-studies"></a>Fallstudier

Det globala konsult företaget Avanade använder regelbundet fjärråtgärder för att hantera de enheter som används av deras 30 000-anställda. I ett [nytt blogg inlägg](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/)nämndes CIO of Avanade:

> *Vår omedelbara vinst från att ha Intune-funktionerna var möjligheten att fjärråterställa Windows på en dator. Detta är viktigt för oss för borttappade eller stulna datorer, vilket är vanligare i vår mycket mobila personal.* 
>  *Detta är funktioner som vi annars skulle ha haft att bygga och underhålla i ett anpassat ConfigMgr-paket.*

Mer information om hur du använder dessa fjärråtgärder finns i [tillgängliga enhets åtgärder](../../intune/remote-actions/device-management.md#available-device-actions).


## <a name="value-proposition"></a>Värde förslag

När en Configuration Manager enhet är samhanterad lägger den genast till de funktioner som Configuration Manager inte har inbyggt. Nu kan du nu utföra en fjärran sluten åtgärd som stöds av Intune. 

Med samhantering är Configuration Manager enheterna precis som andra Intune-hanterade enheter. De har till exempel en fullständig förekomst i molnet och du kan nå dem så länge de har Internet åtkomst. Du kan utföra alla dessa åtgärder utan att vidta ytterligare åtgärder utöver att aktivera samhantering.

Eftersom den automatiska registreringen är transparent för användaren påverkas inte produktiviteten. Användaren behöver inte göra något.


### <a name="available-remote-actions"></a>Tillgängliga fjärråtgärder

Använd dessa fjärråtgärder från Intune när du [aktiverar samhantering](how-to-enable.md) i Configuration Manager.

#### <a name="remove-devices"></a>Ta bort enheter
- **Dra tillbaka**: den här åtgärden tar bort hanterade appar och data (där det är tillämpligt), inställningar och e-postprofiler som har tilldelats enheten. Enheten tas sedan bort från Intune-hanteringen. Den här processen sker nästa gång enheten checkar in och tar emot en ras-åtgärd. Funktionen dra kvar användarens personliga data på enheten.  

- **Rensning**: den här åtgärden återställer en enhet till fabriks inställningarna. Om du väljer att **behålla registrerings tillstånd och användar konto**behålls användar data. Annars raderas enheten på ett säkert sätt.  

- **Ta bort**: om du vill ta bort enheter från Intune på Azure Portal tar du bort dem från fönstret för den aktuella enheten. Nästa gången enheten checkar in, tas alla organisations data som lagras på den bort.  

Mer information finns i [ta bort enheter med rensning, borttagning eller manuell avregistrering av enheten](../../intune/remote-actions/devices-wipe.md).

#### <a name="selective-wipe"></a>Selektiv rensning
<!--SCCMDocs issue 973-->
När du väljer en **selektiv rensning av app**tas företags program data bort utan att person uppgifter tas bort. Använd den här åtgärden när en enhet rapporteras som förlorad eller stulen. 

Mer information finns i [så här rensar du endast företags data från Intune-hanterade appar] (.. /.. /intune/apps/apps-selective-wipe.md.

#### <a name="sync"></a>Sync
Enhetsåtgärden **Synkronisera** tvingar den valda enheten att omedelbart checka in med Intune. När en enhet checkar in tar den omedelbart emot eventuella väntande åtgärder eller principer som du har tilldelat till den.

Den här funktionen kan hjälpa dig att validera och felsöka principer som du har tilldelat utan att du behöver vänta på nästa schemalagda incheckning.

Mer information finns i [synkronisera enheter för att få de senaste principerna och åtgärderna med Intune](../../intune/remote-actions/device-sync.md).

#### <a name="restart"></a>Starta om
Åtgärden **starta om** enhet gör att enheten du väljer att starta om. Den här åtgärden är användbar när det finns en väntande omstart, men användaren inte är tillgänglig för att göra det.

Mer information finns i [starta om enheter med Intune](../../intune/remote-actions/device-restart.md).

#### <a name="fresh-start"></a>Börja om på nytt
Åtgärden **ny start** enhet tar bort alla appar som är installerade på en enhet som kör Windows 10, version 1703 eller senare. Ny start hjälper till att ta bort förinstallerade appar (OEM) som vanligt vis installeras med en ny enhet.

Om du väljer att inte behålla användar data återställs enheten i sitt tillstånd. Den avregistrerar sig från Azure AD och MDM.

Om du har fördefinierade standarder för vilka appar som ska finnas på enheten eliminerar den här åtgärden de som inte uppfyller dina kriterier.

Mer information finns i [använda ny start för att återställa Windows 10-enheter med Intune](../../intune/remote-actions/device-fresh-start.md). 

#### <a name="remote-control"></a>Fjärrstyrning
Enheter som hanteras av Intune kan fjärradministreras med hjälp av [TeamViewer](https://www.teamviewer.com/). TeamViewer är ett program från tredje part som du hämtar separat.

Mer information finns i [använda TeamViewer för att fjärradministrera Intune-enheter](../../intune/remote-actions/teamviewer-support.md).



## <a name="configure"></a>Konfigurera

Förutom fjärr styrning via TeamViewer, för att börja använda dessa fjär renhets åtgärder i Intune, krävs ingen ytterligare konfiguration när du har [aktiverat samhantering](how-to-enable.md).

Mer information om hur du använder TeamViewer för fjärr styrning finns i [använda TeamViewer för att fjärradministrera Intune-enheter](../../intune/remote-actions/teamviewer-support.md).
