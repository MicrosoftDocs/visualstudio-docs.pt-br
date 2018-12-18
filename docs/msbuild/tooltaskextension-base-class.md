---
title: Classe base de ToolTaskExtension | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- MSBuild.ToolTask.ToolCommandFailed
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: 258ae433-f68a-49f1-b276-da20e3472e68
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8856011e8b85f049c53947a785f1479e1db25368
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49888548"
---
# <a name="tooltaskextension-base-class"></a>Classe base ToolTaskExtension
Muitas tarefas são herdadas da classe <xref:Microsoft.Build.Tasks.ToolTaskExtension>, que é herdada da classe <xref:Microsoft.Build.Utilities.ToolTask>, que é herdada da classe <xref:Microsoft.Build.Utilities.Task>. Esta cadeia de herança adiciona vários parâmetros nas tarefas que derivam deles. Esses parâmetros são listados neste documento.  

## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros das classes base.  


| Parâmetro | Descrição |
| - | - |
| <xref:Microsoft.Build.Utilities.Task.BuildEngine%2A> | Parâmetro <xref:Microsoft.Build.Framework.IBuildEngine> opcional.<br /><br /> Especifica a interface de mecanismo de compilação disponível para tarefas. O mecanismo de compilação define automaticamente esse parâmetro para permitir que tarefas retornem para ele. |
| <xref:Microsoft.Build.Utilities.Task.BuildEngine2%2A> | Parâmetro <xref:Microsoft.Build.Framework.IBuildEngine2> opcional.<br /><br /> Especifica a interface de mecanismo de compilação disponível para tarefas. O mecanismo de compilação define automaticamente esse parâmetro para permitir que tarefas retornem para ele.<br /><br /> Esta é uma propriedade de conveniência para que os autores de tarefa que herdam desta classe não precisem converter o valor de `IBuildEngine` para `IBuildEngine2`. |
| <xref:Microsoft.Build.Utilities.Task.BuildEngine3%2A> | Parâmetro <xref:Microsoft.Build.Framework.IBuildEngine3> opcional.<br /><br /> Especifica a interface de mecanismo de compilação disponível pelo host. |
| <xref:Microsoft.Build.Utilities.ToolTask.EchoOff%2A> | Parâmetro `bool` opcional.<br /><br /> Quando definido como `true`, essa tarefa passa **/Q** para a linha de comando de *cmd.exe*, de modo que a linha de comando não é copiada para stdout. |
| <xref:Microsoft.Build.Utilities.ToolTask.EnvironmentVariables%2A> | Parâmetro de matriz `String` opcional.<br /><br /> Matriz de pares de variáveis de ambiente, separadas por sinais de igual. Essas variáveis são passadas para o executável gerado além, ou seletivamente substituindo, o bloco de ambiente regular. |
| <xref:Microsoft.Build.Utilities.ToolTask.ExitCode%2A> | Parâmetro somente leitura de saída `Int32` opcional.<br /><br /> Especifica o código de saída é fornecido pelo comando executado. Se a tarefa registra erros, mas o processo tem um código de saída de 0 (êxito), isso é definido como -1. |
| <xref:Microsoft.Build.Utilities.Task.HostObject%2A> | Parâmetro <xref:Microsoft.Build.Framework.ITaskHost> opcional.<br /><br /> Especifica a instância do objeto de host (pode ser nulo). O mecanismo de compilação define essa propriedade se o IDE do host associou um objeto de host com essa tarefa em particular. |
| <xref:Microsoft.Build.Tasks.ToolTaskExtension.Log%2A> | Parâmetro <xref:Microsoft.Build.Utilities.TaskLoggingHelper> somente leitura opcional.<br /><br /> Obtém uma instância de uma classe <xref:Microsoft.Build.Tasks.TaskLoggingHelperExtension> que contém métodos de registro de tarefa em log. |
| <xref:Microsoft.Build.Utilities.ToolTask.LogStandardErrorAsError%2A> | Opção parâmetro `bool`.<br /><br /> Se `true`, todas as mensagens recebidas no fluxo de erro padrão são registradas como erros. |
| <xref:Microsoft.Build.Utilities.ToolTask.StandardErrorImportance%2A> | Parâmetro `String` opcional.<br /><br /> Importância para fazer o texto de log do fluxo de saída do padrão. |
| <xref:Microsoft.Build.Utilities.ToolTask.StandardOutputImportance%2A> | Parâmetro `String` opcional.<br /><br /> Importância para fazer o texto de log do fluxo de saída do padrão. |
| <xref:Microsoft.Build.Utilities.ToolTask.Timeout%2A> | Parâmetro `Int32` opcional virtual.<br /><br /> Especifica a quantidade de tempo em milissegundos após o qual o executável da tarefa é encerrado. O valor padrão é `Int.MaxValue`, indicando que não há período de tempo limite. O tempo limite está em milissegundos. |
| <xref:Microsoft.Build.Utilities.ToolTask.ToolExe%2A> | Parâmetro `string` opcional virtual.<br /><br /> Projetos podem implementar para substituir um ToolName. Tarefas podem substituir isso para preservar o ToolName. |
| <xref:Microsoft.Build.Utilities.ToolTask.ToolPath%2A> | Parâmetro `string` opcional.<br /><br /> Especifica o local de onde a tarefa carrega o arquivo executável subjacente. Se esse parâmetro não for especificado, a tarefa usará o caminho de instalação do SDK correspondente à versão do framework que está executando [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]. |
| <xref:Microsoft.Build.Utilities.ToolTask.UseCommandProcessor%2A> | Parâmetro `bool` opcional.<br /><br /> Quando definido como `true`, essa tarefa cria um arquivo em lotes para a linha de comando e o executa usando o processador de comando em vez de executar o comando diretamente. |
| <xref:Microsoft.Build.Utilities.ToolTask.YieldDuringToolExecution%2A> | Parâmetro `bool` opcional.<br /><br /> Quando definido como `true`, essa tarefa gera o nó quando a tarefa está em execução. |

## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Tarefas](../msbuild/msbuild-tasks.md)