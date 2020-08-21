---
title: Utöka och migrera lokal plats till Microsoft Azure
titleSuffix: Configuration Manager
description: Lär dig mer om hur du använder Migreringsverktyget för att program mässigt skapa virtuella Azure-datorer för Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1c975c5e-efd1-4d47-a315-39ccb32633dc
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d5f0c9127cc5c5819368eb0454d7bc63546ccc1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699508"
---
# <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>Utöka och migrera lokal plats till Microsoft Azure

*Gäller för: Configuration Manager (Current Branch)*


Det här verktyget introducerades i version 1910 och hjälper dig att program mässigt skapa virtuella Azure-datorer (VM) för Configuration Manager. <!--3556022--> Den kan installeras med standardinställningar webbplats roller som en passiv plats Server, hanterings platser och distributions platser. När du har validerat de nya rollerna kan du använda dem som ytterligare plats system för hög tillgänglighet. Du kan också ta bort den lokala plats system rollen och bara behålla rollen för den virtuella Azure-datorn.

## <a name="prerequisites"></a>Förutsättningar

- En Azure-prenumeration

- Virtuellt Azure-nätverk med ExpressRoute-Gateway

<!-- - A standalone primary site. A hierarchy with a central administration site isn't currently supported. can comment this out because TP only supports a standalone primary!-->

- Ditt användar konto måste vara en Configuration Manager **Fullständig administratör** och ha administratörs behörighet på den primära plats servern.

- Om du vill lägga till en passiv server måste den primära platsen uppfylla [kraven på plats serverns hög tillgänglighet](../servers/deploy/configure/site-server-high-availability.md#prerequisites). Till exempel krävs ett [innehålls bibliotek för fjärrnätverket](../plan-design/hierarchy/the-content-library.md#bkmk_remote).

### <a name="required-azure-permissions"></a>Azure-behörigheter som krävs

Du behöver följande behörigheter i Azure när du kör verktyget:
<!--5789222-->
Microsoft. Resources/Subscriptions/resourceGroups/Read <br>
Microsoft. Resources/Subscriptions/resourceGroups/Write <br>
Microsoft. Resources/Deployments/Read <br>
Microsoft. Resources/Deployments/Write <br>
Microsoft. Resources/Deployments/validate/Action <br>
Microsoft. Compute/virtualMachines/Extensions/Read <br>
Microsoft. Compute/virtualMachines/tillägg/Skriv <br>
Microsoft. Compute/virtualMachines/Read <br>
Microsoft. Compute/virtualMachines/Write <br>
Microsoft. Network/virtualNetworks/Read <br>
Microsoft.Network/virtualNetworks/subnets/read <br>
Microsoft.Network/virtualNetworks/subnets/join/action <br>
Microsoft. Network/networkInterfaces/Read <br>
Microsoft. Network/networkInterfaces/Write <br>
Microsoft. Network/networkInterfaces/JOIN/åtgärd <br>
Microsoft. Network/networkSecurityGroups/Write <br>
Microsoft. Network/networkSecurityGroups/Read <br>
Microsoft. Network/networkSecurityGroups/JOIN/åtgärd <br>
Microsoft. Storage/storageAccounts/Write <br>
Microsoft. Storage/storageAccounts/Read <br>
Microsoft. Storage/storageAccounts/listnycklar/åtgärd <br>
Microsoft. Storage/storageAccounts/listServiceSas/åtgärd <br>
Microsoft. Storage/storageAccounts/blobServices/containers/Write <br>
Microsoft. Storage/storageAccounts/blobServices/containers/Read <br>
Microsoft. nyckel valv/valv/distribution/åtgärd <br>
Microsoft. nyckel valv/valv/läsa <br>


Mer information om behörigheter och tilldelning av roller finns i [Hantera åtkomst till Azure-resurser med RBAC](/azure/role-based-access-control/role-assignments-portal).

## <a name="run-the-tool"></a>Kör verktyget

1. Logga in på den primära plats servern och kör följande verktyg i Configuration Manager installations katalog: `Cd.Latest\SMSSETUP\TOOLS\ExtendMigrateToAzure\ExtendMigrateToAzure.exe`

1. Granska informationen på fliken **Allmänt** och växla sedan till fliken **Azure-information** .

1. På fliken  **Azure information** väljer du din **Azure-miljö**och loggar sedan **in**.

    > [!TIP]
    > Du kan behöva lägga till `https://*.microsoft.com` i listan över betrodda webbplatser för att logga in korrekt.

    [![Fliken Azure-information i verktyget utöka och migrera](./media/3556022-azure-information-tab.png)](./media/3556022-azure-information-tab.png#lightbox)

1. När du har loggat in väljer du ditt **prenumerations-ID** och **virtuellt nätverk**. Verktyget visar bara nätverk med en ExpressRoute-Gateway.

## <a name="site-server-high-availability"></a>Hög tillgänglighet för plats Server

1. På fliken **plats Server hög tillgänglighet** väljer du **kontrol lera** för att utvärdera din webbplats beredskap.

    Om någon av kontrollerna inte fungerar väljer du **Mer information** för att ta reda på hur problemet kan åtgärdas. Mer information om dessa krav finns i [plats serverns hög tillgänglighet](../servers/deploy/configure/site-server-high-availability.md#prerequisites).

2. Om du vill utöka eller migrera plats servern till Azure väljer du **skapa en plats server i Azure**. Fyll sedan i följande fält:

    |Namn|Beskrivning|
    |---|---|
    |**Prenumeration**|Skrivskyddad. Visar prenumerationens namn och ID.|
    |**Resursgrupp**| Visar en lista över tillgängliga resurs grupper. Om du behöver skapa en ny resurs grupp använder du [Azure Portal](https://portal.azure.com)och kör sedan verktyget igen.|
    |**Plats**| Skrivskyddad. Bestäms av det virtuella nätverkets plats|
    |**Storlek på virtuell dator**|Välj en storlek som passar din arbets belastning. Microsoft rekommenderar **Standard_DS3_v2**.|
    |**Operativsystem**|Skrivskyddad. Verktyget använder Windows Server 2019.|
    |**Disktyp**|Skrivskyddad. Verktyget använder Premium SSD för bästa prestanda.|
    |**Virtuellt nätverk**|Skrivskyddad.|
    |**Undernät**|Välj det undernät som ska användas. Om du behöver skapa ett nytt undernät använder du [Azure Portal](https://portal.azure.com).|
    |**Dator namn**|Ange namnet på den virtuella datorn för den passiva plats servern i Azure. Det är samma namn som visas i [Azure Portal](https://portal.azure.com).|
    |**Lokalt administratörs användar namn**|Ange namnet på den lokala administrativa användaren som den virtuella Azure-datorn skapar innan den ansluter till domänen.|
    |**Lokalt administratörs lösen ord**|Lösen ordet för den lokala administrativa användaren. Skydda lösen ordet vid Azure-distribution genom att lagra lösen ordet som en hemlighet i [Azure Key Vault](/azure/key-vault/key-vault-overview). Använd sedan referensen här. Om det behövs skapar du en ny från [Azure Portal](https://portal.azure.com).|
    |**Domän-FQDN**|Det fullständigt kvalificerade domän namnet för den Active Directory domänen som ska anslutas. Som standard hämtar verktyget det här värdet från den aktuella datorn.|
    |**Domän användar namn**|Namnet på den domän användare som har behörighet att ansluta till domänen. Som standard använder verktyget namnet på den för tillfället inloggade användaren.|
    |**Domän lösen ord**|Lösen ordet för domän användaren att ansluta till domänen. Verktyget verifierar det när du har valt **Starta**. Skydda lösen ordet vid Azure-distribution genom att lagra lösen ordet som en hemlighet i [Azure Key Vault](/azure/key-vault/key-vault-overview). Använd sedan referensen här. Om det behövs skapar du en ny från [Azure Portal](https://portal.azure.com).|
    |**Domänens DNS-IP**|Används för att ansluta till domänen. Som standard använder verktyget den aktuella DNS-servern från den aktuella datorn.|
    |**Typ**|Skrivskyddad. Den visar *passiv plats Server* som typ.|

    > [!IMPORTANT]
    > Som standard är de virtuella datorerna inställda på **Nej** för **Använd befintlig Windows Server-licens**. Om du vill använda dina lokala Windows Server-licenser med Software Assurance konfigurerar du den här inställningen i [Azure Portal](https://portal.azure.com) när de virtuella datorerna har tillhandahållits. Mer information finns i [Azure Hybrid-förmån för Windows Server](/windows-server/get-started/azure-hybrid-benefit).

1. Starta etableringen av den virtuella Azure-datorn genom att välja **Start**. Om du vill övervaka distributions statusen växlar du till fliken **distributioner i Azure** i verktyget. Om du vill hämta den senaste statusen väljer du **Uppdatera distributions status**.

    > [!TIP]
    > Du kan också använda [Azure Portal](https://portal.azure.com) för att kontrol lera status, hitta fel och fastställa möjliga korrigeringar.

1. När distributionen är klar går du till dina SQL-servrar och beviljar behörigheter för den nya virtuella Azure-datorn. Mer information finns i [krav för hög tillgänglighet för plats Server](../servers/deploy/configure/site-server-high-availability.md#prerequisites).

1. Om du vill lägga till den virtuella Azure-datorn som en plats server i passivt läge väljer du **Lägg till plats server i passivt läge**.

1. När platsen lägger till plats servern i passivt läge visar fliken **plats Server hög tillgänglighet** statusen.

   [![Passiv plats Server har lagts till på fliken plats Server hög tillgänglighet](./media/3556022-site-server-passive-mode.png)](./media/3556022-site-server-passive-mode.png#lightbox)

1. Gå sedan till fliken [distributioner på Azure](#bkmk_deploy-azure) för att slutföra distributionen.

## <a name="site-database"></a>Platsdatabas

Verktyget har för närvarande inga aktiviteter för att migrera databasen från den lokala platsen till Azure. Du kan välja att flytta databasen från en lokal SQL Server till en Azure-SQL Server VM. I verktyget visas följande artiklar på fliken **plats databas** för att hjälpa:

- [Säkerhetskopiera och återställa databasen](../servers/manage/backup-and-recovery.md)
- [Konfigurera SQL Always on och Tillåt att data replikeras](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup)
- [Migrera en SQL-databas till en Azure-SQL Server VM](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)

## <a name="site-system-roles"></a>Platssystemroller

1. Växla till fliken **plats system roller** . Om du vill etablera en ny plats system roll med standardinställningarna väljer du **Skapa ny**. Du kan etablera roller som hanterings platsen, distributions platsen och program uppdaterings platsen. Alla roller är inte tillgängliga för närvarande i verktyget.

    [![Fliken plats system roller i verktyget utöka och migrera](./media/3556022-site-system-roles-tab.png)](./media/3556022-site-system-roles-tab.png#lightbox)

1. I etablerings fönstret fyller du i fälten för att etablera plats rollens virtuella dator i Azure. Dessa uppgifter liknar listan ovan för plats servern.

1. Starta etableringen av den virtuella Azure-datorn genom att välja **Start**. Om du vill övervaka distributions statusen växlar du till fliken **distributioner i Azure** i verktyget. Om du vill hämta den senaste statusen väljer du **Uppdatera distributions status**.

    > [!TIP]
    > Du kan också använda [Azure Portal](https://portal.azure.com) för att kontrol lera status, hitta fel och fastställa möjliga korrigeringar.

1. Upprepa processen för att lägga till fler plats system roller.

1. Gå sedan till fliken [distributioner på Azure](#bkmk_deploy-azure) för att slutföra distributionen.

1. När distributionen är klar går du till Configuration Manager-konsolen för att göra ytterligare ändringar i plats rollen.

## <a name="deployments-in-azure"></a><a name="bkmk_deploy-azure"></a> Distributioner i Azure

1. När Azure har skapat den virtuella datorn växlar du till fliken **distributioner på Azure** i verktyget. Välj **distribuera** om du vill konfigurera rollen med standardinställningarna.

1. Välj **Kör** för att starta PowerShell-skriptet.

    [![Distribuera plats roller genom att köra det genererade PowerShell-skriptet](./media/3556022-run-powershell-script-deployment.png)](./media/3556022-run-powershell-script-deployment.png#lightbox)

1. Upprepa den här processen om du vill konfigurera fler roller.

## <a name="add-site-roles-to-an-existing-virtual-machine-deployment"></a><a name="bkmk_add_role"></a> Lägg till plats roller i en befintlig distribution av virtuell dator
<!--5665775, 6307931-->
Från och med Configuration Manager version 2002 har verktyget utöka och migrera lokal plats till Microsoft Azure stöd för etablering av flera plats system roller på en enda virtuell Azure-dator. Du kan lägga till plats system roller när den första distributionen av virtuella Azure-datorer har slutförts. Gör så här om du vill lägga till en ny roll till en befintlig virtuell dator:
1. På fliken **distributioner på Azure** klickar du på en distribution av virtuell dator som har statusen **slutförd** .
1. Klicka på knappen **Skapa nytt** för att lägga till ytterligare en roll till den virtuella datorn.


## <a name="next-steps"></a>Nästa steg

Granska ändringarna i [Azure Portal](https://portal.azure.com)