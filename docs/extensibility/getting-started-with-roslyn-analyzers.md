---
title: Introdução ao analisadores Roslyn | Microsoft Docs
ms.date: 04/02/2018
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 367c2ec8-3059-46a5-9d1c-57bead0419e7
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 6077fb8a9f0db360389953ef6a7ed25c6d242247
ms.sourcegitcommit: d7f232a7596420e40ff8051d42cdf90203af4a74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52821286"
---
# <a name="get-started-with-roslyn-analyzers"></a>Introdução ao analisadores Roslyn

Com os analisadores de código ao vivo, com base em projeto no Visual Studio, os autores do API podem ser fornecidas a análise de código específica de domínio como parte de seus pacotes NuGet. Porque desses analisadores serem alimentados pela plataforma do compilador .NET (cujo codinome é "Roslyn"), eles podem produzir alertas em seu código enquanto você digita, mesmo antes de terminar a linha (não precisa mais esperar para compilar seu código para descobrir problemas). Os analisadores também podem surgir uma correção automática de código por meio do prompt de lâmpada do Visual Studio para deixá-lo limpar seu código imediatamente.

## <a name="get-started"></a>Introdução

[Passo a passo e introdução de analisadores de código em tempo real de Roslyn](https://msdn.microsoft.com/magazine/dn879356.aspx)

[Adicionar correções de código passo a passo: fornecer correções de usuários para problemas de analisador](https://msdn.microsoft.com/magazine/dn904670.aspx)

[Introdução e instruções passo a passo do analisador do mundo real de falar](https://channel9.msdn.com/events/Build/2015/3-725)

[Analisador do mundo real Roslyn](../extensibility/roslyn-analyzers-and-code-aware-library-for-immutablearrays.md) que você também pode assistir como um [falar](https://channel9.msdn.com/events/Build/2015/3-725)

[Vários exemplos no GitHub, agrupados em três tipos de analisadores](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)

[Introdução e tour alguns analisadores falar](https://channel9.msdn.com/Events/dotnetConf/2015/NET-Compiler-Platform-Roslyn-Analyzers-and-the-Rise-of-Code-Aware-Libraries)

## <a name="see-also"></a>Consulte também

- [Visão geral de analisadores de Roslyn](../code-quality/roslyn-analyzers-overview.md)
- [Tutorial: Escrever sua primeira correção de código e o analisador](/dotnet/csharp/roslyn-sdk/tutorials/how-to-write-csharp-analyzer-code-fix)
- [Referência de versão de pacote de plataforma do .NET compilador](roslyn-version-support.md)
- [Docs mais no site do GitHub OSS](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)
- [Regras do FxCop implementadas com analisadores de Roslyn no GitHub](https://github.com/dotnet/roslyn/tree/master/src/Diagnostics/FxCop)