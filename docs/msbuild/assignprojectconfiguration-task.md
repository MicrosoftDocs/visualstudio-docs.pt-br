---
title: Tarefa AssignProjectConfiguration | Microsoft Docs
description: Use a tarefa MSBuild AssignProjectConfiguration para aceitar uma lista de cadeias de caracteres de configuração e atribuí-las a projetos especificados.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: 09633a0b-8f6f-4aba-8058-7cb4d13ce2c0
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 496b6d538385473d50baec80e30fbc269e06c1f6
ms.sourcegitcommit: d3bca34f82de03fa34ecdd72233676c17fb3cb14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92353389"
---
# <a name="assignprojectconfiguration-task"></a>Tarefa AssignProjectConfiguration

Essa tarefa aceita cadeias de caracteres de configuração de lista e as atribui a projetos especificados.

## <a name="task-parameters"></a>Parâmetros de tarefa

 A tabela a seguir descreve os parâmetros da tarefa `AssignProjectConfiguration`.

|Parâmetro|Descrição|
|---------------|-----------------|
|`ProjectReferences`|<xref:Microsoft.Build.Framework.ITaskItem> `[]` Parâmetro de entrada necessário.<br /><br /> Os projetos a serem configurados.|
|`SolutionConfigurationContents`|Parâmetro de saída `string` opcional.<br /><br /> Contém uma cadeia de caracteres XML com uma configuração de projeto para cada projeto. As configurações são atribuídas aos projetos nomeados.|
|`DefaultToVcxPlatformMapping`|Parâmetro de saída `string` opcional.<br /><br /> Contém uma lista delimitada por ponto e vírgula de mapeamentos dos nomes de plataforma usados pela maioria dos tipos para aqueles usados por arquivos *.vcxproj*.<br /><br /> Por exemplo:<br /><br /> `"AnyCPU=Win32;X86=Win32;X64=X64"`|
|`VcxToDefaultPlatformMapping`|Opcional<br /><br /> Parâmetro de saída `string`.<br /><br /> Contém uma lista delimitada por ponto-e-vírgula de mapeamentos de nomes de plataforma *. vcxproj* para os nomes de plataforma usados pela maioria dos tipos.<br /><br /> Por exemplo:<br /><br /> `"Win32=AnyCPU;X64=X64"`|
|`CurrentProjectConfiguration`|Parâmetro de saída `string` opcional.<br /><br /> Contém a configuração para o projeto atual.|
|`CurrentProjectPlatform`|Parâmetro de saída `string` opcional.<br /><br /> Contém a plataforma para o projeto atual.|
|`OnlyReferenceAndBuildProjectsEnabledInSolutionConfiguration`|Parâmetro de saída `bool` opcional.<br /><br /> Contém um sinalizador que indica que referências devem ser criadas mesmo que tenham sido desabilitadas na configuração do projeto.|
|`ShouldUnsetParentConfigurationAndPlatform`|Parâmetro de saída `bool` opcional.<br /><br /> Contém um sinalizador que indica se a configuração pai e a plataforma devem ser desfeitas.|
|`OutputType`|Parâmetro de saída `string` opcional.<br /><br /> Contém o tipo de saída para o projeto.|
|`ResolveConfigurationPlatformUsingMappings`|Parâmetro de saída `bool` opcional.<br /><br /> Contém um sinalizador que indica se o build deve usar os mapeamentos padrão para resolver a configuração e a plataforma do aprovado nas referências do projeto.|
|`AssignedProjects`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Contém a lista de caminhos de referência resolvidos.|
|`UnassignedProjects`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Contém a lista de itens de referência de projeto que não puderam ser resolvidos usando a lista de saídas pré-resolvida.|

## <a name="remarks"></a>Comentários

 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, confira [Classe base TaskExtension](../msbuild/taskextension-base-class.md).

## <a name="see-also"></a>Veja também

- [Tarefas](../msbuild/msbuild-tasks.md)
- [Referência de tarefas](../msbuild/msbuild-task-reference.md)
