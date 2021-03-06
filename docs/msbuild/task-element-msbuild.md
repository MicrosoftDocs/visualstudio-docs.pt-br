---
title: Elemento Task de Target (MSBuild) | Microsoft Docs
description: Saiba mais sobre o elemento Task do destino do MSBuild, que cria e executa uma instância de uma tarefa do MSBuild.
ms.custom: SEO-VS-2020
ms.date: 03/13/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Task element [MSBuild]
- <Task> element [MSBuild]
ms.assetid: d82e2485-e5f0-4936-a357-745bacccc299
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a4b8e3cb3acccc2e7ae4c6c2d93353bec79a3690
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99966039"
---
# <a name="task-element-of-target-msbuild"></a>Elemento Task de Target (MSBuild)

Cria e executa uma instância de uma tarefa do MSBuild. O nome do elemento é determinado pelo nome da tarefa que está sendo criada.

 \<Project> \<Target>

## <a name="syntax"></a>Sintaxe

```xml
<Task Parameter1="Value1"... ParameterN="ValueN"
    ContinueOnError="WarnAndContinue/true/ErrorAndContinue/ErrorAndStop/false"
    Condition="'String A' == 'String B'" >
    <Output... />
</Task>
```

## <a name="attributes-and-elements"></a>Atributos e elementos

 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|`Condition`|Atributo opcional. Condição a ser avaliada. Para obter mais informações, consulte [Condições](../msbuild/msbuild-conditions.md).|
|`ContinueOnError`|Atributo opcional. Pode conter um dos seguintes valores:<br /><br /> -   **WarnAndContinue** ou **true**. Quando uma tarefa falha, as tarefas subsequentes no elemento de [destino](../msbuild/target-element-msbuild.md) e a compilação continuam a ser executadas, e todos os erros da tarefa são tratados como avisos.<br />-   **ErrorAndContinue**. Quando uma tarefa falha, as tarefas subsequentes no elemento de `Target` e o build continuam em execução e todos os erros da tarefa são tratados como erros.<br />-   **ErrorAndStop** ou **false** (padrão). Quando uma tarefa falha, as tarefas restantes do elemento de `Target` e o build não são executadas e todo o elemento de `Target` e o build são considerados como em falha.<br /><br /> As versões do .NET Framework antes da 4.5 ofereciam suporte somente aos valores `true` e `false`.<br /><br /> Para obter mais informações, consulte [como ignorar erros em tarefas](../msbuild/how-to-ignore-errors-in-tasks.md).|
|`Parameter`|Será necessário se a classe de tarefa contiver uma ou mais propriedades rotuladas com o atributo `[Required]`.<br /><br /> Um parâmetro de tarefa definido pelo usuário que contém o valor do parâmetro como seu valor. Pode haver qualquer quantidade de parâmetros no elemento `Task`, com cada atributo mapeado para uma propriedade do .NET na classe tarefa.|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[Saída](../msbuild/output-element-msbuild.md)|Armazena saídas da tarefa no arquivo de projeto. Pode haver zero ou mais elementos `Output` em uma tarefa.|

### <a name="parent-elements"></a>Elementos pai

| Elemento | Descrição |
| - | - |
| [Target (destino)](../msbuild/target-element-msbuild.md) | Elemento contêiner para tarefas do MSBuild. |

## <a name="remarks"></a>Comentários

 Um `Task` elemento em um arquivo de projeto do MSBuild cria uma instância de uma tarefa, define as propriedades nela e a executa. O elemento `Output` armazena parâmetros de saída em propriedades ou itens para serem usados em outro local do arquivo de projeto.

 Se houver elementos [OnError](../msbuild/onerror-element-msbuild.md) no elemento pai `Target` de uma tarefa, eles ainda serão avaliados se a tarefa falhar e `ContinueOnError` tiver o valor de `false`. Para obter mais informações sobre tarefas, consulte [Tarefas](../msbuild/msbuild-tasks.md).

## <a name="example"></a>Exemplo

 O exemplo de código a seguir cria uma instância da classe [tarefa Csc](../msbuild/csc-task.md), define seis propriedades e executa a tarefa. Após a execução, o valor da propriedade `OutputAssembly` do objeto é colocada em uma lista de itens com o nome `FinalAssemblyName`.

```xml
<Target Name="Compile" DependsOnTarget="Resources" >
    <Csc Sources="@(CSFile)"
          TargetType="library"
          Resources="@(CompiledResources)"
          EmitDebugInformation="$(includeDebugInformation)"
          References="@(Reference)"
          DebugType="$(debuggingType)" >
        <Output TaskParameter="OutputAssembly"
                  ItemName="FinalAssemblyName" />
    </Csc>
</Target>
```

## <a name="see-also"></a>Consulte também

- [Tarefas](../msbuild/msbuild-tasks.md)
- [Referência de tarefas](../msbuild/msbuild-task-reference.md)
- [Referência de esquema de arquivo de projeto](../msbuild/msbuild-project-file-schema-reference.md)
