---
title: '&lt;&gt;Elemento Package (Bootstrapper) | Microsoft Docs'
description: O elemento Package é o elemento XML de nível superior dentro de um arquivo de pacote. O elemento Package é obrigatório.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <package> element [bootstrapper]
ms.assetid: ecd06658-ad02-4440-bccd-88437b7fb816
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7645731cf5b955601541a122f2fdb3fa3d794cc3
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2020
ms.locfileid: "94350732"
---
# <a name="ltpackagegt-element-bootstrapper"></a>&lt;&gt;Elemento Package (Bootstrapper)
O `Package` elemento é o elemento XML de nível superior dentro de um arquivo de pacote.

## <a name="syntax"></a>Syntax

```xml
<Package
    Culture
    Name
    LicenseAgreement
>
    <InstallChecks>
        <AssemblyCheck
            Property
            Name
            PublicKeyToken
            Version
            Language
            ProcessorArchitecture
        />
        <RegistryCheck
            Property
            Key
            Value
        />
        <ExternalCheck
            PackageFile
            Property
            Arguments
            Log
        />
        <FileCheck
            Property
            FileName
            SearchPath
            SpecialFolder
            SearchDepth
        />
        <MsiProductCheck
            Property
            Product
            Feature
        />
        <RegistryFileCheck
            Property
            Key
            Value
            File
            SearchDepth
        />
    </InstallChecks>

    <Commands
        Reboot
    >
        <Command
            PackageFile
            Arguments
            EstimatedInstallSeconds
            EstimatedDiskBytes
            EstimatedTempBytes
            Log
        >
            <InstallConditions>
                <BypassIf
                    Property
                    Compare
                    Value
                    Schedule
                />
                <FailIf
                    Property
                    Compare
                    Value
                    String
                    Schedule
                />
            </InstallConditions>
            <ExitCodes>
                <ExitCode
                    Value
                    Result
                    String
                />
            </ExitCodes>
        </Command>
    </Commands>

    <PackageFiles
        CopyAllComponents
    >
        <PackageFile
            Name
            Path
            HomeSite
            PublicKey
        />
    </PackageFiles>

    <Strings>
        <String
            Name
        >
        </String>
    </Strings>

    <Schedules>
        <Schedule
            Name
        >
           <BuildList />
           <BeforePackage />
           <AfterPackage />
        </Schedule>
    </Schedules>
</Package>
```

## <a name="elements-and-attributes"></a>Elementos e atributos
 O `Package` elemento é obrigatório. Ele tem os atributos a seguir.

| Atributo | Descrição |
|--------------------| - |
| `Culture` | Obrigatórios. Define a cultura para este pacote, que determina o idioma a ser usado. Esse atributo é uma chave para o `Strings` elemento, que lista cadeias de caracteres específicas de cultura para nomes de produtos e mensagens de erro durante a instalação. |
| `Name` | Obrigatórios. O nome do pacote exibido para o desenvolvedor em uma ferramenta como [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . Esse atributo é uma chave para o `Strings` elemento, que deve conter um `String` elemento com as `Name` `Culture` Propriedades e definidas para corresponder às `Name` `Culture` Propriedades e de `Package` . |
| `LicenseAgreement` | Opcional. Especifica o nome do arquivo no pacote de distribuição que contém o contrato de licença do End-User (EULA).  Esse arquivo pode ser de texto sem formatação ( *. txt* ) ou Rich Text. ( *. rtf* ) |

## <a name="example"></a>Exemplo
 O exemplo de código a seguir mostra um arquivo de pacote completo para redistribuição do .NET Framework 2,0.

```xml
<?xml version="1.0" encoding="utf-8" ?>

<Package
  xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"
  Name="DisplayName"
  Culture="Culture"
  LicenseAgreement="eula.rtf"
>

    <PackageFiles>
        <PackageFile Name="eula.rtf"/>
    </PackageFiles>

    <!-- Defines a localizable string table for error messages-->
    <Strings>
        <String Name="DisplayName">.NET Framework 2.0</String>
        <String Name="Culture">en</String>
        <String Name="AdminRequired">Administrator permissions are required to install the .NET Framework 2.0. Contact your administrator.</String>
        <String Name="InvalidPlatformWin9x">Installation of the .NET Framework 2.0 is not supported on Windows 95. Contact your application vendor.</String>
        <String Name="InvalidPlatformWinNT">Installation of the .NET Framework 2.0 is not supported on Windows NT 4.0. Contact your application vendor.</String>
        <String Name="InvalidPlatformIE">Installation of the .NET Framework 2.0 requires Internet Explorer 5.01 or greater. Contact your application vendor.</String>
        <String Name="InvalidPlatformArchitecture">This version of the .NET Framework 2.0 is not supported on a 64-bit operating system. Contact your application vendor.</String>
        <String Name="WindowsInstallerImproperInstall">Due to an error with Windows Installer, the installation of the .NET Framework 2.0 cannot proceed.</String>
        <String Name="AnotherInstanceRunning">Another instance of setup is already running. The running instance must complete before this setup can proceed.</String>
        <String Name="BetaNDPFailure">A beta version of the .NET Framework was detected on the computer. Uninstall any previous beta versions of .NET Framework before continuing.</String>
        <String Name="GeneralFailure">A failure occurred attempting to install the .NET Framework 2.0.</String>
        <String Name="DotNetFXExe">http://go.microsoft.com/fwlink/?LinkId=37283</String>
        <String Name="InstMsiAExe">http://go.microsoft.com/fwlink/?LinkId=37285</String>
        <String Name="Msi30Exe">http://go.microsoft.com/fwlink/?LinkId=37287</String>
    </Strings>

</Package>
```

## <a name="see-also"></a>Veja também
- [Referência de esquema de produto e pacote](../deployment/product-and-package-schema-reference.md)