---
title: Ändra och ersätta program
titleSuffix: Configuration Manager
description: Lär dig hur du arbetar med Configuration Manager program versioner och ersätter program.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 30170d70-489f-47f7-bebf-9ed0115db26b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 6afed00b8207edb338b2a6dc62e083a5267fa47e
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343141"
---
# <a name="revise-and-supersede-applications-in-configuration-manager"></a>Ändra och ersätt program i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I det här avsnittet får du lära dig hur du arbetar med Configuration Manager program versioner och hur du ersätter program med en ny version.  

##  <a name="application-revisions"></a> Programrevisioner  
 När du gör ändringar i ett program eller en distributions typ som finns i ett program skapar Configuration Manager en ny revision av programmet. Du kan visa historik över programrevisioner. Du kan också visa revisionernas egenskaper, återställa till en tidigare programrevision eller ta bort gamla revisioner.  

### <a name="to-display-an-application-revision-history"></a>Granska revisionshistoriken för program  

1.  I Configuration Manager-konsolen väljer du program **bibliotek**  >  **program hantering**  >  **program**och väljer sedan det program som du vill använda.  

3.  På fliken **Start** i gruppen **program** väljer du **revisions historik** för att öppna dialog rutan **program revisions historik** .  

### <a name="to-view-an-application-revision"></a>Visa en programrevision  

1.  Välj en program revision i dialog rutan **program revisions historik** och välj sedan **Visa**.  

2.  Granska det valda programmets egenskaper i dialogrutan **Egenskaper** .  

    > [!NOTE]  
    >  Programegenskaperna är skrivskyddade i dialogrutan.  

3.  Stäng dialogrutan **Egenskaper** .  

### <a name="to-restore-an-application-revision"></a>Återställa en programrevision  

1.  Välj en program revision i dialog rutan **program revisions historik** och välj sedan **Återställ**.  

2.  I dialog rutan **Bekräfta återställning av ändringar** väljer du **Ja** för att återställa den valda program revisionen.  

### <a name="to-delete-an-application-revision"></a>Ta bort en programrevision  

1.  Välj en program revision i dialog rutan **program revisions historik** och välj sedan **ta bort**.  

2.  I dialog rutan **ta bort program revision** väljer du **Ja**.  

> [!IMPORTANT]  
>  Du kan bara ta bort den aktuella program revisionen om programmet har dragits tillbaka och saknar referenser.  

##  <a name="application-supersedence"></a> Programersättning  
 Med program hanteringen i Configuration Manager kan du uppgradera eller ersätta befintliga program med hjälp av en ersättande relation. När du ersätter ett program kan du ange en ny distributions typ som ersätter det ersatta programmets distributions typ och även bestämma om du vill uppgradera eller avinstallera det ersatta programmet innan det ersättande programmet installeras. I allmänhet rekommenderar vi att du begränsar ersättnings kedjor till fem nivåer djup med högsta.
 
> [!IMPORTANT]  
>  En distributionstyp kan inte ersättas av en distributionstyp som har distribuerats till en annan samlingstyp, när du väljer att avinstallera en ersatt distributionstyp.  Det innebär till exempel att en distributionstyp som har distribuerats till en enhetssamling inte kan ersättas med en distributionstyp som har distribuerats till en användarsamling, om du väljer att avinstallera den ersatta distributionstypen.  

### <a name="decide-whether-to-upgrade-or-replace-an-application"></a>Bestäm om du vill uppgradera eller ersätta ett program  
 Du anger om du vill ersätta eller uppgradera en app i dialogrutan **Ange ersättande relation** i egenskapsdialogrutan för programmet. Typen av ersättning beror på om du markerar alternativet **Avinstallera** i den här dialogrutan:  

-   Om du vill uppdatera till en nyare version av samma program (med samma program-ID) ska **du inte** Markera **Avinstallera**.  

-   Om du vill ändra till ett annat program (med ett annat program-ID) ska du markera **Avinstallera**. Du måste ta bort den ersatta versionen av programmet.  

### <a name="supersede-dependent-applications"></a>Ersätt beroende program  
 I det här exemplet refererar **huvud programmet** till den app som du distribuerar och som har beroenden.  

 Du kan skapa en ersättningsrelation som uppdaterar det beroende programmet till en ny version.  

1. Kontrollera att det nya beroende programmet och det ursprungliga beroende programmet finns i samma beroendegrupp i masterprogrammet.  

2. Skapa en ersättningsrelation som ersätter det ursprungliga beroende programmet med det nya beroende programmet.  

   Under nya installationer av huvud programmet installeras det nya beroende programmet. Befintliga installationer av huvud programmet uppdateras med det nya beroende programmet.  

   Slut resultatet är att alla distributioner av huvud programmet använder det nya beroende programmet.  

### <a name="further-considerations"></a>Ytterligare överväganden  

-   Du kan ange flera ersättningsrelationer för beroende program. Det högsta beroende programmet i ersättningskedjan installeras.  

-   Beroende program måste distribueras till enheten där huvud programmet är installerat eller beroende program installeras inte.  

-   För nya installationer av masterprogrammet och om du har flera beroenden, är det beroendeordningen som avgör vilken version av det beroende programmet som installeras.  

### <a name="to-specify-a-supersedence-relationship"></a>Ange en ersättande relation  

1.  I Configuration Manager-konsolen väljer du program **bibliotek**  >  **program hantering**  >  **program**och väljer sedan det program som ersätter ett annat program.  

3.  På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper** för att öppna dialog rutan **Egenskaper** för program namn.  

4.  På fliken **ersättning** i dialog rutan *<egenskaper för \> program namn* väljer du **Properties** **Lägg till**.  

5.  Klicka på **Bläddra** i dialogrutan **Ange ersättande relation**.  

6.  I dialog rutan **Välj program** väljer du det program som du vill ersätta och väljer sedan **OK**.  

7.  I dialog rutan **ange ersättande relation** väljer du den distributions typ som ersätter det ersatta programmets distributions typ.  

    > [!NOTE]  
    >  Som standard avinstalleras inte distributions typen för det ersatta programmet av den nya distributions typen. Det här är ett vanligt scenario för att distribuera en uppgradering till ett befintligt program. Välj **Avinstallera** för att ta bort den befintliga distributionstypen innan den nya distributionstypen installeras. Om du vill uppgradera ett program bör du prova att det fungerar i en labbmiljö.  

8.  Välj **OK** för att stänga dialog rutan **ange ersättande relation** .  

9. Klicka på **OK** för att stänga dialog rutan **Egenskaper** för *<program \> namn* .  

### <a name="to-display-applications-that-supersede-the-current-application"></a>Visa program som ersätter ett aktuellt program  

1.  Välj **program varu bibliotek**i Configuration Manager-konsolen.  

2.  I arbets ytan **program bibliotek** expanderar du **program hantering**, väljer **program**och väljer sedan det program som du vill använda.  

3.  På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper** för att öppna dialog rutan **Egenskaper** för * \><program namn* .  

4.  På fliken **referenser** i dialog rutan *<egenskaper för \> program namn* väljer du **Properties** **program som ersätter det här programmet** från List rutan **Relations typ** .  

5.  Granska listan med program som ersätter det valda programmet och välj sedan **OK** för att stänga dialog rutan **Egenskaper** för *<program \> namn* .  
