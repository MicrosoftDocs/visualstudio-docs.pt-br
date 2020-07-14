---
title: Estrutura de destino e plataforma de destino do MSBuild | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: df6517c5-edd6-4cc4-97ad-b3cdfc78e799
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2c55ce57adb5b86941b5953732d57a642eb4f943
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350830"
---
# <a name="msbuild-target-framework-and-target-platform"></a>Estrutura de destino e plataforma de destino do MSBuild

Um projeto pode ser compilado para executar tanto em uma *estrutura de destino*, que é uma versão específica do .NET Framework, quanto em uma *plataforma de destino*, que é uma arquitetura de software específico.  Por exemplo, você pode direcionar um aplicativo para ser executado no .NET Framework 2,0 em uma plataforma de 32 bits que seja compatível com a família de processadores 80x86 ("x86"). A combinação de estrutura de destino e plataforma de destino é conhecida como o *contexto de destino*.

> [!IMPORTANT]
> Este artigo mostra a maneira antiga de especificar uma estrutura de destino. Os projetos no estilo SDK permitem TargetFrameworks diferentes, como o netstandard. Para obter mais informações, confira [Estruturas de destino](/dotnet/standard/frameworks).

## <a name="target-framework-and-profile"></a>Perfil e estrutura de destino

 Uma estrutura de destino é a versão específica do .NET Framework na qual o projeto foi criado para ser executado. A especificação de uma estrutura de destino é necessária porque ela habilita funcionalidades do compilador e referências do assembly são exclusivas para essa versão da estrutura.

 Atualmente, as seguintes versões do .NET Framework estão disponíveis para uso:

- O .NET Framework 2.0 (incluído no Visual Studio 2005)

- O .NET Framework 3,0 (incluído no Windows Vista)

- O .NET Framework 3,5 (incluído no Visual Studio 2008)

- O .NET Framework 4.5.2

- O .NET Framework 4,6 (incluído no Visual Studio 2015)

- O .NET Framework 4.6.1

- O .NET Framework 4.6.2

- O .NET Framework 4.7

- O .NET Framework 4.7.1

- O .NET Framework 4.7.2

- O .NET Framework 4.8

As versões do .NET Framework são diferentes entre si na lista de assemblies que cada uma torna disponível para fazer referência. Por exemplo, você não pode compilar aplicativos Windows Presentation Foundation (WPF) a menos que seu projeto seja direcionado para o .NET Framework versão 3.0 ou superior.

A estrutura de destino é especificada na propriedade `TargetFrameworkVersion` no arquivo de projeto. Você pode alterar a estrutura de destino para um projeto usando as páginas de propriedades do projeto no IDE (ambiente de desenvolvimento integrado) do Visual Studio. Para obter mais informações, consulte [Como direcionar a uma versão do .NET Framework](../ide/visual-studio-multi-targeting-overview.md). Os valores disponíveis para `TargetFrameworkVersion` são `v2.0`, `v3.0`, `v3.5`, `v4.5.2`, `v4.6`, `v4.6.1`, `v4.6.2`, `v4.7`, `v4.7.1`, `v4.7.2` e `v4.8`.

```xml
<TargetFrameworkVersion>v4.0</TargetFrameworkVersion>
```

 Um *perfil de destino* é um subconjunto de uma estrutura de destino. Por exemplo, o .NET Framework 4 Client Profile não inclui referências aos assemblies do MSBuild.

 > [!NOTE]
 > Os perfis de destino se aplicam somente a [bibliotecas de classes portáteis](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library).

 O perfil de destino é especificada na propriedade `TargetFrameworkProfile` em um arquivo de projeto. Você pode alterar o perfil de destino usando o controle de estrutura de destino nas páginas de propriedades do projeto no IDE.

```xml
<TargetFrameworkVersion>v4.0</TargetFrameworkVersion>
<TargetFrameworkProfile>Client</TargetFrameworkProfile>
```

## <a name="target-platform"></a>Plataforma de destino

 A *plataforma* é a combinação de hardware e software que define um ambiente de runtime específico. Por exemplo,

- `x86` designa um sistema operacional Windows de 32 bits em execução em um processador Intel 80x86 ou equivalente.

- `x64` designa um sistema operacional Windows de 64 bits em execução em um processador Intel x64 ou equivalente.

- `Xbox` designa a plataforma Microsoft Xbox 360.

Uma *plataforma de destino* é a plataforma específica na qual seu projeto é criado para ser executado. A plataforma de destino é especificada na propriedade de build `PlatformTarget` em um arquivo de projeto. Você pode alterar a plataforma de destino usando as páginas de propriedades do projeto ou **Gerenciador de Configurações** no IDE.

```xml
<PropertyGroup>
   <PlatformTarget>x86</PlatformTarget>
</PropertyGroup>

```

Uma *configuração de destino* é um subconjunto de uma plataforma de destino. Por exemplo, a configuração `x86` `Debug` não inclui a maioria das otimizações de código. A configuração de destino é especificada na propriedade de build `Configuration` em um arquivo de projeto. Você pode alterar a configuração de destino usando as páginas de propriedades do projeto ou **Gerenciador de Configurações**.

```xml
<PropertyGroup>
   <PlatformTarget>x86</PlatformTarget>
   <Configuration>Debug</Configuration>
</PropertyGroup>

```

## <a name="see-also"></a>Veja também

- [Multiplataforma](../msbuild/msbuild-multitargeting-overview.md)
