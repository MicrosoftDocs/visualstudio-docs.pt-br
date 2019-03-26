---
title: Tarefas específicas do MSBuild para o Visual C++ | Microsoft Docs
ms.date: 03/10/2019
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, tasks specific to Visual C++
ms.assetid: 05410f0c-7356-4692-bc00-20664421c9ff
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 243ed824ba278300a798a34b05854129e8197504
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2019
ms.locfileid: "57984008"
---
# <a name="msbuild-tasks-specific-to-visual-c"></a>Tarefas do MSBuild específicas para o Visual C++
Tarefas fornecem o código que é executado durante o processo de compilação. Quando o Visual C++ é instalado, as tarefas a seguir estão disponíveis, além das que são instaladas com o [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]. Para saber mais, confira [Visão geral do MSBuild (Visual C++)](/cpp/build/msbuild-visual-cpp-overview).

 Além dos parâmetros para cada tarefa, todas as tarefas também têm os seguintes parâmetros.

| Parâmetro | Descrição |
|-------------------| - |
| `Condition` | Parâmetro `String` opcional.<br /><br /> A expressão `Boolean` que o mecanismo [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] usa para determinar se essa tarefa será executada. Para obter informações sobre as condições que são suportadas pelo [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)], confira [Condições](../msbuild/msbuild-conditions.md). |
| `ContinueOnError` | Parâmetro opcional. Pode conter um dos seguintes valores:<br /><br /> -   **WarnAndContinue** ou **verdadeiro**. Quando uma tarefa falha, as tarefas subsequentes no elemento de [Destino](../msbuild/target-element-msbuild.md) e a compilação continuam em execução, e todos os erros da tarefa são tratados como avisos<br />-   **ErrorAndContinue**. Quando uma tarefa falha, as tarefas subsequentes no elemento de `Target` e o build continuam em execução e todos os erros da tarefa são tratados como erros.<br />-   **ErrorAndStop** ou **falso** (padrão). Quando uma tarefa falha, as tarefas restantes do elemento de `Target` e o build não são executadas e todo o elemento `Target` e a compilação são considerados como com falha.<br /><br /> As versões do .NET Framework antes da 4.5 ofereciam suporte somente aos valores `true` e `false`.<br /><br /> Para obter mais informações, confira [Como: Ignorar erros em tarefas](../msbuild/how-to-ignore-errors-in-tasks.md). |

### <a name="related-topics"></a>Tópicos relacionados

|Título|Descrição|
|-----------|-----------------|
|[Tarefa BscMake](../msbuild/bscmake-task.md)|Encapsula a ferramenta Utilitário de Manutenção de Informações de Procura da Microsoft (*bscmake.exe*).|
|[Tarefa CL](../msbuild/cl-task.md)|Encapsula a ferramenta de compilador Visual C++ (*cl.exe*).|
|[Tarefa CPPClean](../msbuild/cppclean-task.md)|Exclui os arquivos temporários que o MSBuild cria quando um projeto Visual C++ é criado.|
|[ClangCompile task](../msbuild/clangcompile-task.md)|Encapsula a ferramenta de compilador Visual C++ (*clang.exe*).|
|[Tarefa CustomBuild](../msbuild/custombuild-task.md)|Encapsula a ferramenta de compilador Visual C++ (*cmd.exe*).|
|[Tarefa FXC](../msbuild/fxc-task.md)|Use os compiladores de sombreador HLSL no processo de compilação.|
|[GetOutOfDateItems](../msbuild/getoutofdateitems-task.md)|Lê tlogs antigos, grava novos tlogs e retorna um conjunto de itens não atualizados. (tarefa auxiliar)|
|[GetOutputFileName](../msbuild/getoutputfilename-task.md)|Obtém o nome do arquivo de saída para cl e outras ferramentas, que permitem especificar somente o diretório de saída ou o nome de arquivo completo, ou nada. (tarefa auxiliar)|
|[Tarefa LIB](../msbuild/lib-task.md)|Encapsula a ferramenta Gerenciador de Biblioteca de 32 bits da Microsoft (*lib.exe*).|
|[Tarefa Link](../msbuild/link-task.md)|Encapsula a ferramenta de vinculador do Visual C++ (*link.exe*).|
|[Tarefa MIDL](../msbuild/midl-task.md)|Encapsula a ferramenta do compilador da MIDL (linguagem IDL) da Microsoft (*midl.exe*).|
|[Tarefa MT](../msbuild/mt-task.md)|Encapsula a Ferramenta de Manifesto da Microsoft (*mt.exe*).|
|[Tarefa MultiToolTask](../msbuild/multitooltask-task.md)|Sem descrição.|
|[Tarefa ParallelCustomBuild](../msbuild/parallelcustombuild-task.md)|Executar instâncias paralelas da [tarefa CustomBuild](../msbuild/custombuild-task.md).|
|[Tarefa RC](../msbuild/rc-task.md)|Encapsula a ferramenta do compilador de recurso do Microsoft Windows (*rc.exe*).|
|[Tarefa SetEnv](../msbuild/setenv-task.md)|Define ou exclui o valor de uma variável de ambiente especificada.|
|[Classe base TrackedVCToolTask](../msbuild/trackedvctooltask-base-class.md)|Herda de [VCToolTask](../msbuild/vctooltask-base-class.md).|
|[Tarefa VCMessage](../msbuild/vcmessage-task.md)|Logs de mensagens de erro e mensagens de aviso durante uma compilação. (Não pode ser estendida. Somente para uso interno.)|
|[Classe base VCToolTask](../msbuild/vctooltask-base-class.md)|Herda de [ToolTask](/dotnet/api/microsoft.build.utilities.tooltask).|
|[Tarefa XDCMake](../msbuild/xdcmake-task.md)|Encapsula a ferramenta de Documentação XML (*xdcmake.exe*), que mescla arquivos de comentário (*.xdc*) do documento XML com um arquivo *.xml*.|
|[Tarefa XSD](../msbuild/xsd-task.md)|Encapsula a ferramenta de definição de esquema XML (*xsd.exe*), a qual gera arquivos de classe ou de esquema com base em uma origem. *Consulte a observação abaixo.*|
|[Referência do MSBuild](../msbuild/msbuild-reference.md)|Descreve os elementos do sistema MSBuild.|
|[Tarefas](../msbuild/msbuild-tasks.md)|Descreve tarefas que são unidades de código que podem ser combinadas para produzirem uma compilação.|
|[Produção de tarefas](../msbuild/task-writing.md)|Descreve como criar uma tarefa.|

> [!NOTE]
> A partir do Visual Studio 2017, o suporte a projetos em C++ para *xsd.exe* foi preterido. Você ainda pode usar as APIs **Microsoft.VisualC.CppCodeProvider** manualmente adicionando *CppCodeProvider.dll* ao cache de assembly global.