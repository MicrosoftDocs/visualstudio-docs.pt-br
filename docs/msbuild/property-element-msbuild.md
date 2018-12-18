---
title: Elemento Property (MSBuild) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <Property> Element [MSBuild]
- Property Element [MSBuild]
ms.assetid: 69ab08ab-3e76-41dd-a01b-49aa1d2e0cac
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d44b88f5d97fb8c70391506dc2daab99482d6a44
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39154974"
---
# <a name="property-element-msbuild"></a>Elemento Property (MSBuild)
Contém um nome e valor de propriedade definidos pelo usuário. Cada propriedade usada em um projeto [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] deve ser especificada como filho de um elemento `PropertyGroup`.  

 \<Project>  
 \<PropertyGroup>  

## <a name="syntax"></a>Sintaxe  

```xml  
<Property Condition="'String A' == 'String B'">  
    Property Value  
</Property>  
```  

## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  

### <a name="attributes"></a>Atributos  

|Atributo|Descrição|  
|---------------|-----------------|  
|`Condition`|Atributo opcional.<br /><br /> Condição a ser avaliada. Para obter mais informações, consulte [Condições](../msbuild/msbuild-conditions.md).|  

### <a name="child-elements"></a>Elementos filho  
 nenhuma.  

### <a name="parent-elements"></a>Elementos pai  

|Elemento|Descrição|  
|-------------|-----------------|  
|[PropertyGroup](../msbuild/propertygroup-element-msbuild.md)|Elemento de agrupamento para propriedades.|  

## <a name="text-value"></a>Valor de texto  
 Um valor de texto é opcional.  

 Esse texto especifica o valor da propriedade e pode conter XML.  

## <a name="remarks"></a>Comentários  
 Nomes de propriedade estão limitados a apenas a caracteres ASCII. Valores de propriedades são referenciados no projeto, colocando o nome da propriedade entre "`$(`" e "`)`". Por exemplo, `$(builddir)\classes` resolveria para *build\classes*, se a propriedade `builddir` tivesse o valor `build`. Para saber mais sobre as propriedades, confira [Propriedades do MSBuild](../msbuild/msbuild-properties.md).  

## <a name="example"></a>Exemplo  
 O código a seguir define a propriedade `Optimization` para `false` e a propriedade `DefaultVersion` para `1.0` se a propriedade `Version` estiver vazia.  

```xml  
<PropertyGroup>  
    <Optimization>false</Optimization>  
    <DefaultVersion Condition="'$(Version)' == ''" >1.0</DefaultVersion>  
</PropertyGroup>  
```  

## <a name="see-also"></a>Consulte também
[Propriedades do MSBuild](../msbuild/msbuild-properties.md)  
 [Referência de esquema de arquivos de projeto](../msbuild/msbuild-project-file-schema-reference.md)
