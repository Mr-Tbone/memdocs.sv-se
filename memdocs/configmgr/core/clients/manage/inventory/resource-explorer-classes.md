---
title: Resursläsaren standard lager klasser
titleSuffix: Configuration Manager
description: Visar de klasser som visas i Resursläsaren
ms.date: 11/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d333f4c-0f85-4278-b421-064cf01529a5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 81cf8e1779e072d3eee6a5ed7080b6a63fd07451
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710736"
---
# <a name="resource-explorer-default-inventory-classes"></a>Resursläsaren standard lager klasser

*Gäller för: Configuration Manager (aktuell gren)*

I den här artikeln beskrivs standard inventerings klasserna i Resursläsaren.

Detta är standard inventerings klasserna:

## <a name="1394-controller"></a>1394-styrenhet

Namnrymd: root\cimv2

klass Win32_1394Controller


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- Nollängd Under text

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- Nollängd Tillverkare

- UInt32 MaxNumberControlled

- Nollängd Namn

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- UInt16 ProtocolSupported

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName

- DateTime TimeOfLastReset



## <a name="account-sid"></a>Konto-SID

Namnrymd: root\cimv2

klass Win32_AccountSID

- Nollängd Brevpost

- Nollängd Inställningen



## <a name="activesync-service"></a>ActiveSync-tjänst

Namnrymd: root\SmsDm

klass SMS_ActiveSyncService


- UInt32 Major version

- UInt32 MinorVersion

- Nollängd LastSyncTime



## <a name="amt-agent"></a>AMT-agent

Namnrymd: root\cimv2\sms

klass SMS_AMTObject


- UInt32 DeviceID

- Nollängd Bel

- Nollängd AMTApps

- Nollängd BiosVersion

- Nollängd BuildNumber

- Nollängd Utvecklingsverktyget

- Nollängd LegacyMode

- Nollängd Netstack

- UInt32 ProvisionMode

- UInt32 ProvisionState

- Nollängd RecoveryBuildNum

- Nollängd RecoveryVersion

- Nollängd SKU

- UInt32 TLSMode

- Nollängd Nyttolast

- UInt32 ZTCEnabled



## <a name="appv-client-application"></a>AppV-klientprogram

Namnrymd: root\AppV

klass AppvClientApplication


- Nollängd ApplicationId

- Nollängd PackageId

- Nollängd PackageVersionId

- Booleskt EnabledForUser

- Booleskt EnabledGlobally

- Nollängd Namn

- Nollängd TargetPath

- Nollängd 2.0.1



## <a name="appv-client-package"></a>AppV-klient paket

Namnrymd: root\AppV

klass AppvClientPackage


- Nollängd PackageId

- Nollängd VersionId

- Nollängd Till gångar []

- Nollängd DeploymentMachineData

- Nollängd DeploymentUserData

- Booleskt HasAssetIntelligence

- Booleskt Någon

- Booleskt IsPublishedGlobally

- Booleskt IsPublishedToUser

- Nollängd Namn

- UInt64 PackageSize

- Nollängd Sökväg

- UInt16 PercentLoaded

- Nollängd UserConfigurationData

- Nollängd 2.0.1



## <a name="autostart-software"></a>Autostarta program vara

Namnrymd: root\cimv2\sms

klass SMS_AutoStartSoftware


- Nollängd FilePropertiesHash

- Nollängd BinFileVersion

- Nollängd BinProductVersion

- Nollängd Beteckning

- Nollängd Sökväg

- Nollängd FilePropertiesHashEx

- Nollängd FileVersion

- Nollängd Sökvägen

- Nollängd Momsproduktbokföringsmallar

- Nollängd ProductVersion

- Nollängd Förläggare

- Nollängd Startuptype tjänst

- Nollängd StartupValue



## <a name="baseboard"></a>BaseBoard

Namnrymd: root\cimv2

klass Win32_BaseBoard


- Nollängd Taggredigerare

- Nollängd Under text

- Nollängd ConfigOptions[]

- Nollängd Beteckning

- Booleskt HostingBoard

- Booleskt HotSwappable

- DateTime InstallDate

- Nollängd Tillverkare

- Nollängd Förlag

- Nollängd Namn

- Nollängd OtherIdentifyingInfo

- Nollängd PartNumber

- Booleskt PoweredOn

- Nollängd Momsproduktbokföringsmallar

- Booleskt Flyttbar

- Booleskt Replaceable

- Nollängd RequirementsDescription

- Booleskt RequiresDaughterBoard

- Nollängd SerialNumber

- Nollängd SKU

- Nollängd SlotLayout

- Booleskt SpecialRequirements

- Nollängd Statusfältet

- Nollängd 2.0.1



## <a name="battery"></a>Batteri

Namnrymd: root\cimv2

klass Win32_Battery


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- UInt16 BatteryStatus

- Nollängd Under text

- UInt16 Kemiska

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- UInt32 DesignCapacity

- UInt64 DesignVoltage

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- UInt16 EstimatedChargeRemaining

- UInt32 EstimatedRunTime

- UInt32 ExpectedLife

- UInt32 FullChargeCapacity

- DateTime InstallDate

- UInt32 LastErrorCode

- UInt32 MaxRechargeTime

- Nollängd Namn

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- Nollängd SmartBatteryVersion

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName

- UInt32 TimeOnBattery

- UInt32 TimeToFullCharge



## <a name="bitlocker"></a>BitLocker

Namnrymd: root\cimv2\security\MicrosoftVolumeEncryption

klass Win32_EncryptableVolume


- Nollängd DeviceID

- Nollängd DriveLetter

- Nollängd PersistentVolumeID

- UInt32 ProtectionStatus



## <a name="bitlocker-encryption-details"></a>Information om BitLocker-kryptering

Namnrymd: root\cimv2

klass Win32_BitLockerEncryptionDetails


- Nollängd BitlockerPersistentVolumeId

- (SInt32) Kompabilitet

- (SInt32) ConversionStatus

- Nollängd DeviceId

- Nollängd DriveLetter

- (SInt32) EncryptionMethod

- Nollängd EnforcePolicyDate

- Booleskt IsAutoUnlockEnabled

- (SInt32) KeyProtectorTypes[]

- Nollängd MbamPersistentVolumeId

- (SInt32) MbamVolumeType

- Nollängd NoncomplianceDetectedDate

- (SInt32) ProtectionStatus

- (SInt32) ReasonsForNonCompliance[]



## <a name="bitlocker-policy"></a>BitLocker-princip

Namnrymd: root\cimv2

klass Win32Reg_MBAMPolicy


- Nollängd EncodedComputerName

- UInt32 EncryptionMethod

- UInt32 FixedDataDriveAutoUnlock

- UInt32 FixedDataDriveEncryption

- UInt32 FixedDataDrivePassphrase

- Nollängd KeyName

- Nollängd LastConsoleUser

- UInt32 MBAMMachineError

- UInt32 MBAMPolicyEnforced

- UInt32 OsDriveEncryption

- UInt32 OsDriveProtector

- DateTime UserExemptionDate



## <a name="boot-configuration"></a>Start konfiguration

Namnrymd: root\cimv2

klass Win32_BootConfiguration


- Nollängd Namn

- Nollängd BootDirectory

- Nollängd ConfigurationPath

- Nollängd Beteckning

- Nollängd LastDrive

- Nollängd ScratchDirectory

- Nollängd SettingID

- Nollängd TempDirectory



## <a name="browser-helper-object"></a>Webb läsar hjälp objekt

Namnrymd: root\cimv2\sms

klass SMS_BrowserHelperObject


- Nollängd FilePropertiesHash

- Nollängd BinFileVersion

- Nollängd BinProductVersion

- Nollängd N

- Nollängd Beteckning

- Nollängd Sökväg

- Nollängd FilePropertiesHashEx

- Nollängd FileVersion

- Nollängd Momsproduktbokföringsmallar

- Nollängd ProductVersion

- Nollängd Förläggare

- Nollängd 2.0.1



## <a name="ccm_rax"></a>CCM_RAX

Namnrymd: root\ccm\cimodels

klass CCM_RAXInfo


- Nollängd Undanta

- Nollängd FeedURL

- Nollängd UserSID



## <a name="cd-rom"></a>CD-ROM

Namnrymd: root\cimv2

klass Win32_CDROMDrive


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- UInt16 Funktioner []

- Nollängd CapabilityDescriptions[]

- Nollängd Under text

- Nollängd CompressionMethod

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- UInt64 DefaultBlockSize

- Nollängd Beteckning

- Nollängd Kombinationsenhet

- Booleskt DriveIntegrity

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- Nollängd ErrorMethodology

- UInt16 FileSystemFlags

- UInt32 FileSystemFlagsEx

- Nollängd IDENTITET

- DateTime InstallDate

- UInt32 LastErrorCode

- Nollängd Tillverkare

- UInt64 MaxBlockSize

- UInt32 MaximumComponentLength

- UInt64 MaxMediaSize

- Booleskt MediaLoaded

- Nollängd MediaType

- UInt64 MinBlockSize

- Nollängd Namn

- Booleskt NeedsCleaning

- UInt32 NumberOfMediaSupported

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- Nollängd RevisionLevel

- UInt32 SCSIBus

- UInt16 SCSILogicalUnit

- UInt16 SCSIPort

- UInt16 SCSITargetId

- UInt64 Ändra

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName

- Nollängd Volym

- Nollängd VolumeSerialNumber



## <a name="client-events"></a>Klient händelser

Namnrymd: root\ccm\invagt

klass ClientEvents


- Nollängd EventName

- UInt16 Reparationer



## <a name="computer-system"></a>Datorsystem

Namnrymd: root\cimv2

klass Win32_ComputerSystem


- Nollängd Namn

- UInt16 AdminPasswordStatus

- Booleskt AutomaticResetBootOption

- Booleskt AutomaticResetCapability

- UInt16 BootOptionOnLimit

- UInt16 BootOptionOnWatchDog

- Booleskt BootROMSupported

- Nollängd BootupState

- Nollängd Under text

- UInt16 ChassisBootupState

- (SInt16) CurrentTimeZone

- Booleskt DaylightInEffect

- Nollängd Beteckning

- Nollängd Domänsuffix

- UInt16 DomainRole

- UInt16 FrontPanelResetStatus

- Booleskt InfraredSupported

- Nollängd InitialLoadInfo[]

- DateTime InstallDate

- UInt16 KeyboardPasswordStatus

- Nollängd LastLoadInfo

- Nollängd Tillverkare

- Nollängd Förlag

- Nollängd NameFormat

- Booleskt NetworkServerModeEnabled

- UInt32 NumberOfProcessors

- Nollängd OEMLogoBitmap

- Nollängd OEMStringArray[]

- (SInt64) PauseAfterReset

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- UInt16 PowerOnPasswordStatus

- UInt16 PowerState

- UInt16 PowerSupplyState

- Nollängd PrimaryOwnerContact

- Nollängd PrimaryOwnerName

- UInt16 ResetCapability

- (SInt16) ResetCount

- (SInt16) ResetLimit

- Nollängd Roller []

- Nollängd Statusfältet

- Nollängd SupportContactDescription[]

- UInt16 SystemStartupDelay

- Nollängd SystemStartupOptions[]

- (UInt8) SystemStartupSetting

- Nollängd SystemType

- UInt16 ThermalState

- UInt64 TotalPhysicalMemory

- Nollängd Användar

- UInt16 WakeUpType



## <a name="computer-system-ex"></a>Dator system ex

Namnrymd: root\cimv2

klass CCM_ComputerSystemExtended


- Nollängd Namn

- UInt16 PCSystemType



## <a name="computer-system-product"></a>Dator System produkt

Namnrymd: root\cimv2

klass Win32_ComputerSystemProduct


- Nollängd IdentifyingNumber

- Nollängd Namn

- Nollängd 2.0.1

- Nollängd Under text

- Nollängd Beteckning

- Nollängd SKUNumber

- Nollängd UUID

- Nollängd Leverantörsspecifika



## <a name="sms-advanced-client-ports"></a>SMS Avancerad klient-portar

Namnrymd: root\cimv2

klass Win32Reg_SMSAdvancedClientPorts


- Nollängd InstanceKey

- UInt32 HttpsPortName

- UInt32 PortName



## <a name="sms-advanced-client-ssl-configurations"></a>SSL-konfigurationer för SMS Avancerad klient

Namnrymd: root\cimv2

klass Win32Reg_SMSAdvancedClientSSLConfiguration


- Nollängd InstanceKey

- Nollängd CertificateSelectionCriteria

- Nollängd CertificateStore

- UInt32 ClientAlwaysOnInternet

- UInt32 HttpsStateFlags

- Nollängd InternetMPHostName

- UInt32 SelectFirstCertificate



## <a name="sms-advanced-client-state"></a>Status för SMS-Avancerad klient

Namnrymd: root\ccm

klass CCM_InstalledComponent


- Nollängd Namn

- Nollängd DisplayName

- Nollängd 2.0.1



## <a name="connected-device"></a>Ansluten enhet

Namnrymd: root\SmsDm

klass SMS_ActiveSyncConnectedDevice


- Nollängd DeviceOEMInfo

- Nollängd DeviceType

- Nollängd OS_Major

- Nollängd OS_Minor

- Nollängd OS_Platform

- Nollängd ProcessorArchitecture

- Nollängd ProcessorLevel

- Nollängd ProcessorRevision

- Nollängd InstalledClientID

- Nollängd InstalledClientServer

- Nollängd InstalledClientVersion

- Nollängd LastSyncTime

- Nollängd OS_AdditionalInfo

- Nollängd OS_Build



## <a name="sms_defaultbrowser"></a>SMS_DefaultBrowser

Namnrymd: root\cimv2\sms

klass SMS_DefaultBrowser


- Nollängd BrowserProgId



## <a name="desktop"></a>skrivbords-

Namnrymd: root\cimv2

klass Win32_Desktop


- Nollängd Namn

- UInt32 BorderWidth

- Nollängd Under text

- Booleskt CoolSwitch

- UInt32 CursorBlinkRate

- Nollängd Beteckning

- Booleskt DragFullWindows

- UInt32 GridGranularity

- UInt32 IconSpacing

- Nollängd IconTitleFaceName

- UInt32 IconTitleSize

- Booleskt IconTitleWrap

- Nollängd Ofta

- Booleskt ScreenSaverActive

- Nollängd ScreenSaverExecutable

- Booleskt ScreenSaverSecure

- UInt32 ScreenSaverTimeout

- Nollängd SettingID

- Nollängd Bilder

- Booleskt WallpaperStretched

- Booleskt WallpaperTiled



## <a name="desktop-monitor"></a>Skriv bords skärm

Namnrymd: root\cimv2

klass Win32_DesktopMonitor


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- UInt32 Bredd

- Nollängd Under text

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- UInt16 DisplayType

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- DateTime InstallDate

- Booleskt IsLocked

- UInt32 LastErrorCode

- Nollängd MonitorManufacturer

- Nollängd MonitorType

- Nollängd Namn

- UInt32 PixelsPerXLogicalInch

- UInt32 PixelsPerYLogicalInch

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- UInt32 ScreenHeight

- UInt32 ScreenWidth

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName



## <a name="device-info"></a>Enhets information

Namnrymd: reserverad

klass Device_Info


- Nollängd CertExpiry

- Nollängd Enhet

- Nollängd Tillverkare

- Nollängd Förlag

- Nollängd GRANSKNING



## <a name="mdm-devdetail"></a>MDM-DevDetail

Namnrymd: root\cimv2\mdm\dmmap

klass MDM_DevDetail_Ext01


- Nollängd Instans

- Nollängd ParentID

- Nollängd DeviceHardwareData

- Nollängd WLANMACAddress



## <a name="disk"></a>Disk

Namnrymd: root\cimv2

klass Win32_DiskDrive


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- UInt32 BytesPerSector

- UInt16 Funktioner []

- Nollängd CapabilityDescriptions[]

- Nollängd Under text

- Nollängd CompressionMethod

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- UInt64 DefaultBlockSize

- Nollängd Beteckning

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- Nollängd ErrorMethodology

- UInt32 Tabbindex

- DateTime InstallDate

- Nollängd InterfaceType

- UInt32 LastErrorCode

- Nollängd Tillverkare

- UInt64 MaxBlockSize

- UInt64 MaxMediaSize

- Booleskt MediaLoaded

- Nollängd MediaType

- UInt64 MinBlockSize

- Nollängd Förlag

- Nollängd Namn

- Booleskt NeedsCleaning

- UInt32 NumberOfMediaSupported

- UInt32 Partitioner

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- UInt32 SCSIBus

- UInt16 SCSILogicalUnit

- UInt16 SCSIPort

- UInt16 SCSITargetId

- UInt32 SectorsPerTrack

- UInt64 Ändra

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName

- UInt64 TotalCylinders

- UInt32 TotalHeads

- UInt64 TotalSectors

- UInt64 TotalTracks

- UInt32 TracksPerCylinder



## <a name="partition"></a>Partition

Namnrymd: root\cimv2

klass Win32_DiskPartition


- Nollängd DeviceID

- UInt16 Fjärråtkomstservrar

- UInt16 Offlinetillgänglighet

- UInt64 Storlek

- Booleskt Startbar

- Booleskt BootPartition

- Nollängd Under text

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- UInt32 DiskIndex

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- Nollängd ErrorMethodology

- UInt32 HiddenSectors

- UInt32 Tabbindex

- DateTime InstallDate

- UInt32 LastErrorCode

- Nollängd Namn

- UInt64 NumberOfBlocks

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- Booleskt Primär partition

- Nollängd Anledning

- Booleskt RewritePartition

- UInt64 Ändra

- UInt64 StartingOffset

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName

- Nollängd Bastyp



## <a name="dma"></a>DMA

Namnrymd: root\cimv2

klass Win32_DeviceMemoryAddress

- UInt64 StartingAddress

- Nollängd Under text

- Nollängd Beteckning

- UInt64 EndingAddress

- DateTime InstallDate

- Nollängd MemoryType

- Nollängd Namn

- Nollängd Statusfältet



## <a name="dma-channel"></a>DMA-kanal

Namnrymd: root\cimv2

klass Win32_DMAChannel


- UInt32 DMAChannel

- UInt16 AddressSize

- UInt16 Offlinetillgänglighet

- Booleskt BurstMode

- UInt16 ByteMode

- Nollängd Under text

- UInt16 ChannelTiming

- Nollängd Beteckning

- DateTime InstallDate

- UInt32 MaxTransferSize

- Nollängd Namn

- UInt32 Lastning

- Nollängd Statusfältet

- UInt16 TransferWidths[]

- UInt16 TypeCTiming

- UInt16 WordMode



## <a name="driver---vxd"></a>Driv rutin-VxD

Namnrymd: root\cimv2

klass Win32_DriverVXD


- Nollängd Namn

- Nollängd SoftwareElementID

- UInt16 SoftwareElementState

- UInt16 TargetOperatingSystem

- Nollängd 2.0.1

- Nollängd BuildNumber

- Nollängd Under text

- Nollängd Kod

- Nollängd Reglering

- Nollängd Beteckning

- Nollängd DeviceDescriptorBlock

- Nollängd IdentificationCode

- DateTime InstallDate

- Nollängd LanguageEdition

- Nollängd Tillverkare

- Nollängd OtherTargetOS

- Nollängd PM_API

- Nollängd SerialNumber

- UInt32 ServiceTableSize

- Nollängd Statusfältet

- Nollängd V86_API



## <a name="embedded-device-information"></a>Inbäddad enhets information

Namnrymd: root\cimv2\sms

klass CCM_EmbeddedDeviceInformation


- Nollängd DeviceType

- Nollängd Förlag

- Nollängd OEMName



## <a name="environment"></a>Miljö

Namnrymd: root\cimv2

klass Win32_Environment


- Nollängd Namn

- Nollängd Användar

- Nollängd Under text

- Nollängd Beteckning

- DateTime InstallDate

- Nollängd Statusfältet

- Booleskt SystemVariable

- Nollängd VariableValue



## <a name="firmware"></a>Inbyggd programvara

Namnrymd: root\cimv2\sms

klass SMS_Firmware


- Booleskt UEFI

- Booleskt SecureBoot



## <a name="usm-folder-redirection-health"></a>USM POLICYEGENSKAPER för mappomdirigering

Namnrymd: root\cimv2\sms

klass SMS_FolderRedirectionHealth


- Nollängd Mappnamn

- Nollängd SID

- (UInt8) HealthStatus

- DateTime LastSuccessfulSyncTime

- (UInt8) LastSyncStatus

- DateTime LastSyncTime

- Booleskt OfflineAccessEnabled

- Nollängd OfflineFileNameFolderGUID

- Booleskt Snart



## <a name="ide-controller"></a>IDE-styrenhet

Namnrymd: root\cimv2

klass Win32_IDEController


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- Nollängd Under text

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- Nollängd Tillverkare

- UInt32 MaxNumberControlled

- Nollängd Namn

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- UInt16 ProtocolSupported

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName

- DateTime TimeOfLastReset



## <a name="add-remove-programs-64"></a>Lägg till ta bort program (64)

Namnrymd: root\cimv2

klass Win32Reg_AddRemovePrograms64


- Nollängd ProdID

- Nollängd DisplayName

- Nollängd InstallDate

- Nollängd Förläggare

- Nollängd 2.0.1



## <a name="add-remove-programs"></a>Lägg till ta bort program

Namnrymd: root\cimv2

klass Win32Reg_AddRemovePrograms


- Nollängd ProdID

- Nollängd DisplayName

- Nollängd InstallDate

- Nollängd Förläggare

- Nollängd 2.0.1



## <a name="installed-executable"></a>Installerad körbar fil

Namnrymd: root\cimv2\sms

klass SMS_InstalledExecutable


- Nollängd ExecutableName

- Nollängd ProductCode

- Nollängd BinFileVersion

- Nollängd BinProductVersion

- Nollängd Beteckning

- Nollängd FilePropertiesHash

- Nollängd FilePropertiesHashEx

- UInt32 Storlek

- Nollängd FileVersion

- Booleskt HasPatchAdded

- Nollängd InstalledFilePath

- Booleskt IsSystemFile

- Booleskt IsVitalFile

- UInt32 Språk

- Nollängd Momsproduktbokföringsmallar

- Nollängd ProductVersion

- Nollängd Förläggare



## <a name="installed-software"></a>Installerad program vara

Namnrymd: root\cimv2\sms

klass SMS_InstalledSoftware


- Nollängd SoftwareCode

- Nollängd ARPDisplayName

- Nollängd ChannelCode

- Nollängd ChannelID

- Nollängd CM_DSLID

- Nollängd EvidenceSource

- DateTime InstallDate

- UInt32 InstallDirectoryValidation

- Nollängd InstalledLocation

- Nollängd InstallSource

- UInt32 InstallType

- UInt32 Språk

- Nollängd LocalPackage

- Nollängd MPC

- UInt32 OsComponent

- Nollängd PackageCode

- Nollängd ProductID

- Nollängd Namn

- Nollängd ProductVersion

- Nollängd Förläggare

- Nollängd RegisteredUser

- Nollängd ServicePack

- Nollängd SoftwarePropertiesHash

- Nollängd SoftwarePropertiesHashEx

- Nollängd UninstallString

- Nollängd UpgradeCode

- UInt32 VersionMajor

- UInt32 VersionMinor



## <a name="irq-table"></a>IRQ-tabell

Namnrymd: root\cimv2

klass Win32_IRQResource


- UInt32 IRQNumber

- UInt16 Offlinetillgänglighet

- Nollängd Under text

- Nollängd Beteckning

- Booleskt All

- DateTime InstallDate

- Nollängd Namn

- Booleskt Delbart

- Nollängd Statusfältet

- UInt16 TriggerLevel

- UInt16 TriggerType

- UInt32 Vektor



## <a name="keyboard"></a>Tangentbord

Namnrymd: root\cimv2

klass Win32_Keyboard


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- Nollängd Under text

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- DateTime InstallDate

- Booleskt IsLocked

- UInt32 LastErrorCode

- Nollängd Layoutändringar

- Nollängd Namn

- UInt16 NumberOfFunctionKeys

- UInt16 Ords

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName



## <a name="load-order-group"></a>Läs in beställnings grupp

Namnrymd: root\cimv2

klass Win32_LoadOrderGroup


- Nollängd Namn

- Nollängd Under text

- Nollängd Beteckning

- Booleskt DriverEnabled

- UInt32 GroupOrder

- DateTime InstallDate

- Nollängd Statusfältet



## <a name="logical-disk"></a>Logisk disk

Namnrymd: root\cimv2\sms

klass SMS_LogicalDisk


- Nollängd DeviceID

- UInt16 Fjärråtkomstservrar

- UInt16 Offlinetillgänglighet

- UInt64 Storlek

- Nollängd Under text

- Booleskt Okomprimera

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- UInt32 DriveType

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- Nollängd ErrorMethodology

- Nollängd Fil Systems

- UInt64 FreeSpace

- DateTime InstallDate

- UInt32 LastErrorCode

- UInt32 MaximumComponentLength

- UInt32 MediaType

- Nollängd Namn

- UInt64 NumberOfBlocks

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- Nollängd ProviderName

- Nollängd Anledning

- UInt64 Ändra

- Nollängd Statusfältet

- UInt16 StatusInfo

- Booleskt SupportsFileBasedCompression

- Nollängd SystemName

- Nollängd Volym

- Nollängd VolumeSerialNumber



## <a name="memory"></a>Minne

Namnrymd: root\cimv2

klass CCM_LogicalMemoryConfiguration


- Nollängd Namn

- UInt64 AvailableVirtualMemory

- UInt64 TotalPageFileSpace

- UInt64 TotalPhysicalMemory

- UInt64 TotalVirtualMemory



## <a name="device-bluetooth"></a>Bluetooth-enhet

Namnrymd: reserverad

klass Device_Bluetooth


- Booleskt Aktiva



## <a name="device-camera"></a>Enhets kamera

Namnrymd: reserverad

klass Device_Camera


- Booleskt Aktiva



## <a name="device-certificates"></a>Enhets certifikat

Namnrymd: reserverad

klass Device_Certificates


- Nollängd Begäran

- Nollängd Bastyp

- Nollängd IssuedBy

- Nollängd IssuedTo

- DateTime Fälten

- DateTime ValidTo



## <a name="device-client"></a>Enhets klient

Namnrymd: reserverad

klass Device_Client


- Booleskt DownloadWhenRoaming

- Booleskt SyncWhenRoaming



## <a name="device-client-agent-version"></a>Enhets klient agent version

Namnrymd: reserverad

klass Device_ClientAgentVersion


- Nollängd 2.0.1



## <a name="device-computer-system"></a>Enhetens dator system

Namnrymd: reserverad

klass Device_ComputerSystem


- Nollängd CellularTechnology

- Nollängd DeviceClientID

- Nollängd DeviceManufacturer

- Nollängd DeviceModel

- Nollängd DMVersion

- Nollängd FirmwareVersion

- Nollängd HardwareVersion

- Nollängd IMEI

- Nollängd IMSI

- (UInt8) IsActivationLockEnabled

- (UInt8) Jailbrokade

- Nollängd MEID

- Nollängd OEM

- Nollängd PhoneNumber

- Nollängd Plattforms typ

- UInt32 ProcessorArchitecture

- UInt32 ProcessorLevel

- UInt32 ProcessorRevision

- Nollängd Momsproduktbokföringsmallar

- Nollängd ProductVersion

- Nollängd SerialNumber

- Nollängd SoftwareVersion

- Nollängd SubscriberCarrierNetwork



## <a name="device-display"></a>Enhets visning

Namnrymd: reserverad

klass Device_Display


- UInt32 HorizontalResolution

- UInt64 NumberOfColors

- UInt32 VerticalResolution



## <a name="device-email"></a>E-postadress till enhet

Namnrymd: reserverad

klass Device_Email


- Nollängd OwnerEmailAddress

- Nollängd SyncDomain

- Nollängd SyncServer

- Nollängd SyncUser

- Nollängd Bastyp



## <a name="device-encryption"></a>Enhets kryptering

Namnrymd: reserverad

klass Device_Encryption


- UInt32 EmailEncryptionAlgorithm

- UInt32 EmailEncryptionNegotiation

- Booleskt EmailEncryptionRequired

- Booleskt EmailSigningAlgorithm

- Booleskt EmailSigningRequired

- Booleskt EncryptionCompliance

- Booleskt PhoneMemoryEncrypted

- Booleskt StorageCardEncrypted



## <a name="device-exchange"></a>Enhets utbyte

Namnrymd: reserverad

klass Device_Exchange


- Booleskt ConflictResolution

- (SInt32) HTMLEmailTruncation

- UInt32 Format

- UInt32 MaxCalendarAge

- UInt32 MaxEmailAge

- (SInt32) MaxMailFileAttachmentSize

- UInt32 OffPeakSyncFrequency

- UInt32 PeakDays

- Nollängd PeakEndTime

- Nollängd PeakStartTime

- UInt32 PeakSyncFrequency

- (SInt32) PlainTextEmailTruncation

- Booleskt SendEmailImmediately

- Booleskt SyncCalendar

- Booleskt SyncContacts

- Booleskt SyncEmail

- Booleskt SyncTasks

- Booleskt SyncWhenRoaming



## <a name="device-installed-applications"></a>Enhets installerade program

Namnrymd: reserverad

klass Device_InstalledApplications


- Nollängd Namn

- Nollängd 2.0.1



## <a name="device-irda"></a>Enhets-IrDA

Namnrymd: reserverad

klass Device_IrDA


- Booleskt Aktiva



## <a name="mobile-device-location"></a>Plats för mobil enhet

Namnrymd: reserverad

klass MDM_RemoteFind


- (Real32) Latitud

- (Real32) Long



## <a name="device-memory"></a>Enhets minne

Namnrymd: reserverad

klass Device_Memory


- UInt64 ProgramFree

- UInt64 ProgramTotal

- UInt64 RemovableStorageFree

- UInt64 RemovableStorageTotal

- UInt64 StorageFree

- UInt64 StorageTotal



## <a name="device-os-information"></a>Enhetens OS-information

Namnrymd: reserverad

klass Device_OSInformation


- Nollängd Språk

- Nollängd Systemet

- Nollängd 2.0.1



## <a name="device-password"></a>Enhets lösen ord

Namnrymd: reserverad

klass Device_Password


- Booleskt AllowRecoveryPassword

- UInt32 AutolockTimeout

- Booleskt Aktiva

- UInt32 Dag

- UInt32 Uppdatering

- UInt32 MaxAttemptsBeforeWipe

- UInt32 MinComplexChars

- UInt32 MinLength

- (UInt8) PasswordQuality

- UInt32 Bastyp



## <a name="device-policy"></a>Enhets princip

Namnrymd: reserverad

klass Device_Policy


- Nollängd Namn

- Booleskt Tillämpas



## <a name="device-power"></a>Enhets effekt

Namnrymd: reserverad

klass Device_Power


- UInt32 BacklightACTimeout

- UInt32 BacklightBatTimeout

- (SInt32) BackupPercent

- (SInt32) BatteryPercent



## <a name="mobile-device-security-status"></a>Säkerhets status för mobil enhet

Namnrymd: reserverad

klass MDM_SecurityStatus


- UInt32 HardwareEncryptionCaps

- (UInt8) PasscodeCompliant

- (UInt8) PasscodeCompliantWithProfiles

- (UInt8) PasscodePresent

- (UInt8) RequireEncryption



## <a name="device-windows-security-policy"></a>Enhetens Windows säkerhets princip

Namnrymd: reserverad

klass Device_WindowsSecurityPolicy


- UInt32 IDENTITET

- Nollängd Namn

- UInt32 Värde



## <a name="device-wlan"></a>Enhets-WLAN

Namnrymd: reserverad

klass Device_WLAN


- Booleskt Aktiva

- Nollängd EthernetMAC

- Nollängd WiFiMAC



## <a name="modem"></a>/Faxmodem

Namnrymd: root\cimv2

klass Win32_POTSModem


- Nollängd DeviceID

- UInt16 AnswerMode

- Nollängd AttachedTo

- UInt16 Offlinetillgänglighet

- Nollängd BlindOff

- Nollängd BlindOn

- Nollängd Under text

- Nollängd CompatibilityFlags

- UInt16 CompressionInfo

- Nollängd CompressionOff

- Nollängd CompressionOn

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd ConfigurationDialog

- Nollängd CountriesSupported[]

- Nollängd CountrySelected

- Nollängd CurrentPasswords[]

- Nollängd DCB

- Nollängd Objekt

- Nollängd Beteckning

- Nollängd DeviceLoader

- Nollängd DeviceType

- UInt16 DialType

- DateTime DriverDate

- Booleskt ErrorCleared

- Nollängd ErrorControlForced

- UInt16 ErrorControlInfo

- Nollängd ErrorControlOff

- Nollängd ErrorControlOn

- Nollängd ErrorDescription

- Nollängd FlowControlHard

- Nollängd FlowControlOff

- Nollängd FlowControlSoft

- Nollängd InactivityScale

- UInt32 InactivityTimeout

- UInt32 Tabbindex

- DateTime InstallDate

- UInt32 LastErrorCode

- UInt32 MaxBaudRateToPhone

- UInt32 MaxBaudRateToSerialPort

- UInt16 MaxNumberOfPasswords

- Nollängd Förlag

- Nollängd ModemInfPath

- Nollängd ModemInfSection

- Nollängd ModulationBell

- Nollängd ModulationCCITT

- UInt16 ModulationScheme

- Nollängd Namn

- Nollängd PNPDeviceID

- Nollängd PortSubClass

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- Nollängd Protokollprefixet

- Nollängd Egenskaperna

- Nollängd ProviderName

- Nollängd Baljväxt

- Nollängd Återställning

- Nollängd ResponsesKeyName

- (UInt8) RingsBeforeAnswer

- Nollängd SpeakerModeDial

- Nollängd SpeakerModeOff

- Nollängd SpeakerModeOn

- Nollängd SpeakerModeSetup

- Nollängd SpeakerVolumeHigh

- UInt16 SpeakerVolumeInfo

- Nollängd SpeakerVolumeLow

- Nollängd SpeakerVolumeMed

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd StringFormat

- Booleskt SupportsCallback

- Booleskt SupportsSynchronousConnect

- Nollängd SystemName

- Nollängd Avgränsare

- DateTime TimeOfLastReset

- Nollängd Ton

- Nollängd VoiceSwitchFeature



## <a name="motherboard"></a>Kort

Namnrymd: root\cimv2

klass Win32_MotherboardDevice


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- Nollängd Under text

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- Nollängd Namn

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- Nollängd PrimaryBusType

- Nollängd RevisionNumber

- Nollängd SecondaryBusType

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName


## <a name="nap-client"></a>NAP-klient

Namnrymd: root\Nap

klass NAP_Client


- (Sträng) namn

- (Sträng) Beskrivning

- (String) fixupURL

- (Boolean) napEnabled

- (String) napProtocolVersion

- (String) probationTime

- (UInt32) systemIsolationState



## <a name="nap-system-health-agent"></a>Hälso agent för NAP-system

Namnrymd: root\Nap

klass NAP_SystemHealthAgent


- UInt32 IDENTITET

- (Sträng) Beskrivning

- (UInt32) fixupState

- (Sträng) friendlyName

- (String) infoClsid

- (Boolean) isBound

- (UInt8) procent

- (String) registrationDate

- (Sträng) Lev

- (Sträng) version



## <a name="network-adapter"></a>Nätverkskort

Namnrymd: root\cimv2

klass Win32_NetworkAdapter


- Nollängd DeviceID

- Nollängd AdapterType

- Booleskt AutoSense

- UInt16 Offlinetillgänglighet

- Nollängd Under text

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- UInt32 Tabbindex

- DateTime InstallDate

- Booleskt Installeras

- UInt32 LastErrorCode

- Nollängd MACAddress

- Nollängd Tillverkare

- UInt32 MaxNumberControlled

- UInt64 MaxSpeed

- Nollängd Namn

- Nollängd NetworkAddresses []

- Nollängd PermanentAddress

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- Nollängd Namn

- Nollängd ServiceName

- UInt64 Hastighet

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName

- DateTime TimeOfLastReset



## <a name="network-adapter-configuration"></a>Konfiguration av nätverkskort

Namnrymd: root\cimv2

klass Win32_NetworkAdapterConfiguration


- UInt32 Tabbindex

- Booleskt ArpAlwaysSourceRoute

- Booleskt ArpUseEtherSNAP

- Nollängd Under text

- Nollängd DatabasePath

- Booleskt DeadGWDetectEnabled

- Nollängd DefaultIPGateway[]

- (UInt8) DefaultTOS

- (UInt8) DefaultTTL

- Nollängd Beteckning

- Booleskt DHCPEnabled

- DateTime DHCPLeaseExpires

- DateTime DHCPLeaseObtained

- Nollängd Server

- Nollängd DNSDomain

- Nollängd DNSDomainSuffixSearchOrder[]

- Booleskt DNSEnabledForWINSResolution

- Nollängd DNSHostName

- Nollängd DNSServerSearchOrder[]

- Booleskt DomainDNSRegistrationEnabled

- UInt32 Värdet

- Booleskt FullDNSRegistrationEnabled

- UInt16 GatewayCostMetric[]

- (UInt8) IGMPLevel

- Nollängd IPAddress []

- UInt32 IPConnectionMetric

- Booleskt IPEnabled

- Booleskt IPFilterSecurityEnabled

- Booleskt IPPortSecurityEnabled

- Nollängd IPSecPermitIPProtocols[]

- Nollängd IPSecPermitTCPPorts[]

- Nollängd IPSecPermitUDPPorts[]

- Nollängd IPSubnet []

- Booleskt IPUseZeroBroadcast

- Nollängd IPXAddress

- Booleskt IPXEnabled

- Nollängd IPXFrameType

- UInt32 IPXMediaType

- Nollängd IPXNetworkNumber[]

- Nollängd IPXVirtualNetNumber

- UInt32 KeepAliveInterval

- UInt32 KeepAliveTime

- Nollängd MACAddress

- UInt32 STORLEK

- UInt32 NumForwardPackets

- Booleskt PMTUBHDetectEnabled

- Booleskt PMTUDiscoveryEnabled

- Nollängd ServiceName

- Nollängd SettingID

- UInt32 TcpipNetbiosOptions

- UInt32 TcpMaxConnectRetransmissions

- UInt32 TcpMaxDataRetransmissions

- UInt32 TcpNumConnections

- Booleskt TcpUseRFC1122UrgentPointer

- UInt16 TcpWindowSize

- Booleskt WINSEnableLMHostsLookup

- Nollängd WINSHostLookupFile

- Nollängd WINSPrimaryServer

- Nollängd WINSScopeID

- Nollängd WINSSecondaryServer



## <a name="network-client"></a>Nätverks klient

Namnrymd: root\cimv2

klass Win32_NetworkClient


- Nollängd Namn

- Nollängd Under text

- Nollängd Beteckning

- DateTime InstallDate

- Nollängd Tillverkare

- Nollängd Statusfältet



## <a name="network-login-profile"></a>Nätverks inloggnings profil

Namnrymd: root\cimv2

klass Win32_NetworkLoginProfile


- Nollängd Namn

- DateTime AccountExpires

- UInt32 AuthorizationFlags

- UInt32 BadPasswordCount

- Nollängd Under text

- UInt32 Tabellen

- Nollängd Kommentar

- UInt32 CountryCode

- Nollängd Beteckning

- UInt32 Flagg

- Nollängd FullName

- Nollängd HomeDirectory

- Nollängd HomeDirectoryDrive

- DateTime LastLogoff

- DateTime LastLogon

- Nollängd LogonHours

- Nollängd LogonServer

- UInt64 MaximumStorage

- UInt32 NumberOfLogons

- Nollängd Komponentparametrar

- DateTime Lösen ord

- DateTime PasswordExpires

- UInt32 PrimaryGroupId

- UInt32 Höjd

- Nollängd Upphandlarprofil

- Nollängd ScriptPath

- Nollängd SettingID

- UInt32 UnitsPerWeek

- Nollängd UserComment

- UInt32 UserId

- Nollängd UserType

- Nollängd Arbets stationer



## <a name="nt-eventlog-file"></a>NT EventLog-fil

Namnrymd: root\cimv2

klass Win32_NTEventlogFile


- Nollängd Namn

- UInt32 AccessMask

- Booleskt Arkivattributet

- Nollängd Under text

- Booleskt Okomprimera

- Nollängd CompressionMethod

- DateTime CreationDate

- Nollängd Beteckning

- Nollängd Kombinationsenhet

- Nollängd EightDotThreeFileName

- Booleskt Krypterade

- Nollängd EncryptionMethod

- Nollängd Utöka

- Nollängd Sökväg

- UInt64 Storlek

- Nollängd Typen

- Nollängd FSName

- Booleskt Dölja

- DateTime InstallDate

- UInt64 InUseCount

- DateTime LastAccessed

- DateTime LastModified

- Nollängd LogfileName

- Nollängd Tillverkare

- UInt32 MaxFileSize

- UInt32 NumberOfRecords

- UInt32 OverwriteOutDated

- Nollängd OverWritePolicy

- Nollängd Sökväg

- Booleskt Lättare

- Nollängd Källor []

- Nollängd Statusfältet

- Booleskt Säker

- Nollängd 2.0.1

- Booleskt Skrivbar



## <a name="office365proplusconfigurations"></a>Office365ProPlusConfigurations

Namnrymd: root\cimv2

klass Office365ProPlusConfigurations


- Nollängd KeyName

- Nollängd AutoUpgrade

- Nollängd CCMManaged

- Nollängd CDNBaseUrl

- (String) cfgUpdateChannel

- Nollängd ClientCulture

- Nollängd ClientFolder

- Nollängd GPOChannel

- Nollängd GPOOfficeMgmtCOM

- Nollängd InstallationPath

- Nollängd LastScenario

- Nollängd LastScenarioResult

- Nollängd OfficeMgmtCOM

- Nollängd Systemet

- Nollängd SharedComputerLicensing

- Nollängd UpdateChannel

- Nollängd UpdatePath

- Nollängd UpdatesEnabled

- Nollängd UpdateUrl

- Nollängd VersionToReport



## <a name="office-addin"></a>Office-tillägg

Namnrymd: root\ccm\InvAgt

klass CCM_OfficeAddin


- Nollängd Designen

- Nollängd IDENTITET

- Nollängd OfficeApp

- Nollängd Bastyp

- UInt32 AverageLoadTimeInMilliseconds

- Nollängd N

- Nollängd CompanyName

- UInt32 CrashCount

- Nollängd Beteckning

- UInt32 ErrorCount

- Nollängd Sökväg

- UInt64 Storlek

- UInt32 FileTimestamp

- Nollängd FileVersion

- Nollängd FriendlyName

- Nollängd FriendlyNameHash

- Nollängd IdHash

- UInt32 LoadBehavior

- UInt32 LoadCount

- UInt32 LoadFailCount

- Nollängd Namn

- Nollängd ProductVersion



## <a name="office-client-metric"></a>Office-klientens mått

Namnrymd: root\ccm\InvAgt

klass CCM_OfficeClientMetric


- Nollängd OfficeApp

- UInt32 CompatibilityErrorCount

- UInt32 CrashedSessionCount

- UInt32 MacroCompileErrorCount

- UInt32 MacroRuntimeErrorCount

- UInt32 SessionCount



## <a name="office-device-summary"></a>Sammanfattning av Office-enhet

Namnrymd: root\ccm\InvAgt

klass CCM_OfficeDeviceSummary


- Booleskt IsProPlusInstalled

- Booleskt IsTelemetryEnabled



## <a name="office-document-metric"></a>Mått för Office-dokument

Namnrymd: root\ccm\InvAgt

klass CCM_OfficeDocumentMetric


- Nollängd OfficeApp

- UInt32 TotalCloudDocs

- UInt32 TotalLegacyDocs

- UInt32 TotalLocalDocs

- UInt32 TotalMacroDocs

- UInt32 TotalNonMacroDocs

- UInt32 TotalUncDocs



## <a name="office-document-solution"></a>Office-dokument lösning

Namnrymd: root\ccm\InvAgt

klass CCM_OfficeDocumentSolution


- Nollängd DocumentSolutionId

- Nollängd OfficeApp

- UInt32 CompatibilityErrorCount

- UInt32 CrashCount

- Nollängd ExampleFileName

- UInt32 LoadCount

- UInt32 LoadFailCount

- UInt32 MacroCompileErrorCount

- UInt32 MacroRuntimeErrorCount

- Nollängd Bastyp



## <a name="office-macro-error"></a>Fel i Office-makro

Namnrymd: root\ccm\InvAgt

klass CCM_OfficeMacroError


- Nollängd DocumentSolutionId

- UInt32 ErrorCode

- UInt32 Reparationer

- UInt64 LastOccurrence

- Nollängd Bastyp



## <a name="office-product-info"></a>Office-produkt information

Namnrymd: root\ccm\InvAgt

klass CCM_OfficeProductInfo


- Nollängd Namn

- Nollängd ProductVersion

- Nollängd Designen

- Nollängd Kanalig

- UInt32 IsProPlusInstalled

- Nollängd Språk

- Nollängd LicenseState



## <a name="office-vba-rule-violation"></a>Överträdelse av Office VBA-regel

Namnrymd: root\ccm\InvAgt

klass CCM_OfficeVbaRuleViolation


- UInt32 RuleId

- UInt32 FileCount

- Nollängd OfficeApp



## <a name="office-vbasummary"></a>Office-VbaSummary

Namnrymd: root\ccm\InvAgt

klass CCM_OfficeVbaScanResultsSummary


- UInt32 Fördefinierade

- UInt32 Design64

- UInt32 DuplicateVba

- Booleskt HasResults

- UInt32 HasVba

- UInt32 Otillgänglig

- UInt32 Åtgärder

- UInt32 Issues64

- UInt32 IssuesNone

- UInt32 IssuesNone64

- UInt32 Utelåsta

- UInt32 NoVba

- UInt32 Känslig

- UInt32 RemLimited

- UInt32 RemLimited64

- UInt32 RemSignificant

- UInt32 RemSignificant64

- UInt32 Resultat

- UInt32 Score64

- UInt32 Totalt

- UInt32 Signaturverifiering

- UInt32 Validation64



## <a name="operating-system"></a>Operativsystem

Namnrymd: root\cimv2

klass Win32_OperatingSystem


- Nollängd Namn

- Nollängd BootDevice

- Nollängd BuildNumber

- Nollängd BuildType

- Nollängd Under text

- Nollängd Kod

- Nollängd CountryCode

- Nollängd CSDVersion

- (SInt16) CurrentTimeZone

- Booleskt Förbigå

- Nollängd Beteckning

- Booleskt Distribuera

- (UInt8) ForegroundApplicationBoost

- UInt64 FreePhysicalMemory

- UInt64 FreeSpaceInPagingFiles

- UInt64 FreeVirtualMemory

- DateTime InstallDate

- DateTime LastBootUpTime

- DateTime LocalDateTime

- Nollängd Språk

- Nollängd Tillverkare

- UInt32 MaxNumberOfProcesses

- UInt64 MaxProcessMemorySize

- Nollängd MUILanguages[]

- UInt32 NumberOfLicensedUsers

- UInt32 NumberOfProcesses

- UInt32 NumberOfUsers

- UInt32 OperatingSystemSKU

- Nollängd Organisation

- Nollängd OSArchitecture

- UInt32 OSLanguage

- UInt32 OSProductSuite

- UInt16 OSType

- Nollängd OtherTypeDescription

- Nollängd PlusProductID

- Nollängd PlusVersionNumber

- Booleskt Huvud

- UInt32 ProductType

- Nollängd RegisteredUser

- Nollängd SerialNumber

- UInt16 ServicePackMajorVersion

- UInt16 ServicePackMinorVersion

- UInt64 SizeStoredInPagingFiles

- Nollängd Statusfältet

- Nollängd SystemDevice

- Nollängd SystemDirectory

- UInt64 TotalSwapSpaceSize

- UInt64 TotalVirtualMemorySize

- UInt64 TotalVisibleMemorySize

- Nollängd 2.0.1

- Nollängd WindowsDirectory



## <a name="operating-system-ex"></a>Operativ system ex

Namnrymd: root\cimv2

klass CCM_OperatingSystemExtended


- Nollängd Namn

- UInt32 SKU



## <a name="operating-system-recovery-configuration"></a>Konfiguration av operativ system återställning

Namnrymd: root\cimv2

klass Win32_OSRecoveryConfiguration


- Nollängd Namn

- Booleskt Autoomstart

- Nollängd Under text

- Nollängd DebugFilePath

- Nollängd Beteckning

- Booleskt KernelDumpOnly

- Booleskt OverwriteExistingDebugFile

- Booleskt SendAdminAlert

- Nollängd SettingID

- Booleskt WriteDebugInfo

- Booleskt WriteToSystemLog



## <a name="optional-feature"></a>Valfri funktion

Namnrymd: root\cimv2

klass Win32_OptionalFeature


- Nollängd Namn

- Nollängd Under text

- Nollängd Beteckning

- DateTime InstallDate

- UInt32 InstallState

- Nollängd Statusfältet



## <a name="page-file-setting"></a>Inställning av sid fil

Namnrymd: root\cimv2

klass Win32_PageFileSetting


- Nollängd Namn

- Nollängd Under text

- Nollängd Beteckning

- UInt32 InitialSize

- UInt32 MaximumSize

- Nollängd SettingID



## <a name="parallel-port"></a>Parallell port

Namnrymd: root\cimv2

klass Win32_ParallelPort


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- UInt16 Funktioner []

- Nollängd CapabilityDescriptions[]

- Nollängd Under text

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- Booleskt DMASupport

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- UInt32 MaxNumberControlled

- Nollängd Namn

- Booleskt OSAutoDiscovered

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- UInt16 ProtocolSupported

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName

- DateTime TimeOfLastReset



## <a name="bios"></a>BIOS

Namnrymd: root\cimv2

klass Win32_BIOS


- Nollängd Namn

- Nollängd SoftwareElementID

- UInt16 SoftwareElementState

- UInt16 TargetOperatingSystem

- Nollängd 2.0.1

- UInt16 BiosCharacteristics[]

- Nollängd BIOSVersion[]

- Nollängd BuildNumber

- Nollängd Under text

- Nollängd Kod

- Nollängd CurrentLanguage

- Nollängd Beteckning

- Nollängd IdentificationCode

- UInt16 InstallableLanguages

- DateTime InstallDate

- Nollängd LanguageEdition

- Nollängd ListOfLanguages[]

- Nollängd Tillverkare

- Nollängd OtherTargetOS

- Booleskt PrimaryBIOS

- DateTime ReleaseDate

- Nollängd SerialNumber

- Nollängd SMBIOSBIOSVersion

- UInt16 SMBIOSMajorVersion

- UInt16 SMBIOSMinorVersion

- Booleskt SMBIOSPresent

- Nollängd Statusfältet



## <a name="pcmcia-controller"></a>PCMCIA-styrenhet

Namnrymd: root\cimv2

klass Win32_PCMCIAController


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- Nollängd Under text

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- Nollängd Tillverkare

- UInt32 MaxNumberControlled

- Nollängd Namn

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- UInt16 ProtocolSupported

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName

- DateTime TimeOfLastReset



## <a name="physical-memory"></a>Fysiskt minne

Namnrymd: root\cimv2

klass Win32_PhysicalMemory


- Nollängd CreationClassName

- Nollängd Taggredigerare

- Nollängd BankLabel

- UInt64 Kapaciteten

- Nollängd Under text

- UInt16 DataWidth

- Nollängd Beteckning

- Nollängd DeviceLocator

- UInt16 FormFactor

- Booleskt HotSwappable

- DateTime InstallDate

- UInt16 InterleaveDataDepth

- UInt32 InterleavePosition

- Nollängd Tillverkare

- UInt16 MemoryType

- Nollängd Förlag

- Nollängd Namn

- Nollängd OtherIdentifyingInfo

- Nollängd PartNumber

- UInt32 PositionInRow

- Booleskt PoweredOn

- Booleskt Flyttbar

- Booleskt Replaceable

- Nollängd SerialNumber

- Nollängd SKU

- UInt32 Hastighet

- Nollängd Statusfältet

- UInt16 TotalWidth

- UInt16 TypeDetail

- Nollängd 2.0.1



## <a name="physicaldisk"></a>Fysisk

Namnrymd: root\microsoft\windows\storage

klass MSFT_PhysicalDisk


- Nollängd ObjectId

- UInt64 AllocatedSize

- UInt16 BusType

- UInt16 CannotPoolReason[]

- Booleskt CanPool

- Nollängd Beteckning

- Nollängd DeviceId

- UInt16 EnclosureNumber

- Nollängd FirmwareVersion

- Nollängd FriendlyName

- UInt16 HealthStatus

- Booleskt IsIndicationEnabled

- Booleskt IsPartial

- UInt64 LogicalSectorSize

- Nollängd Tillverkare

- UInt16 MediaType

- Nollängd Förlag

- UInt16 OperationalStatus []

- Nollängd OtherCannotPoolReasonDescription

- Nollängd PartNumber

- Nollängd PhysicalLocation

- UInt64 PhysicalSectorSize

- Nollängd SerialNumber

- UInt64 Ändra

- UInt16 SlotNumber

- Nollängd SoftwareVersion

- UInt32 SpindleSpeed

- UInt16 SupportedUsages[]

- Nollängd UniqueId

- UInt16 Användningsvyn



## <a name="pnp-device-driver"></a>DRIV RUTIN FÖR PNP-ENHET

Namnrymd: root\cimv2

klass Win32_PnpEntity


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- Nollängd Under text

- Nollängd ClassGuid

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd CreationClassName

- Nollängd Beteckning

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- Nollängd Tillverkare

- Nollängd Namn

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- Nollängd Telefonitjänstprovider

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemCreationClassName

- Nollängd SystemName



## <a name="pointing-device"></a>Pekdon

Namnrymd: root\cimv2

klass Win32_PointingDevice


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- Nollängd Under text

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- UInt16 DeviceInterface

- UInt32 DoubleSpeedThreshold

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- UInt16 Hand

- Nollängd HardwareType

- Nollängd InfFileName

- Nollängd InfSection

- DateTime InstallDate

- Booleskt IsLocked

- UInt32 LastErrorCode

- Nollängd Tillverkare

- Nollängd Namn

- (UInt8) NumberOfButtons

- Nollängd PNPDeviceID

- UInt16 PointingType

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- UInt32 QuadSpeedThreshold

- UInt32 Lösning

- UInt32 SampleRate

- Nollängd Statusfältet

- UInt16 StatusInfo

- UInt32 Synch

- Nollängd SystemName



## <a name="portable-battery"></a>Bärbart batteri

Namnrymd: root\cimv2

klass Win32_PortableBattery


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- UInt16 BatteryStatus

- UInt16 CapacityMultiplier

- Nollängd Under text

- UInt16 Kemiska

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- UInt32 DesignCapacity

- UInt64 DesignVoltage

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- UInt16 EstimatedChargeRemaining

- UInt32 EstimatedRunTime

- UInt32 ExpectedLife

- UInt32 FullChargeCapacity

- DateTime InstallDate

- UInt32 LastErrorCode

- Nollängd Sökvägen

- Nollängd ManufactureDate

- Nollängd Tillverkare

- UInt16 MaxBatteryError

- UInt32 MaxRechargeTime

- Nollängd Namn

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- Nollängd SmartBatteryVersion

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName

- UInt32 TimeOnBattery

- UInt32 TimeToFullCharge



## <a name="ports"></a>Portar

Namnrymd: root\cimv2

klass Win32_PortResource

- UInt64 StartingAddress

- Booleskt Aliasuppsättning

- Nollängd Under text

- Nollängd Beteckning

- UInt64 EndingAddress

- DateTime InstallDate

- Nollängd Namn

- Nollängd Statusfältet



## <a name="power-capabilities"></a>Energispar funktioner

Namnrymd: root\CCM\powermanagementagent

klass CCM_PwrMgmtSystemPowerCapabilities


- UInt32 PreferredPMProfile

- Booleskt ApmPresent

- Booleskt BatteriesAreShortTerm

- Booleskt FullWake

- Booleskt LidPresent

- Nollängd MinDeviceWakeState

- Booleskt ProcessorThrottle

- Nollängd RtcWake

- Booleskt SystemBatteriesPresent

- Booleskt SystemS1

- Booleskt SystemS2

- Booleskt SystemS3

- Booleskt SystemS4

- Booleskt SystemS5

- Booleskt UpsPresent

- Booleskt VideoDimPresent



## <a name="power-configurations"></a>Energi konfiguration

Namnrymd: root\CCM\policy\machine\actualconfig

klass CCM_PowerConfig


- Nollängd PowerConfigID

- UInt32 DurationInSec

- Nollängd NonPeakPowerPlan

- Nollängd NonPeakPowerPlanName

- Nollängd PeakPowerPlan

- Nollängd PeakPowerPlanName

- Nollängd PeakStartTimeHoursMin

- Nollängd WakeUpTimeHoursMin



## <a name="power-management-insomnia-reasons"></a>Orsaker till energispar funktioner i sömnlöshet

Namnrymd: root\CCM\powermanagementagent

klass CCM_PwrMgmtLastSuspendError


- Nollängd Beställaren

- Nollängd RequesterType

- Nollängd RequestType

- DateTime Tid

- UInt32 AdditionalCode

- Nollängd AdditionalInfo

- Nollängd RequesterInfo

- Booleskt UnknownRequester



## <a name="power-management-daily"></a>Energispar funktioner per dag

Namnrymd: root\CCM\powermanagementagent

klass CCM_PwrMgmtActualDay


- DateTime Ikraftträdande

- Nollängd TypeOfEvent

- (UInt32) hr0_1

- (UInt32) hr1_2

- (UInt32) hr10_11

- (UInt32) hr11_12

- (UInt32) hr12_13

- (UInt32) hr13_14

- (UInt32) hr14_15

- (UInt32) hr15_16

- (UInt32) hr16_17

- (UInt32) hr17_18

- (UInt32) hr18_19

- (UInt32) hr19_20

- (UInt32) hr2_3

- (UInt32) hr20_21

- (UInt32) hr21_22

- (UInt32) hr22_23

- (UInt32) hr23_0

- (UInt32) hr3_4

- (UInt32) hr4_5

- (UInt32) hr5_6

- (UInt32) hr6_7

- (UInt32) hr7_8

- (UInt32) hr8_9

- (UInt32) hr9_10

- (UInt32) minutesTotal



## <a name="power-client-opt-out-settings"></a>Inställningar för avanmälan av energi klient

Namnrymd: root\ccm\ClientSDK

klass CCM_PowerManagementClientOptoutSetting


- Booleskt AdminAllowOptout

- Booleskt EffectiveClientOptOut

- Booleskt IsClientOptOut



## <a name="power-management-monthly"></a>Energispar funktioner varje månad

Namnrymd: root\CCM\powermanagementagent

klass CCM_PwrMgmtMonth


- DateTime MonthStart

- (UInt32) minutesComputerActive

- (UInt32) minutesComputerOn

- (UInt32) minutesComputerShutdown

- (UInt32) minutesComputerSleep

- (UInt32) minutesMonitorOn

- (UInt32) minutesTotal

- Nollängd TypeOfEvent



## <a name="power-settings"></a>Energi inställningar

Namnrymd: root\cimv2\sms

klass SMS_PowerSettings


- Nollängd LED

- Nollängd ACSettingIndex

- Nollängd ACValue

- Nollängd DCSettingIndex

- Nollängd DCValue

- Nollängd Namn

- Nollängd UnitSpecifier



## <a name="print-jobs"></a>Utskrifts jobb

Namnrymd: root\cimv2

klass Win32_PrintJob


- Nollängd Namn

- Nollängd Under text

- Nollängd DataType

- Nollängd Beteckning

- Nollängd Handling

- Nollängd DriverName

- DateTime ElapsedTime

- Nollängd HostPrintQueue

- DateTime InstallDate

- UInt32 JobId

- Nollängd JobStatus

- Nollängd Varandra

- Nollängd Innehavare

- UInt32 PagesPrinted

- Nollängd Komponentparametrar

- Nollängd PrintProcessor

- UInt32 Förtur

- UInt32 Ändra

- DateTime /St

- Nollängd Statusfältet

- UInt32 StatusMask

- DateTime TimeSubmitted

- UInt32 TotalPages

- DateTime UntilTime



## <a name="printer-configuration"></a>Skrivar konfiguration

Namnrymd: root\cimv2

klass Win32_PrinterConfiguration


- Nollängd Namn

- UInt32 BitsPerPel

- Nollängd Under text

- Booleskt COLLATE

- UInt32 På

- UInt32 Innehåll

- Nollängd Beteckning

- Nollängd Enhet

- UInt32 DisplayFlags

- UInt32 DisplayFrequency

- UInt32 DitherType

- UInt32 DriverVersion

- Booleskt Duplex

- Nollängd FormName

- UInt32 HorizontalResolution

- UInt32 ICMIntent

- UInt32 ICMMethod

- UInt32 LogPixels

- UInt32 MediaType

- UInt32 Orientering

- UInt32 PaperLength

- Nollängd PaperSize

- UInt32 PaperWidth

- UInt32 PelsHeight

- UInt32 PelsWidth

- UInt32 PrintQuality

- UInt32 Skala

- Nollängd SettingID

- UInt32 SpecificationVersion

- UInt32 TTOption

- UInt32 VerticalResolution

- UInt32 XResolution

- UInt32 YResolution



## <a name="printer-device"></a>Skrivar enhet

Namnrymd: root\cimv2

klass Win32_Printer


- Nollängd DeviceID

- UInt32 Dokumentattribut

- UInt16 Offlinetillgänglighet

- UInt32 AveragePagesPerMinute

- UInt16 Funktioner []

- Nollängd CapabilityDescriptions[]

- Nollängd Under text

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- UInt32 DefaultPriority

- Nollängd Beteckning

- UInt16 DetectedErrorState

- Nollängd DriverName

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- UInt32 HorizontalResolution

- DateTime InstallDate

- UInt32 JobCountSinceLastReset

- UInt16 LanguagesSupported[]

- UInt32 LastErrorCode

- Nollängd Sökvägen

- Nollängd Namn

- UInt16 PaperSizesSupported[]

- Nollängd PNPDeviceID

- Nollängd PortName

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- Nollängd PrinterPaperNames[]

- UInt32 PrinterState

- UInt16 PrinterStatus

- Nollängd PrintJobDataType

- Nollängd PrintProcessor

- Nollängd SeparatorFile

- Nollängd Namnet

- Nollängd Resurs

- Booleskt SpoolEnabled

- DateTime /St

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName

- DateTime TimeOfLastReset

- DateTime UntilTime

- UInt32 VerticalResolution



## <a name="process"></a>Process

Namnrymd: root\cimv2

klass Win32_Process


- Nollängd Sköt

- Nollängd Under text

- DateTime CreationDate

- Nollängd Beteckning

- Nollängd ExecutablePath

- UInt16 ExecutionState

- UInt32 HandleCount

- DateTime InstallDate

- UInt64 KernelModeTime

- UInt32 MaximumWorkingSetSize

- UInt32 MinimumWorkingSetSize

- Nollängd Namn

- Nollängd OSName

- UInt64 OtherOperationCount

- UInt64 OtherTransferCount

- UInt32 PageFaults

- UInt32 PageFileUsage

- UInt32 ParentProcessId

- UInt32 PeakPageFileUsage

- UInt64 PeakVirtualSize

- UInt32 PeakWorkingSetSize

- UInt32 Förtur

- UInt64 PrivatePageCount

- UInt32 ProcessId

- UInt32 QuotaNonPagedPoolUsage

- UInt32 QuotaPagedPoolUsage

- UInt32 QuotaPeakNonPagedPoolUsage

- UInt32 QuotaPeakPagedPoolUsage

- UInt64 ReadOperationCount

- UInt64 ReadTransferCount

- UInt32 SessionId

- Nollängd Statusfältet

- DateTime TerminationDate

- UInt32 ThreadCount

- UInt64 UserModeTime

- UInt64 VirtualSize

- Nollängd WindowsVersion

- UInt64 WorkingSetSize

- UInt64 WriteOperationCount

- UInt64 WriteTransferCount



## <a name="processor"></a>Processor

Namnrymd: root\cimv2\sms

klass SMS_Processor


- Nollängd DeviceID

- UInt16 AddressWidth

- UInt16 Designen

- UInt16 Offlinetillgänglighet

- UInt16 BrandID

- Nollängd Under text

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd CPUHash

- Nollängd CPUKey

- UInt16 CpuStatus

- UInt32 CurrentClockSpeed

- UInt16 CurrentVoltage

- UInt16 DataWidth

- Nollängd Beteckning

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- UInt32 ExtClock

- UInt16 Föräldra

- DateTime InstallDate

- Booleskt Is64Bit

- Booleskt IsHyperthreadCapable

- Booleskt IsHyperthreadEnabled

- Booleskt IsMobile

- Booleskt IsTrustedExecutionCapable

- Booleskt IsVitualizationCapable

- UInt32 L2CacheSize

- UInt32 L2CacheSpeed

- UInt32 L3CacheSize

- UInt32 L3CacheSpeed

- UInt32 LastErrorCode

- UInt16 Nivå

- UInt16 LoadPercentage

- Nollängd Tillverkare

- UInt32 MaxClockSpeed

- Nollängd Namn

- UInt32 NormSpeed

- UInt32 NumberOfCores

- UInt32 NumberOfLogicalProcessors

- Nollängd OtherFamilyDescription

- Booleskt PartOfDomain

- UInt32 PCache

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- Nollängd ProcessorId

- UInt16 ProcessorType

- UInt16 Revision

- Nollängd Rollinnehavaren

- Nollängd SocketDesignation

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd Gå

- Nollängd SystemName

- Nollängd UniqueId

- UInt16 UpgradeMethod

- Nollängd 2.0.1

- UInt32 VoltageCaps

- Nollängd Arbets



## <a name="protected-volume-information"></a>Information om skyddad volym

Namnrymd: root\cimv2\sms

klass CCM_ProtectedVolumeInfo


- Nollängd Namn

- Nollängd DriveLetter

- UInt32 Skydds typ



## <a name="protocol"></a>Protokoll

Namnrymd: root\cimv2

klass Win32_NetworkProtocol


- Nollängd Namn

- Nollängd Under text

- Booleskt ConnectionlessService

- Nollängd Beteckning

- Booleskt GuaranteesDelivery

- Booleskt GuaranteesSequencing

- DateTime InstallDate

- UInt32 MaximumAddressSize

- UInt32 MaximumMessageSize

- Booleskt MessageOriented

- UInt32 MinimumAddressSize

- Booleskt PseudoStreamOriented

- Nollängd Statusfältet

- Booleskt SupportsBroadcasting

- Booleskt SupportsConnectData

- Booleskt SupportsDisconnectData

- Booleskt SupportsEncryption

- Booleskt SupportsExpeditedData

- Booleskt SupportsFragmentation

- Booleskt SupportsGracefulClosing

- Booleskt SupportsGuaranteedBandwidth

- Booleskt SupportsMulticasting

- Booleskt SupportsQualityofService



## <a name="quick-fix-engineering"></a>Snabb korrigerings teknik

Namnrymd: root\cimv2

klass Win32_QuickFixEngineering


- Nollängd HotFixID

- Nollängd ServicePackInEffect

- Nollängd Under text

- Nollängd Beteckning

- Nollängd FixComments

- DateTime InstallDate

- Nollängd InstalledBy

- Nollängd InstalledOn

- Nollängd Namn

- Nollängd Statusfältet



## <a name="ccm-recently-used-applications"></a>Nyligen använda CCM-program

Namnrymd: root\cimv2\sms

klass CCM_RecentlyUsedApps


- Nollängd ExplorerFileName

- Nollängd FolderPath

- Nollängd LastUserName

- Nollängd AdditionalProductCodes

- Nollängd CompanyName

- Nollängd FileDescription

- Nollängd FilePropertiesHash

- UInt32 Storlek

- Nollängd FileVersion

- DateTime LastUsedTime

- UInt32 LaunchCount

- (String) msiDisplayName

- (String) msiPublisher

- (String) msiVersion

- Nollängd OriginalFileName

- Nollängd ProductCode

- UInt32 ProductLanguage

- Nollängd Namn

- Nollängd ProductVersion

- Nollängd SoftwarePropertiesHash



## <a name="registry"></a>Register

Namnrymd: root\cimv2

klass Win32_Registry


- Nollängd Namn

- Nollängd Under text

- UInt32 CurrentSize

- Nollängd Beteckning

- DateTime InstallDate

- UInt32 MaximumSize

- UInt32 ProposedSize

- Nollängd Statusfältet



## <a name="scsi-controller"></a>SCSI-styrenhet

Namnrymd: root\cimv2

klass Win32_SCSIController


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- Nollängd Under text

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- UInt32 ControllerTimeouts

- Nollängd Beteckning

- Nollängd DeviceMap

- Nollängd DriverName

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- Nollängd HardwareVersion

- UInt32 Tabbindex

- DateTime InstallDate

- UInt32 LastErrorCode

- Nollängd Tillverkare

- UInt32 MaxDataWidth

- UInt32 MaxNumberControlled

- UInt64 MaxTransferRate

- Nollängd Namn

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- UInt16 ProtectionManagement

- UInt16 ProtocolSupported

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName

- DateTime TimeOfLastReset



## <a name="serial-port-configuration"></a>Konfiguration av seriell port

Namnrymd: root\cimv2

klass Win32_SerialPortConfiguration


- Nollängd Namn

- Booleskt AbortReadWriteOnError

- UInt32 Överföringshastigheten

- Booleskt BinaryModeEnabled

- UInt32 BitsPerByte

- Nollängd Under text

- Booleskt ContinueXMitOnXOff

- Booleskt CTSOutflowControl

- Nollängd Beteckning

- Booleskt DiscardNULLBytes

- Booleskt DSROutflowControl

- Booleskt DSRSensitivity

- Nollängd DTRFlowControlType

- UInt32 EOFCharacter

- UInt32 ErrorReplaceCharacter

- Booleskt ErrorReplacementEnabled

- UInt32 EventCharacter

- Booleskt IsBusy

- Nollängd Paritet

- Booleskt ParityCheckEnabled

- Nollängd RTSFlowControlType

- Nollängd SettingID

- Nollängd StopBits

- UInt32 XOffCharacter

- UInt32 XOffXMitThreshold

- UInt32 XOnCharacter

- UInt32 XOnXMitThreshold

- UInt32 XOnXOffInFlowControl

- UInt32 XOnXOffOutFlowControl



## <a name="serial-ports"></a>Serie portar

Namnrymd: root\cimv2

klass Win32_SerialPort


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- Booleskt Binär

- UInt16 Funktioner []

- Nollängd CapabilityDescriptions[]

- Nollängd Under text

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- UInt32 MaxBaudRate

- UInt32 MaximumInputBufferSize

- UInt32 MaximumOutputBufferSize

- UInt32 MaxNumberControlled

- Nollängd Namn

- Booleskt OSAutoDiscovered

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- UInt16 ProtocolSupported

- Nollängd ProviderType

- Booleskt SettableBaudRate

- Booleskt SettableDataBits

- Booleskt SettableFlowControl

- Booleskt SettableParity

- Booleskt SettableParityCheck

- Booleskt SettableRLSD

- Booleskt SettableStopBits

- Nollängd Statusfältet

- UInt16 StatusInfo

- Booleskt Supports16BitMode

- Booleskt SupportsDTRDSR

- Booleskt SupportsElapsedTimeouts

- Booleskt SupportsIntTimeouts

- Booleskt SupportsParityCheck

- Booleskt SupportsRLSD

- Booleskt SupportsRTSCTS

- Booleskt SupportsSpecialCharacters

- Booleskt SupportsXOnXOff

- Booleskt SupportsXOnXOffSet

- Nollängd SystemName

- DateTime TimeOfLastReset



## <a name="server-feature"></a>Serverfunktion

Namnrymd: root\cimv2

klass Win32_ServerFeature


- UInt32 IDENTITET

- Nollängd Namn

- UInt32 ParentID



## <a name="services"></a>Tjänster

Namnrymd: root\cimv2

klass Win32_Service


- Nollängd Namn

- Booleskt AcceptPause

- Booleskt AcceptStop

- Nollängd Under text

- UInt32 Tidszon

- Nollängd Beteckning

- Booleskt DesktopInteract

- Nollängd DisplayName

- Nollängd ErrorControl

- UInt32 ExitCode

- DateTime InstallDate

- Nollängd PathName

- UInt32 ProcessId

- UInt32 ServiceSpecificExitCode

- Nollängd ServiceType

- Booleskt Igång

- Nollängd Start mode

- Nollängd StartName

- Nollängd Låst

- Nollängd Statusfältet

- Nollängd SystemName

- UInt32 TagId

- UInt32 WaitHint



## <a name="shares"></a>Resurser

Namnrymd: root\cimv2

klass Win32_Share


- Nollängd Namn

- UInt32 AccessMask

- Booleskt AllowMaximum

- Nollängd Under text

- Nollängd Beteckning

- DateTime InstallDate

- UInt32 MaximumAllowed

- Nollängd Sökväg

- Nollängd Statusfältet

- UInt32 Bastyp



## <a name="sw-licensing-product"></a>Licens produkt för SW

Namnrymd: root\cimv2

klass produkt


- Nollängd IDENTITET

- Nollängd ApplicationID

- Nollängd Beteckning

- DateTime EvaluationEndDate

- UInt32 GracePeriodRemaining

- UInt32 LicenseStatus

- Nollängd MachineURL

- Nollängd Namn

- Nollängd OfflineInstallationId

- Nollängd PartialProductKey

- Nollängd ProcessorURL

- Nollängd ProductKeyID

- Nollängd ProductKeyURL

- Nollängd UseLicenseURL



## <a name="sw-licensing-service"></a>Licensierings tjänst för SW

Namnrymd: root\cimv2

klass program


- Nollängd 2.0.1

- Nollängd ClientMachineID

- UInt32 IsKeyManagementServiceMachine

- UInt32 KeyManagementServiceCurrentCount

- Nollängd KeyManagementServiceMachine

- Nollängd KeyManagementServiceProductKeyID

- UInt32 PolicyCacheRefreshRequired

- UInt32 RequiredClientCount

- UInt32 VLActivationInterval

- UInt32 VLRenewalInterval



## <a name="software-shortcut"></a>Program gen väg

Namnrymd: root\cimv2\sms

klass SMS_SoftwareShortcut


- Nollängd ShortcutKey

- Nollängd BinFileVersion

- Nollängd BinProductVersion

- Nollängd Beteckning

- Nollängd FilePropertiesHash

- Nollängd FilePropertiesHashEx

- UInt32 Storlek

- Nollängd FileVersion

- UInt32 Språk

- Nollängd ParentName

- Nollängd Momsproduktbokföringsmallar

- Nollängd ProductCode

- Nollängd ProductVersion

- Nollängd Förläggare

- Nollängd ShortcutName

- UInt32 ShortcutType

- Nollängd TargetExecutable



## <a name="sms_softwaretag"></a>SMS_SoftwareTag

Namnrymd: root\cimv2\sms

klass SMS_SoftwareTag


- Nollängd TagCreatorRegid

- Nollängd UniqueID

- Nollängd DisplayVersion

- Booleskt EntitlementRequired

- Nollängd Namn

- Nollängd SoftwareCreator

- Nollängd SoftwareCreatorRegid

- Nollängd SoftwareLicensor

- Nollängd SoftwareLicensorRegid

- Nollängd TagCreator

- (SInt32) VersionMajor

- (SInt32) VersionMinor



## <a name="sound-devices"></a>Ljud enheter

Namnrymd: root\cimv2

klass Win32_SoundDevice


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- Nollängd Under text

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- UInt16 DMABufferSize

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- Nollängd Tillverkare

- UInt32 MPU401Address

- Nollängd Namn

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- Nollängd Namn

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName



## <a name="system-account"></a>Systemkonto

Namnrymd: root\cimv2

klass Win32_SystemAccount


- Nollängd Domänsuffix

- Nollängd Namn

- Nollängd Under text

- Nollängd Beteckning

- DateTime InstallDate

- Nollängd SID

- (UInt8) SIDType

- Nollängd Statusfältet



## <a name="system-boot-data"></a>System starts data

Namnrymd: root\CCM

klass CCM_SystemBootData


- UInt64 SystemStartTime

- UInt32 BiosDuration

- UInt16 BootDiskMediaType

- UInt32 BootDuration

- UInt32 EventLogStart

- UInt32 GPDuration

- Nollängd OSVersion

- UInt32 UpdateDuration



## <a name="system-boot-summary"></a>System starts Sammanfattning

Namnrymd: root\CCM

klass CCM_SystemBootSummary


- UInt32 AverageBootFrequency

- UInt32 LatestBiosDuration

- UInt32 LatestBootDuration

- UInt32 LatestCoreBootDuration

- UInt32 LatestEventLogStart

- UInt32 LatestGPDuration

- UInt32 LatestUpdateDuration

- UInt32 MaxBiosDuration

- UInt32 MaxBootDuration

- UInt32 MaxCoreBootDuration

- UInt32 MaxEventLogStart

- UInt32 MaxGPDuration

- UInt32 MaxUpdateDuration

- UInt32 MedianBiosDuration

- UInt32 MedianBootDuration

- UInt32 MedianCoreBootDuration

- UInt32 MedianEventLogStart

- UInt32 MedianGPDuration

- UInt32 MedianUpdateDuration



## <a name="system-console-usage"></a>Användning av system konsol

Namnrymd: root\cimv2\sms

klass SMS_SystemConsoleUsage


- DateTime SecurityLogStartDate

- Nollängd TopConsoleUser

- UInt32 TotalConsoleTime

- UInt32 TotalConsoleUsers

- UInt32 TotalSecurityLogTime



## <a name="system-console-user"></a>System konsol användare

Namnrymd: root\cimv2\sms

klass SMS_SystemConsoleUser


- Nollängd SystemConsoleUser

- DateTime LastConsoleUse

- UInt32 NumberOfConsoleLogons

- UInt32 TotalUserConsoleMinutes



## <a name="system-devices"></a>System enheter

Namnrymd: root\cimv2\sms

klass CCM_SystemDevices


- Nollängd Namn

- Nollängd CompatibleIDs[]

- Nollängd DeviceID

- Nollängd HardwareIDs[]

- Booleskt IsPnP



## <a name="system-drivers"></a>System driv rutiner

Namnrymd: root\cimv2

klass Win32_SystemDriver


- Nollängd Namn

- Booleskt AcceptPause

- Booleskt AcceptStop

- Nollängd Under text

- Nollängd Beteckning

- Booleskt DesktopInteract

- Nollängd DisplayName

- Nollängd ErrorControl

- UInt32 ExitCode

- DateTime InstallDate

- Nollängd PathName

- UInt32 ServiceSpecificExitCode

- Nollängd ServiceType

- Booleskt Igång

- Nollängd Start mode

- Nollängd StartName

- Nollängd Låst

- Nollängd Statusfältet

- Nollängd SystemName

- UInt32 TagId



## <a name="system-enclosure"></a>Systeminneslutning

Namnrymd: root\cimv2

klass Win32_SystemEnclosure


- Nollängd Taggredigerare

- Booleskt AudibleAlarm

- Nollängd BreachDescription

- Nollängd CableManagementStrategy

- Nollängd Under text

- UInt16 ChassisTypes[]

- (SInt16) CurrentRequiredOrProduced

- Nollängd Beteckning

- UInt16 HeatGeneration

- Booleskt HotSwappable

- DateTime InstallDate

- Booleskt LockPresent

- Nollängd Tillverkare

- Nollängd Förlag

- Nollängd Namn

- UInt16 NumberOfPowerCords

- Nollängd OtherIdentifyingInfo

- Nollängd PartNumber

- Booleskt PoweredOn

- Booleskt Flyttbar

- Booleskt Replaceable

- UInt16 SecurityBreach

- UInt16 SecurityStatus

- Nollängd SerialNumber

- Nollängd ServiceDescriptions[]

- UInt16 ServicePhilosophy[]

- Nollängd SKU

- Nollängd SMBIOSAssetTag

- Nollängd Statusfältet

- Nollängd TypeDescriptions[]

- Nollängd 2.0.1

- Booleskt VisibleAlarm



## <a name="tape-drive"></a>Band enhet

Namnrymd: root\cimv2

klass Win32_TapeDrive


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- UInt16 Funktioner []

- Nollängd CapabilityDescriptions[]

- Nollängd Under text

- UInt32 Komprimering

- Nollängd CompressionMethod

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- UInt64 DefaultBlockSize

- Nollängd Beteckning

- UInt32 ECC

- UInt32 EOTWarningZoneSize

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- Nollängd ErrorMethodology

- UInt32 FeaturesHigh

- UInt32 FeaturesLow

- Nollängd IDENTITET

- DateTime InstallDate

- UInt32 LastErrorCode

- Nollängd Tillverkare

- UInt64 MaxBlockSize

- UInt64 MaxMediaSize

- UInt32 MaxPartitionCount

- Nollängd MediaType

- UInt64 MinBlockSize

- Nollängd Namn

- Booleskt NeedsCleaning

- UInt32 NumberOfMediaSupported

- UInt32 Utfyllnad

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- UInt32 ReportSetMarks

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName



## <a name="time-zone"></a>Tidszon

Namnrymd: root\cimv2

klass Win32_TimeZone


- Nollängd StandardName

- (SInt32) Vinkel

- Nollängd Under text

- (SInt32) DaylightBias

- UInt32 DaylightDay

- (UInt8) DaylightDayOfWeek

- UInt32 DaylightHour

- UInt32 DaylightMillisecond

- UInt32 DaylightMinute

- UInt32 DaylightMonth

- Nollängd DaylightName

- UInt32 DaylightSecond

- UInt32 DaylightYear

- Nollängd Beteckning

- Nollängd SettingID

- UInt32 StandardBias

- UInt32 StandardDay

- (UInt8) StandardDayOfWeek

- UInt32 StandardHour

- UInt32 StandardMillisecond

- UInt32 StandardMinute

- UInt32 StandardMonth

- UInt32 StandardSecond

- UInt32 StandardYear



## <a name="tpm"></a>TPM

Namnrymd: root\CIMv2\Security\MicrosoftTpm

klass Win32_Tpm


- Booleskt IsActivated_InitialValue

- Booleskt IsEnabled_InitialValue

- Booleskt IsOwned_InitialValue

- UInt32 ManufacturerId

- Nollängd ManufacturerVersion

- Nollängd ManufacturerVersionInfo

- Nollängd PhysicalPresenceVersionInfo

- Nollängd SpecVersion



## <a name="tpm-status"></a>TPM-status

Namnrymd: root\cimv2\sms

klass SMS_TPM


- Booleskt IsReady

- UInt32 Mer

- Booleskt IsApplicable



## <a name="ts-issued-license"></a>TS-utfärdad licens

Namnrymd: root\cimv2

klass Win32_TSIssuedLicense


- UInt32 LicenseId

- DateTime ExpirationDate

- DateTime IssueDate

- UInt32 KeyPackId

- UInt32 LicenseStatus

- (String) sHardwareId

- (String) sIssuedToComputer

- (String) sIssuedToUser



## <a name="ts-license-key-pack"></a>Nyckel paket för TS-licens

Namnrymd: root\cimv2

klass Win32_TSLicenseKeyPack


- UInt32 KeyPackId

- UInt32 AvailableLicenses

- Nollängd Beteckning

- UInt32 IssuedLicenses

- UInt32 KeyPackType

- UInt32 ProductType

- Nollängd ProductVersion

- UInt32 TotalLicenses



## <a name="uninterruptible-power-supply"></a>Avbrotts fri ström källa

Namnrymd: root\cimv2

klass Win32_UninterruptiblePowerSupply


- Nollängd DeviceID

- UInt16 ActiveInputVoltage

- UInt16 Offlinetillgänglighet

- Booleskt BatteryInstalled

- Booleskt CanTurnOffRemotely

- Nollängd Under text

- Nollängd CommandFile

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- UInt16 EstimatedChargeRemaining

- UInt32 EstimatedRunTime

- UInt32 FirstMessageDelay

- DateTime InstallDate

- Booleskt IsSwitchingSupply

- UInt32 LastErrorCode

- Booleskt LowBatterySignal

- UInt32 MessageInterval

- Nollängd Namn

- Nollängd PNPDeviceID

- Booleskt PowerFailSignal

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- UInt32 Range1InputFrequencyHigh

- UInt32 Range1InputFrequencyLow

- UInt32 Range1InputVoltageHigh

- UInt32 Range1InputVoltageLow

- UInt32 Range2InputFrequencyHigh

- UInt32 Range2InputFrequencyLow

- UInt32 Range2InputVoltageHigh

- UInt32 Range2InputVoltageLow

- UInt16 RemainingCapacityStatus

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName

- UInt32 TimeOnBackup

- UInt32 TotalOutputPower

- UInt16 TypeOfRangeSwitching

- Nollängd Omsport



## <a name="usb-controller"></a>USB-styrenhet

Namnrymd: root\cimv2

klass Win32_USBController


- Nollängd DeviceID

- UInt16 Offlinetillgänglighet

- Nollängd Under text

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd Beteckning

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- DateTime InstallDate

- UInt32 LastErrorCode

- Nollängd Tillverkare

- UInt32 MaxNumberControlled

- Nollängd Namn

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- UInt16 ProtocolSupported

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName

- DateTime TimeOfLastReset



## <a name="usb-device"></a>USB-enhet

Namnrymd: root\cimv2

klass Win32_USBDevice


- Nollängd DeviceID

- Nollängd Under text

- Nollängd ClassGuid

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd CreationClassName

- Nollängd Beteckning

- Nollängd Tillverkare

- Nollängd Namn

- Nollängd PNPDeviceID

- Nollängd Telefonitjänstprovider

- Nollängd Statusfältet

- Nollängd SystemCreationClassName

- Nollängd SystemName



## <a name="usm-user-profile"></a>USM POLICYEGENSKAPER användar profil

Namnrymd: root\cimv2

klass Win32_UserProfile


- Nollängd SID

- (UInt8) HealthStatus

- Nollängd LastAttemptedProfileDownloadTime

- Nollängd LastAttemptedProfileUploadTime

- Nollängd LastBackgroundRegistryUploadTime

- DateTime LastDownloadTime

- DateTime LastUploadTime

- DateTime LastUseTime

- Booleskt Läst

- Nollängd LocalPath

- UInt32 RefCount

- Booleskt RoamingConfigured

- Nollängd RoamingPath

- Booleskt RoamingPreference

- Booleskt Speciella

- UInt32 Statusfältet



## <a name="video-controller"></a>Video styrenhet

Namnrymd: root\cimv2

klass Win32_VideoController


- Nollängd DeviceID

- UInt16 AcceleratorCapabilities[]

- Nollängd AdapterCompatibility

- Nollängd AdapterDACType

- UInt32 AdapterRAM

- UInt16 Offlinetillgänglighet

- Nollängd CapabilityDescriptions[]

- Nollängd Under text

- UInt32 ColorTableEntries

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- UInt32 CurrentBitsPerPixel

- UInt32 CurrentHorizontalResolution

- UInt64 CurrentNumberOfColors

- UInt32 CurrentNumberOfColumns

- UInt32 CurrentNumberOfRows

- UInt32 CurrentRefreshRate

- UInt16 CurrentScanMode

- UInt32 CurrentVerticalResolution

- Nollängd Beteckning

- UInt32 DeviceSpecificPens

- UInt32 DitherType

- DateTime DriverDate

- Nollängd DriverVersion

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- UInt32 ICMIntent

- UInt32 ICMMethod

- Nollängd InfFilename

- Nollängd InfSection

- DateTime InstallDate

- Nollängd InstalledDisplayDrivers

- UInt32 LastErrorCode

- UInt32 MaxMemorySupported

- UInt32 MaxNumberControlled

- UInt32 MaxRefreshRate

- UInt32 MinRefreshRate

- Booleskt Skrivare

- Nollängd Namn

- UInt16 NumberOfColorPlanes

- UInt32 NumberOfVideoPages

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- UInt16 ProtocolSupported

- UInt32 ReservedSystemPaletteEntries

- UInt32 SpecificationVersion

- Nollängd Statusfältet

- UInt16 StatusInfo

- Nollängd SystemName

- UInt32 SystemPaletteEntries

- DateTime TimeOfLastReset

- UInt16 VideoArchitecture

- UInt16 VideoMemoryType

- UInt16 VideoMode

- Nollängd VideoModeDescription

- Nollängd VideoProcessor



## <a name="virtual-application-packages"></a>Virtuella programpaket

Namnrymd: root\Microsoft\appvirt\client

klass paket


- Nollängd PackageGUID

- UInt64 CachedLaunchSize

- UInt16 CachedPercentage

- UInt64 CachedSize

- UInt64 LaunchSize

- Nollängd Namn

- Nollängd SftPath

- UInt64 TotalSize

- Nollängd 2.0.1

- Nollängd VersionGUID



## <a name="virtual-applications"></a>Virtuella program

Namnrymd: root\Microsoft\appvirt\client

klass program


- Nollängd Namn

- Nollängd 2.0.1

- Nollängd CachedOsdPath

- UInt32 GlobalRunningCount

- DateTime LastLaunchOnSystem

- Booleskt Vid

- Nollängd OriginalOsdPath

- Nollängd PackageGUID



## <a name="virtual-machine-64"></a>Virtuell dator (64)

Namnrymd: root\cimv2

klass Win32Reg_SMSGuestVirtualMachine64


- Nollängd InstanceKey

- Nollängd PhysicalHostName

- Nollängd PhysicalHostNameFullyQualified



## <a name="virtual-machine"></a>Virtuell dator

Namnrymd: root\cimv2

klass Win32Reg_SMSGuestVirtualMachine


- Nollängd InstanceKey

- Nollängd PhysicalHostName

- Nollängd PhysicalHostNameFullyQualified



## <a name="virtual-machine-details"></a>Information om virtuell dator

Namnrymd: root\vm\VirtualServer

klass VirtualMachine


- Nollängd Namn

- UInt32 CpuUtilization

- UInt64 DiskBytesRead

- UInt64 DiskBytesWritten

- UInt64 DiskSpaceUsed

- UInt64 HeartbeatCount

- UInt32 HeartbeatInterval

- UInt32 HeartbeatPercentage

- UInt32 HeartbeatRate

- UInt64 NetworkBytesReceived

- UInt64 NetworkBytesSent

- UInt64 PhysicalMemoryAllocated

- UInt32 Drift tid



## <a name="volume"></a>Volym

Namnrymd: root\cimv2

klass Win32_Volume


- Nollängd DeviceID

- UInt16 Fjärråtkomstservrar

- Booleskt Automount

- UInt16 Offlinetillgänglighet

- UInt64 Storlek

- UInt64 Kapaciteten

- Nollängd Under text

- Booleskt Okomprimera

- UInt32 ConfigManagerErrorCode

- Booleskt ConfigManagerUserConfig

- Nollängd CreationClassName

- Nollängd Beteckning

- Booleskt DirtyBitSet

- Nollängd DriveLetter

- UInt32 DriveType

- Booleskt ErrorCleared

- Nollängd ErrorDescription

- Nollängd ErrorMethodology

- Nollängd Fil Systems

- UInt64 FreeSpace

- Booleskt IndexingEnabled

- DateTime InstallDate

- Nollängd Etikett

- UInt32 LastErrorCode

- UInt32 MaximumFileNameLength

- Nollängd Namn

- UInt64 NumberOfBlocks

- Nollängd PNPDeviceID

- UInt16 PowerManagementCapabilities[]

- Booleskt PowerManagementSupported

- Nollängd Anledning

- Booleskt QuotasEnabled

- Booleskt QuotasIncomplete

- Booleskt QuotasRebuilding

- UInt32 SerialNumber

- Nollängd Statusfältet

- UInt16 StatusInfo

- Booleskt SupportsDiskQuotas

- Booleskt SupportsFileBasedCompression

- Nollängd SystemCreationClassName

- Nollängd SystemName



## <a name="ccm_webappinstallinfo"></a>CCM_WebAppInstallInfo

Namnrymd: root\ccm\cimodels

klass CCM_WebAppInstallInfo


- Nollängd AppDeliveryTypeId

- UInt32 AppDtRevision

- Nollängd TargetURL

- Nollängd UserSID

- Nollängd URLFileName

- Nollängd URLPath



## <a name="sms_windows8application"></a>SMS_Windows8Application

Namnrymd: root\cimv2\sms

klass SMS_Windows8Application


- Nollängd FullName

- Nollängd ApplicationName

- Nollängd Designen

- Booleskt ConfigMgrManaged

- Nollängd DependencyApplicationNames

- Nollängd FamilyName

- Nollängd InstalledLocation

- Booleskt IsFramework

- Nollängd Förläggare

- Nollängd PublisherId

- Nollängd 2.0.1



## <a name="sms_windows8applicationuserinfo"></a>SMS_Windows8ApplicationUserInfo

Namnrymd: root\cimv2\sms

klass SMS_Windows8ApplicationUserInfo


- Nollängd FullName

- Nollängd UserSecurityId

- Nollängd InstallState

- Nollängd UserAccountName



## <a name="windows-update"></a>Windows Update

Namnrymd: root\cimv2

klass Win32Reg_SMSWindowsUpdate


- Nollängd InstanceKey

- UInt32 AUOptions

- UInt32 NoAutoUpdate

- UInt32 UseWUServer



## <a name="windows-update-agent-version"></a>Windows Update Agent version

Namnrymd: root\cimv2\sms

klass Win32_WindowsUpdateAgentVersion


- Nollängd 2.0.1



## <a name="write-filter-state"></a>Skriv filter status

Namnrymd: root\cimv2\sms

klass CCM_WriteFilterState


- Booleskt WriteFilterEnabled
