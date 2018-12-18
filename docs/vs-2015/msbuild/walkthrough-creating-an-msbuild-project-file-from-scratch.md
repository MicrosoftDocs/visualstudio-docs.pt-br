---
title: 'Passo a passo: Criando um arquivo de projeto do MSBuild do zero | Microsoft Docs'
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
ms.assetid: e3acff7c-cb4e-4ae1-8be2-a871bcff847b
caps.latest.revision: 22
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ad32edc94bea49010dfb7073cacbd84419513783
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49913885"
---
# <a name="walkthrough-creating-an-msbuild-project-file-from-scratch"></a>Instruções passo a passo: criando um arquivo de projeto do MSBuild do zero
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
As linguagens de programação que tenham como destino o .NET Framework usam arquivos de projetos do MSBuild para descrever e controlar o processo de compilação de aplicativos. Quando você usa o Visual Studio para criar um arquivo de projeto do MSBuild, o XML apropriado é adicionado ao arquivo automaticamente. Entretanto, talvez você ache útil compreender como o XML é organizado e como é possível alterá-lo para controlar uma compilação.  
  
 Para obter informações sobre como criar um arquivo de projeto para um projeto em C++, consulte [MSBuild (Visual C++)](http://msdn.microsoft.com/library/7a1be7ff-0312-4669-adf2-5f5bf507d560).  
  
 Este passo a passo mostra como criar um arquivo de projeto básico de forma incremental, usando somente um editor de texto. Este passo a passo possui as seguintes etapas:  
  
- Criar um arquivo de origem de aplicativo mínimo.  
  
- Criar um arquivo de projeto MSBuild mínimo.  
  
- Estender a variável de ambiente PATH para incluir MSBuild.  
  
- Compilar o aplicativo usando o arquivo de projeto.  
  
- Adicionar propriedades para controlar a compilação.  
  
- Controlar a compilação alterando os valores de propriedade.  
  
- Adicionar destinos à compilação.  
  
- Controlar a compilação especificando destinos.  
  
- Compilar de forma incremental.  
  
  Este passo a passo mostra como compilar o projeto no prompt de comando e como examinar os resultados. Para obter mais informações sobre o MSBuild e como executá-lo no prompt de comandos, consulte [Passo a passo: Usando o MSBuild](../msbuild/walkthrough-using-msbuild.md).  
  
  Para concluir este passo a passo, você deve ter o .NET Framework (versão 2.0, 3.5, 4.0 ou 4.5) instalado, pois ele inclui o MSBuild, e o compilador do Visual C#.  
  
## <a name="creating-a-minimal-application"></a>Criando um aplicativo mínimo  
 Esta seção mostra como criar um arquivo de origem de aplicativo mínimo do Visual C# usando um editor de texto.  
  
#### <a name="to-create-the-minimal-application"></a>Para criar o aplicativo mínimo  
  
1.  No prompt de comando, navegue até a pasta na qual você deseja criar o aplicativo, por exemplo, \Meus Documentos\ ou \Área de Trabalho\\.  
  
2.  Digite **md HelloWorld** para criar uma subpasta chamada \HelloWorld\\.  
  
3.  Digite **cd HelloWorld** para mudar para a nova pasta.  
  
4.  Inicie o Bloco de Notas ou outro editor de texto e digite o código a seguir.  
  
    ```  
    using System;  
  
    class HelloWorld  
    {  
        static void Main()  
        {  
    #if DebugConfig  
            Console.WriteLine("WE ARE IN THE DEBUG CONFIGURATION");  
    #endif  
  
            Console.WriteLine("Hello, world!");  
        }  
    }  
    ```  
  
5.  Salve esse arquivo de código-fonte e o nomeie como Helloworld.cs.  
  
6.  Compile o aplicativo digitando **csc helloworld.cs** no prompt de comando.  
  
7.  Teste o aplicativo digitando **helloworld** no prompt de comando.  
  
     A mensagem **Hello, world!** deve ser exibida.  
  
8.  Exclua o aplicativo digitando **del helloworld.exe** no prompt de comando.  
  
## <a name="creating-a-minimal-msbuild-project-file"></a>Criando um arquivo de projeto MSBuild mínimo  
 Agora que você possui um arquivo de origem de aplicativo mínimo, poderá criar um arquivo de projeto mínimo para compilar o aplicativo. Esse arquivo de projeto contém os seguintes elementos:  
  
-   O nó raiz `Project` necessário.  
  
-   Um nó `ItemGroup` para conter elementos do item.  
  
-   Um elemento do item que se refere ao arquivo de origem do aplicativo.  
  
-   Um nó `Target` para conter tarefas que são necessárias para compilar o aplicativo.  
  
-   Um elemento `Task` para iniciar o compilador do Visual C# para compilar o aplicativo.  
  
#### <a name="to-create-a-minimal-msbuild-project-file"></a>Para criar um arquivo de projeto MSBuild mínimo  
  
1. No editor de texto, substitua o texto existente usando estas duas linhas:  
  
   ```  
   <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
   </Project>  
   ```  
  
2. Insira este nó `ItemGroup` como um elemento filho do nó `Project`:  
  
   ```  
   <ItemGroup>  
     <Compile Include="helloworld.cs" />  
   </ItemGroup>  
   ```  
  
    Observe que este `ItemGroup` já contém um elemento do item.  
  
3. Adicione um nó `Target` como um elemento filho do nó `Project`. Nomeie o nó `Build`.  
  
   ```  
   <Target Name="Build">  
   </Target>  
   ```  
  
4. Insira este elemento da tarefa como um elemento filho do nó `Target`:  
  
   ```  
   <Csc Sources="@(Compile)"/>  
   ```  
  
5. Salve esse arquivo de projeto e o nomeie como Helloworld.csproj.  
  
   O seu arquivo de projeto mínimo deve se assemelhar ao seguinte código:  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <ItemGroup>  
    <Compile Include="helloworld.cs" />  
  </ItemGroup>  
  <Target Name="Build">  
    <Csc Sources="@(Compile)"/>    
  </Target>  
</Project>  
```  
  
 As tarefas no destino Compilar são executadas em sequência. Nesse caso, a tarefa `Csc` do compilador do Visual C# é a única tarefa. Ela espera que uma lista de arquivos de origem seja compilada e isso ocorre pelo valor do item `Compile`. O item `Compile` faz referências a apenas um arquivo de origem, Helloworld.cs.  
  
> [!NOTE]
>  No elemento do item, você pode usar o caractere curinga de asterisco (*) para fazer referência a todos os arquivos que tenham a extensão de nome de arquivo .cs, como a seguir:  
>   
>  `<Compile Include="*.cs" />`  
>   
>  No entanto, não recomendamos o uso de caracteres curinga, pois eles tornam a depuração e o direcionamento seletivo mais difícil se arquivos de origem forem adicionados ou excluídos.  
  
## <a name="extending-the-path-to-include-msbuild"></a>Estendendo o caminho para incluir o MSBuild  
 Para poder acessar o MSBuild, você deve estender a variável de ambiente PATH para incluir a pasta do .NET Framework.  
  
#### <a name="to-add-msbuild-to-your-path"></a>Para adicionar o MSBuild ao seu caminho  
  
-   Iniciando no Visual Studio 2013, você pode localizar o MSBuild.exe na pasta do MSBuild (`%ProgramFiles%\MSBuild` em um sistema operacional de 32 bits ou `%ProgramFiles(x86)%\MSBuild` em um sistema operacional de 64 bits).  
  
     No prompt de comando, digite **definir PATH=%PATH%;%ProgramFiles%\MSBuild** ou **definir PATH=%PATH%;%ProgramFiles(x86)%\MSBuild**.  
  
     Como alternativa, se você tiver o Visual Studio instalado, poderá usar o **Prompt de comando do Visual Studio**, que tem um caminho que inclui a pasta do MSBuild.  
  
## <a name="using-the-project-file-to-build-the-application"></a>Usando o arquivo de projeto para compilar o aplicativo  
 Agora, para compilar o aplicativo, use o arquivo de projeto recém-criado.  
  
#### <a name="to-build-the-application"></a>Para compilar o aplicativo  
  
1.  No prompt de comando, digite **msbuild helloworld.csproj /t:Build**.  
  
     Ele compila o destino Compilar do arquivo de projeto Helloworld chamando o compilador do Visual C# para criar o aplicativo Helloworld.  
  
2.  Teste o aplicativo digitando **helloworld**.  
  
     A mensagem **Hello, world!** deve ser exibida.  
  
> [!NOTE]
>  Você pode ver mais detalhes sobre a compilação aumentando o nível de detalhamento. Para configurar o nível de detalhamento como "detalhado", digite um destes comandos no prompt de comando:  
>   
>  **msbuild helloworld.csproj /t:Build /verbosity:detailed**  
  
## <a name="adding-build-properties"></a>Adicionando propriedades de compilação  
 Você pode adicionar propriedades de compilação ao arquivo de projeto para controlar ainda mais a compilação. Agora, adicione estas propriedades:  
  
-   Uma propriedade `AssemblyName` para especificar o nome do aplicativo.  
  
-   Uma propriedade `OutputPath` para especificar uma pasta para conter o aplicativo.  
  
#### <a name="to-add-build-properties"></a>Para adicionar propriedades de compilação  
  
1. Exclua o aplicativo existente digitando **del helloworld.exe** no prompt de comando.  
  
2. No arquivo de projeto, insira este elemento `PropertyGroup` imediatamente depois de abrir o elemento `Project`:  
  
   ```  
   <PropertyGroup>  
     <AssemblyName>MSBuildSample</AssemblyName>  
     <OutputPath>Bin\</OutputPath>  
   </PropertyGroup>  
   ```  
  
3. Adicione esta tarefa no destino Compilar, imediatamente antes da tarefa `Csc`:  
  
   ```  
   <MakeDir Directories="$(OutputPath)"      Condition="!Exists('$(OutputPath)')" />  
   ```  
  
    A tarefa `MakeDir` cria uma pasta que é chamada pela propriedade `OutputPath`, contanto que não exista atualmente nenhuma pasta com esse nome.  
  
4. Adicione esse atributo `OutputAssembly` à tarefa `Csc`:  
  
   ```  
   <Csc Sources="@(Compile)" OutputAssembly="$(OutputPath)$(AssemblyName).exe" />  
   ```  
  
    Isso instrui o compilador do Visual C# a produzir um assembly que é chamado pela propriedade `AssemblyName` e para colocá-lo na pasta que é chamada pela propriedade `OutputPath`.  
  
5. Salve as alterações.  
  
   O seu arquivo de projeto deve agora se assemelhar ao seguinte código:  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <PropertyGroup>  
    <AssemblyName>MSBuildSample</AssemblyName>  
    <OutputPath>Bin\</OutputPath>  
  </PropertyGroup>  
  <ItemGroup>  
    <Compile Include="helloworld.cs" />  
  </ItemGroup>  
  <Target Name="Build">  
    <MakeDir Directories="$(OutputPath)" Condition="!Exists('$(OutputPath)')" />  
    <Csc Sources="@(Compile)" OutputAssembly="$(OutputPath)$(AssemblyName).exe" />  
  </Target>  
</Project>  
```  
  
> [!NOTE]
>  Recomendamos que você adicione um delimitador de caminho de barra invertida (\\) no final do nome da pasta ao especificá-lo no elemento `OutputPath`, em vez de adicioná-lo ao atributo `OutputAssembly` da tarefa `Csc`. Portanto,  
>   
>  `<OutputPath>Bin\</OutputPath>`  
>   
>  `OutputAssembly=="$(OutputPath)$(AssemblyName).exe" />`  
>   
>  é melhor que  
>   
>  `<OutputPath>Bin</OutputPath>`  
>   
>  `OutputAssembly=="$(OutputPath)\$(AssemblyName).exe" />`  
  
## <a name="testing-the-build-properties"></a>Testando as propriedades de compilação  
 Agora, você pode compilar o aplicativo usando o arquivo de projeto no qual usou as propriedades de compilação para especificar a pasta de saída e o nome do aplicativo.  
  
#### <a name="to-test-the-build-properties"></a>Para testar as propriedades de compilação  
  
1.  No prompt de comando, digite **msbuild helloworld.csproj /t:Build**.  
  
     Com isso, você cria a pasta \Bin\ e chama o compilador do Visual C# para criar o aplicativo MSBuildSample e colocá-lo na pasta \Bin\.  
  
2.  Para verificar se a pasta \Bin\ foi criada e se ela contém o aplicativo MSBuildSample, digite **dir Bin**.  
  
3.  Exclua o aplicativo digitando **Bin\MSBuildSample**.  
  
     A mensagem **Hello, world!** deve ser exibida.  
  
## <a name="adding-build-targets"></a>Adicionando destinos Compilar  
 Em seguida, adicione mais dois destinos ao arquivo de projeto, como a seguir:  
  
- Um destino Limpar que exclui arquivos antigos.  
  
- Um destino Recompilar que usa o atributo `DependsOnTargets` para forçar a tarefa Limpar a executar a tarefa Compilar.  
  
  Agora que você tem vários destinos, poderá configurar o destino Compilar como o destino padrão.  
  
#### <a name="to-add-build-targets"></a>Para adicionar destinos de compilação  
  
1. No arquivo de projeto, adicione esses dois destinos imediatamente após o destino Compilar:  
  
   ```  
   <Target Name="Clean" >  
     <Delete Files="$(OutputPath)$(AssemblyName).exe" />  
   </Target>  
   <Target Name="Rebuild" DependsOnTargets="Clean;Build" />  
   ```  
  
    O destino Limpar chama a tarefa Excluir para excluir o aplicativo. O destino Recompilar não é executado até que o destino Limpar e o destino Compilar tenham sido executados. Embora o destino Recompilar não tenha tarefas, ele faz com que o destino Limpar seja executado antes do destino Compilar.  
  
2. Adicione esse atributo `DefaultTargets` ao elemento `Project` inicial:  
  
   ```  
   <Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
   ```  
  
    Isso configura o destino Compilar como o destino padrão.  
  
   O seu arquivo de projeto deve agora se assemelhar ao seguinte código:  
  
```  
<Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <PropertyGroup>  
    <AssemblyName>MSBuildSample</AssemblyName>  
    <OutputPath>Bin\</OutputPath>  
  </PropertyGroup>  
  <ItemGroup>  
    <Compile Include="helloworld.cs" />  
  </ItemGroup>  
  <Target Name="Build">  
    <MakeDir Directories="$(OutputPath)" Condition="!Exists('$(OutputPath)')" />  
    <Csc Sources="@(Compile)" OutputAssembly="$(OutputPath)$(AssemblyName).exe" />  
  </Target>  
  <Target Name="Clean" >  
    <Delete Files="$(OutputPath)$(AssemblyName).exe" />  
  </Target>  
  <Target Name="Rebuild" DependsOnTargets="Clean;Build" />  
</Project>  
```  
  
## <a name="testing-the-build-targets"></a>Testando os destinos Compilar  
 Você pode experimentar os novos destinos de compilação para testar esses recursos do arquivo de projeto:  
  
-   Compilando a compilação padrão.  
  
-   Configurando o nome do aplicativo no prompt de comando.  
  
-   Excluindo o aplicativo antes de outro aplicativo ser compilado.  
  
-   Excluindo o aplicativo sem compilar outro aplicativo.  
  
#### <a name="to-test-the-build-targets"></a>Para testar os destinos de compilação  
  
1.  No prompt de comando, digite **msbuild helloworld.csproj /p:AssemblyName=Greetings**.  
  
     Como você não usou a opção **/t** para configurar de forma explícita o destino, o MSBuild executa o destino de build padrão. A opção **/p** substitui a propriedade `AssemblyName` e dá a ela o novo valor, `Greetings`. Isso faz com que um novo aplicativo, Greetings.exe, seja criado na pasta \Bin\.  
  
2.  Para verificar se a pasta \Bin\ contém o aplicativo MSBuildSample e o novo aplicativo Greetings, digite **dir Bin**.  
  
3.  Teste o aplicativo Greetings digitando **Bin\Greetings**.  
  
     A mensagem **Hello, world!** deve ser exibida.  
  
4.  Exclua o aplicativo MSBuildSample digitando **msbuild helloworld.csproj /t:clean**.  
  
     Isso executa a tarefa Limpar para remover o aplicativo que tem o `AssemblyName` valor da propriedade `MSBuildSample` padrão.  
  
5.  Exclua o aplicativo Greetings digitando **msbuild helloworld.csproj /t:clean /p:AssemblyName=Greetings**.  
  
     Isso executa a tarefa Limpar para remover o aplicativo que tem o valor da propriedade especificado **AssemblyName**, `Greetings`.  
  
6.  Para verificar se a pasta \Bin\ está vazia agora, digite **dir Bin**.  
  
7.  Digite **msbuild**.  
  
     Embora um arquivo de projeto não esteja especificado, o MSBuild compila o arquivo helloworld.csproj, pois há somente um arquivo na pasta atual. Isso faz com que um novo aplicativo MSBuildSample seja criado na pasta \Bin\.  
  
     Para verificar se a pasta \Bin\ contém o aplicativo MSBuildSample, digite **dir Bin**.  
  
## <a name="building-incrementally"></a>Compilando de forma incremental  
 Você pode informar ao MSBuild para compilar um destino somente se os arquivos de origem ou os arquivos de destino do qual dependem o destino tiverem sido alterados. O MSBuild usa o carimbo de data/hora de um arquivo para determinar se ele foi alterado.  
  
#### <a name="to-build-incrementally"></a>Para compilar de forma incremental  
  
1.  No arquivo de projeto, adicione esses atributos ao destino Compilar inicial:  
  
    ```  
    Inputs="@(Compile)" Outputs="$(OutputPath)$(AssemblyName).exe"  
    ```  
  
     Isso especifica que o destino Compilar depende dos arquivos de entrada especificados no grupo de itens `Compile` e que o destino de saída é o arquivo de aplicativo.  
  
     O destino Compilar resultante deve se assemelhar ao seguinte código:  
  
    ```  
    <Target Name="Build" Inputs="@(Compile)" Outputs="$(OutputPath)$(AssemblyName).exe">  
      <MakeDir Directories="$(OutputPath)" Condition="!Exists('$(OutputPath)')" />  
      <Csc Sources="@(Compile)" OutputAssembly="$(OutputPath)$(AssemblyName).exe" />  
    </Target>  
    ```  
  
2.  Teste o destino de build digitando **msbuild /v:d** no prompt de comando.  
  
     Lembre-se de que helloworld.csproj é o arquivo de projeto padrão e de que Compilar é o destino padrão.  
  
     A opção **/v:d** especifica uma descrição detalhada do processo de build.  
  
     Estas linhas devem ser exibidas:  
  
     **Ignorando o destino de "Build" porque todos os arquivos de saída estão atualizados em relação aos arquivos de entrada.**  
  
     **Arquivos de entrada: HelloWorld.cs**  
  
     **Arquivos de saída: BinMSBuildSample.exe**  
  
     O MSBuild ignora o destino Compilar, pois nenhum dos arquivos de origem foi alterado desde a última compilação do aplicativo.  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  
 O exemplo a seguir mostra um arquivo de projeto que compila um aplicativo [!INCLUDE[csprcs](../includes/csprcs-md.md)] e registra uma mensagem que contém o nome do arquivo de saída.  
  
### <a name="code"></a>Código  
  
```csharp  
<Project DefaultTargets = "Compile"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >  
  
    <!-- Set the application name as a property -->  
    <PropertyGroup>  
        <appname>HelloWorldCS</appname>  
    </PropertyGroup>  
  
    <!-- Specify the inputs by type and file name -->  
    <ItemGroup>  
        <CSFile Include = "consolehwcs1.cs"/>  
    </ItemGroup>  
  
    <Target Name = "Compile">  
        <!-- Run the Visual C# compilation using input files of type CSFile -->  
        <CSC  
            Sources = "@(CSFile)"  
            OutputAssembly = "$(appname).exe">  
            <!-- Set the OutputAssembly attribute of the CSC task  
            to the name of the executable file that is created -->  
            <Output  
                TaskParameter = "OutputAssembly"  
                ItemName = "EXEFile" />  
        </CSC>  
        <!-- Log the file name of the output file -->  
        <Message Text="The output file is @(EXEFile)"/>  
    </Target>  
</Project>  
```  
  
### <a name="comments"></a>Comentários  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  
 O exemplo a seguir mostra um arquivo de projeto que compila um aplicativo [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] e registra uma mensagem que contém o nome do arquivo de saída.  
  
### <a name="code"></a>Código  
  
```vb  
<Project DefaultTargets = "Compile"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >  
  
    <!-- Set the application name as a property -->  
    <PropertyGroup>  
        <appname>HelloWorldVB</appname>  
    </PropertyGroup>  
  
    <!-- Specify the inputs by type and file name -->  
    <ItemGroup>  
        <VBFile Include = "consolehwvb1.vb"/>  
    </ItemGroup>  
  
    <Target Name = "Compile">      
        <!-- Run the Visual Basic compilation using input files of type VBFile -->  
        <VBC  
            Sources = "@(VBFile)"  
            OutputAssembly= "$(appname).exe">  
            <!-- Set the OutputAssembly attribute of the VBC task  
            to the name of the executable file that is created -->  
            <Output  
                TaskParameter = "OutputAssembly"  
                ItemName = "EXEFile" />  
        </VBC>  
        <!-- Log the file name of the output file -->  
        <Message Text="The output file is @(EXEFile)"/>  
    </Target>  
</Project>  
```  
  
## <a name="whats-next"></a>O que vem a seguir?  
 O Visual Studio pode fazer automaticamente muito do trabalho que é mostrado neste passo a passo. Para saber como usar o Visual Studio para criar, editar, compilar e testar arquivos de projeto MSBuild, consulte [Passo a passo: Usando o MSBuild](../msbuild/walkthrough-using-msbuild.md).  
  
## <a name="see-also"></a>Consulte também  
[Visão geral do MSBuild](msbuild.md)  
 [Referência do MSBuild](../msbuild/msbuild-reference.md)


