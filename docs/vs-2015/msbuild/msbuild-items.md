---
title: Itens do MSBuild | Microsoft Docs
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
- MSBuild, Items
ms.assetid: d762eff4-c92a-4b5f-a944-1ca30aa22319
caps.latest.revision: 38
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d517d3fd24b17c33a7bba9f888fbb904631be5f1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49851927"
---
# <a name="msbuild-items"></a>Itens do MSBuild
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Itens do MSBuild são entradas no sistema de build e eles normalmente representam arquivos. Os itens são agrupados em tipos de item com base em seus nomes de elemento. Os tipos de item são listas nomeadas de itens que podem ser usados como parâmetros para tarefas. As tarefas usam os valores do item para executar as etapas do processo de build.  
  
 Como os itens são nomeados pelo tipo de item ao qual pertencem, os termos “item” e “valor de item” podem ser usados alternadamente.  
  
 **Neste tópico**  
  
-   [Criando itens em um arquivo de projeto](#BKMK_Creating1)  
  
-   [Criando itens durante a execução](#BKMK_Creating2)  
  
-   [Referenciando itens em um arquivo de projeto](#BKMK_ReferencingItems)  
  
-   [Usando caracteres curinga para especificar itens](#BKMK_Wildcards)  
  
-   [Usando o atributo Exclude](#BKMK_ExcludeAttribute)  
  
-   [Metadados de item](#BKMK_ItemMetadata)  
  
    -   [Referenciando metadados de item em um arquivo de projeto](#BKMK_ReferencingItemMetadata)  
  
    -   [Metadados de itens conhecidos](#BKMK_WellKnownItemMetadata)  
  
    -   [Transformando os tipos de item ao usar metadados](#BKMK_Transforming)  
  
-   [Definições de item](#BKMK_ItemDefinitions)  
  
-   [Atributos de itens em um ItemGroup de um destino](#BKMK_AttributesWithinTargets)  
  
    -   [Remover atributo](#BKMK_RemoveAttribute)  
  
    -   [Atributo KeepMetadata](#BKMK_KeepMetadata)  
  
    -   [Atributo RemoveMetadata](#BKMK_RemoveMetadata)  
  
    -   [Atributo KeepDuplicates](#BKMK_KeepDuplicates)  
  
##  <a name="BKMK_Creating1"></a> Criando itens em um arquivo de projeto  
 Os itens são declarados no arquivo de projeto como elementos filho de um elemento [ItemGroup](../msbuild/itemgroup-element-msbuild.md). O nome do elemento filho é o tipo do item. O atributo `Include` do elemento especifica os itens (arquivos) a serem incluídos com esse tipo de item. Por exemplo, o XML a seguir cria um tipo de item chamado `Compile`, que inclui dois arquivos.  
  
```  
<ItemGroup>  
    <Compile Include = "file1.cs"/>  
    <Compile Include = "file2.cs"/>  
</ItemGroup>  
```  
  
 O item "file2.cs" não substitui o item "file1.cs"; em vez disso, o nome do arquivo é acrescentado à lista de valores para o tipo de item `Compile`. Você não pode remover um item de um tipo de item durante a fase de avaliação de um build.  
  
 O XML a seguir cria o mesmo tipo de item declarando os dois arquivos em um atributo `Include`. Observe que os nomes de arquivo são separados por ponto e vírgula.  
  
```  
<ItemGroup>  
    <Compile Include = "file1.cs;file2.cs"/>  
</ItemGroup>  
```  
  
##  <a name="BKMK_Creating2"></a> Criando itens durante a execução  
 Os itens que estão fora dos elementos de [destino](../msbuild/target-element-msbuild.md) são valores designados durante a fase de avaliação de um build. Durante a fase de execução subsequente, os itens podem ser criados ou modificados das seguintes maneiras:  
  
-   Qualquer tarefa pode emitir um item. Para emitir um item, o elemento [Task](../msbuild/task-element-msbuild.md) deve ter um elemento filho [Output](../msbuild/output-element-msbuild.md) que tem um atributo `ItemName`.  
  
-   A tarefa [CreateItem](../msbuild/createitem-task.md) pode emitir um item. Esse uso é preterido.  
  
-   A partir do .NET Framework 3.5, os elementos `Target` podem conter elementos [ItemGroup](../msbuild/itemgroup-element-msbuild.md) que podem conter elementos de item.  
  
##  <a name="BKMK_ReferencingItems"></a> Referenciando itens em um arquivo de projeto  
 Para referenciar tipos de item em todo o arquivo de projeto, use a sintaxe @(`ItemType`). Por exemplo, você faria referência no tipo de item no exemplo anterior usando `@(Compile)`. Usando esta sintaxe, você pode passar itens para tarefas, especificando o tipo de item como um parâmetro dessa tarefa. Para obter mais informações, consulte [Como selecionar os arquivos a serem compilados](../msbuild/how-to-select-the-files-to-build.md).  
  
 Por padrão, os itens de um tipo de item são separados por ponto e vírgula (;) quando são expandidos. Você pode usar a sintaxe @(*ItemType*, '*separator*') para especificar um separador diferente do padrão. Para mais informações, consulte [Como exibir uma lista de itens separada por vírgulas](../msbuild/how-to-display-an-item-list-separated-with-commas.md).  
  
##  <a name="BKMK_Wildcards"></a> Usando caracteres curinga para especificar itens  
 Você pode usar os caracteres curinga **, \* e ? para especificar um grupo de arquivos como entradas para um build em vez de listar cada arquivo separadamente.  
  
- O caractere curinga ? corresponde a um único caractere.  
  
- O caractere curinga * corresponde a zero ou mais caracteres.  
  
- A sequência de caractere curinga ** corresponde a um caminho parcial.  
  
  Por exemplo, você pode especificar todos os arquivos .cs no diretório que contém o arquivo de projeto usando o seguinte elemento no arquivo de projeto.  
  
```  
<CSFile Include="*.cs"/>  
```  
  
 O elemento a seguir seleciona todos os arquivos .vb na unidade D:  
  
```  
<VBFile Include="D:/**/*.vb"/>  
```  
  
 Para mais informações sobre os caracteres curinga, consulte [Como selecionar os arquivos a serem compilados](../msbuild/how-to-select-the-files-to-build.md).  
  
##  <a name="BKMK_ExcludeAttribute"></a> Usando o atributo Exclude  
 Os elementos de item podem conter o atributo `Exclude`, que exclui itens específicos (arquivos) do tipo de item. O atributo `Exclude` normalmente é usado junto com caracteres curinga. Por exemplo, o XML a seguir adiciona cada arquivo .cs no diretório para o tipo de item de CSFile, exceto o arquivo `DoNotBuild.cs`.  
  
```  
<ItemGroup>  
    <CSFile  Include="*.cs"  Exclude="DoNotBuild.cs"/>  
</ItemGroup>  
```  
  
 O atributo `Exclude` afeta somente os itens adicionados pelo atributo `Include` no elemento do item que contém ambos. O exemplo a seguir não excluiria o arquivo Form1.cs, que foi adicionado no elemento do item anterior.  
  
```  
<Compile Include="*.cs" />  
<Compile Include="*.res" Exclude="Form1.cs">  
```  
  
 Para mais informações, consulte [Como excluir arquivos do build](../msbuild/how-to-exclude-files-from-the-build.md).  
  
##  <a name="BKMK_ItemMetadata"></a> Metadados de item  
 Os itens que podem conter metadados, além das informações nos atributos `Include` e `Exclude`. Esses metadados podem ser usados por tarefas que exigem mais informações sobre os itens ou para os destinos e tarefas de lote. Para obter mais informações, consulte [Envio em lote](../msbuild/msbuild-batching.md).  
  
 Os metadados são uma coleção de pares chave-valor que são declarados no arquivo de projeto como elementos filho de um elemento do item. O nome do elemento filho é o nome dos metadados e o valor do elemento filho é o valor dos metadados.  
  
 Os metadados são associados ao elemento do item que os contém. Por exemplo, o XML a seguir adiciona metadados `Culture` que têm o valor `Fr` para os itens "one.cs" e "two.cs" do tipo de item CSFile.  
  
```  
<ItemGroup>  
    <CSFile Include="one.cs;two.cs">  
        <Culture>Fr</Culture>  
    </CSFile>  
</ItemGroup>  
```  
  
 Um item pode ter zero ou mais valores de metadados. Você pode alterar os valores de metadados a qualquer momento. Se definir metadados para um valor vazio, você efetivamente vai removê-lo do build.  
  
###  <a name="BKMK_ReferencingItemMetadata"></a> Referenciando metadados de item em um arquivo de projeto  
 Você pode fazer referência a metadados de item em todo o arquivo de projeto usando a sintaxe %(`ItemMetadataName`). Se existir a ambiguidade, você poderá qualificar uma referência usando o nome do tipo de item. Por exemplo, você pode especificar %(*ItemType.ItemMetaDataName*). O exemplo a seguir usa os metadados Display para colocar em lote a tarefa Message. Para obter mais informações sobre como usar os metadados do item para envio em lote, consulte [Metadados de Item no envio em lote de tarefas](../msbuild/item-metadata-in-task-batching.md).  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <Stuff Include="One.cs" >  
            <Display>false</Display>  
        </Stuff>  
        <Stuff Include="Two.cs">  
            <Display>true</Display>  
        </Stuff>  
    </ItemGroup>  
    <Target Name="Batching">  
        <Message Text="@(Stuff)" Condition=" '%(Display)' == 'true' "/>  
    </Target>  
</Project>  
```  
  
###  <a name="BKMK_WellKnownItemMetadata"></a> Metadados de itens conhecidos  
 Sempre que um item é adicionado a um tipo de item, esse item é atribuído a alguns metadados conhecidos. Por exemplo, todos os itens que têm metadados `%(Filename)` conhecidos, cujo valor é o nome de arquivo do item. Para obter mais informações, consulte [Metadados de itens conhecidos](../msbuild/msbuild-well-known-item-metadata.md).  
  
###  <a name="BKMK_Transforming"></a> Transformando os tipos de item ao usar metadados  
 Você pode transformar listas de itens em novas listas de item usando metadados. Por exemplo, você pode transformar um tipo de item `CppFiles` que tem itens que representam arquivos .cpp em uma lista correspondente de arquivos .obj usando a expressão `@(CppFiles -> '%(Filename).obj')`.  
  
 O código a seguir cria um tipo de item `CultureResource` que contém cópias de todos os itens `EmbeddedResource` com metadados `Culture`. O valor de metadados `Culture` se torna o valor dos novos metadados `CultureResource.TargetDirectory`.  
  
```  
<Target Name="ProcessCultureResources">  
    <ItemGroup>  
        <CultureResource Include="@(EmbeddedResource)"  
            Condition="'%(EmbeddedResource.Culture)' != ''">  
            <TargetDirectory>%(EmbeddedResource.Culture) </TargetDirectory>  
        </CultureResource>  
    </ItemGroup>  
</Target>  
```  
  
 Para obter mais informações, consulte [Transformações](../msbuild/msbuild-transforms.md).  
  
##  <a name="BKMK_ItemDefinitions"></a> Definições de item  
 A partir do .NET Framework 3.5, você pode adicionar metadados padrão a qualquer tipo de item usando o [elemento ItemDefinitionGroup](../msbuild/itemdefinitiongroup-element-msbuild.md). Como metadados conhecidos, os metadados padrão estão associados a todos os itens do tipo de item especificado. Você pode substituir explicitamente metadados padrão em uma definição de item. Por exemplo, o XML a seguir fornece aos itens `Compile` "one.cs" e "three.cs" os metadados `BuildDay` com o valor "Monday". O código fornece ao item "two.cs" os metadados `BuildDay` com o valor "Tuesday".  
  
```  
<ItemDefinitionGroup>  
    <Compile>  
        <BuildDay>Monday</BuildDay>  
    </Compile>  
</ItemDefinitionGroup>  
<ItemGroup>  
    <Compile Include="one.cs;three.cs" />  
    <Compile Include="two.cs">  
        <BuildDay>Tuesday</BuildDay>  
    </Compile>  
</ItemGroup>  
```  
  
 Para obter mais informações, consulte [Definições de item](../msbuild/item-definitions.md).  
  
##  <a name="BKMK_AttributesWithinTargets"></a> Atributos de itens em um ItemGroup de um destino  
 A partir do .NET Framework 3.5, os elementos `Target` podem conter elementos [ItemGroup](../msbuild/itemgroup-element-msbuild.md) que podem conter elementos de item. Os atributos nesta seção são válidos quando são especificados para um item em um `ItemGroup` que é um `Target`.  
  
###  <a name="BKMK_RemoveAttribute"></a> Remover atributo  
 Os itens em um `ItemGroup` de um destino podem conter o atributo `Remove`, que remove itens específicos (arquivos) do tipo de item. Esse atributo foi introduzido no .NET Framework 3.5.  
  
 O exemplo a seguir remove todos os arquivos .config do tipo de item de compilação.  
  
```  
<Target>  
    <ItemGroup>  
        <Compile Remove="*.config"/>  
    </ItemGroup>  
</Target>  
```  
  
###  <a name="BKMK_KeepMetadata"></a> Atributo KeepMetadata  
 Se um item for gerado em um destino, o elemento de item poderá conter o atributo `KeepMetadata`. Se esse atributo for especificado, apenas os metadados que serão especificados na lista de nomes separados por ponto-e-vírgula serão transferidos do item de origem para o item de destino. Um valor vazio para esse atributo é equivalente a não especificação dele. O atributo `KeepMetadata` foi introduzido no .NET Framework 4.5.  
  
 O exemplo a seguir mostra como usar o atributo `KeepMetadata`.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"  
ToolsVersion="4.0">  
  
    <ItemGroup>  
        <FirstItem Include="rhinoceros">  
            <Class>mammal</Class>  
            <Size>large</Size>  
        </FirstItem>  
  
    </ItemGroup>  
    <Target Name="MyTarget">  
        <ItemGroup>  
            <SecondItem Include="@(FirstItem)" KeepMetadata="Class" />  
        </ItemGroup>  
  
        <Message Text="FirstItem: %(FirstItem.Identity)" />  
        <Message Text="  Class: %(FirstItem.Class)" />  
        <Message Text="  Size:  %(FirstItem.Size)"  />  
  
        <Message Text="SecondItem: %(SecondItem.Identity)" />  
        <Message Text="  Class: %(SecondItem.Class)" />  
        <Message Text="  Size:  %(SecondItem.Size)"  />  
    </Target>  
</Project>  
  
<!--  
Output:  
  FirstItem: rhinoceros  
    Class: mammal  
    Size:  large  
  SecondItem: rhinoceros  
    Class: mammal  
    Size:   
-->  
```  
  
###  <a name="BKMK_RemoveMetadata"></a> Atributo RemoveMetadata  
 Se um item for gerado em um destino, o elemento de item poderá conter o atributo `RemoveMetadata`. Se esse atributo for especificado, todos os metadados serão transferidos do item de origem para o item de destino, exceto os metadados cujos nomes estão contidos na lista de nomes separados por ponto-e-vírgula. Um valor vazio para esse atributo é equivalente a não especificação dele. O atributo `RemoveMetadata` foi introduzido no .NET Framework 4.5.  
  
 O exemplo a seguir mostra como usar o atributo `RemoveMetadata`.  
  
```  
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <PropertyGroup>  
        <MetadataToRemove>Size;Material</MetadataToRemove>  
    </PropertyGroup>  
  
    <ItemGroup>  
        <Item1 Include="stapler">  
            <Size>medium</Size>  
            <Color>black</Color>  
            <Material>plastic</Material>  
        </Item1>  
    </ItemGroup>  
  
    <Target Name="MyTarget">  
        <ItemGroup>  
            <Item2 Include="@(Item1)" RemoveMetadata="$(MetadataToRemove)" />  
        </ItemGroup>  
  
        <Message Text="Item1: %(Item1.Identity)" />  
        <Message Text="  Size:     %(Item1.Size)" />  
        <Message Text="  Color:    %(Item1.Color)" />  
        <Message Text="  Material: %(Item1.Material)" />  
        <Message Text="Item2: %(Item2.Identity)" />  
        <Message Text="  Size:     %(Item2.Size)" />  
        <Message Text="  Color:    %(Item2.Color)" />  
        <Message Text="  Material: %(Item2.Material)" />  
    </Target>  
</Project>  
  
<!--  
Output:   
  Item1: stapler  
    Size:     medium  
    Color:    black  
    Material: plastic  
  Item2: stapler  
    Size:       
    Color:    black  
    Material:   
-->  
```  
  
###  <a name="BKMK_KeepDuplicates"></a> Atributo KeepDuplicates  
 Se um item for gerado em um destino, o elemento de item poderá conter o atributo `KeepDuplicates`. `KeepDuplicates` é um atributo `Boolean` que especifica se um item deverá ser adicionado ao grupo de destino se for uma duplicata exata de um item existente.  
  
 Se os itens de origem e de destino tiverem o mesmo valor Include, mas metadados diferentes, o item será adicionado mesmo se `KeepDuplicates` estiver definido como `false`. Um valor vazio para esse atributo é equivalente a não especificação dele. O atributo `KeepDuplicates` foi introduzido no .NET Framework 4.5.  
  
 O exemplo a seguir mostra como usar o atributo `KeepDuplicates`.  
  
```  
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <Item1 Include="hourglass;boomerang" />  
        <Item2 Include="hourglass;boomerang" />  
    </ItemGroup>  
  
    <Target Name="MyTarget">  
        <ItemGroup>  
            <Item1 Include="hourglass" KeepDuplicates="false" />  
            <Item2 Include="hourglass" />  
        </ItemGroup>  
  
        <Message Text="Item1: @(Item1)" />  
        <Message Text="  %(Item1.Identity)  Count: @(Item1->Count())" />  
        <Message Text="Item2: @(Item2)" />  
        <Message Text="  %(Item2.Identity)  Count: @(Item2->Count())" />  
    </Target>  
</Project>  
  
<!--  
Output:   
  Item1: hourglass;boomerang  
    hourglass  Count: 1  
    boomerang  Count: 1  
  Item2: hourglass;boomerang;hourglass  
    hourglass  Count: 2  
    boomerang  Count: 1  
-->  
```  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)  
 [MSBuild](msbuild.md)   
 [Como selecionar os arquivos a serem compilados](../msbuild/how-to-select-the-files-to-build.md)   
 [Como excluir arquivos do build](../msbuild/how-to-exclude-files-from-the-build.md)   
 [Como exibir uma lista de itens separada por vírgulas](../msbuild/how-to-display-an-item-list-separated-with-commas.md)   
 [Definições de itens](../msbuild/item-definitions.md)   
 [Envio em lote](../msbuild/msbuild-batching.md)   
 [Elemento Item (MSBuild)](../msbuild/item-element-msbuild.md)


