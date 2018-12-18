---
title: Funções de itens | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- msbuild, Item functions
ms.assetid: 5e6df3cc-2db8-4cbd-8fdd-3ffd03ac0876
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 85dd03080a9dda58532d656161c3c44ae4943251
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39081342"
---
# <a name="item-functions"></a>funções de item
Começando com o MSBuild 4.0, o código em tarefas e destinos pode chamar funções de item para obter informações sobre os itens no projeto. Essas funções simplificam a obtenção de itens Distinct() e são mais rápidas do que executar loop nos itens.  
  
## <a name="string-item-functions"></a>Funções de item de cadeia de caracteres  
 É possível usar métodos e propriedades de cadeia de caracteres no .NET Framework para operar em qualquer valor de item. Para métodos <xref:System.String>, especifique o nome do método. Para propriedades <xref:System.String>, especifique o nome da propriedade após "get_".  
  
 Para itens que têm várias cadeias de caracteres, o método ou propriedade da cadeia de caracteres será executado em cada cadeia de caracteres.  
  
 O exemplo a seguir mostra como usar essas funções de item de cadeia de caracteres.  
  
```xml  
<ItemGroup>  
    <theItem Include="andromeda;tadpole;cartwheel" />  
</ItemGroup>  
  
<Target Name = "go">  
    <Message Text="IndexOf  @(theItem->IndexOf('r'))" />  
    <Message Text="Replace  @(theItem->Replace('tadpole', 'pinwheel'))" />  
    <Message Text="Length   @(theItem->get_Length())" />  
    <Message Text="Chars    @(theItem->get_Chars(2))" />  
</Target>  
  
  <!--  
  Output:  
    IndexOf  3;-1;2  
    Replace  andromeda;pinwheel;cartwheel  
    Length   9;7;9  
    Chars    d;d;r  
  -->  
```  
  
## <a name="intrinsic-item-functions"></a>Funções de item intrínsecas  
 A tabela a seguir lista as funções intrínsecas disponíveis para itens.  
  
|Função|Exemplo|Descrição|  
|--------------|-------------|-----------------|  
|`Count`|`@(MyItem->Count())`|Retorna a contagem dos itens.|  
|`DirectoryName`|`@(MyItem->DirectoryName())`|Retorna o equivalente de `Path.DirectoryName` para cada item.|  
|`Distinct`|`@(MyItem->Distinct())`|Retorna itens com valores `Include` distintos. Os metadados são ignorados. A comparação não diferencia maiúsculas de minúsculas.|  
|`DistinctWithCase`|`@(MyItem->DistinctWithCase())`|Retorna itens com valores `itemspec` distintos. Os metadados são ignorados. A comparação diferencia maiúsculas de minúsculas.|  
|`Reverse`|`@(MyItem->Reverse())`|Retorna os itens em ordem inversa.|  
|`AnyHaveMetadataValue`|`@(MyItem->AnyHaveMetadataValue("MetadataName", "MetadataValue"))`|Retorna um `boolean` para indicar se qualquer item tem o valor e o nome de metadados especificado. A comparação não diferencia maiúsculas de minúsculas.|  
|`ClearMetadata`|`@(MyItem->ClearMetadata())`|Retorna os itens com seus metadados desmarcados. Somente o `itemspec` é mantido.|  
|`HasMetadata`|`@(MyItem->HasMetadata("MetadataName"))`|Retorna os itens que têm o nome de metadados especificado. A comparação não diferencia maiúsculas de minúsculas.|  
|`Metadata`|`@(MyItem->Metadata("MetadataName"))`|Retorna os valores dos metadados que têm o nome de metadados.|  
|`WithMetadataValue`|`@(MyItem->WithMetadataValue("MetadataName", "MetadataValue"))`|Retorna os itens que têm o nome e o valor de metadados especificado. A comparação não diferencia maiúsculas de minúsculas.|  
  
 O exemplo a seguir mostra como usar funções intrínsecas de item.  
  
```xml  
<ItemGroup>  
    <TheItem Include="first">  
        <Plant>geranium</Plant>  
    </TheItem>  
    <TheItem Include="second">  
        <Plant>algae</Plant>  
    </TheItem>  
    <TheItem Include="third">  
        <Plant>geranium</Plant>  
    </TheItem>  
</ItemGroup>  
  
<Target Name="go">  
    <Message Text="MetaData:    @(TheItem->Metadata('Plant'))" />  
    <Message Text="HasMetadata: @(theItem->HasMetadata('Plant'))" />  
    <Message Text="WithMetadataValue: @(TheItem->WithMetadataValue('Plant', 'geranium'))" />  
    <Message Text=" " />  
    <Message Text="Count:   @(theItem->Count())" />  
    <Message Text="Reverse: @(theItem->Reverse())" />  
</Target>  
  
  <!--   
  Output:  
    MetaData:    geranium;algae;geranium  
    HasMetadata: first;second;third  
    WithMetadataValue: first;third  
  
    Count:   3  
    Reverse: third;second;first  
  -->  
```  
  
## <a name="see-also"></a>Consulte também  
 [Itens](../msbuild/msbuild-items.md)
