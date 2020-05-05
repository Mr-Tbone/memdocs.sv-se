---
title: Välj identifieringsmetoder
titleSuffix: Configuration Manager
description: Läs överväganden för vilka metoder som ska användas och på vilka webbplatser som ska köras.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f08ab44a11b48b4446a372c4f6065ea0d7c63e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718352"
---
# <a name="select-discovery-methods-to-use-for-configuration-manager"></a>Välj identifierings metoder som ska användas för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

För att kunna använda identifieringen för Configuration Manager, måste du överväga vilka metoder som ska användas och på vilka webbplatser som ska köras.  

 Eftersom identifieringen kan generera stora mängder nätverks trafik och de resulterande identifierings data posterna (DDR) kan använda betydande processor resurser under bearbetningen använder du bara de identifierings metoder som du behöver för att uppfylla dina mål. Du kan börja med att använda bara en eller två identifierings metoder och sedan senare aktivera ytterligare metoder på ett kontrollerat sätt för att utöka identifierings nivån i din miljö. Informationen i det här avsnittet kan hjälpa dig att fatta välgrundade beslut.  

 Information om de olika identifierings metoderna finns i [om identifierings metoder för Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  

## <a name="select-methods-to-discover-different-things"></a>Välj metoder för att identifiera olika saker  
 Du måste aktivera lämpliga identifierings metoder för att kunna identifiera potentiella Configuration Manager klient datorer eller användar resurser. Du kan använda olika kombinationer av identifierings metoder för att hitta olika resurser och för att upptäcka ytterligare information om resurserna. De identifierings metoder som du använder avgör vilken typ av resurser som identifieras och vilka Configuration Manager tjänster och agenter som används i identifierings processen. De bestämmer också vilken typ av information om resurser som du kan identifiera.  

### <a name="discover-computers"></a>Identifiera datorer   
När du vill identifiera datorer kan du använda **Active Directory system identifiering** eller **nätverks identifiering**.  

 Om du till exempel vill identifiera resurser som kan installera Configuration Manager klienten innan du använder push-installation av klienter kan du köra Active Directory system identifiering. Med den här metoden kan du inte bara identifiera resursen, utan även identifiera grundläggande information till och med utökad information om den från Active Directory Domain Services. Den här informationen kan vara användbar när du skapar komplexa frågor och samlingar som ska användas för tilldelning av klient inställningar eller innehålls distribution.

Du kan också köra nätverks identifiering och använda dess alternativ för att identifiera operativ systemet för resurser (krävs för senare användning av push-installation av klienter). Nätverks identifiering ger dig information om nätverk sto pol Ogin som du inte kan förvärva med andra identifierings metoder. Den här metoden ger dock ingen information om din Active Directorys miljö.

 Det finns också en metod som kallas **pulsslags identifiering**. Det går bara att använda pulsslags identifiering för att tvinga fram identifiering av klienter som du har installerat med andra metoder än push-installation av klienter. Men till skillnad från andra identifierings metoder kan pulsslags identifiering inte identifiera datorer som inte har någon aktiv Configuration Manager-klient. Den returnerar en begränsad uppsättning information som är avsedd att underhålla en befintlig databas post i stället för att utgöra grunden för posten. Information som skickas av pulsslags identifiering kanske inte räcker för att bygga komplexa frågor eller samlingar.  

 Om du använder **Active Directory grupp identifiering** för att identifiera medlemskap i en angiven grupp kan du identifiera begränsad system-eller dator information. Detta ersätter inte en fullständig identifiering av datorer, men kan ge grundläggande information. Den här informationen är inte tillräcklig för push-installation av klienter.  

### <a name="discover-users"></a>Identifiera användare   
När du vill identifiera information om användare kan du använda **Active Directory användar identifiering**. På samma sätt som Active Directory system identifiering identifierar den här metoden användare från Active Directory. Den innehåller grundläggande information förutom utökad Active Directory information. Du kan använda den här informationen för att bygga komplexa frågor och samlingar som liknar dem för datorer.  

### <a name="discover-group-information"></a>Identifiera grupp information   
Använd **Active Directory grupp identifiering**när du vill identifiera information om grupper och grupp medlemskap. Den här identifierings metoden skapar resurs poster för säkerhets grupper.  

 Du kan använda den här metoden för att söka i en speciell Active Directory grupp för att identifiera medlemmarna i gruppen, förutom eventuella kapslade grupper i gruppen. Du kan också använda den här metoden för att söka i en Active Directory plats för grupper och rekursivt söka igenom varje underordnad behållare på den platsen i Active Directory Domain Services.  

 Den här identifierings metoden kan även söka igenom medlemskapet i distributions grupper. Detta kan identifiera grupp relationer för både användare och datorer.  

 När du identifierar en grupp kan du också identifiera begränsad information om dess medlemmar. Detta ersätter inte Active Directory system-eller användar identifierings metoder, men. Det är vanligt vis inte tillräckligt att bygga komplexa frågor och samlingar, eller fungera som grunden för en push-installation av klienter.  

### <a name="discover-infrastructure"></a>Identifiera infrastruktur   
Det finns två metoder som du kan använda för att identifiera nätverks infrastruktur, **Active Directory identifiering av skogar** och **nätverks identifiering**.  

 Använd Active Directory skogs identifiering om du vill söka i en Active Directory-skog efter information om undernät och Active Directory-webbplatskonfigurationer. De här konfigurationerna kan sedan anges automatiskt i Configuration Manager som plats för gränser.  

 Använd Nätverks identifiering när du vill identifiera nätverk sto pol Ogin. Andra identifierings metoder returnerar information som rör Active Directory Domain Services, och kan identifiera den aktuella nätverks platsen för en klient, men de tillhandahåller inte infrastruktur information baserat på undernät och nätverkstopologi i nätverket.  

##  <a name="discovery-data-is-shared-among-sites"></a><a name="bkmk_shared"></a>Identifierings data delas mellan platser  
 När Configuration Manager lägger till identifierings data i en databas, delas det snabbt mellan alla platser i hierarkin. Eftersom det vanligt vis inte finns någon förmån att identifiera samma information på flera platser i hierarkin, bör du överväga att konfigurera en enda instans av varje identifierings metod som du använder för att köra på en enda plats. Det är en bra idé att göra detta i stället för att köra flera instanser av en enda metod på olika platser.  

 Men för vissa miljöer kan det vara praktiskt att tilldela samma identifierings metod som ska köras på flera platser, var och en med separat konfiguration och schema. Om du till exempel använder nätverks identifiering kan du behöva dirigera varje plats för att identifiera det lokala nätverket, i stället för att försöka identifiera alla nätverks platser i ett WAN.

Om du konfigurerar flera instanser av samma identifierings metoder som ska köras på olika platser bör du planera konfigurationen av varje plats noggrant. Du vill undvika att två eller flera platser identifierar samma resurser från nätverket eller Active Directory. Detta kan använda ytterligare nätverks bandbredd och skapa dubbla identifierings data poster.

Följande tabell visar på vilka platser du kan ställa in olika identifierings metoder.  

|Identifierings metod|Platser som stöds|  
|----------------------|-------------------------|  
|Identifiering av Active Directory-skogar|Central administrationsplats<br /><br /> Primär plats|  
|Identifiering av Active Directory-grupper|Primär plats|  
|Identifiering av Active Directory-system|Primär plats|  
|Identifiering av Active Directory-användare|Primär plats|  
|Pulsslags identifiering<sup>1</sup>|Primär plats|  
|Nätverksidentifiering|Primär plats<br /><br /> Sekundär plats|  

 <sup>1</sup> sekundära platser kan inte konfigurera pulsslags identifiering, men kan ta emot pulsslags-DDR från en klient.  

 När sekundära platser kör nätverks identifiering eller tar emot DDR för pulsslags identifiering, överför de DDR med filbaserad replikering till sin överordnade primära plats. Detta beror på att endast primära platser och centrala administrations platser kan bearbeta identifierings data poster. Mer information om hur identifierings data poster behandlas finns i [om identifierings data poster](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs).  

## <a name="considerations-for-different-discovery-methods"></a>Överväganden för olika identifierings metoder  
 Eftersom varje plats Server och nätverks miljö är olika är det en bra idé att begränsa de inledande konfigurationerna för identifiering. Övervaka sedan noga varje plats Server för att kunna bearbeta de identifierings data som genereras.  

När du använder en **Active Directory** identifierings metod för system, användare eller grupper:  

-   Kör identifiering på en plats som har en snabb nätverks anslutning till domän kontrol Lanterna.  

-   Överväg Active Directory replikeringstopologi för att se till att identifieringen har åtkomst till den senaste informationen.  

-   Överväg identifierings konfigurationens omfattning och begränsa identifieringen till endast de Active Directory platser och grupper som du måste identifiera.  

Om du använder **nätverks identifiering**:  

-   Använd en begränsad inledande konfiguration för att identifiera ditt nätverks krets mönster.  

-   När du har identifierat ditt nätverks krets mönster konfigurerar du nätverks identifiering så att den körs på vissa platser som är centrala för de nätverks områden som du vill ska vara mer fullständigt identifierade.  

Eftersom **pulsslags identifiering** inte körs på en speciell plats behöver du inte tänka på det i den allmänna planeringen för var identifieringen ska köras.  

##  <a name="best-practices-for-discovery"></a><a name="bkmk_best"></a>Metod tips för identifiering  
För bästa resultat med identifiering rekommenderar vi följande:

- **Kör Active Directory system identifiering och Active Directory identifiering av användare innan du kör Active Directory grupp identifiering.**  

  När Active Directory grupp identifiering identifierar en tidigare identifierad användare eller dator som medlem i en grupp, försöker den identifiera grundläggande information om användaren eller datorn. Eftersom Active Directory grupp identifiering inte är optimerad för den här typen av identifiering, kan den här processen göra att den körs långsamt. Dessutom identifierar Active Directory Group Discovery bara grundläggande information om de användare och datorer som identifieras, och skapar ingen fullständig användar-eller dator identifierings post. När du kör Active Directory system identifiering och Active Directory användar identifiering är de ytterligare Active Directory attributen för varje objekt typ tillgängliga. Det innebär att Active Directory grupp identifieringen körs mer effektivt.  

- **När du konfigurerar Active Directory grupp identifiering ska du bara ange grupper som du använder med Configuration Manager.**  

  Om du vill kontrol lera användningen av resurser genom att Active Directory grupp identifiering, anger du bara de grupper som du använder med Configuration Manager. Detta beror på att Active Directory grupp identifiering rekursivt söker igenom varje grupp som identifieras för användare, datorer och kapslade grupper. Sökningen av varje kapslad grupp kan expandera omfånget för Active Directory grupp identifiering och minska prestandan. När du ställer in delta identifiering för Active Directory grupp identifiering övervakar identifierings metoden varje grupp efter ändringar. Detta minskar prestanda ytterligare när metoden måste söka efter onödiga grupper.  

- **Konfigurera identifierings metoder med ett längre intervall mellan fullständig identifiering och en mer frekvent delta identifiering.**  

  Eftersom delta identifieringen använder färre resurser än en fullständig identifierings cykel och kan identifiera nya eller ändrade resurser i Active Directory kan du minska frekvensen för fullständiga identifierings cykler så att de körs varje vecka (eller mindre). Delta identifiering för Active Directory system identifiering, Active Directory identifiering av användare och Active Directory grupp identifieringen identifierar nästan alla ändringar i Active Directory objekt och kan upprätthålla korrekta identifierings data för resurser.  

- **Kör Active Directory identifierings metoder på en primär plats som har en nätverks plats som är närmast din Active Directory domänkontrollant.**  

  För att förbättra prestanda för Active Directory identifiering är det en bra idé att köra identifiera på en primär plats som har en snabb nätverks anslutning till domän kontrol Lanterna. Om du kör samma Active Directory identifierings metod på flera platser ställer du in varje identifierings metod för att undvika överlappande. Till skillnad från tidigare versioner av Configuration Manager delas identifierings data mellan platser. Därför är det inte nödvändigt att identifiera samma information på flera platser. Mer information finns i [identifierings data delas mellan platser](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared).  

- **Kör Active Directory skogs identifiering endast på en plats när du planerar att automatiskt skapa gränser från identifierings data.**  

  Om du kör Active Directory skogs identifiering på mer än en plats i en hierarki, är det en bra idé att endast aktivera alternativ för att automatiskt skapa gränser på en enda plats. Detta beror på att när Active Directory identifiering av skogar körs på varje plats och skapar gränser, kan Configuration Manager inte sammanfoga dessa gränser i ett enda gräns objekt. När du konfigurerar Active Directory identifiering av skogar för att automatiskt skapa gränser på flera platser kan resultatet vara dubbla gräns objekt i Configuration Manager-konsolen.  
