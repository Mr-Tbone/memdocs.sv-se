---
title: Principspion
titleSuffix: Configuration Manager
description: Använd policy Spy för att visa och felsöka princip systemet på Configuration Manager klienter.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1012ec24-27d9-4193-8236-918d283c7448
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6038a3332c63a58d1f3c423491b1aa17aa28b080
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723182"
---
# <a name="policy-spy"></a>Principspion

*Gäller för: Configuration Manager (aktuell gren)*

Policyn spion är ett av de [Configuration Manager verktygen](tools.md). Det är ett verktyg för att visa och felsöka princip systemet på Configuration Manager klienter. Öppna användar gränssnittet genom att köra **PolicySpy. exe** . Mer information om användning av kommando rader finns i [kommandoradssyntax](#bkmk_policyspy-syntax).

> [!Important]  
> Kör policy Spy som administratör. Om du inte **Kör som administratör**visas följande fel meddelande i klient informationen:  
> `There is no client installed on this machine. Connection to client policy failed with error 80041003`


## <a name="command-line-syntax"></a><a name="bkmk_policyspy-syntax"></a>Kommandoradssyntax

Princip-spion är främst avsett för användning via användar gränssnittet. Det ger begränsade kommando rads alternativ som stöder automatisering och batchbearbetning.

`PolicySpy.exe [/export <ExportFilename> [<computername>]]`

### <a name="option-export"></a>Alternativet`/export`
Det här alternativet exporterar tyst principen för den lokala eller fjärranslutna datorn. `<ExportFilename>`är fil namnet som verktyget sparar den exporterade XML-principen till. Om du anger `<computername>` alternativet exporterar policy Spy principen för den datorn i stället för den lokala datorn.

> [!Note]  
> Det här kommando rads alternativet ger inte möjlighet att ange användarautentiseringsuppgifter. Om du vill använda alternativa autentiseringsuppgifter för att få åtkomst till en fjärrdator använder du kommandot **runas** för att öppna en ny kommando tolk med de nödvändiga säkerhets uppgifterna.  


## <a name="usage"></a>Användning

### <a name="tools-menu"></a>Verktyg-menyn

Följande åtgärder är tillgängliga på **verktyg** -menyn:  

- **Öppna fjärran sluten**: ansluter till Configuration Manager klient princip på en fjärrdator. Använd dialog rutan Anslut för att hämta namnet på fjärrdatorn och valfria användarautentiseringsuppgifter. Om anslutningen Miss lyckas visas fel information i fönstret klient information. Om anslutningen Miss lyckas igen kan du försöka ansluta genom att välja **Uppdatera** på **Redigera** -menyn eller genom att trycka på F5.  

- **Öppna fil**: öppnar en princip export fil (XML) som skapats av alternativet **Exportera princip** . Verktyget visar den exporterade principen exakt på samma sätt som en live-princip. Vissa funktioner som bara gäller när du ansluter till en faktisk klient inaktive ras.  

- **Begär dator tilldelningar**: utlöser en begäran om dator princip tilldelningar på mål datorn. Den här funktionen är inaktive rad när exporterad princip visas.  

- **Utvärdera dator princip**: utlöser en utvärdering av dator principer på mål datorn. Den här funktionen är inaktive rad när du visar en exporterad princip.  

- **Begär användar tilldelningar**: utlöser en begäran om användar princip tilldelningar för den för tillfället inloggade användaren. Den här funktionen är endast tillgänglig när du visar en princip på den lokala datorn.  

- **Utvärdera användar princip**: utlöser en utvärdering av användar principer för den för tillfället inloggade användaren. Den här funktionen är endast tillgänglig när du visar en princip på den lokala datorn.  

- **Återställ princip**: tar bort alla principer som inte är standard och återställer princip-cookies för platsen. Den utlöser sedan en begäran om dator princip tilldelningar. Den här funktionen är inaktive rad när du visar en exporterad princip.  

- **Exportera princip**: exporterar mål datorns princip till en XML-fil. Visa den här filen på en dator med policy Spy. Öppna export filen genom att välja **Öppna fil** på **verktyg** -menyn. Den här funktionen är inaktive rad när du visar en exporterad princip.  


### <a name="edit-menu"></a>Redigera-menyn

Följande åtgärder är tillgängliga på **Redigera** -menyn:  

- **Ta bort**: tar bort den instans som valts i resultat fönstret. Den här åtgärden stöds bara för princip instanser. Om du försöker ta bort något annat än princip instanser visar verktyget ett fel meddelande. Den här funktionen är inaktive rad när du visar en exporterad princip.  

- **Uppdatera**: alla resultat uppdateras för att visa den senaste informationen. Alla Tree-noder som expanderas före uppdateringen expanderas automatiskt efteråt. Om policy Spy inte har anslutit till mål datorns princip försöker den ansluta igen. Den här funktionen är inaktive rad när du visar en exporterad princip.  

- **Rensa händelser**: tar bort alla objekt från fliken händelser.  



## <a name="results-pane"></a>Resultat fönster

Resultat fönstret visar olika vyer för princip systemet på mål datorn. Öppna dessa vyer genom att klicka på någon av följande fyra flikar: 
- [Faktisk](#bkmk_policyspy-actual)
- [Begärd](#bkmk_policyspy-requested)
- [Default](#bkmk_policyspy-default)
- [Händelser](#bkmk_policyspy-events)


### <a name="actual"></a><a name="bkmk_policyspy-actual"></a>Arbete

På den här fliken visas klientens aktuella princip. Den aktuella principen fastställer en klients beteende och beteendet hos dess klient agenter, till exempel program varu distribution och inventering. Fliken visar resultatet i ett träd format med en rotnod för dator namn området och varje användardefinierat namn område. Expandera en namnområdesnod om du vill visa en lista över klasser. Expandera en klass för att visa en lista över dess instanser. Klass listan innehåller bara klasser som har instanser.


### <a name="requested"></a><a name="bkmk_policyspy-requested"></a>Kräv

Den här fliken visar de princip tilldelningar som klienten hämtade från den tilldelade platsen. Fliken visar resultat i träd format med en rotnod för dator namn området och varje användardefinierat namn område. Om du expanderar en namnområdesnod visas följande noder:  

- **Konfiguration**: visar en lista med konfigurations klasser härledda från CCM_Policy_Config, som innehåller princip objekt, tilldelningar och andra.  

- **Inställningar**: visar alla aktiva inställningar som skapats av principer. Inställningarna visas under noden konfiguration. 

> [!Note]   
> Det kan finnas flera instanser med samma namn eftersom klienten inte har slagit samman dessa inställningar i en slutgiltig resultat uppsättning. Policy Spy visar instanser under den här noden genom att använda RealKey-egenskaperna i stället för de faktiska princip nycklarna. Korrelera dessa instanser till den resultat uppsättning som visas på fliken faktisk.  


### <a name="default"></a><a name="bkmk_policyspy-default"></a>Objekt

Den här fliken visar samma information som den **begärda** fliken. Den innehåller också innehåll i namn områdena DefaultMachine och DefaultUser.


### <a name="events"></a><a name="bkmk_policyspy-events"></a>Planering

Den här fliken visar händelser för princip agenten när de sker. Vyn skapar en prenumeration på WMI-händelser för alla händelser som härletts från CCM_PolicyAgent_Event. Vyn visar högst 200 händelser. Den tar bort de äldsta händelserna överst i listan, om det behövs. Om du väljer det sista objektet i listan, rullas listan automatiskt nedåt när nya händelser läggs till. Annars behåller vyn sin nuvarande position och du måste rulla nedåt eller trycka på End-tangenten för att visa nya händelser. Den här vyn är alltid tom när du visar en exporterad princip.



## <a name="client-info-pane"></a>Fönstret klient information
I fönstret klient information visas en lista över egenskaper för mål datorn. Den visar följande egenskaper, om tillgängligt:  
- Name
- ID
- Version
- Plats
- Tilldelad MP
- Resident MP
- Proxy MP
- Proxy-tillstånd



## <a name="details-pane"></a>Informations fönster
I informations fönstret visas detaljerad information om det aktuella valet. Om ingen markering är aktiv visas information om principens spion, inklusive versionen. Annars visas en MOF-representation (Manage Object Format) för det valda objektet.

Policyn spion använder sin egen rutin för MOF-generering för att skapa en mer användarvänlig HTML-visning än den oformaterad text MOF som genereras av WMI. Med det här beteendet kan policy-spion lägga till följande funktioner för att göra MOF-filen mer lättläst:  

- Markering av syntax  

- Indragna objekt och matriser  

- Egenskaperna är ordnade i system, ärvda och lokala grupper. Som standard komprimeras systemet och ärvda grupper. Du kan direkt se vilka egenskaper som instansen faktiskt använder.  

- Kopiera MOF eller kopiera oformaterad text MOF till Urklipp. Den här funktionen är användbar för att klistra in MOF i andra program genom att direkt anropa verktyget MofComp.  

För instanser av princip objekt härledda från CCM_Policy_Policy, visar informations fönstret princip texten under MOF som visas. Om klienten inte har laddat ned princip texten visar policyn spion en hyperlänk. Klicka på länken för att ladda ned princip innehållet direkt från klientens hanterings plats. Om verktyget hämtar princip innehållet ersätts hyperlänken med svarets innehåll. Annars uppdaterar princip spion skärmen som indikerar att begäran misslyckades.

