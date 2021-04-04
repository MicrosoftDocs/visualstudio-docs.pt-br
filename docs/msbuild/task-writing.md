---
title: Gravação de Tarefa| Microsoft Docs
description: Saiba como você pode criar suas próprias tarefas para fornecer o código que é executado durante o processo de compilação do MSBuild.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, writing tasks
- tasks, creating for MSBuild
- MSBuild, creating tasks
ms.assetid: 3ebc5f87-8f00-46fc-82a1-228f35a6823b
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0db9504404142e5bfdd17a66471820ddad790130
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106214545"
---
# <a name="task-writing"></a>Produção de tarefas

Tarefas fornecem o código que é executado durante o processo de build. Tarefas estão contidas nos destinos. Uma biblioteca de tarefas típicas está incluída no MSBuild e você também pode criar suas próprias tarefas. Para obter mais informações sobre a biblioteca de tarefas que estão incluídas com o MSBuild, consulte [referência de tarefas](../msbuild/msbuild-task-reference.md).

## <a name="tasks"></a>Tarefas

 Exemplos de tarefas incluem [cópia](../msbuild/copy-task.md), que copia um ou mais arquivos, [MakeDir](../msbuild/makedir-task.md), que cria um diretório e [CSC](../msbuild/csc-task.md), que compila arquivos de código-fonte C#. Cada tarefa é implementada como uma classe do .NET que implementa a interface <xref:Microsoft.Build.Framework.ITask>, a qual é definida no assembly *Microsoft.Build.Framework.dll*.

 Há duas abordagens que você pode usar ao implementar uma tarefa:

- Implemente a interface <xref:Microsoft.Build.Framework.ITask> diretamente.

- Derive sua classe da classe auxiliar, <xref:Microsoft.Build.Utilities.Task> , que é definida no assembly *Microsoft.Build.Utilities.dll* . Tarefa implementa ITask e fornece implementações padrão de alguns membros do ITask. Além disso, o registro em log é mais fácil.

Em ambos os casos, você deve adicionar à sua classe um método chamado `Execute`, que é o método que é chamado quando a tarefa é executada. Esse método não usa nenhum parâmetro e retorna um `Boolean` valor: `true` se a tarefa foi bem-sucedida ou `false` se falhou. O exemplo a seguir mostra uma tarefa que não executa nenhuma ação e retorna `true`.

```csharp
using System;
using Microsoft.Build.Framework;
using Microsoft.Build.Utilities;

namespace MyTasks
{
    public class SimpleTask : Task
    {
        public override bool Execute()
        {
            return true;
        }
    }
}
```

 O arquivo de projeto a seguir executa essa tarefa:

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="MyTarget">
        <SimpleTask />
    </Target>
</Project>
```

 Quando executar tarefas, elas também poderá receber entradas do arquivo de projeto se você criar propriedades .NET na classe task. O MSBuild define essas propriedades imediatamente antes de chamar o `Execute` método da tarefa. Para criar uma propriedade de cadeia de caracteres, use o código da tarefa como:

```csharp
using System;
using Microsoft.Build.Framework;
using Microsoft.Build.Utilities;

namespace MyTasks
{
    public class SimpleTask : Task
    {
        public override bool Execute()
        {
            return true;
        }

        public string MyProperty { get; set; }
    }
}
```

 O seguinte arquivo de projeto executa essa tarefa e define `MyProperty` como o valor especificado:

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
   <Target Name="MyTarget">
      <SimpleTask MyProperty="Value for MyProperty" />
   </Target>
</Project>
```

## <a name="register-tasks"></a>Tarefas de registro

 Se um projeto vai executar uma tarefa, o MSBuild deve saber como localizar o assembly que contém a classe Task. As tarefas são registradas usando o [elemento UsingTask (MSBuild)](../msbuild/usingtask-element-msbuild.md).

 O arquivo MSBuild *Microsoft. Common. Tasks* é um arquivo de projeto que contém uma lista de `UsingTask` elementos que registram todas as tarefas que são fornecidas com o MSBuild. Esse arquivo é incluído automaticamente na criação de cada projeto. Se uma tarefa registrada em *Microsoft. Common. Tasks* também estiver registrada no arquivo de projeto atual, o arquivo de projeto atual terá precedência; ou seja, você pode substituir uma tarefa padrão por sua própria tarefa que tem o mesmo nome.

> [!TIP]
> Você pode ver uma lista das tarefas que são fornecidas com o MSBuild exibindo o conteúdo de *Microsoft. Common. Tasks*.

## <a name="raise-events-from-a-task"></a>Gerar eventos de uma tarefa

 Se a tarefa deriva da classe auxiliar <xref:Microsoft.Build.Utilities.Task>, você pode usar qualquer um dos seguintes métodos auxiliares na classe <xref:Microsoft.Build.Utilities.Task> para acionar eventos que serão capturados e exibidos por quaisquer agentes registrados:

```csharp
public override bool Execute()
{
    Log.LogError("messageResource1", "1", "2", "3");
    Log.LogWarning("messageResource2");
    Log.LogMessage(MessageImportance.High, "messageResource3");
    ...
}
```

 Se a tarefa implementa <xref:Microsoft.Build.Framework.ITask> diretamente, você ainda pode acionar esses eventos, mas deve usar a interface IBuildEngine. O exemplo a seguir mostra uma tarefa que implementa ITask e gera um evento personalizado:

```csharp
public class SimpleTask : ITask
{
    public IBuildEngine BuildEngine { get; set; }

    public override bool Execute()
    {
        TaskEventArgs taskEvent =
            new TaskEventArgs(BuildEventCategory.Custom,
            BuildEventImportance.High, "Important Message",
           "SimpleTask");
        BuildEngine.LogBuildEvent(taskEvent);
        return true;
    }
}
```

## <a name="require-task-parameters-to-be-set"></a>Parâmetros de tarefa que precisam de configuração

 Você pode marcar determinadas propriedades de tarefa como "necessárias" para que qualquer arquivo de projeto que executa a tarefa deve definir valores para essas propriedades ou o build falhará. Aplicar o atributo `[Required]` à propriedade .NET em sua tarefa da seguinte maneira:

```csharp
[Required]
public string RequiredProperty { get; set; }
```

 O atributo `[Required]` é definido por <xref:Microsoft.Build.Framework.RequiredAttribute> no namespace <xref:Microsoft.Build.Framework>.

## <a name="how-msbuild-invokes-a-task"></a>Como o MSBuild invoca uma tarefa

Ao invocar uma tarefa, o MSBuild primeiro instancia a classe Task e, em seguida, chama os setters de Propriedade do objeto para os parâmetros de tarefa que são definidos no elemento Task no arquivo de projeto. Se o elemento Task não especificar um parâmetro ou se a expressão especificada no elemento for avaliada como uma cadeia de caracteres vazia, o setter da propriedade não será chamado.

Por exemplo, no projeto

```xml
<Project>
 <Target Name="InvokeCustomTask">
  <CustomTask Input1=""
              Input2="$(PropertyThatIsNotDefined)"
              Input3="value3" />
 </Target>
</Project>
```

somente o setter para `Input3` é chamado.

Uma tarefa não deve depender de nenhuma ordem relativa da invocação de setter de propriedade de parâmetro.

### <a name="task-parameter-types"></a>Tipos de parâmetro de tarefa

O MSBuild controla nativamente as propriedades do tipo `string` , `bool` `ITaskItem` e `ITaskItem[]` . Se uma tarefa aceitar um parâmetro de um tipo diferente, o MSBuild invocará <xref:System.Convert.ChangeType%2A> a conversão de `string` (com todas as referências de item e Propriedade expandidas) para o tipo de destino. Se a conversão falhar para qualquer parâmetro de entrada, o MSBuild emitirá um erro e não chamará o `Execute()` método da tarefa.

## <a name="example-1"></a>Exemplo 1

### <a name="description"></a>Descrição

Essa classe C# a seguir demonstra uma tarefa derivada da <xref:Microsoft.Build.Utilities.Task> classe auxiliar. Esta tarefa retorna `true`, indicando que foi bem-sucedida.

### <a name="code"></a>Código

```csharp
using System;
using Microsoft.Build.Utilities;

namespace SimpleTask1
{
    public class SimpleTask1: Task
    {
        public override bool Execute()
        {
            // This is where the task would presumably do its work.
            return true;
        }
    }
}
```

## <a name="example-2"></a>Exemplo 2

### <a name="description"></a>Descrição

Essa classe C# a seguir demonstra uma tarefa que implementa a <xref:Microsoft.Build.Framework.ITask> interface. Esta tarefa retorna `true`, indicando que foi bem-sucedida.

### <a name="code"></a>Código

```csharp
using System;
using Microsoft.Build.Framework;

namespace SimpleTask2
{
    public class SimpleTask2: ITask
    {
        //When implementing the ITask interface, it is necessary to
        //implement a BuildEngine property of type
        //Microsoft.Build.Framework.IBuildEngine. This is done for
        //you if you derive from the Task class.
        public IBuildEngine BuildEngine { get; set; }

        // When implementing the ITask interface, it is necessary to
        // implement a HostObject property of type object.
        // This is done for you if you derive from the Task class.
        public object HostObject { get; set; }

        public bool Execute()
        {
            // This is where the task would presumably do its work.
            return true;
        }
    }
}
```

## <a name="example-3"></a>Exemplo 3

### <a name="description"></a>Descrição

Essa classe C# demonstra uma tarefa derivada da <xref:Microsoft.Build.Utilities.Task> classe auxiliar. Tem uma propriedade de cadeia de caracteres obrigatória e gera um evento que é exibido por todos os agentes registrados.

### <a name="code"></a>Código

:::code language="csharp" source="../snippets/csharp/VS_Snippets_Misc/msbuild_SimpleTask3/CS/SimpleTask3.cs" id="Snippet1":::

## <a name="example-4"></a>Exemplo 4

### <a name="description"></a>Descrição

O exemplo a seguir mostra um arquivo de projeto invocando a tarefa de exemplo anterior, SimpleTask3.

### <a name="code"></a>Código

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <UsingTask TaskName="SimpleTask3.SimpleTask3"
        AssemblyFile="SimpleTask3\bin\debug\simpletask3.dll"/>

    <Target Name="MyTarget">
        <SimpleTask3 MyProperty="Hello!"/>
    </Target>
</Project>
```

## <a name="see-also"></a>Confira também

- [Referência de tarefas](../msbuild/msbuild-task-reference.md)
