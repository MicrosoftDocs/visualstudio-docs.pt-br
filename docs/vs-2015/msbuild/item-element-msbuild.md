---
title: Elemento Item (MSBuild) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Item Element [MSBuild]
- <Item> Element [MSBuild]
ms.assetid: dcef5f91-0613-4bfc-8ee9-d7004bb6d3a9
caps.latest.revision: 34
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1dfec558a9958d980d25d4160c4b7f2ce269cbb5
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49270017"
---
# <a name="item-element-msbuild"></a>Elemento Item (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Contém um item definido pelo usuário e seus metadados. Cada item usado em um projeto [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] deve ser especificado como o filho de um elemento `ItemGroup`.  
  
 \<Project>  
 \<ItemGroup>  
 \<Item>  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<Item Include="*.cs"  
        Exclude="MyFile.cs"  
        Remove="RemoveFile.cs"  
        Condition="'String A'=='String B'" >  
    <ItemMetadata1>...</ItemMetadata1>  
    <ItemMetadata2>...</ItemMetadata2>  
</Item>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Include`|Atributo obrigatório.<br /><br /> O arquivo ou curinga a ser incluído na lista de itens.|  
|`Exclude`|Atributo opcional.<br /><br /> O arquivo ou curinga a ser excluído da lista de itens.|  
|`Condition`|Atributo opcional.<br /><br /> A condição a ser avaliada. Para obter mais informações, consulte [Condições](../msbuild/msbuild-conditions.md).|  
|`Remove`|Atributo opcional.<br /><br /> O arquivo ou curinga a ser removido da lista de itens.<br /><br /> Esse atributo será válido apenas se for especificado para um item em uma `ItemGroup` que esteja em um `Target`.|  
|`KeepMetadata`|Atributo opcional.<br /><br /> Os metadados dos itens de origem a serem adicionados nos itens de destino. Apenas os metadados cujos nomes são especificados na lista delimitada por ponto e vírgula são transferidos de um item de origem para um item de destino. Para obter mais informações, consulte [Itens](../msbuild/msbuild-items.md).<br /><br /> Esse atributo será válido apenas se for especificado para um item em uma `ItemGroup` que esteja em um `Target`.|  
|`RemoveMetadata`|Atributo opcional.<br /><br /> Os metadados dos itens de origem que não serão transferidos para os itens de destino. Todos os metadados são transferidos de um item de origem para um item de destino, exceto metadados cujos nomes estejam contidos na lista de nomes separados por ponto e vírgula. Para obter mais informações, consulte [Itens](../msbuild/msbuild-items.md).<br /><br /> Esse atributo será válido apenas se for especificado para um item em uma `ItemGroup` que esteja em um `Target`.|  
|`KeepDuplicates`|Atributo opcional.<br /><br /> Especifica se um item deverá ser adicionado ao grupo de destino se for uma duplicata exata de um item existente. Se o item de origem e de destino tiverem o mesmo valor `Include`, mas metadados diferentes, o item será adicionado mesmo se `KeepDuplicates` estiver definido como `false`. Para obter mais informações, consulte [Itens](../msbuild/msbuild-items.md).<br /><br /> Esse atributo será válido apenas se for especificado para um item em uma `ItemGroup` que esteja em um `Target`.|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[ItemMetadata](../msbuild/itemmetadata-element-msbuild.md)|Uma chave de metadados de item definido pelo usuário, que contém o valor de metadados do item. Pode ser que não haja nenhum ou mais de um elemento `ItemMetadata` em um item.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[ItemGroup](../msbuild/itemgroup-element-msbuild.md)|Elemento grouping para itens.|  
  
## <a name="remarks"></a>Comentários  
 Os elementos `Item` definem entradas no sistema de compilação e são agrupados em coleções de itens com base em seus nomes de coleção definida pelo usuário. Essas coleções de itens podem ser usadas como parâmetros para [tarefas](../msbuild/msbuild-tasks.md), que usam os itens individuais nas coleções para executar as etapas do processo de build. Para obter mais informações, consulte [Itens](../msbuild/msbuild-items.md).  
  
 O uso da notação `@(`*myType*`)` permite que uma coleção de itens do tipo *myType* seja expandida em uma lista de cadeias de caracteres delimitada por ponto e vírgula e passada para um parâmetro. Se o parâmetro for do tipo `string`, então o valor do parâmetro será a lista de elementos, separados por ponto e vírgula. Se o parâmetro for uma matriz de cadeias de caracteres (`string[]`), então cada elemento será inserido na matriz com base na localização dos pontos e vírgulas. Se o parâmetro de tarefa for do tipo <xref:Microsoft.Build.Framework.ITaskItem>`[]`, então o valor é o conteúdo da coleção de itens juntamente com quaisquer metadados anexados. Para delimitar cada item usando um caractere que não seja ponto e vírgula, use a sintaxe `@(`*myType*`, '`*separator*`')`.  
  
 O mecanismo [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] pode avaliar curingas como `*` e `?`, bem como curingas recursivos como `/**/*.cs`. Para obter mais informações, consulte [Itens](../msbuild/msbuild-items.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir mostra como declarar dois itens do tipo `CSFile`. O segundo item declarado contém metadados que possuem `MyMetadata` definidos como `HelloWorld`.  
  
```  
<ItemGroup>  
    <CSFile Include="engine.cs; form.cs" />  
    <CSFile Include="main.cs" >  
        <MyMetadata>HelloWorld</MyMetadata>  
    </CSFile>  
</ItemGroup>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Itens](../msbuild/msbuild-items.md)   
 [Propriedades do MSBuild](msbuild-properties1.md)   
 [Referência do esquema de arquivos de projeto](../msbuild/msbuild-project-file-schema-reference.md)



