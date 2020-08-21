---
title: Kryptera återställningsdata
titleSuffix: Configuration Manager
description: Kryptera BitLocker-återställningsnyckel, återställnings paket och TPM-lösenords-hashvärden i nätverket och i Configuration Manager databasen.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 1ee6541a-e243-43ea-be16-d0349f7f0c6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2c74f1ac74b120fac2dabcd5f84f288b41368324
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697304"
---
# <a name="encrypt-recovery-data"></a>Kryptera återställningsdata

*Gäller för: Configuration Manager (aktuell gren)*

<!--3601034-->

När du skapar en princip för BitLocker-hantering distribuerar Configuration Manager återställnings tjänsten till en hanterings plats. På sidan **klient hantering** i hanterings principen för BitLocker kan klienten, om du **konfigurerar BitLocker Management Services**, säkerhetskopiera nyckel återställnings information till plats databasen. Den här informationen omfattar BitLocker-återställningsnyckel, återställnings paket och TPM-lösenords-hashvärden. När användarna är utelåsta från sin skyddade enhet kan du använda den här informationen för att hjälpa dem att återställa åtkomsten till enheten.

Med hänsyn till den känsliga typen av information måste du skydda den under följande omständigheter:

- Configuration Manager kräver en HTTPS-anslutning mellan klienten och återställnings tjänsten för att kryptera data som överförs över nätverket. Det finns två alternativ:

  - HTTPS – Aktivera IIS-webbplatsen på hanterings platsen som är värd för återställnings tjänsten, inte hela hanterings plats rollen. Det här alternativet gäller endast för Configuration Manager version 2002.<!-- 5925660 -->

  - Konfigurera hanterings platsen för HTTPS. I egenskaperna för hanterings platsen måste inställningen **klient anslutningar** vara **https**. Det här alternativet gäller för Configuration Manager version 1910 eller 2002.

    > [!NOTE]
    > Den har för närvarande inte stöd för utökad HTTP.

- Överväg också att kryptera dessa data när de lagras i plats databasen. Om du installerar ett SQL-certifikat kan Configuration Manager kryptera dina data i SQL.

    Om du inte vill skapa ett certifikat för BitLocker-hanterings kryptering kan du välja att använda oformaterad text lagring av återställnings data. När du skapar en princip för BitLocker-hantering aktiverar du alternativet för att **tillåta att återställnings information lagras som oformaterad text**.

    > [!NOTE]
    > Ett annat säkerhets lager är att kryptera hela plats databasen. Om du aktiverar kryptering för databasen finns det inga funktions problem i Configuration Manager.
    >
    > Kryptera med försiktighet, särskilt i storskaliga miljöer. Beroende på vilka tabeller du krypterar och vilken version av SQL du har, kan du märka upp till 25% prestanda försämring. Uppdatera dina säkerhets kopierings-och återställnings planer så att du kan återställa krypterade data.

## <a name="certificate-requirements"></a>Certifikatkrav

### <a name="https-server-authentication-certificate"></a>Certifikat för HTTPS-serverautentisering

<!--5925660-->

I Configuration Manager nuvarande gren version 1910, för att integrera BitLocker-återställningsnyckeln som du var tvungen att aktivera för en hanterings plats. HTTPS-anslutningen är nödvändig för att kryptera återställnings nycklarna över nätverket från Configuration Manager-klienten till hanterings platsen. Det kan vara svårt för många kunder att konfigurera hanterings platsen och alla klienter för HTTPS.

Från och med version 2002 är HTTPS-kravet för IIS-webbplatsen som är värd för återställnings tjänsten, inte hela hanterings plats rollen. Den här ändringen sänker certifikat kraven och krypterar fortfarande återställnings nycklarna vid överföring.

Nu kan hanterings platsens egenskap för **klient anslutningar** vara **http** eller **https**. Om hanterings platsen är konfigurerad för **http**så att den stöder BitLocker-återställnings tjänsten:

1. Hämta ett certifikat för serverautentisering. Bind certifikatet till IIS-webbplatsen på den hanterings plats som är värd för återställnings tjänsten för BitLocker.

2. Konfigurera klienterna så att de litar på certifikatet för serverautentisering. Det finns två metoder för att göra detta förtroende:

    - Använd ett certifikat från en offentlig och globalt betrodd certifikat leverantör. Till exempel, men inte begränsat till, DigiCert, Thawte eller VeriSign. Windows-klienterna innehåller betrodda rot certifikat utfärdare (CAs) från dessa leverantörer. Genom att använda ett certifikat för serverautentisering som utfärdats av någon av dessa providers, bör klienterna automatiskt lita på det.

    - Använd ett certifikat som utfärdats av en certifikat utfärdare från din organisations PKI (Public Key Infrastructure). De flesta PKI-implementeringar lägger till betrodda rot certifikat utfärdare till Windows-klienter. Till exempel, med hjälp av Active Directory Certificate Services med grup princip. Om du utfärdar certifikatet för serverautentisering från en certifikat utfärdare som klienterna inte automatiskt litar på, lägger du till det betrodda rot certifikatet för certifikat utfärdaren till klienter.

> [!TIP]
> De enda klienter som behöver kommunicera med återställnings tjänsten är de klienter som du planerar att rikta mot en BitLocker-hanterings princip och som innehåller en **klient hanterings** regel.

Använd **BitLockerManagementHandler. log** för att felsöka den här anslutningen på klienten. För anslutning till återställnings tjänsten visar loggen den URL som klienten använder. Leta upp en post som börjar med `Checking for Recovery Service at` .

> [!NOTE]
> Om platsen har fler än en hanterings plats aktiverar du HTTPS på alla hanterings platser på den plats som en BitLocker-hanterad klient kan kommunicera med. Om HTTPS-hanterings platsen inte är tillgänglig kan klienten redundansväxla till en HTTP-hanterings plats och sedan inte depositions sin återställnings nyckel.
>
> Den här rekommendationen gäller båda alternativen: Aktivera hanterings platsen för HTTPS eller aktivera IIS-webbplatsen som är värd för återställnings tjänsten på hanterings platsen.

### <a name="sql-encryption-certificate"></a>SQL-krypterings certifikat

Använd det här SQL-certifikatet för Configuration Manager för att kryptera återställnings data för BitLocker i plats databasen. Du kan använda din egen process för att skapa och distribuera BitLocker Management Encryption-certifikatet, så länge det uppfyller följande krav:

- Namnet på krypterings certifikatet för BitLocker-hanteringen måste vara `BitLockerManagement_CERT` .

- Kryptera det här certifikatet med en huvud nyckel för databasen.

- Följande SQL-användare behöver **kontroll** behörigheter för certifikatet:
  - RecoveryAndHardwareCore
  - RecoveryAndHardwareRead
  - RecoveryAndHardwareWrite

- Distribuera samma certifikat vid varje plats databas i hierarkin.

- Skapa certifikatet med den senaste versionen av SQL Server i din miljö. Exempel:
  - Certifikat som skapats med SQL Server 2016 eller senare är kompatibla med SQL Server 2014 eller tidigare.
  - Certifikat som skapats med SQL Server 2014 eller tidigare är inte kompatibla med SQL Server 2016 eller senare.

## <a name="example-scripts"></a>Exempel skript

Dessa SQL-skript är exempel för att skapa och distribuera ett certifikat för BitLocker-hanterings kryptering i Configuration Manager plats databasen.

### <a name="create-certificate"></a>Skapa certifikat

Det här exempel skriptet utför följande åtgärder:

- Skapar ett certifikat
- Anger behörigheter
- Skapar en huvud nyckel för databasen

Innan du använder det här skriptet i en produktions miljö ändrar du följande värden:

- Plats databasens namn ( `CM_ABC` )
- Lösen ord för att skapa huvud nyckeln ( `MyMasterKeyPassword` )
- Förfallo datum för certifikat ( `20391022` )

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN
    CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
    WITH SUBJECT = 'BitLocker Management',
    EXPIRY_DATE = '20391022'

    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="back-up-certificate"></a>Säkerhetskopiera certifikat

Det här exempel skriptet säkerhetskopierar ett certifikat. När du sparar certifikatet i en fil kan du sedan [återställa](#restore-certificate) det till andra plats databaser i hierarkin.

Innan du använder det här skriptet i en produktions miljö ändrar du följande värden:

- Plats databasens namn ( `CM_ABC` )
- Fil Sök väg och namn ( `C:\BitLockerManagement_CERT_KEY` )
- Exportera nyckel lösen ord ( `MyExportKeyPassword` )

``` SQL
USE CM_ABC
BACKUP CERTIFICATE BitLockerManagement_CERT TO FILE = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        ENCRYPTION BY PASSWORD = 'MyExportKeyPassword')
```

> [!IMPORTANT]
> Lagra den exporterade certifikat filen och det associerade lösen ordet på en säker plats.

### <a name="restore-certificate"></a>Återställ certifikat

Det här exempel skriptet återställer ett certifikat från en fil. Använd den här processen för att distribuera ett certifikat som du har skapat på en annan plats databas.

Innan du använder det här skriptet i en produktions miljö ändrar du följande värden:

- Plats databasens namn ( `CM_ABC` )
- Huvud nyckel lösen ord ( `MyMasterKeyPassword` )
- Fil Sök väg och namn ( `C:\BitLockerManagement_CERT_KEY` )
- Exportera nyckel lösen ord ( `MyExportKeyPassword` )

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN

CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
FROM FILE  = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        DECRYPTION BY PASSWORD = 'MyExportKeyPassword')

GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="verify-certificate"></a>Verifiera certifikat

Använd det här SQL-skriptet för att verifiera att SQL har skapat certifikatet med de behörigheter som krävs.

``` SQL
USE CM_ABC
declare @count int
select @count = count(distinct u.name) from sys.database_principals u
join sys.database_permissions p on p.grantee_principal_id = u.principal_id or p.grantor_principal_id = u.principal_id
join sys.certificates c on c.certificate_id = p.major_id
where u.name in('RecoveryAndHardwareCore', 'RecoveryAndHardwareRead', 'RecoveryAndHardwareWrite') and
c.name = 'BitLockerManagement_CERT' and p.permission_name like 'CONTROL'
if(@count >= 3) select 1
else select 0
```

Om certifikatet är giltigt returnerar skriptet värdet `1` .

## <a name="see-also"></a>Se även

Mer information om dessa SQL-kommandon finns i följande artiklar:

- [SQL Server-och databas krypterings nycklar](/sql/relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine)
- [Skapa certifikat](/sql/t-sql/statements/create-certificate-transact-sql)
- [Säkerhetskopiera certifikat](/sql/t-sql/statements/backup-certificate-transact-sql)
- [Skapa huvud nyckel](/sql/t-sql/statements/create-master-key-transact-sql)
- [Säkerhets kopierings huvud nyckel](/sql/t-sql/statements/backup-master-key-transact-sql)
- [Bevilja certifikat behörigheter](/sql/t-sql/statements/grant-certificate-permissions-transact-sql)