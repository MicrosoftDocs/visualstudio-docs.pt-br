---
title: 'Instruções passo a passo: usando o MSBuild | Microsoft Docs'
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
- MSBuild, tutorial
ms.assetid: b8a8b866-bb07-4abf-b9ec-0b40d281c310
caps.latest.revision: 34
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 56d8ea0c4b79764c1326c96b42748b8291349ac2
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49841411"
---
# <a name="walkthrough-using-msbuild"></a>Instruções passo a passo: usando o MSBuild
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O MSBuild é a plataforma de build da Microsoft e do Visual Studio. Estas instruções passo a passo apresentam os componentes essenciais do MSBuild e mostram como gravar, manipular e depurar projetos do MSBuild. Você aprenderá a:  
  
- Criar e manipular um arquivo de projeto.  
  
- Usar as propriedades de build  
  
- Usar itens de build.  
  
  Você pode executar o MSBuild no Visual Studio ou na janela Comando. Nestas instruções passo a passo, você criará um arquivo de projeto do MSBuild usando o Visual Studio. Você editará o arquivo de projeto no Visual Studio e usará uma janela Comando para compilar o projeto e examinar os resultados.  
  
## <a name="creating-an-msbuild-project"></a>Criando um projeto do MSBuild  
 O sistema de projetos do Visual Studio é baseado no MSBuild. Isso facilita a criação de um novo arquivo de projeto usando o Visual Studio. Nesta seção, você criará um arquivo de projeto do Visual C#. Você também poderá escolher criar um arquivo de projeto do Visual Basic. No contexto destas instruções passo a passo, a diferença entre os dois arquivos de projeto é secundária.  
  
#### <a name="to-create-a-project-file"></a>Para criar um arquivo de projeto  
  
1.  Abra o Visual Studio.  
  
2.  No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.  
  
3.  Na caixa de diálogo **Novo Projeto**, selecione o tipo de projeto do Visual C# e o modelo do **Aplicativo do Windows Forms**. Na caixa **Nome**, digite `BuildApp`. Insira um **Local** para a solução, por exemplo, `D:\`. Aceite os padrões para **Criar diretório para a solução** (marcado), **Adicionar ao Controle do Código-Fonte** (não marcado) e **Nome da Solução** (`BuildApp`).  
  
     Clique em **OK** para criar o arquivo de projeto.  
  
## <a name="examining-the-project-file"></a>Examinando o arquivo de projeto  
 Na seção anterior, você usou o Visual Studio para criar um arquivo de projeto do Visual C#. O arquivo de projeto é representado no **Gerenciador de Soluções** pelo nó de projeto chamado BuildApp. Você pode usar o editor de códigos do Visual Studio para examinar o arquivo de projeto.  
  
#### <a name="to-examine-the-project-file"></a>Para examinar o arquivo de projeto  
  
1.  No **Gerenciador de Soluções**, clique no nó de projeto BuildApp.  
  
2.  No navegador **Propriedades**, observe que a propriedade de **Arquivo de Projeto** é BuildApp.csproj. Todos os arquivos de projeto são nomeados com o sufixo "proj". Se você tivesse criado um projeto do Visual Basic, o nome do arquivo de projeto seria BuildApp.vbproj.  
  
3.  Clique com o botão direito do mouse no nó do projeto e clique em **Descarregar Projeto**.  
  
4.  Clique com o botão direito do mouse no nó de projeto novamente e clique em **Editar BuildApp.csproj**.  
  
     O arquivo de projeto aparecerá no editor de códigos.  
  
## <a name="targets-and-tasks"></a>Destinos e tarefas  
 Os arquivos de projeto são arquivos formatados em XML com o nó raiz [Project](../msbuild/project-element-msbuild.md).  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<Project ToolsVersion="12.0" DefaultTargets="Build"  xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
```  
  
 Você deve especificar o namespace xmlns no elemento Project.  
  
 O trabalho de compilar um aplicativo é feito com os elementos [Target](../msbuild/target-element-msbuild.md) e [Task](../msbuild/task-element-msbuild.md).  
  
- Uma tarefa é a menor unidade de trabalho ou, em outras palavras, é o "átomo" de um build. As tarefas são componentes executáveis independentes que podem ter entradas e saídas. Não existem tarefas referenciadas ou definidas no arquivo de projeto no momento. Você adicionará tarefas ao arquivo de projeto nas seções a seguir. Para obter mais informações, consulte o tópico [Tarefas](../msbuild/msbuild-tasks.md).  
  
- Um destino é uma sequência nomeada de tarefas. No momento, há dois destinos ao final do arquivo de projeto incluídos nos comentários HTML: BeforeBuild e AfterBuild.  
  
  ```  
  <Target Name="BeforeBuild">  
  </Target>  
  <Target Name="AfterBuild">  
  </Target>  
  ```  
  
   Para obter mais informações, consulte o tópico [Destinos](../msbuild/msbuild-targets.md).  
  
  No nó Project há um atributo DefaultTargets opcional que seleciona o destino padrão para o build, o qual, neste caso, é Build.  
  
```  
<Project ToolsVersion="12.0" DefaultTargets="Build" ...  
```  
  
 O destino de Build não está definido no arquivo de projeto. Em vez disso, ele é importado de Microsoft.CSharp.targets usando o elemento [Import](../msbuild/import-element-msbuild.md).  
  
```  
<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />  
```  
  
 Os arquivos importados são efetivamente inseridos no arquivo de projeto sempre que são referenciados.  
  
 O MSBuild controla os destinos de um build e garante que cada destino seja compilado não mais de uma vez.  
  
## <a name="adding-a-target-and-a-task"></a>Adicionando um destino e uma tarefa  
 Adicione um destino ao arquivo de projeto. Adicione uma tarefa ao destino que exibe uma mensagem.  
  
#### <a name="to-add-a-target-and-a-task"></a>Para adicionar um destino e uma tarefa  
  
1. Adicione estas linhas ao arquivo de projeto logo após a instrução Import:  
  
   ```  
   <Target Name="HelloWorld">  
   </Target>  
   ```  
  
    Com isso, um destino chamado HelloWorld será criado. Observe que você tem suporte ao IntelliSense ao editar o arquivo de projeto.  
  
2. Adicione linhas ao destino HelloWorld de modo que a seção resultante tenha esta aparência:  
  
   ```  
   <Target Name="HelloWorld">  
     <Message Text="Hello"></Message>  <Message Text="World"></Message>  
   </Target>  
   ```  
  
3. Salve o arquivo de projeto.  
  
   A tarefa Message é uma das muitas tarefas fornecidas com o MSBuild. Para obter uma lista completa das tarefas disponíveis e informações de uso, consulte [Referência das tarefas](../msbuild/msbuild-task-reference.md).  
  
   A tarefa Message usa o valor de cadeia de caracteres do atributo Text como entrada e o exibe no dispositivo de saída. O destino HelloWorld executa a tarefa Message duas vezes: primeiro para exibir "Hello" e, em seguida, para exibir "World".  
  
## <a name="building-the-target"></a>Compilando o destino  
 Execute o MSBuild no **Prompt de Comando do Visual Studio** para compilar o destino HelloWorld definido acima. Use a opção de linha de comando /target ou /t para selecionar o destino.  
  
> [!NOTE]
>  Vamos nos referir ao **Prompt de Comando do Visual Studio** como a **janela Comando** nas seções a seguir.  
  
#### <a name="to-build-the-target"></a>Para compilar o destino  
  
1.  Clique em **Iniciar** e em **Todos os Programas**. Localize e clique no **Prompt de Comando do Visual Studio**, na pasta **Ferramentas do Visual Studio**.  
  
2.  Na janela Comando, acesse a pasta que contém o arquivo de projeto, a qual, neste caso, é D:\BuildApp\BuildApp.  
  
3.  Execute msbuild com a opção de comando /t:HelloWorld. Com isso, o destino HelloWorld é selecionado e compilado:  
  
    ```  
    msbuild buildapp.csproj /t:HelloWorld  
    ```  
  
4.  Examine a saída na **janela Comando**. Você deverá ver as duas linhas "Hello" e "World":  
  
    ```  
    Hello  
    World  
    ```  
  
> [!NOTE]
>  Se em vez disso aparecer `The target "HelloWorld" does not exist in the project`, será porque você provavelmente se esqueceu de salvar o arquivo de projeto no editor de códigos. Salve o arquivo e tente novamente.  
  
 Ao alternar entre o editor de códigos e a janela Comando, você poderá alterar o arquivo de projeto e ver os resultados rapidamente.  
  
> [!NOTE]
>  Se você executar o msbuild sem a opção de comando /t, o msbuild compilará o destino fornecido pelo atributo DefaultTarget do elemento Project, o qual, neste caso, é "Build". Dessa forma, o Aplicativo do Windows Forms BuildApp.exe será compilado.  
  
## <a name="build-properties"></a>Propriedades de build  
 As propriedades de build são pares nome-valor que guiam o build. Várias propriedades de build já estão definidas na parte superior do arquivo de projeto:  
  
```  
<PropertyGroup>  
...  
  <ProductVersion>10.0.11107</ProductVersion>  
  <SchemaVersion>2.0</SchemaVersion>  
  <ProjectGuid>{30E3C9D5-FD86-4691-A331-80EA5BA7E571}</ProjectGuid>  
  <OutputType>WinExe</OutputType>  
...  
</PropertyGroup>  
```  
  
 Todas as propriedades são elementos filho dos elementos PropertyGroup. O nome da propriedade é o nome do elemento filho e o valor da propriedade é o elemento de texto do elemento filho. Por exemplo,  
  
```  
<TargetFrameworkVersion>v12.0</TargetFrameworkVersion>  
```  
  
 define a propriedade chamada TargetFrameworkVersion fornecendo a ela o valor de cadeia de caracteres "v12.0".  
  
 As propriedades de build podem ser redefinidas a qualquer momento. If  
  
```  
<TargetFrameworkVersion>v3.5</TargetFrameworkVersion>  
```  
  
 aparecer mais adiante no arquivo de projeto ou em um arquivo importado posteriormente no arquivo de projeto, a TargetFrameworkVersion usará o novo valor "v3.5".  
  
## <a name="examining-a-property-value"></a>Examinando um valor da propriedade  
 Para obter o valor de uma propriedade, use a seguinte sintaxe, em que PropertyName é o nome da propriedade:  
  
```  
$(PropertyName)  
```  
  
 Use essa sintaxe para examinar algumas das propriedades no arquivo de projeto.  
  
#### <a name="to-examine-a-property-value"></a>Para examinar um valor da propriedade  
  
1.  No editor de códigos, substitua o destino HelloWorld por este código:  
  
    ```  
    <Target Name="HelloWorld">  
      <Message Text="Configuration is $(Configuration)" />  
      <Message Text="MSBuildToolsPath is $(MSBuildToolsPath)" />  
    </Target>  
    ```  
  
2.  Salve o arquivo de projeto.  
  
3.  Na **janela Comando**, digite e execute esta linha:  
  
    ```  
    msbuild buildapp.csproj /t:HelloWorld  
    ```  
  
4.  Examine o resultado. Você deverá ver estas duas linhas (a sua versão do .NET Framework poderá ser diferente):  
  
    ```  
    Configuration is Debug  
    MSBuildToolsPath is C:\Program Files\MSBuild\12.0\bin  
    ```  
  
> [!NOTE]
>  Se essas linhas não aparecerem, será porque você provavelmente se esqueceu de salvar o arquivo de projeto no editor de códigos. Salve o arquivo e tente novamente.  
  
### <a name="conditional-properties"></a>Propriedades condicionais  
 Muitas propriedades, como Configuration, são definidas condicionalmente, ou seja, o atributo Condition aparece no elemento da propriedade. As propriedades condicionais serão definidas ou redefinidas somente se a condição for avaliada como "true". Observe que as propriedades indefinidas recebem o valor padrão de uma cadeia de caracteres vazia. Por exemplo,  
  
```  
<Configuration   Condition=" '$(Configuration)' == '' ">Debug</Configuration>  
```  
  
 significa "Se a propriedade Configuration ainda não foi definida, é preciso defini-la e atribuir a ela o valor 'Debug'".  
  
 Quase todos os elementos do MSBuild podem ter um atributo Condition. Para mais discussões sobre como usar o atributo Condition, consulte [Condições](../msbuild/msbuild-conditions.md).  
  
### <a name="reserved-properties"></a>Propriedades Reservadas  
 O MSBuild reserva alguns nomes de propriedade para armazenar informações sobre o arquivo de projeto e os binários do MSBuild. MSBuildToolsPath é um exemplo de uma propriedade reservada. As propriedades reservadas são referenciadas com a notação $ como qualquer outra propriedade. Para obter mais informações, consulte [Como referenciar o nome ou o local do arquivo de projeto](../msbuild/how-to-reference-the-name-or-location-of-the-project-file.md) e [Propriedades reservadas e conhecidas do MSBuild](../msbuild/msbuild-reserved-and-well-known-properties.md).  
  
### <a name="environment-variables"></a>Variáveis de ambiente  
 Você pode referenciar variáveis de ambiente em arquivos de projeto da mesma maneira que as propriedades de build. Por exemplo, para usar a variável de ambiente PATH em seu arquivo de projeto, use $(Path). Se o projeto contiver uma definição de propriedade que tem o mesmo nome que uma variável de ambiente, a propriedade no projeto substituirá o valor da variável de ambiente. Para obter mais informações, consulte [Como usar variáveis de ambiente em um build](../msbuild/how-to-use-environment-variables-in-a-build.md).  
  
## <a name="setting-properties-from-the-command-line"></a>Definindo propriedades na linha de comando  
 As propriedades podem ser definidas na linha de comando usando a opção de linha de comando /property ou /p. Os valores das propriedades recebidos da linha de comando substituem os valores das propriedades definidos no arquivo de projeto e nas variáveis de ambiente.  
  
#### <a name="to-set-a-property-value-from-the-command-line"></a>Para definir um valor da propriedade da linha de comando  
  
1. Na **janela Comando**, digite e execute esta linha:  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld /p:Configuration=Release  
   ```  
  
2. Examine o resultado. Você deverá ver esta linha:  
  
   ```  
   Configuration is Release.  
   ```  
  
   O MSBuild cria a propriedade Configuration e atribui a ela o valor "Release".  
  
## <a name="special-characters"></a>Caracteres especiais  
 Determinados caracteres têm significado especial em arquivos de projeto do MSBuild. O ponto e vírgula (;) e o asterisco (*) são exemplos desses caracteres. Para usar esses caracteres especiais como literais em um arquivo de projeto, eles devem ser especificados usando a sintaxe %xx, em que xx representa o valor hexadecimal ASCII do caractere.  
  
 Altere a tarefa Message para mostrar o valor da propriedade Configuration com caracteres especiais para torná-la mais legível.  
  
#### <a name="to-use-special-characters-in-the-message-task"></a>Para usar caracteres especiais na tarefa Message  
  
1. No editor de códigos, substitua ambas as tarefas Message por esta linha:  
  
   ```  
   <Message Text="%24(Configuration) is %22$(Configuration)%22" />  
   ```  
  
2. Salve o arquivo de projeto.  
  
3. Na **janela Comando**, digite e execute esta linha:  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld  
   ```  
  
4. Examine o resultado. Você deverá ver esta linha:  
  
   ```  
   $(Configuration) is "Debug"  
   ```  
  
   Para obter mais informações, consulte [Caracteres especiais no MSBuild](../msbuild/msbuild-special-characters.md).  
  
## <a name="build-items"></a>Compilar itens  
 Um item é uma informação, normalmente um nome de arquivo, que é usado como entrada no sistema de build. Por exemplo, uma coleção de itens que representam os arquivos de origem pode ser passada para uma tarefa chamada Compile para compilá-los em um assembly.  
  
 Todos os itens são elementos filho dos elementos ItemGroup. O nome do item é o nome do elemento filho e o valor do item é o valor do atributo Include do elemento filho. Os valores dos itens com o mesmo nome são coletados em tipos de item do nome.  Por exemplo,  
  
```  
<ItemGroup>  
    <Compile Include="Program.cs" />  
    <Compile Include="Properties\AssemblyInfo.cs" />  
</ItemGroup>  
```  
  
 define um grupo de itens que contém dois itens. O tipo de item Compile tem dois valores: "Program.cs" e "Properties\AssemblyInfo.cs".  
  
 O código a seguir cria o mesmo tipo de item declarando os dois arquivos em um atributo Include, separados por ponto e vírgula.  
  
```  
<ItemGroup>  
    <Compile Include="Program.cs;Properties\AssemblyInfo.cs" />  
</ItemGroup>  
```  
  
 Para obter mais informações, consulte [Itens](../msbuild/msbuild-items.md).  
  
> [!NOTE]
>  Os caminhos de arquivo são relativos à pasta que contém o arquivo de projeto do MSBuild.  
  
## <a name="examining-item-type-values"></a>Examinando os valores de tipo de item  
 Para obter os valores de um tipo de item, use a seguinte sintaxe, em que ItemType é o nome do tipo de item:  
  
```  
@(ItemType)  
```  
  
 Use essa sintaxe para examinar o tipo de item Compile no arquivo de projeto.  
  
#### <a name="to-examine-item-type-values"></a>Para examinar os valores de tipo de item  
  
1. No editor de códigos, substitua a tarefa do destino HelloWorld por este código:  
  
   ```  
   <Target Name="HelloWorld">  
     <Message Text="Compile item type contains @(Compile)" />  
   </Target>  
   ```  
  
2. Salve o arquivo de projeto.  
  
3. Na **janela Comando**, digite e execute esta linha:  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld  
   ```  
  
4. Examine o resultado. Você deverá ver esta linha longa:  
  
   ```  
   Compile item type contains Form1.cs;Form1.Designer.cs;Program.cs;Properties\AssemblyInfo.cs;Properties\Resources.Designer.cs;Properties\Settings.Designer.cs  
   ```  
  
   Por padrão, os valores de um tipo de item são separados por ponto e vírgula.  
  
   Para alterar o separador de um tipo de item, use a seguinte sintaxe, em que ItemType é o tipo de item e Separator é uma cadeia de caracteres de um ou mais caracteres de separação:  
  
```  
@(ItemType, Separator)  
```  
  
 Altere a tarefa Message para usar retornos de carro e alimentações de linha (%0A%0D) para exibir os itens Compile em linhas individuais.  
  
#### <a name="to-display-item-type-values-one-per-line"></a>Para exibir os valores de tipo de item em linhas individuais  
  
1.  No editor de códigos, substitua a tarefa Message por esta linha:  
  
    ```  
    <Message Text="Compile item type contains @(Compile, '%0A%0D')" />  
    ```  
  
2.  Salve o arquivo de projeto.  
  
3.  Na **janela Comando**, digite e execute esta linha:  
  
     `msbuild buildapp.csproj /t:HelloWorld`  
  
4.  Examine o resultado. Você deverá ver estas linhas:  
  
    ```  
    Compile item type contains Form1.cs  
    Form1.Designer.cs  
    Program.cs  
    Properties\AssemblyInfo.cs  
    Properties\Resources.Designer.cs  
    Properties\Settings.Designer.cs  
    ```  
  
### <a name="include-exclude-and-wildcards"></a>Incluir, excluir e curingas  
 Você pode usar os curingas "*", "\*\*" e "?" com o atributo Include para adicionar itens a um tipo de item. Por exemplo,  
  
```  
<Photos Include="images\*.jpeg" />  
```  
  
 adiciona todos os arquivos com a extensão de arquivo ".jpeg" na pasta de imagens ao tipo de item Photos, enquanto  
  
```  
<Photos Include="images\**.jpeg" />  
```  
  
 adiciona todos os arquivos com a extensão de arquivo ".jpeg" na pasta de imagens, juntamente com todas as subpastas, ao tipo de item Photos. Para obter mais exemplos, consulte [Como selecionar os arquivos a serem compilados](../msbuild/how-to-select-the-files-to-build.md).  
  
 Observe que, conforme os itens são declarados, eles são adicionados ao tipo de item. Por exemplo,  
  
```  
<Photos Include="images\*.jpeg" />  
<Photos Include="images\*.gif" />  
```  
  
 cria um tipo de item chamado Photo contendo todos os arquivos na pasta de imagens com uma extensão de arquivo ".jpeg" ou ".gif". Isso é equivalente à seguinte linha:  
  
```  
<Photos Include="images\*.jpeg;images\*.gif" />  
```  
  
 Você pode excluir um item de um tipo de item com o atributo Exclude. Por exemplo,  
  
```  
<Compile Include="*.cs" Exclude="*Designer*">  
```  
  
 adiciona todos os arquivos com a extensão de arquivo".cs" ao tipo de item Compile, exceto os arquivos cujos nomes contêm a cadeia de caracteres "Designer". Para obter mais exemplos, consulte [Como excluir arquivos do build](../msbuild/how-to-exclude-files-from-the-build.md).  
  
 O atributo Exclude afeta somente os itens adicionados pelo atributo Include no elemento do item que contém ambos. Por exemplo,  
  
```  
<Compile Include="*.cs" />  
<Compile Include="*.res" Exclude="Form1.cs">  
```  
  
 não excluiria o arquivo Form1.cs, que foi adicionado no elemento do item anterior.  
  
##### <a name="to-include-and-exclude-items"></a>Para incluir e excluir itens  
  
1.  No editor de códigos, substitua a tarefa Message por esta linha:  
  
    ```  
    <Message Text="Compile item type contains @(XFiles)" />  
    ```  
  
2.  Adicione esse grupo de itens logo após o elemento Import:  
  
    ```  
    <ItemGroup>  
       <XFiles Include="*.cs;properties/*.resx" Exclude="*Designer*" />  
    </ItemGroup>  
    ```  
  
3.  Salve o arquivo de projeto.  
  
4.  Na **janela Comando**, digite e execute esta linha:  
  
    ```  
    msbuild buildapp.csproj /t:HelloWorld  
    ```  
  
5.  Examine o resultado. Você deverá ver esta linha:  
  
    ```  
    Compile item type contains Form1.cs;Program.cs;Properties/Resources.resx  
    ```  
  
## <a name="item-metadata"></a>Metadados de item  
 Além das informações coletadas pelos atributos Include e Exclude, os itens podem conter metadados. Esses metadados podem ser usados por tarefas que exigem mais informações sobre os itens que apenas o valor do item.  
  
 Os metadados de item são declarados no arquivo de projeto criando um elemento com o nome dos metadados como um elemento filho do item. Um item pode ter zero ou mais valores de metadados. Por exemplo, o seguinte item CSFile tem metadados Culture com um valor de "Fr":  
  
```  
<ItemGroup>  
    <CSFile Include="main.cs">  
        <Culture>Fr</Culture>  
    </CSFile>  
</ItemGroup>  
```  
  
 Para obter o valor dos metadados de um tipo de item, use a seguinte sintaxe, em que ItemType é o nome do tipo de item e MetaDataName é o nome dos metadados:  
  
```  
%(ItemType.MetaDataName)  
```  
  
#### <a name="to-examine-item-metadata"></a>Para examinar metadados de item  
  
1. No editor de códigos, substitua a tarefa Message por esta linha:  
  
   ```  
   <Message Text="Compile.DependentUpon: %(Compile.DependentUpon)" />  
   ```  
  
2. Salve o arquivo de projeto.  
  
3. Na **janela Comando**, digite e execute esta linha:  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld  
   ```  
  
4. Examine o resultado. Você deverá ver estas linhas:  
  
   ```  
   Compile.DependentUpon:  
   Compile.DependentUpon: Form1.cs  
   Compile.DependentUpon: Resources.resx  
   Compile.DependentUpon: Settings.settings  
   ```  
  
   Observe que "Compile.DependentUpon" aparece várias vezes. O uso de metadados com essa sintaxe em um destino causa o "envio em lotes". Envio em lote significa que as tarefas no destino são executadas uma vez para cada valor exclusivo dos metadados. Trata-se do equivalente em script do MSBuild ao constructo comum de programação "loop for". Para obter mais informações, consulte [Envio em lote](../msbuild/msbuild-batching.md).  
  
### <a name="well-known-metadata"></a>Metadados conhecidos  
 Sempre que um item é adicionado a uma lista de itens, esse item recebe alguns metadados conhecidos. Por exemplo, %(Filename) retorna o nome de arquivo de qualquer item. Para obter uma lista completa dos metadados conhecidos, consulte [Metadados de itens conhecidos](../msbuild/msbuild-well-known-item-metadata.md).  
  
##### <a name="to-examine-well-known-metadata"></a>Para examinar os metadados conhecidos  
  
1. No editor de códigos, substitua a tarefa Message por esta linha:  
  
   ```  
   <Message Text="Compile Filename: %(Compile.Filename)" />  
   ```  
  
2. Salve o arquivo de projeto.  
  
3. Na **janela Comando**, digite e execute esta linha:  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld  
   ```  
  
4. Examine o resultado. Você deverá ver estas linhas:  
  
   ```  
   Compile Filename: Form1  
   Compile Filename: Form1.Designer  
   Compile Filename: Program  
   Compile Filename: AssemblyInfo  
   Compile Filename: Resources.Designer  
   Compile Filename: Settings.Designer  
   ```  
  
   Ao comparar os dois exemplos acima, você poderá ver que, embora nem todos os itens no tipo de item Compile tenham metadados DependentUpon, todos os itens têm os metadados conhecidos Filename.  
  
### <a name="metadata-transformations"></a>Transformações de metadados  
 As listas de itens podem ser transformadas em novas listas de itens. Para transformar uma lista de itens, use a seguinte sintaxe, em que ItemType é o nome do tipo de item e MetadataName é o nome dos metadados:  
  
```  
@(ItemType -> '%(MetadataName)')  
```  
  
 Por exemplo, uma lista de itens dos arquivos de origem pode ser transformada em uma coleção de arquivos-objeto usando uma expressão como `@(SourceFiles -> '%(Filename).obj')`. Para obter mais informações, consulte [Transformações](../msbuild/msbuild-transforms.md).  
  
##### <a name="to-transform-items-using-metadata"></a>Para transformar itens que usam metadados  
  
1. No editor de códigos, substitua a tarefa Message por esta linha:  
  
   ```  
   <Message Text="Backup files: @(Compile->'%(filename).bak')" />  
   ```  
  
2. Salve o arquivo de projeto.  
  
3. Na **janela Comando**, digite e execute esta linha:  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld  
   ```  
  
4. Examine o resultado. Você deverá ver esta linha:  
  
   ```  
   Backup files: Form1.bak;Form1.Designer.bak;Program.bak;AssemblyInfo.bak;Resources.Designer.bak;Settings.Designer.bak  
   ```  
  
   Observe que os metadados expressados nesta sintaxe não causam o envio em lote.  
  
## <a name="whats-next"></a>O que vem a seguir?  
 Para saber como criar um arquivo de projeto simples etapa por etapa, experimente o [Instruções passo a passo: criando um arquivo de projeto do MSBuild do zero](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md).  
  
## <a name="see-also"></a>Consulte também
[Visão geral do MSBuild](msbuild.md)  
 [Referência do MSBuild](../msbuild/msbuild-reference.md)


