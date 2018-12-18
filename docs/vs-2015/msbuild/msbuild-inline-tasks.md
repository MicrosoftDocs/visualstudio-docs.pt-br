---
title: Tarefas embutidas do MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSBuild, tasks
ms.assetid: e72e6506-4a11-4edf-ae8d-cfb5a3b9d8a0
caps.latest.revision: 23
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1f210aa8e33859f41046edc8e524cbfbeaf5417b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49898610"
---
# <a name="msbuild-inline-tasks"></a>Tarefas embutidas do MSBuild
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
As tarefas do MSBuild normalmente são criadas ao compilar uma classe que implementa a interface <xref:Microsoft.Build.Framework.ITask>. Para obter mais informações, consulte [Tarefas](../msbuild/msbuild-tasks.md).  
  
 A partir do .NET Framework versão 4, você pode criar tarefas embutidas no arquivo de projeto. Você não precisa criar um assembly separado para hospedar a tarefa. Isso facilita o controle do código-fonte e a implantação da tarefa. O código-fonte é integrado ao script.  
  
## <a name="the-structure-of-an-inline-task"></a>A estrutura de uma tarefa em linha  
 Uma tarefa em linha é contida por um elemento [UsingTask](../msbuild/usingtask-element-msbuild.md). A tarefa em linha e o elemento `UsingTask` que a contém normalmente são incluídos em um arquivo .targets e importados para outros arquivos de projeto conforme a necessidade. Veja uma tarefa básica em linha. Observe que ela não faz nada.  
  
```  
<Project ToolsVersion="12.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <!-- This simple inline task does nothing. -->  
  <UsingTask  
    TaskName="DoNothing"  
    TaskFactory="CodeTaskFactory"  
    AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v12.0.dll" >  
    <ParameterGroup />  
    <Task>  
      <Reference Include="" />  
      <Using Namespace="" />  
      <Code Type="Fragment" Language="cs">  
      </Code>  
    </Task>  
  </UsingTask>  
</Project>  
```  
  
 O elemento `UsingTask` no exemplo tem três atributos que descrevem a tarefa e a fábrica de tarefas em linha que a compila.  
  
- O atributo `TaskName` nomeia a tarefa, neste caso, `DoNothing`.  
  
- O atributo `TaskFactory` nomeia a classe que implementa a fábrica de tarefas em linha.  
  
- O atributo `AssemblyFile` fornece o local da fábrica de tarefas em linha. Como alternativa, você pode usar o atributo `AssemblyName` para especificar o nome totalmente qualificado da classe de fábrica de tarefas em linha, que normalmente está localizado no GAC (cache de assembly global).  
  
  Os elementos restantes da tarefa `DoNothing` estão vazios w são fornecidos para ilustrar a ordem e a estrutura de uma tarefa em linha. Um exemplo mais robusto será apresentado posteriormente neste tópico.  
  
- O elemento `ParameterGroup` é opcional. Quando especificado, ele declara os parâmetros para a tarefa. Para saber mais sobre os parâmetros de entrada e saídas, confira "Parâmetros de entrada e saída" posteriormente neste tópico.  
  
- O elemento `Task` descreve e contém o código de origem da tarefa.  
  
- O elemento `Reference` especifica referências aos assemblies do .NET que você está usando em seu código. Isso equivale à adição de uma referência a um projeto no Visual Studio. O atributo `Include` especifica o caminho do assembly referenciado.  
  
- O elemento `Using` lista os namespaces que você deseja acessar. Isso se assemelha à instrução `Using` no Visual C#. O atributo `Namespace` especifica o namespace a ser incluído.  
  
  Os elementos `Reference`e `Using` independem da linguagem. As tarefas em linha podem ser escritas em qualquer idioma com suporte do CodeDom .NET, por exemplo, Visual Basic ou Visual C#.  
  
> [!NOTE]
>  Os elementos contidos pelo elemento `Task` são específicos da fábrica de tarefas, nesse caso, a fábrica de tarefas de código.  
  
### <a name="code-element"></a>Elemento Code  
 O último elemento filho a aparecer no elemento `Task` é o elemento `Code`. O elemento `Code` contém ou localiza o código que você deseja compilar em uma tarefa. O que é colocado no elemento `Code` depende de como você deseja escrever a tarefa.  
  
 O atributo `Language` especifica a linguagem em que seu código é escrito. Os valores aceitáveis são `cs` para C#, `vb` para Visual Basic.  
  
 O atributo `Type` especifica o tipo de código que é encontrado no elemento `Code`.  
  
- Se o valor de `Type` é `Class`, o elemento `Code` contém o código para uma classe que deriva da interface <xref:Microsoft.Build.Framework.ITask>.  
  
- Se o valor de `Type` é `Method`, o código define uma substituição do método `Execute` da interface <xref:Microsoft.Build.Framework.ITask>.  
  
- Se o valor de `Type` é `Fragment`, o código define o conteúdo do método `Execute`, mas não a assinatura ou a instrução `return`.  
  
  O próprio código normalmente aparece entre um marcador `<![CDATA[` e um marcador `]]>`. Como o código está em uma seção CDATA, você não precisa se preocupar com o escape de caracteres reservados, por exemplo, "\<" ou ">".  
  
  Como alternativa, você pode usar o atributo `Source` do elemento `Code` para especificar o local de um arquivo que contém o código da sua tarefa. O código no arquivo de origem deve ser do tipo especificado pelo atributo `Type`. Se o atributo `Source` estiver presente, o valor padrão de `Type` será `Class`. Se `Source` é não estiver presente, o valor padrão será `Fragment`.  
  
> [!NOTE]
>  Ao definir a classe de tarefa no arquivo de origem, o nome da classe deve concordar com o atributo `TaskName` do elemento [UsingTask](../msbuild/usingtask-element-msbuild.md) correspondente.  
  
## <a name="hello-world"></a>Hello World  
 Vejamos uma tarefa em linha mais robusta. A tarefa HelloWorld exibe "Hello, world!" no dispositivo de registro de erros em log padrão, que é normalmente o console do sistema ou a janela **Saída** do Visual Studio. O elemento `Reference` no exemplo é incluído apenas para ilustração.  
  
```  
<Project ToolsVersion="12.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <!-- This simple inline task displays "Hello, world!" -->  
  <UsingTask  
    TaskName="HelloWorld"  
    TaskFactory="CodeTaskFactory"  
    AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v4.0.dll" >  
    <ParameterGroup />  
    <Task>  
      <Reference Include="System.Xml"/>  
      <Using Namespace="System"/>  
      <Using Namespace="System.IO"/>  
      <Code Type="Fragment" Language="cs">  
<![CDATA[  
// Display "Hello, world!"  
Log.LogError("Hello, world!");  
]]>  
      </Code>  
    </Task>  
  </UsingTask>  
</Project>  
```  
  
 Você pode salvar a tarefa HelloWorld em um arquivo chamado HelloWorld.targets e chamá-la de um projeto da maneira a seguir.  
  
```  
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <Import Project="HelloWorld.targets" />  
  <Target Name="Hello">  
    <HelloWorld />  
  </Target>  
</Project>  
```  
  
## <a name="input-and-output-parameters"></a>Parâmetros de entrada e saída  
 Os parâmetros de tarefa em linha são elementos filhos de um elemento `ParameterGroup`. Cada parâmetro tem o nome do elemento que o define. O código a seguir define o parâmetro `Text`.  
  
```  
<ParameterGroup>  
    <Text />  
</ParameterGroup>  
```  
  
 Os parâmetros podem ter um ou mais destes atributos:  
  
- `Required` é um atributo opcional que é `false` por padrão. Se `true`, o parâmetro é necessário e deve receber um valor antes de chamar a tarefa.  
  
- `ParameterType` é um atributo opcional que é `System.String` por padrão. Ele pode ser definido como qualquer tipo totalmente qualificado que seja um item ou um valor que pode ser convertido em uma cadeia de caracteres usando System.Convert.ChangeType. (Em outras palavras, qualquer tipo que possa ser passado de e para uma tarefa externa.)  
  
- `Output` é um atributo opcional que é `false` por padrão. Se `true`, o parâmetro deve receber um valor antes de retornar do método Execute.  
  
  Por exemplo,  
  
```  
<ParameterGroup>  
    <Expression Required="true" />  
      <Files ParameterType="Microsoft.Build.Framework.ITaskItem[]" Required="true" />  
    <Tally ParameterType="System.Int32" Output="true" />  
</ParameterGroup>  
```  
  
 define esses três parâmetros:  
  
- `Expression` é um parâmetro de entrada obrigatório do tipo System.String.  
  
- `Files` é um parâmetro de entrada de lista do item obrigatório.  
  
- `Tally`é um parâmetro de saída do tipo System.Int32.  
  
  Se o elemento `Code` tem o atributo `Type` de `Fragment` ou `Method`, as propriedades são criadas automaticamente para cada parâmetro. Caso contrário, as propriedades devem ser declaradas explicitamente no código-fonte da tarefa e devem coincidir exatamente com suas definições de parâmetro.  
  
## <a name="example"></a>Exemplo  
 A tarefa em linha a seguir substitui todas as ocorrências de um token no arquivo especificado pelo valor especificado.  
  
```  
<Project xmlns='http://schemas.microsoft.com/developer/msbuild/2003' ToolsVersion="12.0">  
  
  <UsingTask TaskName="TokenReplace" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v12.0.dll">  
    <ParameterGroup>  
      <Path ParameterType="System.String" Required="true" />  
      <Token ParameterType="System.String" Required="true" />  
      <Replacement ParameterType="System.String" Required="true" />  
    </ParameterGroup>  
    <Task>  
      <Code Type="Fragment" Language="cs"><![CDATA[  
string content = File.ReadAllText(Path);  
content = content.Replace(Token, Replacement);  
File.WriteAllText(Path, content);  
  
]]></Code>  
    </Task>  
  </UsingTask>  
  
  <Target Name='Demo' >  
    <TokenReplace Path="C:\Project\Target.config" Token="$MyToken$" Replacement="MyValue"/>  
  </Target>  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Passo a passo: criando uma tarefa embutida](../msbuild/walkthrough-creating-an-inline-task.md)



