---
title: 'Passo a passo: criando uma tarefa embutida | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, tutorial
- MSBuild, tasks
ms.assetid: 438194cb-668c-41a9-a7e2-c118d14c1ea7
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d345d532c29931577edbe0441003cc80b069e335
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85289138"
---
# <a name="walkthrough-create-an-inline-task"></a>Passo a passo: Criar uma tarefa embutida

As tarefas do MSBuild normalmente são criadas ao compilar uma classe que implementa a interface <xref:Microsoft.Build.Framework.ITask>. A partir do .NET Framework versão 4, você pode criar tarefas embutidas no arquivo de projeto. Você não precisa criar um assembly separado para hospedar a tarefa. Para obter mais informações, consulte [tarefas em linha](../msbuild/msbuild-inline-tasks.md).

 Este passo a passo mostra como criar e executar essas tarefas embutidas:

- Uma tarefa que não tem nenhum parâmetro de entrada ou saída.

- Uma tarefa que não tem nenhum parâmetro de entrada e nenhum parâmetro de saída.

- Uma tarefa que tem dois parâmetros de entrada e um parâmetro de saída que retorna uma propriedade MSBuild.

- Uma tarefa que tem dois parâmetros de entrada e um parâmetro de saída que retorna um item MSBuild.

Para criar e executar as tarefas, use o Visual Studio e a **janela de prompt de comando do Visual Studio**, da seguinte maneira:

1. Criae um arquivo de projeto do MSBuild usando o Visual Studio.

2. Modifique o arquivo de projeto no Visual Studio para criar a tarefa embutida.

3. Use a **Janela de Prompt de Comando** para compilar o projeto e examinar os resultados.

## <a name="create-and-modify-an-msbuild-project"></a>Criar e modificar um projeto do MSBuild

 O sistema de projetos do Visual Studio é baseado no MSBuild. Portanto, você pode criar um arquivo de projeto de build usando o Visual Studio. Nesta seção, você criará um arquivo de projeto do Visual C#. (Em vez disso, você também pode criar um arquivo de projeto do Visual Basic. No contexto deste tutorial, a diferença entre os dois arquivos de projeto é secundária.)

#### <a name="to-create-and-modify-a-project-file"></a>Para criar e modificar um arquivo de projeto

1. No Visual Studio, crie um novo projeto usando o modelo de **aplicativo Windows Forms** C#. Na caixa **Nome**, digite `InlineTasks`. Digite um **Local** para a solução, por exemplo, *D:\\*. Certifique-se de que **Criar diretório para a solução** está selecionado, **Adicionar ao Controle do Código-Fonte** não está marcado e que **Nome da Solução** é **InlineTasks**.

3. Clique em **OK** para criar o arquivo de projeto.

3. Em **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto **InlineTasks** e clique em **descarregar projeto**.

4. Clique com o botão direito do mouse no nó de projeto novamente e clique em **Editar InlineTasks.csproj**.

     O arquivo de projeto aparecerá no editor de códigos.

## <a name="add-a-basic-hello-task"></a>Adicionar uma tarefa básica Hello

 Agora, adicione o arquivo de projeto uma tarefa básica que exibe a mensagem "Olá, mundo!" Também adicione um destino de TestBuild padrão para invocar a tarefa.

#### <a name="to-add-a-basic-hello-task"></a>Para adicionar uma tarefa básica Hello

1. Na no nó raiz `Project`, altere o atributo `DefaultTargets` para `TestBuild`. O nó `Project` resultante deve ser semelhante a este exemplo:

   ```xml
   <Project ToolsVersion="4.0" DefaultTargets="TestBuild" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
   ```

2. Adicione a seguinte tarefa embutida e o seguinte destino ao arquivo de projeto, imediatamente antes da marca `</Project>`.

   ```xml
   <UsingTask TaskName="Hello" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v4.0.dll" >
     <ParameterGroup />
     <Task>
       <Code Type="Fragment" Language="cs">
         Log.LogMessage(MessageImportance.High, "Hello, world!");
       </Code>
     </Task>
   </UsingTask>
   <Target Name="TestBuild">
     <Hello />
   </Target>
   ```

3. Salve o arquivo de projeto.

   Esse código cria uma tarefa embutida chamada Hello e não tem parâmetros, referências ou `Using` diretivas. A tarefa Olá contém apenas uma linha de código, que exibe uma mensagem de saudação do dispositivo de registro em log padrão, normalmente a janela do console.

### <a name="run-the-hello-task"></a>Executar a tarefa Hello

 Execute o MSBuild com a **janela Prompt de comando** para construir a tarefa Olá e processar o destino TestBuild que a invoca.

##### <a name="to-run-the-hello-task"></a>Para executar a tarefa Olá

1. Clique em **Iniciar**, clique em **Todos os Programas** e, em seguida, localize a pasta **Ferramentas do Visual Studio** e clique em **Prompt de Comando do Visual Studio**.

2. Na **janela do prompt de comando**, localize a pasta que contém o arquivo de projeto, neste caso, *D:\InlineTasks\InlineTasks \\ *.

3. Digite **MSBuild** sem opções de comando e pressione **Enter**. Por padrão, isso cria o arquivo *InlineTasks. csproj* e processa o TestBuild de destino padrão, que invoca a tarefa de saudação.

4. Examine a saída na **janela do Prompt de Comando**. Você deverá ver esta linha:

    `Hello, world!`

   > [!NOTE]
   > Se você não vir a mensagem de saudação, tente salvar o arquivo de projeto novamente e, em seguida, execute a tarefa de Olá.

   Ao alternar entre o editor de códigos e a **janela do Prompt de Comando**, você poderá alterar o arquivo de projeto e ver os resultados rapidamente.

## <a name="define-the-echo-task"></a>Definir a tarefa Echo

 Crie uma tarefa embutida que aceita um parâmetro de cadeia de caracteres e exibe a cadeia de caracteres no dispositivo de registro em log padrão.

#### <a name="to-define-the-echo-task"></a>Para definir a tarefa Echo

1. No editor de código, substitua a tarefa Olá e o destino TestBuild usando o código a seguir.

   ```xml
   <UsingTask TaskName="Echo" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v4.0.dll" >
     <ParameterGroup>
       <Text Required="true" />
     </ParameterGroup>
     <Task>
       <Code Type="Fragment" Language="cs">
         Log.LogMessage(MessageImportance.High, Text);
       </Code>
     </Task>
   </UsingTask>
   <Target Name="TestBuild">
     <Echo Text="Greetings!" />
   </Target>
   ```

2. Na **janela do prompt de comando**, digite **MSBuild** sem opções de comando e pressione **Enter**. Por padrão, isso processa o TestBuild de destino padrão, que invoca a tarefa Echo.

3. Examine a saída na **janela do Prompt de Comando**. Você deverá ver esta linha:

    `Greetings!`

   Esse código define uma tarefa embutida chamada Echo e tem apenas um parâmetro de entrada Text necessário. Por padrão, os parâmetros são do tipo System.String. O valor do parâmetro Text é definido quando o destino TestBuild invoca a tarefa de Echo.

## <a name="define-the-adder-task"></a>Definir a tarefa Adder

 Crie uma tarefa embutida que adiciona dois parâmetros inteiros e emite sua soma como uma propriedade de MSBuild.

#### <a name="to-define-the-adder-task"></a>Para definir a tarefa Adder

1. No editor de código, substitua a tarefa Echo e o destino TestBuild usando o código a seguir.

   ```xml
   <UsingTask TaskName="Adder" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v4.0.dll" >
     <ParameterGroup>
       <A ParameterType="System.Int32" Required="true" />
       <B ParameterType="System.Int32" Required="true" />
       <C ParameterType="System.Int32" Output="true" />
     </ParameterGroup>
     <Task>
       <Code Type="Fragment" Language="cs">
         C = A + B;
       </Code>
     </Task>
   </UsingTask>
   <Target Name="TestBuild">
     <Adder A="4" B="5">
       <Output PropertyName="Sum" TaskParameter="C" />
     </Adder>
     <Message Text="The sum is $(Sum)" Importance="High" />
   </Target>
   ```

2. Na **janela do prompt de comando**, digite **MSBuild** sem opções de comando e pressione **Enter**. Por padrão, isso processa o TestBuild de destino padrão, que invoca a tarefa Echo.

3. Examine a saída na **janela do Prompt de Comando**. Você deverá ver esta linha:

    `The sum is 9`

   Esse código define uma tarefa embutida chamada Adder e tem dois parâmetros necessários de entrada de inteiro, A e B, além de um parâmetro de saída inteiro, C. A tarefa adicionador adiciona dois parâmetros de entrada e retorna a soma no parâmetro de saída. A soma é emitida como a propriedade `Sum` do MSBuild. Os valores dos parâmetros de entrada são definidos quando o destino TestBuild invoca a tarefa Adder.

## <a name="define-the-regx-task"></a>Definir a tarefa RegX

 Crie uma tarefa embutida que aceite um grupo de itens e uma expressão regular e retorne uma lista de todos os itens que tenham conteúdo do arquivo que corresponda à expressão.

#### <a name="to-define-the-regx-task"></a>Para definir a tarefa RegX

1. No editor de código, substitua a tarefa Adder e o destino TestBuild usando o código a seguir.

   ```xml
   <UsingTask TaskName="RegX" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v4.0.dll" >
     <ParameterGroup>
       <Expression Required="true" />
       <Files ParameterType="Microsoft.Build.Framework.ITaskItem[]" Required="true" />
       <Result ParameterType="Microsoft.Build.Framework.ITaskItem[]" Output="true" />
     </ParameterGroup>
     <Task>
       <Using Namespace="System.Text.RegularExpressions"/>
       <Code Type="Fragment" Language="cs">
   <![CDATA[
         if (Files.Length > 0)
         {
           Result = new TaskItem[Files.Length];
           for (int i = 0; i < Files.Length; i++)
           {
             ITaskItem item = Files[i];
             string path = item.GetMetadata("FullPath");
             using(StreamReader rdr = File.OpenText(path))
             {
               if (Regex.Match(rdr.ReadToEnd(), Expression).Success)
               {
                 Result[i] = new TaskItem(item.ItemSpec);
               }
             }
           }
         }
   ]]>
       </Code>
     </Task>
   </UsingTask>
   <Target Name="TestBuild">
     <RegX Expression="public|protected" Files="@(Compile)">
       <Output ItemName="MatchedFiles" TaskParameter="Result" />
     </RegX>
     <Message Text="Input files: @(Compile)" Importance="High" />
     <Message Text="Matched files: @(MatchedFiles)" Importance="High" />
   </Target>
   ```

2. Na **janela do prompt de comando**, digite **MSBuild** sem opções de comando e pressione **Enter**. Por padrão, isso processa o TestBuild de destino padrão, que invoca a tarefa RegX.

3. Examine a saída na **janela do Prompt de Comando**. Você deverá ver estas linhas:

   ```
   Input files: Form1.cs;Form1.Designer.cs;Program.cs;Properties\AssemblyInfo.cs;Properties\Resources.Designer.cs;Properties\Settings.Designer.cs
   ```

   ```
   Matched files: Form1.cs;Form1.Designer.cs;Properties\Settings.Designer.cs
   ```

   Esse código define uma tarefa embutida chamada RegX e tem estes três parâmetros:

- `Expression` é um parâmetro de entrada de cadeia de caracteres obrigatório que tem um valor que é a expressão regular com a qual a correspondência deve ser realizada. Neste exemplo, a expressão corresponde às palavras "public" ou "protected".

- `Files` é um parâmetro de entrada de lista de item obrigatório que tem um valor que é uma lista de arquivos a serem pesquisados em busca da correspondência. Neste exemplo, `Files` é definido como o item `Compile`, que lista os arquivos de origem do projeto.

- `Result` é um parâmetro de saída que tem um valor que é a lista de arquivos com o conteúdo que corresponde à expressão regular.

  Os valores dos parâmetros de entrada são definidos quando o destino TestBuild invoca a tarefa RegX. A tarefa RegX lê todos os arquivos e retorna a lista de arquivos que correspondem à expressão regular. Essa lista é retornada como o parâmetro de saída `Result`, que é emitido como o item `MatchedFiles` do MSBuild.

### <a name="handle-reserved-characters"></a>Gerenciar caracteres reservados

 O analisador de MSBuild processa tarefas embutidas como XML. Os caracteres que têm significado reservado em XML, por exemplo, " \<" and "> ", são detectados e manipulados como se fossem XML, e não o código-fonte do .net. Para incluir os caracteres reservados em expressões de código como `Files.Length > 0`, escreva o elemento `Code` para que seu conteúdo fique contido em uma expressão CDATA, da seguinte maneira:

 ```xml
<Code Type="Fragment" Language="cs">
  <![CDATA[

  if (Files.Length > 0)
  {
      // Your code goes here.
  }
  ]]>
</Code>
```

## <a name="see-also"></a>Veja também

- [Tarefas embutidas](../msbuild/msbuild-inline-tasks.md)
- [Tarefas](../msbuild/msbuild-tasks.md)
- [Destinos](../msbuild/msbuild-targets.md)
