---
title: Elemento ItemGroup (MSBuild) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ItemGroup
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ItemGroup element [MSBuild]
- <ItemGroup> element [MSBuild]
ms.assetid: aac894e3-a9f1-4bbc-a796-6ef07001f35b
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c8e1be72076fe1d13ef9f0c4144ce097d0743305
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49825855"
---
# <a name="itemgroup-element-msbuild"></a>Elemento ItemGroup (MSBuild)
Contém um conjunto de elementos [Item](../msbuild/item-element-msbuild.md) definidos pelo usuário. Cada item usado em um projeto [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] deve ser especificado como filho de um elemento `ItemGroup`.  
  
 \<Project>  
 \<ItemGroup>  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<ItemGroup Condition="'String A' == 'String B'">  
    <Item1>... </Item1>  
    <Item2>... </Item2>  
</ItemGroup>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Condition`|Atributo opcional. Condição a ser avaliada. Para obter mais informações, consulte [Condições](../msbuild/msbuild-conditions.md).|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Item](../msbuild/item-element-msbuild.md)|Define as entradas do processo de build. Pode não haver nenhum ou pode haver mais de um elemento `Item` em um `ItemGroup`.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
| Elemento | Descrição |
| - | - |
| [Projeto](../msbuild/project-element-msbuild.md) | Elemento raiz necessário de um arquivo de projeto [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]. |
| [Target](../msbuild/target-element-msbuild.md) | A partir do .NET Framework 3.5, o elemento `ItemGroup` pode aparecer dentro de um elemento `Target`. Para obter mais informações, consulte [Destinos](../msbuild/msbuild-targets.md). |
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir mostra as coleções de itens definidos pelo usuário `Res` e `CodeFiles`, declaradas dentro de um elemento `ItemGroup`. Cada um dos itens na coleção de itens `Res` contém um elemento [ItemMetadata](../msbuild/itemmetadata-element-msbuild.md) filho definido pelo usuário.  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <Res Include = "Strings.fr.resources" >  
            <Culture>fr</Culture>  
        </Res>  
        <Res Include = "Dialogs.fr.resources" >  
            <Culture>fr</Culture>  
        </Res>  
  
        <CodeFiles Include="**\*.cs" Exclude="**\generated\*.cs" />  
        <CodeFiles Include="..\..\Resources\Constants.cs" />  
    </ItemGroup>  
...  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema de arquivos de projeto](../msbuild/msbuild-project-file-schema-reference.md)   
 [Itens](../msbuild/msbuild-items.md)   
 [Itens de projeto comuns do MSBuild](../msbuild/common-msbuild-project-items.md)