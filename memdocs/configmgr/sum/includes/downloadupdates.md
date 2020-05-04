1.  I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** och väljer noden **program uppdateringar** .  

2.  Välj följande programuppdatering för att utföra nedladdningen med någon av följande metoder:  

    -   Välj en eller flera program uppdaterings grupper från noden **program uppdaterings grupper** . Klicka sedan på **Hämta** i menyfliksområdet.  

    -   Välj en eller flera program uppdateringar från noden **alla program uppdateringar** . Klicka sedan på **Hämta** i menyfliksområdet.  

        > [!NOTE]  
        >  I noden **alla program uppdateringar** visar Configuration Manager endast program uppdateringar med en **kritisk** och **säkerhets** klassificering som har släppts under de senaste 30 dagarna.  

        > [!TIP]  
        >  Klicka på **Lägg till kriterier** för att filtrera program uppdateringar som visas i noden **alla program uppdateringar** . Spara Sök kriterier som du ofta använder och hantera sedan sparade sökningar på fliken **Sök** .  


3.  Konfigurera följande inställningar på sidan **distributions paket** i guiden hämta program uppdateringar:  

    -  **Välj distributionspaket**: Välj den här inställningen för att välja ett befintligt distributionspaket för programuppdateringarna som finns i distributionen.  

        > [!NOTE]  
        >  Program uppdateringar som platsen redan har laddat ned till det valda distributions paketet laddas inte ned igen.  

    -  **Skapa ett nytt distributionspaket**: Välj den här inställningen för att skapa ett nytt distributionspaket för programuppdateringarna i distributionen. Konfigurera följande inställningar:  

        -   **Namn**: Anger namnet på distributionspaketet. Paketnamnet måste vara ett unikt namn som kort beskriver paketinnehållet. Den är begränsad till 50 tecken.  

        -   **Beskrivning**: Ange en beskrivning som ger information om distributionspaketet. Den valfria beskrivningen är begränsad till 127 tecken.    

        -   **Paketkälla**: Anger platsen för källfilerna för programuppdateringen. Ange en nätverks Sök väg för käll platsen, till exempel `\\server\sharename\path`eller klicka på **Bläddra** för att hitta nätverks platsen. Skapa en delad mapp för distributions paketets källfiler innan du fortsätter till nästa sida.  

             - Du kan inte använda den angivna platsen som källa till ett annat program distributions paket.  

             - Du kan ändra paketets käll plats i egenskaperna för distributions paketet när Configuration Manager skapar distributions paketet. Om du gör det kopierar du först innehållet från den ursprungliga paket källan till den nya paket käll platsen.  

             -  Dator kontot för SMS-providern och användaren som kör guiden för att ladda ned program uppdateringarna måste båda ha **Skriv** behörighet till nedladdnings platsen. Begränsa åtkomsten till nedladdnings platsen. Den här begränsningen minskar risken för angripare som manipulerar källfilerna för program uppdatering.  

        - **Aktivera binär differentiell replikering**: Aktivera den här inställningen för att minimera nätverks trafiken mellan platser. Binär differentiell replikering (BDR) uppdaterar endast det innehåll som har ändrats i paketet, i stället för att uppdatera hela paket innehållet. Mer information finns i [binär differentiell replikering](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

4.  På sidan **distributions platser** anger du de distributions platser eller distributions plats grupper som ska vara värdar för program uppdaterings filerna. Mer information om distributionsplatser finns i [Konfigurationer av distributionsplatser](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Den här sidan är bara tillgänglig när du skapar ett nytt distributionspaket för programuppdatering.  

5.  Sidan **distributions inställningar** är bara tillgänglig när du skapar ett nytt distributions paket för program uppdatering. Ange följande inställningar:  

    -   **Distributionsprioritet**: Använd den här inställningen om du vill ange distributionsprioritet för distributionspaketet. Distributionsprioriteten tillämpas när distributionspaketet skickas till distributionsplatser på underordnande platser. Distributions paketen skickas i prioritetsordning: hög, medel eller låg. Paket med identisk prioritering skickas i den ordning de skapades. Om det inte finns någon efter släpning bearbetas paketet omedelbart oavsett prioritet. Som standard skickar platsen paket med **medelhög** prioritet.  

    -   **Aktivera för distribution på begäran**: Använd den här inställningen för att aktivera innehålls distribution på begäran till distributions platser som kon figurer ATS för den här funktionen och i klientens aktuella avgränsnings grupp. När du aktiverar den här inställningen skapar hanterings platsen en utlösare för distributions hanteraren för att distribuera innehållet till alla distributions platser när en klient begär innehållet för paketet och innehållet inte är tillgängligt. Mer information finns i [innehålls distribution på begäran](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).  

    -   **Inställningar för förinstallerad distributionsplats**: Använd den här inställningen om du vill ange hur innehåll ska distribueras till förinstallerade distributionsplatser. Välj ett av följande alternativ:  

        -   **Hämta innehåll automatiskt när paket tilldelas distributionsplatser**: Använd den här inställningen för att ignorera förinställda inställningar och distribuera innehåll till distributionsplatsen.   

        -   **Hämta endast innehållsändringar till distributionsplatsen**: Använd den här inställningen för att förinstallera innehåll till distributionsplatsen och distribuera sedan innehållsändringar till distributionsplatsen.  

        -   **Kopiera innehållet i det här paketet manuellt till distributionsplatsen**: Använd den här inställningen för att alltid förinstallera innehåll på distributionsplatsen. Det här alternativet är standardinställningen.  

        Mer information om hur du förinstallerar innehåll på distributionsplatser finns i [Använda förinstallerat innehåll](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  


6.  På sidan **hämtnings plats** anger du den plats som Configuration Manager använder för att ladda ned källfilerna för program uppdatering. Välj ett av följande alternativ:  

    -   **Hämta program uppdateringar från Internet**: Välj den här inställningen för att ladda ned program uppdateringar från platsen på Internet. Det här alternativet är standardinställningen.  

    -   **Hämta program uppdateringar från en plats i mitt nätverk**: Välj den här inställningen för att ladda ned program uppdateringarna från en lokal katalog eller delad mapp. Den här inställningen är användbar när den dator som kör guiden inte har Internet åtkomst. Alla datorer med Internet åtkomst kan preliminärt ladda ned program uppdateringarna. Lagra dem sedan på en plats i det lokala nätverket som är tillgängligt från den dator där guiden körs.  


7.  På sidan **Val av språk** väljer du de språk för vilka platsen hämtar de valda program uppdateringarna. Platsen hämtar bara de här uppdateringarna om de är tillgängliga på de valda språken. Program uppdateringar som inte är språkspecifika laddas alltid ned. Som standard väljer guiden de språk som du har konfigurerat i egenskaperna för program uppdaterings platsen. Minst ett språk måste väljas innan du fortsätter till nästa sida. Om du bara väljer språk som en program uppdatering inte stöder, Miss lyckas nedladdningen för uppdateringen.  

8. På sidan **Sammanfattning** kontrollerar du inställningarna som du har valt i guiden och klickar sedan på **Nästa** för att ladda ned program uppdateringarna.  

9. På sidan **slut för ande** kontrollerar du att program uppdateringarna har hämtats och klickar sedan på **Stäng**.  
