---
title: Använda Windows Defender Application Control på HoloLens 2-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Konfigurera CSP:n Windows Defender Application Control (WDAC) för att tillåta eller blockera appar från att öppnas på HoloLens 2-enheter i Microsoft Intune. Använd PowerShell och en anpassad konfigurationsprofil.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6d2d19b03253725bde7b0ee27f3c94b42adb5917
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990127"
---
# <a name="use-wdac-and-windows-powershell-to-allow-or-blocks-apps-on-hololens-2-devices-with-microsoft-intune"></a>Använda WDAC och Windows PowerShell för att tillåta eller blockera appar på HoloLens 2-enheter med Microsoft Intune

Microsoft HoloLens 2-enheter har stöd för [CSP:n Windows Defender Application Control (WDAC)](https://docs.microsoft.com/windows/client-management/mdm/applicationcontrol-csp) som ersätter [CSP:n AppLocker](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp).

Med Windows PowerShell och Microsoft Intune kan du använda CSP:n WDAC för att tillåta eller blockera vissa appar från att öppnas på Microsoft HoloLens 2-enheter. Du kanske till exempel vill tillåta eller förhindra att Cortana-appen öppnas på HoloLens 2-enheter i organisationen.

Den här funktionen gäller för:

- HoloLens 2-enheter som kör Windows Holographic for Business

CSP:n WDAC baseras på [funktionen Windows Defender Application Control (WDAC)](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control). Du kan också [använda flera WDAC-policyer](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/deploy-multiple-windows-defender-application-control-policies).

Den här artikeln visar hur du:

1. Använder Windows PowerShell till att skapa WDAC-policyer.
2. Använder Windows PowerShell till att konvertera WDAC-policyinställningar till XML, uppdaterar XML-filen och sedan konverterar XML-filen till en binärfil.
3. Skapa en [anpassad enhetskonfigurationsprofil](custom-settings-windows-holographic.md) i Microsoft Intune, lägg till den här binära WDAC-policyfilen och tillämpa policyn på dina HoloLens 2-enheter.

Du måste skapa en anpassad konfigurationsprofil i Intune för att använda CSP:n Windows Defender Application Control (WDAC). 

Använd stegen i den här artikeln som mall för att tillåta eller neka specifika appar från att öppnas på HoloLens 2-enheter.

## <a name="prerequisites"></a>Krav

- Vara bekant med Windows PowerShell.
- Logga in i Intune som medlem i:

  - Intune-rollen som **Policy- och profilansvarig** eller **Rolladministratör i Intune**

    ELLER

  - Azure AD-rollen **Global administratör** eller **Intune-tjänstadministratör**

  Mer information finns i [Rollbaserad åtkomstkontroll (RBAC) med Intune](../fundamentals/role-based-access-control.md).

- Skapa en användargrupp eller enhetsgrupp med dina HoloLens 2-enheter. Mer information finns i [Användargrupper jämfört med enhetsgrupper](device-profile-assign.md#user-groups-vs-device-groups).

## <a name="example"></a>Exempel

I det här exemplet används Windows PowerShell till att skapa en WDAC-policy (Windows Defender Application Control). Policyn förhindrar att vissa appar öppnas. Använd sedan Intune till att distribuera policyn till HoloLens 2-enheter.

1. Öppna appen **Windows PowerShell** på din stationära dator.
2. Hämta information om det installerade programpaketet på din stationära dator:

    ```powershell
    $package1 = Get-AppxPackage -name *<applicationname>*
    ```

    Ange till exempel:

    ```powershell
    $package1 = Get-AppxPackage -name *cortana*
    ```

    Bekräfta sedan att paketet har programattribut:

    ```powershell
    $package1
    ```

    Du ser attribut som liknar följande appinformation:

    ```powershell
    Name              : Microsoft.Windows.Cortana
    Publisher         : CN=Microsoft Windows, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
    Architecture      : Neutral
    ResourceId        : neutral
    Version           : 1.13.0.18362
    PackageFullName   : Microsoft.Windows.Cortana_1.13.0.18362_neutral_neutral_cw5n1h2txyewy
    InstallLocation   : C:\Windows\SystemApps\Microsoft.Windows.Cortana_cw5n1h2txyewy
    IsFramework       : False
    PackageFamilyName : Microsoft.Windows.Cortana_cw5n1h2txyewy
    PublisherId       : cw5n1h2txyewy
    IsResourcePackage : False
    IsBundle          : False
    IsDevelopmentMode : False
    NonRemovable      : True
    IsPartiallyStaged : False
    SignatureKind     : System
    Status            : Ok
    ```

3. Skapa en WDAC-policy och lägg till appaketet i regeln DENY:

    ```powershell
    $rule = New-CIPolicyRule -Package $package1 -Deny
    ```

4. Upprepa steg 2 och 3 för de andra program som du vill neka:

    ```powershell
    $rule += New-CIPolicyRule -Package $package<2..n> -Deny
    ```

    Ange till exempel:

    ```powershell
    $package2 = Get-AppxPackage -name *windowsstore*
    $rule += New-CIPolicyRule -Package $package<2..n>  -Deny
    ```

5. Konvertera WDAC-policyn till **newPolicy.xml**:

    ```powershell
    New-CIPolicy -rules $rule -f .\newPolicy.xml -UserPEs
    ```

    Om du vill rikta in dig mot alla versioner av en app ser du till att `PackageVersion="65535.65535.65535.65535"` finns i noden Deny i newPolicy.xml:

    ```xml
    <Deny ID="ID_DENY_D_1" FriendlyName="Microsoft.WindowsStore_8wekyb3d8bbwe FileRule" PackageFamilyName="Microsoft.WindowsStore_8wekyb3d8bbwe" PackageVersion="65535.65535.65535.65535" />
    ```

    Du kan använda följande versioner för `PackageFamilyNameRules`:

    - **Tillåt**: Ange `PackageVersion, 0.0.0.0`, vilket innebär ”Tillåt den här versionen och senare”.
    - **Deny**: Ange `PackageVersion, 65535.65535.65535.65535`, vilket innebär ”Neka den här versionen och tidigare”.

6. Sammanfoga **newPolicy.xml** med standardpolicyn i din stationära dator. Det här steget skapar filen **mergedPolicy.xml**. Tillåt till exempel att Windows-appar, WHQL-signerade drivrutiner och Store-signerade appar får köras:

    ```powershell
    Merge-CIPolicy -PolicyPaths .\newPolicy.xml,C:\Windows\Schemas\codeintegrity\examplepolicies\DefaultWindows_Audit.xml -o mergedPolicy.xml
    ```

7. Inaktivera regeln **Audit mode** i **mergedPolicy.xml**. När du sammanfogar aktiveras granskningsläget automatiskt:

    ```powershell
    Set-RuleOption -o 3 -Delete .\mergedPolicy.xml
    ```

8. Aktivera regeln **InvalidateEAs on a reboot** i **mergedPolicy.xml**:

    ```powershell
    Set-RuleOption -o 15 .\mergedPolicy.xml
    ```

    Mer information om de här reglerna finns i [Förstå regler för WDAC-policyer och filer](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create).

9. Konvertera **mergedPolicy.xml** till binärformat. Det här steget skapar **compiledPolicy.bin**. Sedan lägger du till binärfilen **compiledPolicy.bin** i Intune.

    ```powershell
    ConvertFrom-CIPolicy .\mergedPolicy.xml .\compiledPolicy.bin
    ```

10. Skapa den anpassade enhetskonfigurationsprofilen i Intune:

    1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) skapar du en anpassad enhetskonfigurationsprofil för Windows 10.

        De olika stegen beskrivs i [Skapa en anpassad profil med OMA-URI i Intune](custom-settings-configure.md).

    2. När du skapar profilen anger du följande inställningar:

      - **OMA-URI**: Ange `./Vendor/MSFT/ApplicationControl/Policies/<PolicyGUID>`. Ersätt `<PolicyGUID>` med noden PolicyTypeID i filen **mergedPolicy.xml** som du skapade i steg 6.

        Med vårt exempel anger du `./Vendor/MSFT/ApplicationControl/Policies/A244370E-44C9-4C06-B551-F6016E563076`.

        Policyns GUID **måste matcha** noden PolicyTypeID i filen **mergedPolicy.xml** (som du skapade i steg 6).

      - **Datatyp**: Ställ in som **Base64-fil**. Det konverterar automatiskt filen från binärformat till base64.
      - **Certifikatfil**: Ladda upp binärfilen **compiledPolicy.bin** (som du skapade i steg 9).

      Inställningarna ser ut ungefär som följande inställningar:

      :::image type="content" source="./media/custom-profile-hololens/custom-applicationcontrol-omauri.png" alt-text="Lägg till en anpassad OMA-URI för att konfigurera CSP:n ApplicationControl i Microsoft Intune.":::

11. När profilen är [tilldelad](device-profile-assign.md) till din HoloLens 2-grupp kontrollerar du profilens status. När profilen har tillämpats startar du om HoloLens 2-enheterna.

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

[Läs mer om anpassade profiler i Intune](custom-settings-configure.md).
