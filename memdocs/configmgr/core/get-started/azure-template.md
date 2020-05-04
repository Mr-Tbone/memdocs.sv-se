---
title: Skapa ett labb i Azure
titleSuffix: Configuration Manager
description: Automatisera skapandet av ett Configuration Manager Technical Preview-labb eller nuvarande gren utvärderings labb med Azure-mallar
ms.date: 07/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dd2a8b3bfb7c4b8af277616c7eaed329bc143bb7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711604"
---
# <a name="create-a-configuration-manager-lab-in-azure"></a>Skapa ett Configuration Manager labb i Azure

*Gäller för: Configuration Manager (Technical Preview Branch)*

<!--3556017-->

I den här guiden beskrivs hur du skapar en Configuration Manager lab-miljö i Microsoft Azure. Azure-mallar används för att förenkla och automatisera skapandet av ett labb med hjälp av Azure-resurser. Två Azure-mallar tillhandahålls: 

- Configuration Manager Technical Preview Azure-mallen installerar den senaste versionen av Configuration Manager Technical Preview-grenen.
- Configuration Manager aktuell gren Azure-mall installerar utvärderingen av den senaste versionen av Configuration Manager aktuella grenen. 

Mer information finns i [Configuration Manager på Azure](../understand/configuration-manager-on-azure.md).



## <a name="prerequisites"></a>Krav

Den här processen kräver en Azure-prenumeration där du kan skapa följande objekt: 
- Två Standard_B2s virtuella datorer för domän-och MP-& DP-roller.
- En Standard_B2ms virtuell dator för primär plats Server och SQL Database-Server.
- Standard_LRS lagrings konto

> [!Tip]  
> Se [pris Kalkylatorn för Azure](https://azure.microsoft.com/pricing/calculator/) för att hjälpa till att fastställa potentiella kostnader.  



## <a name="process"></a>Process

1. Gå till [Configuration Manager Technical Preview-mallen](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/) eller [Configuration Manager aktuella gren mal len](https://azure.microsoft.com/resources/templates/sccm-currentbranch/).  

2. Välj **distribuera till Azure**, så öppnas Azure Portal.  

3. Slutför Azure snabb starts mal len med följande information:

    - Grundläggande inställningar  

        - **Prenumeration**: namnet på den prenumeration som de virtuella datorerna ska skapas i  

        - **Resurs grupp**: Välj en resurs grupp som ska användas för dessa virtuella datorer  

        - **Plats**: Välj ett Azure-datacenter som ska vara värd för den här labb miljön  

    - Inställningar  

        - **Prefix**: datorernas namn. Mer information finns i [information om virtuella Azure-datorer](#azure-vm-info).  

        - **Admin-användar**namn: namnet på en användare på de virtuella datorerna med administratörs behörighet. Du använder den här användaren för att logga in på de virtuella datorerna.  

        - **Administratörs lösen ord**: lösen ordet måste uppfylla Azures komplexitets krav. Mer information finns i [adminPassword](https://docs.microsoft.com/rest/api/compute/virtualmachines/createorupdate#osprofile).  

    > [!Important]  
    > Följande inställningar krävs av Azure. Använd standardvärdena. Ändra inte dessa värden.  
    > 
    > - plats för artefakter: platsen för skripten för den här mallen ** \_** <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - artefakt platsens SAS-token: sasToken krävs för att få åtkomst till artefakt platsen ** \_**  
    > 
    > - **Plats**: platsen för alla resurser

4. Läs de allmänna villkoren. Om du samtycker väljer du **Jag accepterar villkoren som anges ovan**. Välj sedan **köp** för att fortsätta. 

Azure validerar inställningarna och påbörjar sedan distributionen. Kontrol lera distributionens status i Azure Portal. 

> [!NOTE]
> Processen kan ta 2-4 timmar. Även om Azure Portal visar att distributionen lyckades, fortsätter konfigurations skripten att köras. Starta inte om de virtuella datorerna under processen.

Om du vill se status för konfigurations skripten ansluter du `<prefix>PS1` till servern och visar följande fil: `%windir%\TEMP\ProvisionScript\PS1.json`. Om du ser alla steg som slutförda utförs processen.

För att ansluta till de virtuella datorerna får du först från Azure Portal de offentliga IP-adresserna för varje virtuell dator. När du ansluter till den virtuella datorn är `contoso.com`domän namnet. Använd de autentiseringsuppgifter som du angav i distributions mal len. Mer information finns i [så här ansluter du och loggar in på en virtuell Azure-dator som kör Windows](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon).



## <a name="azure-vm-info"></a>Information om virtuell Azure-dator

Alla tre virtuella datorer har följande specifikationer:
- 150 GB disk utrymme
- Både en offentlig och en privat IP-adress. De offentliga IP-adresserna finns i en nätverks säkerhets grupp som endast tillåter fjärr skrivbords anslutningar på TCP-port 3389. 

Prefixet som du angav i distributions mal len är prefixet för den virtuella datorns namn. Om du till exempel anger "contoso" som prefix är `contosoDC`domänkontrollantens dator namn.


### `<prefix>DC01`

- Active Directory-domänkontrollant
- Standard_B2s, som har två CPU och 4 GB minne
- Windows Server 2019 Data Center Edition

#### <a name="windows-features-and-roles"></a>Windows-funktioner och Windows-roller
- Active Directory Domain Services (lägger till)
- .NET
- RDC (Remote Differential Compression)


### `<prefix>PS01`

- Standard_B2ms, som har två CPU och 8 GB minne
- Windows Server 2016 Data Center Edition
- SQL Server
- Windows 10 ADK med Windows PE 
- Configuration Manager primär plats

#### <a name="windows-features-and-roles"></a>Windows-funktioner och Windows-roller
- .NET
- RDC (Remote Differential Compression) 
- IIS (Internet Information Service)


### `<prefix>DPMP01`

- Standard_B2s, som har två CPU och 4 GB minne
- Windows Server 2019 Data Center Edition
- Distributionsplats
- Hanteringsplats

#### <a name="windows-features-and-roles"></a>Windows-funktioner och Windows-roller
- .NET
- RDC (Remote Differential Compression) 
- IIS (Internet Information Service)
- BITS (Background Intelligent Transfer Service)

### `<prefix>CL01`

- Endast för Configuration Manager aktuella gren utvärderings mallen
- Windows 10
- Configuration Manager-klient
