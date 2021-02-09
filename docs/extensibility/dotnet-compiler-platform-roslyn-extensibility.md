---
title: Extensibilidade de .NET Compiler Platform ( &quot; Roslyn &quot; ) | Microsoft Docs
description: Saiba mais sobre o .NET Compiler Platform, que permite que as ferramentas e os desenvolvedores compartilhem nos compiladores de informações ricas sobre programas.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 564201b3-1e18-4b88-b615-42c2f57f3fe8
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8c0286bb35f8a58a2f5fd6cfa95cff62d523567c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99883552"
---
# <a name="net-compiler-platform-quotroslynquot-extensibility"></a>Extensibilidade de .NET Compiler Platform ( &quot; Roslyn &quot; )
A missão principal do .NET Compiler Platform ("Roslyn") é abrir os compiladores do C# e do Visual Basic e permitir que ferramentas e desenvolvedores compartilhem nos compiladores de informações ricas sobre programas. As ferramentas de análise de código melhoram a qualidade do código e os geradores de código auxiliam na construção do aplicativo. Como as ferramentas são mais inteligentes, elas precisam acessar cada vez mais o conhecimento de código profundo que apenas os compiladores possuem. Em vez de serem tradutores opacos (código-fonte no e código do objeto), os compiladores do Roslyn oferecem APIs que você pode usar para tarefas relacionadas a código em suas ferramentas e aplicativos.

 A melhor parte é que os compiladores do Roslyn, suas APIs, exemplos e instruções passo a passos, e as ferramentas reais criadas com base nessas APIs são totalmente abertas em [github.com/dotnet/Roslyn](https://github.com/dotnet/Roslyn). Acesse o site do OSS para saber mais e comece a usar o Roslyn. Você encontrará links para obter os recursos mais recentes de C# e Visual Basic que podem ser usados como um usuário final, bem como links para começar como um construtor de ferramentas que aproveita as APIs Roslyn.

## <a name="see-also"></a>Confira também
- [Introdução aos analisadores do Roslyn](../extensibility/getting-started-with-roslyn-analyzers.md)
