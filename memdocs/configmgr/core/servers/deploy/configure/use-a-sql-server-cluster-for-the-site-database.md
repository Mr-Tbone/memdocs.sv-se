---
title: SQL Server kluster
titleSuffix: Configuration Manager
description: Använd ett SQL Server-kluster som värd för Configuration Manager plats databasen
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d035e6fbd776a03ce38a4cd0fc12755100b60c91
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643252"
---
# <a name="use-a-sql-server-cluster-for-the-site-database"></a>Använd ett SQL Server-kluster för plats databasen

*Gäller för: Configuration Manager (aktuell gren)*

Du kan använda ett SQL Server redundanskluster som värd för Configuration Manager-plats databasen. Ett kluster ger stöd för redundans och förbättrar tillförlitligheten för plats databasen. Det ger dock inte ytterligare bearbetning eller belastnings Utjämnings förmåner. Ett SQL Server redundanskluster använder dessutom delad lagring och introducerar en enskild felpunkt. Det kan uppstå försämring av prestanda, eftersom plats servern måste hitta den aktiva noden i SQL Server klustret innan den ansluter till plats databasen.  

> [!IMPORTANT]  
> En lyckad uppsättning SQL Server kluster förlitar sig på dokumentation och procedurer som finns i SQL Server-dokumentations biblioteket.  


Innan du installerar Configuration Manager förbereder du SQL Server-klustret så att det stöder Configuration Manager. Mer information finns i [förbereda en klustrad SQL Server instans](#bkmk_prepare).

Under installationen av Configuration Manager installeras Windows tjänsten Volume Shadow Copy Writer på varje fysisk datornod i Microsoft Windows Server-klustret. Den här tjänsten stöder underhålls åtgärden **plats Server för säkerhets kopiering** .  

När platsen har installerats söker Configuration Manager efter ändringar i klusternoden varje timme. Configuration Manager hanterar automatiskt de ändringar som påträffas som påverkar dess komponent installationer. Till exempel en nods redundans eller en ny nod läggs till i SQL Server klustret.  



## <a name="supported-options"></a>Alternativ som stöds

Följande alternativ stöds för SQL Server redundanskluster som används som plats databas:

- Ett enda instans kluster  

- Konfigurationer med flera instanser  

- Flera aktiva noder  

- Både en namngiven eller en standard instans  



## <a name="prerequisites"></a>Krav

Tänk på följande krav:  

- Platsdatabasen måste vara fjärransluten till platsservern. Klustret kan inte innehålla plats system servern.  

    > [!Note]  
    > Från och med version 1810 blockerar Configuration Manager installations processen inte längre installationen av plats Server rollen på en dator med Windows-rollen för redundanskluster. Tidigare kunde du inte hitta plats databasen på plats servern. Med den här ändringen kan du skapa en plats med hög tillgänglighet med färre servrar genom att använda ett SQL-kluster och en plats server i passivt läge. Mer information finns i [alternativ för hög tillgänglighet](high-availability-options.md). <!--3607761, fka 1359132-->  

- Lägg till plats serverns dator konto i gruppen lokala **Administratörer** på varje server i klustret.  

- För att stödja Kerberos-autentisering aktiverar du **TCP/IP-** nätverkets kommunikations protokoll för nätverks anslutningen för varje SQL Server klusternod. **Namngivna pipes** -protokollet krävs inte, men kan användas för att felsöka problem med Kerberos-autentisering. Inställningarna för nätverks protokoll konfigureras i **Konfigurationshanteraren för SQL Server**under **SQL Server nätverks konfiguration**.  

- Det finns särskilda certifikat krav när du använder ett SQL Server-kluster för plats databasen. Mer information finns i följande artiklar:
  - [Installera ett certifikat i ett SQL-kluster för växling vid fel](https://docs.microsoft.com/sql/database-engine/configure-windows/manage-certificates?view=sql-server-ver15#provision-failover-cluster-cert)
  - [PKI-certifikatkrav för Configuration Manager](../../../plan-design/network/pki-certificate-requirements.md#BKMK_PKIcertificates_for_servers)

  > [!NOTE]
  > Om du inte etablerar ett certifikat i SQL Configuration Manager skapar och etablerar ett självsignerat certifikat för SQL.<!-- 7099499 -->

## <a name="limitations"></a>Begränsningar

Tänk på följande begränsningar:  


### <a name="installation-and-configuration"></a>Installation och konfiguration

- Sekundära platser kan inte använda ett SQL Server-kluster.  

- När du anger ett SQL Server kluster är alternativet för att ange fil platser som inte är standard för plats databasen inte tillgängligt.  


### <a name="sms-provider"></a>SMS-provider

Du kan inte installera en instans av SMS-providern på ett SQL Server kluster. Det stöds inte heller på en dator som kör som en klustrad SQL Server nod.  


### <a name="data-replication-options"></a>Alternativ för datareplikering

Om du använder **distribuerade vyer**kan du inte använda ett SQL Server-kluster som värd för plats databasen.  


### <a name="backup-and-recovery"></a>Säkerhetskopiering och återställning

Configuration Manager stöder inte Data Protection Manager (DPM) säkerhets kopiering för ett SQL Server kluster som använder en namngiven instans. Det stöder DPM-säkerhetskopiering på ett SQL Server kluster som använder standard instansen av SQL Server.  



## <a name="prepare-a-clustered-sql-server-instance"></a><a name="bkmk_prepare"></a>Förbereda en klustrad SQL Server instans  

Här är de viktigaste uppgifterna som slutförs för att förbereda plats databasen:

- Skapa det virtuella SQL Server-klustret som ska vara värd för platsdatabasen i en befintlig Windows Server-klustermiljö. Information om hur du installerar och konfigurerar ett SQL Server kluster finns i dokumentationen som är speciell för din version av SQL Server. Mer information finns i [skapa ett nytt SQL Server redundanskluster](https://docs.microsoft.com/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup?view=sql-server-2017).  

- På varje dator i SQL Server klustret placerar du en fil i rotmappen på varje enhet där du inte vill att Configuration Manager ska installera plats komponenter. Ge filen namnet `NO_SMS_ON_DRIVE.SMS`. Som standard installerar Configuration Manager vissa komponenter på varje fysisk nod för att stödja åtgärder som säkerhets kopiering.  

- Lägg till plats serverns dator konto i gruppen lokala **Administratörer** på varje Windows Server-klusternod.  

- I den virtuella SQL Server-instansen tilldelar du rollen **sysadmin** SQL Server till det användar konto som kör Configuration Manager-installationen.  


### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Installera en ny plats med en klustrad SQL Server  

Om du vill installera en plats som använder en klustrad plats databas kör du Configuration Manager-installationen efter din normala process för att installera en-plats, med följande ändringar:  

- Ange namnet på den virtuella SQL Server-klusterinstans där platsdatabasen ska finnas på sidan **Databasinformation** . Den virtuella instansen ersätter namnet på datorn som kör SQL Server.  

    > [!IMPORTANT]  
    > När du anger namnet på den virtuella SQL Server kluster instansen ska du inte ange det virtuella Windows Server-namnet som skapats av Windows Server-klustret. Om du använder det virtuella Windows Server-namnet installeras plats databasen på den lokala hård disken på noden aktiva Windows Server-klusternoder. Detta förhindrar en lyckad redundansväxling i händelse av problem på noden.  
