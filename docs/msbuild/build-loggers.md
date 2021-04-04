---
title: Agentes de Build | Microsoft Docs
description: Use os agentes de log do MSBuild para gerenciar e personalizar a saída de sua compilação e exibir mensagens, erros ou avisos em resposta a eventos de compilação específicos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, writing loggers
- MSBuild, logging
- logging [MSBuild]
ms.assetid: fa34810d-185a-4d22-92bd-9852915e5f1d
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b676fe015f5f513a069ffaf6ae4fac59c1a5fa68
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106213895"
---
# <a name="build-loggers"></a>Agentes de build

Agentes fornecem uma maneira de personalizar a saída do build e exibir mensagens, erros ou avisos em resposta a eventos de build específicos. Cada agente é implementado como uma classe .NET que implementa a interface <xref:Microsoft.Build.Framework.ILogger>, definida no assembly *Microsoft.Build.Framework.dll*.

Há duas abordagens que você pode usar ao implementar um agente:

- Implemente a interface <xref:Microsoft.Build.Framework.ILogger> diretamente.
- Derive sua classe da classe auxiliar, <xref:Microsoft.Build.Utilities.Logger> , que é definida no assembly *Microsoft.Build.Utilities.dll* . O <xref:Microsoft.Build.Utilities.Logger> implementa o <xref:Microsoft.Build.Framework.ILogger> e fornece implementações padrão de alguns membros do <xref:Microsoft.Build.Framework.ILogger>.

  Este tópico explicará como escrever um agente simples que deriva de <xref:Microsoft.Build.Utilities.Logger> e exibe mensagens no console em resposta a determinados eventos de build.

## <a name="register-for-events"></a>Registrar-se para obter eventos

A finalidade de um agente é reunir informações sobre o andamento do build quando ele for relatado pelo mecanismo de build e, em seguida, relatar informações de maneira útil. Todos os agentes devem substituir o método <xref:Microsoft.Build.Utilities.Logger.Initialize%2A>, que é onde o agente se registra para eventos. Neste exemplo, o agente registra-se nos eventos <xref:Microsoft.Build.Framework.IEventSource.TargetStarted>, <xref:Microsoft.Build.Framework.IEventSource.ProjectStarted> e <xref:Microsoft.Build.Framework.IEventSource.ProjectFinished>.

:::code language="csharp" source="../snippets/csharp/VS_Snippets_Misc/msbuild_SimpleConsoleLogger/CS/msbuild_SimpleConsoleLogger.cs" id="Snippet2":::

## <a name="respond-to-events"></a>Responder a eventos

Agora que o agente está registrado para eventos específicos, ele precisa lidar com esses eventos quando eles ocorrem. Para os eventos <xref:Microsoft.Build.Framework.IEventSource.ProjectStarted> e <xref:Microsoft.Build.Framework.IEventSource.ProjectFinished>, o agente simplesmente escreve uma frase curta e o nome do arquivo de projeto envolvido no evento. Todas as mensagens do agente são gravadas na janela do console.

:::code language="csharp" source="../snippets/csharp/VS_Snippets_Misc/msbuild_SimpleConsoleLogger/CS/msbuild_SimpleConsoleLogger.cs" id="Snippet3":::

## <a name="respond-to-logger-verbosity-values"></a>Responder a valores de detalhes do agente

Em alguns casos, talvez você queira registrar apenas informações de um evento se a opção MSBuild.exe **-detalhes** contiver um determinado valor. Neste exemplo, o <xref:Microsoft.Build.Framework.IEventSource.TargetStarted> manipulador de eventos registra apenas uma mensagem se a <xref:Microsoft.Build.Utilities.Logger.Verbosity%2A> propriedade, que é definida pela opção **-detalhamento** , é igual a <xref:Microsoft.Build.Framework.LoggerVerbosity> `Detailed` .

:::code language="csharp" source="../snippets/csharp/VS_Snippets_Misc/msbuild_SimpleConsoleLogger/CS/msbuild_SimpleConsoleLogger.cs" id="Snippet4":::

## <a name="specify-a-logger"></a>Especificar um agente

Depois que o agente é compilado em um assembly, você precisa dizer ao MSBuild para usar esse agente durante as compilações. Isso é feito usando a opção **-logger** com *MSBuild.exe*. Para obter mais informações sobre as opções disponíveis para o *MSBuild.exe*, confira [Referência de linha de comando](../msbuild/msbuild-command-line-reference.md).

A linha de comando a seguir cria o projeto *MyProject.csproj* e usa a classe de agente implementada em *SimpleLogger.dll*. A opção **-nologomarca** oculta a faixa e a mensagem de direitos autorais e a opção **-noconsolelogger** desabilita o agente de log do MSBuild padrão.

```cmd
MSBuild -nologo -noconsolelogger -logger:SimpleLogger.dll
```

A linha de comando a seguir compila o projeto com o mesmo agente, mas com um nível `Verbosity` de `Detailed`.

```cmd
MSBuild -nologo -noconsolelogger -logger:SimpleLogger.dll -verbosity:Detailed
```

## <a name="example-1"></a>Exemplo 1

### <a name="description"></a>Descrição

O exemplo a seguir contém o código completo do agente.

### <a name="code"></a>Código

:::code language="csharp" source="../snippets/csharp/VS_Snippets_Misc/msbuild_SimpleConsoleLogger/CS/msbuild_SimpleConsoleLogger.cs" id="Snippet1":::

## <a name="example-2"></a>Exemplo 2

### <a name="description"></a>Descrição

O exemplo a seguir mostra como implementar um agente que grava o log de um arquivo em vez de exibi-lo na janela do console.

### <a name="code"></a>Código

:::code language="csharp" source="../snippets/csharp/VS_Snippets_Misc/msbuild_BasicLogger/CS/msbuild_BasicLogger.cs" id="Snippet1":::

## <a name="see-also"></a>Confira também

- [Obter logs de build](../msbuild/obtaining-build-logs-with-msbuild.md)
- [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)
