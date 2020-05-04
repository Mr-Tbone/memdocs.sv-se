---
title: Skapa globala villkor
titleSuffix: Configuration Manager
description: Skapa globala villkor för att ange hur ett program tillhandahålls och distribueras till klient enheter.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2d5f871a-19dc-4bd3-a3ad-4230c7a69f1b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ae27e50e5093d7443c35df33b1757caec6086627
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710288"
---
# <a name="how-to-create-global-conditions-in-configuration-manager"></a>Så här skapar du globala villkor i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I Configuration Manager är globala villkor regler som representerar affärs villkor eller tekniska villkor som du kan använda för att ange hur ett program tillhandahålls och distribueras till klient enheter. Du kommer åt globala villkor från sidan **Krav** i guiden Skapa distributionstyp.  

> [!NOTE]  
>  Du kan bara redigera globala villkor från den plats där de skapades.  

 Använd följande procedurer för att skapa Configuration Manager globala villkor.  

## <a name="provide-basic-information-about-the-global-condition"></a>Ange grundläggande information om det globala villkoret  
 Det finns flera olika typer av globala villkor. Olika alternativ associeras med de olika typerna av globala villkor. När du väljer en speciell typ av global villkor visar Configuration Manager de alternativ som gäller för ditt val.  

1.  I Configuration Manager-konsolen väljer du **program bibliotek** > **program hantering** > **globala villkor**.  

3.  På fliken **Start** går du till gruppen **skapa** och väljer **Skapa globalt villkor**.  

4.  Ge det globala villkoret ett namn och eventuellt en beskrivning i dialogrutan **Skapa globalt villkor** .  

5.  I list rutan **enhets typ** väljer du om det globala villkoret gäller för en **Windows** -dator eller en **Windows Mobile** -enhet.  

6.  Välj ett av de följande alternativen i listrutan **Typ av villkor** :  

    -   **Inställning** – Det här alternativet innebär att en kontroll görs av att ett eller flera objekt finns på klientenheterna. Du kan till exempel kontrol lera att det finns en fil, en mapp eller ett register nyckel värde på en klienten het.  

    -   **Uttryck** – med det här alternativet kan du konfigurera mer komplexa regler för att kontrol lera om villkoret är uppfyllt på klient enheter. Du kan till exempel kontrol lera om det fysiska minnet på en dator är mellan 2 GB och 4 GB eller om en mobil enhet använder Touch Screen-indata.  

## <a name="set-up-rules-for-the-global-condition"></a>Konfigurera regler för det globala villkoret  
 Proceduren för att definiera globala villkors regler varierar beroende på om du konfigurerar en inställning eller ett uttryck. Använd den aktuella proceduren här för att konfigurera en inställning eller ett uttryck för det globala villkoret.  

### <a name="to-set-up-a-setting-for-the-global-condition"></a>Konfigurera en inställning för det globala villkoret  

1. Välj **Inställning** i listrutan **Typ av villkor**.  

2. Välj i listrutan **Inställningstyp** det objekt du vill använda som villkor för vilket kraven kontrolleras. Följande inställnings typer och konfigurationer är tillgängliga.  

   - **Active Directory-fråga**  

     -   **LDAP-prefix** – Ange ett giltigt LDAP-prefix till Active Directory Domain Services-frågan för att bedöma efterlevnaden på klientdatorerna. Du kan använda **LDAP://** eller **GC://**.  

     -   **Unikt namn (DN)** – ange det unika namnet på Active Directory Domain Services-objektet som ska utvärderas för kompatibilitet på klient datorer.  

     -   **Sökfilter** – Ange eventuellt ett LDAP-filter för att begränsa Active Directory Domain Services-frågan och bedöma efterlevnaden på klientdatorerna.  

     -   **Sökomfång** – Ange sökomfånget i Active Directory Domain Services:  

         -   **Grundläggande** – frågar bara det angivna objektet.  

         -   **En nivå** – det här alternativet används inte i den här versionen av Configuration Manager.  

         -   **Under träd** – frågar det angivna objektet och dess fullständiga under träd i katalogen.  

     -   **Egenskap** – Ange egenskapen hos Active Directory Domain Services-objektet som ska användas för att bedöma efterlevnaden på klientdatorerna.  

     -   **Fråga** – visar LDAP-frågan som är konstruerad från posterna i **LDAP-prefix**, **unikt namn (DN)**, **Sök filter** om det har angetts och **egenskap**. Den här frågan används för att bedöma efterlevnaden på klientdatorerna.  

   - **Sammansättning**  

     -   **Sammansättningsnamn** – Anger namnet på sammansättningsobjektet som du vill söka efter. Namnet får inte vara samma som andra sammansättnings objekt av samma typ, och namnet måste vara registrerat i den globala sammansättningscachen. Sammansättnings namnet får innehålla högst 256 tecken.  

     > [!NOTE]  
     >  En sammansättning är ett stycke kod som flera program kan dela på. Sammansättningar kan ha fil namns tillägget. dll eller. exe. Den globala sammansättningscachen där alla delade sammansättningar lagras är en mapp på klientdatorerna som heter *%systemroot%\assembly* .  

   - **Fil system**  

     - **Typ** – Välj om du vill söka efter en **fil** eller **mapp**i list rutan.  

     - **Sökväg** – Ange sökvägen till den angivna filen eller mappen på klientdatorerna. Du kan använda systemmiljövariabler och miljövariabeln *%USERPROFILE%* i sökvägen.  

       > [!NOTE]  
       >  Om du använder miljövariabeln *%USERPROFILE%* i fälten **Sökväg** eller **Fil- eller mappnamn** , söks alla användarprofiler på klientdatorn igenom. Det kan leda till att du hittar flera exemplar av filen eller mappen.  

     - **Fil- eller mappnamn** – Ange namnet på fil- eller mappobjektet som du vill söka efter. Du kan använda systemmiljövariabler och miljövariabeln *%USERPROFILE%* i fil- eller mappnamnet. Du kan också använda * och? jokertecken i fil namnet.  

       > [!NOTE]  
       >  Du kan få väldigt många resultat om du anger ett fil- eller mappnamn och använder jokertecken. Detta kan leda till hög resursanvändning på klient datorn och hög nätverks trafik när resultatet rapporteras till Configuration Manager.  

     - **Inkludera undermappar** – aktivera det här alternativet om du även vill söka igenom eventuella undermappar under den angivna sökvägen.  

     - **Den här filen eller mappen är associerad med ett 64-bitars program** – välj om 64-bitars system filens plats (*% windir%* där) ska genomsökas utöver den 32-bitars system fil platsen (*% windir%* \syswow64) på Configuration Manager klienter som kör en 64-bitars version av Windows.  

       > [!NOTE]  
       >  Om samma fil eller mapp finns bland både 64- och 32-bitars systemfiler på samma 64-bitarsdator, upptäcks flera filer genom det globala villkoret.  

       Inställningstypen **Filsystem** stöder inte UNC-sökvägar till en nätverksresurs i fältet **Sökväg** .  

   - **IIS-metabas**  

     -   **Metabassökväg** – Ange en giltig sökväg till IIS-metabasen.  

     -   **Egenskaps-ID** – Ange IIS-metabasinställningens numeriska egenskap.  

   - **Registernyckel**  

     -   **Hive** – Välj den registrerings data fil i list rutan som du vill söka i.  

     -   **Nyckel** – Ange vilket registernyckelsnamn du vill söka efter. Formatet måste vara *nyckel\undernyckel*.  

     -   **Registernyckeln är associerad med ett 64-bitarsprogram** – Detta anger om du vill söka igenom 64-bitars registernycklar utöver 32-bitars registernycklar på klienter som kör en 64-bitarsversion av Windows.  

         > [!NOTE]  
         >  Om samma registernyckel finns både i 64- och 32-bitarsregistret på samma 64-bitarsdator, upptäcks bägge registernycklarna genom det globala villkoret.  

   - **Register värde**  

     -   **Registreringsdatafil** – Välj i vilken registreringsdatafil du vill söka i listrutan.  

     -   **Nyckel** – Ange vilket registernyckelsnamn du vill söka efter. Formatet måste vara *nyckel\undernyckel*.  

     -   **Värde** – Ange vilket värde som måste finnas i den angivna registernyckeln.  

     -   **Registernyckeln är associerad med ett 64-bitarsprogram** – Detta anger om du vill söka igenom 64-bitars registernycklar utöver 32-bitars registernycklar på klienter som kör en 64-bitarsversion av Windows.  

         > [!NOTE]  
         >  Om samma registernyckel finns både i 64- och 32-bitarsregistret på samma 64-bitarsdator, upptäcks bägge registernycklarna genom det globala villkoret.  

   - **Över**  

     -   **Identifierings skript** – Välj **Lägg** till för att ange eller bläddra till det skript som ska användas. Du kan använda Windows PowerShell-, VBScript-eller JScript-skript.  

     -   **Köra skript med hjälp av autentiseringsuppgifter för den inloggade användaren** – om du aktiverar det här alternativet körs skriptet på klient datorer med hjälp av autentiseringsuppgifterna för den användare som är inloggad.  

         > [!NOTE]  
         >  Värdet som skriptet returnerar används för att bedöma efterlevnaden av det globala villkoret. Om du till exempel använder VBScript kan du använda kommandot **wscript. ECHO result** för att returnera det variabla värdet till det globala villkoret.  
         >   
         >  Om skriptet returnerar flera värden måste dessa värden finnas på en enda rad och avgränsas med ett semikolon. Om värdena är på separata rader misslyckas utvärderingen.  

   - **SQL-fråga**  

     -   **SQL Server-instans** – Välj om du vill att SQL-frågan ska köras på standardinstansens namn, alla instansers namn eller på en angiven databasinstans namn.  

         > [!NOTE]  
         >  Instansnamnet måste gälla en lokal instans av SQL Server. Du bör använda ett skript om du vill referera till en klustrad instans av SQL Server.  

     -   **Databas** – Ange namnet på Microsoft SQL Server-databasen som SQL-frågan ska köras mot.  

     -   **Kolumn** – Ange kolumnnamnet som returernas av Transact-SQL-uttrycket som ska användas för att bedöma efterlevnaden av det globala villkoret.  

     -   **Transact-SQL-uttryck:** – Ange den fullständiga SQL-frågan som ska användas i det globala villkoret. Du kan också välja **Öppna** för att öppna en befintlig SQL-fråga.  

   - **WQL-fråga**  

     -   **Namnområde** – Ange det WMI-namnområde som ska användas för att sätta samman en WQL-fråga som används för att bedöma efterlevnaden på klientdatorerna. Standardvärdet är Root\cimv2.  

     -   **Klass** – Anger den WMI-klass som ska användas för att sätta samman en WQL-fråga som används för att bedöma efterlevnaden på klientdatorerna.  

     -   **Egenskap** – Anger den WMI-egenskap som ska användas för att sätta samman en WQL-fråga som används för att bedöma efterlevnaden på klientdatorerna.  

     -   **WQL-fråga WHERE-sats** – Du kan använda inställningen **WQL-fråga WHERE-sats** om du vill ange en WHERE-sats som ska tillämpas på det angivna namnområdet, på klassen och på egenskapen på klientdatorerna.  

   - **XPath-fråga**  

     -   **Sökväg** – Ange sökvägen till XML-filen på klientdatorer som ska användas för åtkomstefterlevnad. Configuration Manager stöder användningen av alla variabler i Windows system-miljön och användar variabeln *% USERPROFILE%* i Sök vägs namnet.  

     -   **XML-filnamn** – ange namnet på filen som innehåller den XML-fråga som ska användas för att utvärdera kompatibiliteten på klient datorerna.  

     -   **Inkludera undermappar** – Markera det här alternativet om du även vill söka igenom eventuella undermappar på den angivna sökvägen.  

     -   **Den här filen är associerad med ett 64-bitars program** – välj om 64-bitars system filens plats (*% windir%* där) ska genomsökas utöver den 32-bitars system fil platsen (*% windir%* \syswow64) på Configuration Manager klienter som kör en 64-bitars version av Windows.  

     -   **XPath-fråga** – En giltig XPath-fråga (XML path language) som ska användas för att bedöma efterlevnaden på klientdatorer.  

     -   **Namnområden** – Detta alternativ gör att dialogrutan **XML-namnområden** öppnas. Där kan du ange vilka namnområden och prefix som ska användas i XPath-frågan.  

3. Välj i listrutan **Datatyp** i vilket format data ska returneras från villkoret innan de används för att kontrollera att kraven är uppfyllda.  

   > [!NOTE]  
   >  List rutan **datatyp** visas inte för alla inställnings typer.  

4. Ange ytterligare information om den här inställningen under List rutan **inställnings typ** . Vilka objekt som du kan konfigurera varierar beroende på vilken inställnings typ du har valt.  

5. Välj **OK** för att spara regeln och stänga dialog rutan **Skapa globalt villkor** .  

### <a name="set-up-an-expression-for-the-global-condition"></a>Konfigurera ett uttryck för det globala villkoret  

1.  Välj **Uttryck** i listrutan **Typ av villkor**.  

2.  Välj **Lägg till sats** för att öppna dialog rutan **Lägg till sats** .  

3.  Ange huruvida detta uttryck gäller en enhet eller en användare i listrutan **Välj kategori** . Om du vill använda ett redan konfigurerat globalt villkor kan du även välja **Anpassat** .  

4.  Välj det villkor du vill använda för att bedöma huruvida användaren eller enheten uppfyller kraven i regeln i listrutan **Välj ett villkor** . Innehållet i listan varierar beroende på vilken kategori som valts.  

5.  Välj i listrutan **Välj operator** den operator som du vill använda för att jämföra det valda villkoret med det angivna värdet och därmed bedöma huruvida användaren eller enheten uppfyller regelns krav. Tillgängliga operatörer varierar beroende på vilket villkor som valts.  

6.  Ange i fältet **Värde** de värden som ska användas med det valda villkoret och den valda operatorn för att bedöma huruvida användaren eller enheten uppfyller regelns krav. Tillgängliga värden varierar beroende på vilket villkor och vilken operatör som valts.  

7.  Välj **OK** för att spara uttrycket och stänga dialog rutan **Lägg till sats** .  

8.  När du har lagt till satser i det globala villkoret väljer du **OK** för att stänga dialog rutan **Skapa globalt villkor** och spara det globala villkoret.  
