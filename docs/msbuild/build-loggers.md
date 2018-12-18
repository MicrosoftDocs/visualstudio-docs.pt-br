---
title: Agentes de Build | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, writing loggers
- MSBuild, logging
- logging [MSBuild]
ms.assetid: fa34810d-185a-4d22-92bd-9852915e5f1d
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2e1faf28c05dec58117e5d34e21e7c8020ad3a4d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49894281"
---
# <a name="build-loggers"></a>Agentes de build
Agentes fornecem uma maneira de personalizar a saída do build e exibir mensagens, erros ou avisos em resposta a eventos de build específicos. Cada agente é implementado como uma classe .NET que implementa a interface <xref:Microsoft.Build.Framework.ILogger>, definida no assembly *Microsoft.Build.Framework.dll*.  
  
 Há duas abordagens que você pode usar ao implementar um agente:  
  
- Implemente a interface <xref:Microsoft.Build.Framework.ILogger> diretamente.  
  
- Derive a classe da classe auxiliar, <xref:Microsoft.Build.Utilities.Logger>, definida no assembly *Microsoft.Build.Utilities.dll*. O <xref:Microsoft.Build.Utilities.Logger> implementa o <xref:Microsoft.Build.Framework.ILogger> e fornece implementações padrão de alguns membros do <xref:Microsoft.Build.Framework.ILogger>.  
  
  Este tópico explicará como escrever um agente simples que deriva de <xref:Microsoft.Build.Utilities.Logger> e exibe mensagens no console em resposta a determinados eventos de build.  
  
## <a name="register-for-events"></a>Registrar-se para obter eventos  
 A finalidade de um agente é reunir informações sobre o andamento do build quando ele for relatado pelo mecanismo de build e, em seguida, relatar informações de maneira útil. Todos os agentes devem substituir o método <xref:Microsoft.Build.Utilities.Logger.Initialize%2A>, que é onde o agente se registra para eventos. Neste exemplo, o agente registra-se nos eventos <xref:Microsoft.Build.Framework.IEventSource.TargetStarted>, <xref:Microsoft.Build.Framework.IEventSource.ProjectStarted> e <xref:Microsoft.Build.Framework.IEventSource.ProjectFinished>.  
  
 [!code-csharp[msbuild_SimpleConsoleLogger#2](../msbuild/codesnippet/CSharp/build-loggers_1.cs)]  
  
## <a name="respond-to-events"></a>Responder a eventos  
 Agora que o agente está registrado para eventos específicos, ele precisa lidar com esses eventos quando eles ocorrem. Para os eventos <xref:Microsoft.Build.Framework.IEventSource.ProjectStarted> e <xref:Microsoft.Build.Framework.IEventSource.ProjectFinished>, o agente simplesmente escreve uma frase curta e o nome do arquivo de projeto envolvido no evento. Todas as mensagens do agente são gravadas na janela do console.  
  
 [!code-csharp[msbuild_SimpleConsoleLogger#3](../msbuild/codesnippet/CSharp/build-loggers_2.cs)]  
  
## <a name="respond-to-logger-verbosity-values"></a>Responder a valores de detalhes do agente  
 Em alguns casos, talvez você queira registrar somente as informações de um evento se a opção MSBuild.exe **–verbosity** contiver um determinado valor. Neste exemplo, o manipulador de eventos <xref:Microsoft.Build.Framework.IEventSource.TargetStarted> registrará no log apenas uma mensagem se a propriedade <xref:Microsoft.Build.Utilities.Logger.Verbosity%2A>, que é definida pela opção **–verbosity**, for igual a <xref:Microsoft.Build.Framework.LoggerVerbosity>`Detailed`.  
  
 [!code-csharp[msbuild_SimpleConsoleLogger#4](../msbuild/codesnippet/CSharp/build-loggers_3.cs)]  
  
## <a name="specify-a-logger"></a>Especificar um agente  
 Depois que o agente for compilado em um assembly, você precisará informar ao [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] para usar esse agente durante builds. Isso é feito usando a opção **–logger** com o *MSBuild.exe*. Para obter mais informações sobre as opções disponíveis para o *MSBuild.exe*, confira [Referência de linha de comando](../msbuild/msbuild-command-line-reference.md).  
  
 A linha de comando a seguir cria o projeto *MyProject.csproj* e usa a classe de agente implementada em *SimpleLogger.dll*. A opção **–nologo** oculta a faixa e a mensagem de direitos autorais e a opção **–noconsolelogger** desabilita o agente de console [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] padrão.  
  
```cmd  
MSBuild -nologo -noconsolelogger -logger:SimpleLogger.dll  
```  
  
 A linha de comando a seguir compila o projeto com o mesmo agente, mas com um nível `Verbosity` de `Detailed`.  
  
```cmd  
MSBuild -nologo -noconsolelogger -logger:SimpleLogger.dll -verbosity:Detailed  
```  

## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  
 O exemplo a seguir contém o código completo do agente.  
  
### <a name="code"></a>Código  
 [!code-csharp[msbuild_SimpleConsoleLogger#1](../msbuild/codesnippet/CSharp/build-loggers_4.cs)]  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  
 O exemplo a seguir mostra como implementar um agente que grava o log de um arquivo em vez de exibi-lo na janela do console.  
  
### <a name="code"></a>Código  
 [!code-csharp[msbuild_BasicLogger#1](../msbuild/codesnippet/CSharp/build-loggers_5.cs)]  
  
## <a name="see-also"></a>Consulte também  
 [Obter logs de build](../msbuild/obtaining-build-logs-with-msbuild.md)   
 [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)