---
title: Visão geral da multiplataforma do MSBuild | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
ms.assetid: eecbcd65-9fbc-4307-a321-46d3c3b79b12
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f5b60f44dd1d32a9d19814b4d2194e7586d86865
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "90838311"
---
# <a name="msbuild-multitargeting-overview"></a>Visão geral da multiplataforma no MSBuild
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Usando o MSBuild, você pode compilar um aplicativo para ser executado em qualquer uma das várias versões do .NET Framework e em qualquer uma das várias plataformas de sistema. Por exemplo, você pode compilar um aplicativo para execução no .NET Framework 2.0 em uma plataforma de 32 bits e pode compilar o mesmo aplicativo para ser executado no .NET Framework 4.5 em uma plataforma de 64 bits.  
  
> [!IMPORTANT]
> Apesar do nome "multiplataforma", um projeto pode direcionar apenas uma estrutura e apenas uma plataforma por vez.  
  
 Estes são alguns dos recursos de multiplataforma do MSBuild:  
  
- Você pode desenvolver um aplicativo destinado a uma versão anterior do .NET Framework, por exemplo, as versões 2.0, 3.5 ou 4.  
  
- Você pode direcionar uma estrutura que não sejam o .NET Framework, por exemplo, o Silverlight Framework.  
  
- Você pode direcionar um *perfil de estrutura*, que é um subconjunto predefinido de uma estrutura de destino.  
  
- Se um service pack para a versão atual do .NET Framework for lançado, você poderá visá-lo.  
  
- O direcionamento do MSBuild garante que um aplicativo use apenas a funcionalidade que está disponível na estrutura e na plataforma direcionadas.  
  
## <a name="target-framework-and-platform"></a>Plataforma e estrutura de destino  
 Uma *estrutura de destino* é a versão do .NET Framework sobre a qual um projeto é compilado para executar, e uma *plataforma de destino* é a plataforma do sistema em que o projeto é compilado para executar.  Por exemplo, você talvez queira um aplicativo .NET Framework 2.0 para ser executado em uma plataforma de 32 bits que seja compatível com a família de processadores x86 802 (x86) de destino. A combinação de estrutura de destino e plataforma de destino é conhecida como o *contexto de destino*. Para obter mais informações, consulte [estrutura de destino e plataforma de destino](../msbuild/msbuild-target-framework-and-target-platform.md).  
  
## <a name="toolset-toolsversion"></a>Toolset (ToolsVersion)  
 Um conjunto de ferramentas juntos coleta as ferramentas, tarefas e destinos que são usados para criar o aplicativo. Um conjunto de ferramentas inclui compiladores como csc.exe e vbc.exe, o arquivo de destinos comuns (microsoft.common.targets), e as tarefas comuns de arquivo (microsoft.common.tasks). O 4.5 o conjunto de ferramentas pode ser usado para o destino .NET Framework versões 2.0, 3.0, 3.5, 4 e 4.5. No entanto, o Conjunto de ferramentas 2.0 só pode ser usado para direcionar o .NET Framework versão 2.0. Para obter mais informações, consulte [Conjunto de ferramentas (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md).  
  
## <a name="reference-assemblies"></a>Assemblies de Referência  
 Os assemblies de referência especificados no Conjunto de ferramentas ajudam a projetar e a compilar um aplicativo. Esses assemblies de referência não apenas habilitar uma compilação de destino específico, mas também restringem componentes e recursos no IDE do Visual Studio para aqueles que são compatíveis com o destino. Para obter mais informações, consulte [resolvendo assemblies em tempo de design](../msbuild/resolving-assemblies-at-design-time.md)  
  
## <a name="configuring-targets-and-tasks"></a>Configurando destinos e tarefas  
 Você pode configurar destinos do MSBuild e tarefas para execução fora de processo com o MSBuild para que você pode direcionar contextos são consideravelmente diferentes daquele que você estiver executando em.  Por exemplo, você pode direcionar um aplicativo do .NET Framework 2.0 de 32 bits, enquanto o computador de desenvolvimento é executada em uma plataforma de 64 bits com o .NET Framework 4.5. Para obter mais informações, consulte [Configurando destinos e tarefas](../msbuild/configuring-targets-and-tasks.md).  
  
## <a name="troubleshooting"></a>Solução de problemas  
 Você pode encontrar erros se você tentar fazer referência a um assembly que não é parte do contexto de destino. Para saber mais sobre esses erros e o que fazer sobre eles, veja [de solução de problemas de direcionamento erros do .NET Framework](../msbuild/troubleshooting-dotnet-framework-targeting-errors.md).
