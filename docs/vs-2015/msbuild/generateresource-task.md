---
title: Tarefa GenerateResource | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GenerateResource
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, GenerateResource task
- GenerateResource task [MSBuild]
ms.assetid: c0aff32f-f2cc-46f6-9c3e-a5c9f8f912b1
caps.latest.revision: 18
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6686e34ade66a3d4f2ec8ef23c9649bb5d7a1c47
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49212492"
---
# <a name="generateresource-task"></a>Tarefa GenerateResource
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Converte entre arquivos .txt e .resx (formato de recurso com base em XML) e arquivos .resources binários do Common Language Runtime que podem ser inseridos em um executável binário do tempo de execução ou compilados em assemblies satélite. Essa tarefa geralmente é usada para converter arquivos. txt ou. resx em arquivos .resource. A tarefa `GenerateResource` é funcionalmente semelhante a [resgen.exe](http://msdn.microsoft.com/library/8ef159de-b660-4bec-9213-c3fbc4d1c6f4).  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `GenerateResource`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`AdditionalInputs`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Contém entradas adicionais para a verificação de dependência realizada por tarefa. Por exemplo, os arquivos de projeto e de destino normalmente devem ser entradas, de modo que se eles forem atualizados, todos os recursos serão regenerados.|  
|`EnvironmentVariables`|Parâmetro `String[]` opcional.<br /><br /> Especifica uma matriz de pares nome-valor das variáveis de ambiente que devem ser passados para o resgen.exe gerado, além (ou substituindo seletivamente) do bloco de ambiente comum.|  
|`ExcludedInputPaths`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica uma matriz de itens que especificam os caminhos dos quais entradas controladas serão ignoradas durante a verificação de atualização.|  
|`ExecuteAsTool`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, executa tlbimp.exe e aximp.exe da estrutura de destino apropriada fora de processo para gerar os assemblies de wrapper necessários. Esse parâmetro habilita multi-targeting de `ResolveComReferences`.|  
|`FilesWritten`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Contém os nomes de todos os arquivos gravados em disco. Isso inclui o arquivo de cache, se houver. Esse parâmetro é útil para implementações do Clean.|  
|`MinimalRebuildFromTracking`|Parâmetro `Boolean` opcional.<br /><br /> Obtém ou define uma opção que especifica se o build incremental controlado será usado. Se `true`, o build incremental é ativado; caso contrário, será forçada uma recompilação.|  
|`NeverLockTypeAssemblies`|Parâmetro `Boolean` opcional.<br /><br /> Especifica o nome dos arquivos gerados, como arquivos .resources. Se você não especificar um nome, o nome do arquivo de entrada correspondente será usado e o arquivo .resources criado será colocado no diretório contendo o arquivo de entrada.|  
|`OutputResources`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Especifica o nome dos arquivos gerados, como arquivos .resources. Se você não especificar um nome, o nome do arquivo de entrada correspondente será usado e o arquivo .resources criado será colocado no diretório contendo o arquivo de entrada.|  
|`PublicClass`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, cria uma classe de recurso fortemente tipada como uma classe pública.|  
|`References`|Parâmetro `String[]` opcional.<br /><br /> Referências das quais carregar arquivos .resx. Elementos de dados de arquivo resx podem ter um tipo .NET. Quando o arquivo. resx é lido, isso deve ser resolvido. Normalmente, ele é resolvido com êxito usando o tipo padrão ao carregar regras. Se você fornecer assemblies em `References`, eles terão prioridade.<br /><br /> Esse parâmetro não é necessário para recursos fortemente tipados.|  
|`SdkToolsPath`|Parâmetro `String` opcional.<br /><br /> Especifica o caminho para as ferramentas do SDK, por exemplo, resgen.exe.|  
|`Sources`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem>`[]` obrigatório.<br /><br /> Especifica os itens a converter. Itens passados para esse parâmetro devem ter uma das seguintes extensões de arquivo:<br /><br /> -   `.txt`: especifica a extensão a ser convertida por um arquivo de texto. Os arquivos de texto só podem conter recursos de cadeia de caracteres.<br />-   `.resx`: especifica a extensão a ser convertida por um arquivo de recurso com base em XML.<br />-   `.restext`: especifica o mesmo formato como .txt. Essa extensão diferente é útil se você quiser distinguir claramente os arquivos de origem que contêm recursos de outros arquivos de origem no processo de build.<br />-   `.resources`: especifica a extensão a ser convertida por um arquivo de recurso.|  
|`StateFile`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> opcional.<br /><br /> Especifica o caminho para um arquivo de cache opcional que é usado para acelerar a verificação de dependência de links em arquivos de entrada .resx.|  
|`StronglyTypedClassName`|Parâmetro `String` opcional.<br /><br /> Especifica o nome de classe para a classe de recurso fortemente tipada. Se esse parâmetro não for especificado, o nome base do arquivo de recurso será usado.|  
|`StronglyTypedFilename`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> opcional.<br /><br /> Especifica o nome do arquivo para o arquivo de origem. Se esse parâmetro não for especificado, o nome de classe será usado como o nome de arquivo base, com a extensão dependendo da linguagem. Por exemplo: `MyClass.cs`.|  
|`StronglyTypedLanguage`|Parâmetro `String` opcional.<br /><br /> Especifica a linguagem a ser usada ao gerar a fonte de classe para o recurso fortemente tipado. Esse parâmetro deve corresponder exatamente uma das linguagens usadas por CodeDomProvider. Por exemplo `VB` ou `C#`.<br /><br /> Ao passar um valor para esse parâmetro, você instrui a tarefa a gerar recursos fortemente tipados.|  
|`StronglyTypedManifestPrefix`|Parâmetro `String` opcional.<br /><br /> Especifica o prefixo de manifesto ou namespace de recurso para usar na origem de classe gerada para o recurso fortemente tipado.|  
|`StronglyTypedNamespace`|Parâmetro `String` opcional.<br /><br /> Especifica o namespace para usar na origem de classe gerada para o recurso fortemente tipado. Se esse parâmetro não for especificado, todos os recursos fortemente tipados estarão no namespace global.|  
|`TLogReadFiles`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem>`[]` somente leitura opcional.<br /><br /> Obtém uma matriz de itens que representam os logs de acompanhamento de leitura.|  
|`TLogWriteFiles`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem>`[]` somente leitura opcional.<br /><br /> Obtém uma matriz de itens que representam os logs de acompanhamento de gravação.|  
|`ToolArchitecture`|Opcional [String] (<!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  -->) parâmetro.<br /><br /> Usado para determinar se o Tracker.exe precisa ou não ser usado para gerar ResGen.exe.<br /><br /> Deve ser analisável para um membro da enumeração <xref:Microsoft.Build.Utilities.ExecutableType>. Se `String.Empty`, usa uma heurística para determinar uma arquitetura padrão. Deve ser analisável para um membro da enumeração Microsoft.Build.Utilities.ExecutableType.|  
|`TrackerFrameworkPath`|Parâmetro <!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  --> opcional.<br /><br /> Especifica o caminho para o local apropriado do .NET Framework que contém FileTracker.dll.<br /><br /> Se definido, o usuário assume a responsabilidade de assegurar que o número de bits do FileTracker.dll que esse usuário passa corresponde ao número de bits do ResGen.exe que ele pretende usar. Se não for definido, a tarefa decide o local apropriado com base na versão atual do .NET Framework.|  
|`TrackerLogDirectory`|Parâmetro <!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  --> opcional.<br /><br /> Especifica o diretório intermediário no qual os logs de acompanhamento da execução dessa tarefa serão colocados.|  
|`TrackerSdkPath`|Parâmetro <!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  --> opcional.<br /><br /> Especifica o caminho para o local apropriado do SDK do Windows que contém Tracker.exe.<br /><br /> Se definido, o usuário assume a responsabilidade de assegurar que o número de bits do Tracker.exe que esse usuário passa corresponde ao número de bits do ResGen.exe que ele pretende usar. Se não for definido, a tarefa decide o local apropriado com base no SDK do Windows atual.|  
|`TrackFileAccess`|Opcional [booliano] (<!-- TODO: review code entity reference <xref:assetId:///Boolean?qualifyHint=False&amp;autoUpgrade=True>  -->) parâmetro.<br /><br /> Se é true, o diretório do arquivo de entrada é usado para resolver caminhos de arquivo relativos.|  
|`UseSourcePath`|Parâmetro `Boolean` opcional.<br /><br /> Se é `true`, especifica que o diretório do arquivo de entrada deve ser usado para resolver caminhos de arquivo relativos.|  
  
## <a name="remarks"></a>Comentários  
 Já que arquivos .resx podem conter links para outros arquivos de recurso, não é suficiente simplesmente comparar carimbos de data/hora de arquivos .resx e arquivos .resource para ver se as saídas estão atualizadas. Em vez disso, a tarefa `GenerateResource` segue os links nos arquivos. resx e verifica também os carimbos de data/hora dos arquivos vinculados. Isso significa que, geralmente, você não deve usar os atributos `Inputs` e `Outputs` no destino que contém a tarefa `GenerateResource`, pois isso pode fazer com que ela seja ignorada quando, na verdade, ela deve ser executada.  
  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, consulte [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  
  
 Ao usar o MSBuild 4.0 para projetos de destino do .NET 3.5, o build pode falhar em recursos x86. Para contornar esse problema, é possível criar o destino como um assembly AnyCPU.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a tarefa `GenerateResource` para gerar arquivos .resources dos arquivos especificados pela coleção de itens `Resx`.  
  
```  
<GenerateResource  
    Sources="@(Resx)"  
    OutputResources="@(Resx->'$(IntermediateOutputPath)%(Identity).resources')">  
    <Output  
        TaskParameter="OutputResources"  
        ItemName="Resources"/>  
</GenerateResource>  
```  
  
 A tarefa `GenerateResource` usa os metadados \<LogicalName> de um item \<EmbeddedResource> para nomear os recursos que são inseridos em um assembly.  
  
 Supondo que o assembly é chamado myAssembly, o código a seguir gera um recurso inserido denominado someQualifier.someResource.resources:  
  
```  
<ItemGroup>   <EmbeddedResource Include="myResource.resx">       <LogicalName>someQualifier.someResource.resources</LogicalName>   </EmbeddedResource></ItemGroup>  
```  
  
 Sem os metadados \<LogicalName>, o recurso será nomeado myAssembly.myResource.resources.  Este exemplo aplica-se somente ao processo de build do Visual Basic e Visual C#.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



