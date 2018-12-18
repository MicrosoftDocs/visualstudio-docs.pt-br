---
title: Estrutura de destino e plataforma de destino do MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
ms.assetid: df6517c5-edd6-4cc4-97ad-b3cdfc78e799
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: bfb45efc199ea1f643c71bdc19a90862bb6c5dd6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49916056"
---
# <a name="msbuild-target-framework-and-target-platform"></a>Estrutura de destino e plataforma de destino do MSBuild
Um projeto pode ser compilado para executar tanto em uma *estrutura de destino*, que é uma versão específica do .NET Framework, quanto em uma *plataforma de destino*, que é uma arquitetura de software específico.  Por exemplo, você pode direcionar um aplicativo para execução no .NET Framework 2.0 em uma plataforma de 32 bits compatível com a família de processadores 802x86 ("x86"). A combinação de estrutura de destino e plataforma de destino é conhecida como o *contexto de destino*.  
  
## <a name="target-framework-and-profile"></a>Perfil e estrutura de destino  
 Uma estrutura de destino é a versão específica do [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] no qual seu projeto é criado para ser executado. A especificação de uma estrutura de destino é necessária porque ela habilita funcionalidades do compilador e referências do assembly são exclusivas para essa versão da estrutura.  
  
 Atualmente, as seguintes versões do .NET Framework estão disponíveis para uso:  
  
- O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 2.0 (incluído no Visual Studio 2005)  
  
- O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 3.0 (incluído no [!INCLUDE[wiprlhext](../debugger/includes/wiprlhext_md.md)])  
  
- O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 3.5 (incluído no [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)])  
  
- O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 4.5.2  
  
- O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 4.6 (incluído no [!INCLUDE[vs_dev14](../misc/includes/vs_dev14_md.md)])  

- O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 4.6.1  

- O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 4.6.2  

- O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 4.7  

- O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 4.7.1  

As versões do .NET Framework são diferentes entre si na lista de assemblies que cada uma torna disponível para fazer referência. Por exemplo, você não pode compilar aplicativos Windows Presentation Foundation (WPF) a menos que seu projeto seja direcionado para o .NET Framework versão 3.0 ou superior.  

A estrutura de destino é especificada na propriedade `TargetFrameworkVersion` no arquivo de projeto. Você pode alterar a estrutura de destino para um projeto usando as páginas de propriedades do projeto no IDE (ambiente de desenvolvimento integrado) do Visual Studio. Para obter mais informações, consulte [Como direcionar a uma versão do .NET Framework](../ide/how-to-target-a-version-of-the-dotnet-framework.md). Os valores disponíveis para `TargetFrameworkVersion` são `v2.0`, `v3.0`, `v3.5`, `v4.5.2`, `v4.6`, `v4.6.1`, `v4.6.2`, `v4.7` e `v4.7.1`.  
  
```xml  
<TargetFrameworkVersion>v4.0</TargetFrameworkVersion>  
```  
  
 Um *perfil de destino* é um subconjunto de uma estrutura de destino. Por exemplo, o .NET Framework 4 Client Profile não inclui referências aos assemblies do MSBuild.  
  
 O perfil de destino é especificada na propriedade `TargetFrameworkProfile` em um arquivo de projeto. Você pode alterar o perfil de destino usando o controle de estrutura de destino nas páginas de propriedades do projeto no IDE. Para obter mais informações, consulte [Como direcionar a uma versão do .NET Framework](../ide/how-to-target-a-version-of-the-dotnet-framework.md).  
  
```xml  
<TargetFrameworkVersion>v4.0</TargetFrameworkVersion>  
<TargetFrameworkProfile>Client</TargetFrameworkProfile>  
```  
  
## <a name="target-platform"></a>Plataforma de destino  
 A *plataforma* é a combinação de hardware e software que define um ambiente de tempo de execução específico. Por exemplo,  
  
-   `x86` designa um sistema operacional Windows de 32 bits em execução em um processador Intel 80x86 ou equivalente.  

-   `x64` designa um sistema operacional Windows de 64 bits em execução em um processador Intel x64 ou equivalente.
  
-   `Xbox` designa a plataforma Microsoft Xbox 360.  

Uma *plataforma de destino* é a plataforma específica na qual seu projeto é criado para ser executado. A plataforma de destino é especificada na propriedade de build `PlatformTarget` em um arquivo de projeto. Você pode alterar a plataforma de destino usando as páginas de propriedades do projeto ou **Gerenciador de Configurações** no IDE.  

```xml  
<PropertyGroup>  
   <PlatformTarget>x86</PlatformTarget>  
</PropertyGroup>  

```  

Uma *configuração de destino* é um subconjunto de uma plataforma de destino. Por exemplo, a configuração `x86``Debug` não inclui a maioria das otimizações de código. A configuração de destino é especificada na propriedade de build `Configuration` em um arquivo de projeto. Você pode alterar a configuração de destino usando as páginas de propriedades do projeto ou **Gerenciador de Configurações**.  

```xml  
<PropertyGroup>  
   <PlatformTarget>x86</PlatformTarget>  
   <Configuration>Debug</Configuration>  
<PropertyGroup>  
  
```  

## <a name="see-also"></a>Consulte também  
 [Multiplataforma](../msbuild/msbuild-multitargeting-overview.md)
