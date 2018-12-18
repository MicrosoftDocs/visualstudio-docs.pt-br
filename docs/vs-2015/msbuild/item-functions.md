---
title: Funções de itens | Microsoft Docs
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
- msbuild, Item functions
ms.assetid: 5e6df3cc-2db8-4cbd-8fdd-3ffd03ac0876
caps.latest.revision: 32
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 687d740a379bd3b04bd47d0d2e3111bb71e7934d
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49207916"
---
# <a name="item-functions"></a>Funções de itens
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Começando com o MSBuild 4.0, o código em tarefas e destinos pode chamar funções de item para obter informações sobre os itens no projeto. Essas funções simplificam a obtenção de itens Distinct() e são mais rápidas do que executar loop nos itens.  
  
## <a name="string-item-functions"></a>Funções de Item de Cadeia de Caracteres  
 É possível usar métodos e propriedades de cadeia de caracteres no .NET Framework para operar em qualquer valor de item. Para métodos <xref:System.String>, especifique o nome do método. Para propriedades <xref:System.String>, especifique o nome da propriedade após "get_".  
  
 Para itens que têm várias cadeias de caracteres, o método ou propriedade da cadeia de caracteres será executado em cada cadeia de caracteres.  
  
 O exemplo a seguir mostra como usar essas funções de item de cadeia de caracteres.  
  
```  
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
  
## <a name="intrinsic-item-functions"></a>Funções Intrínsecas de Item  
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
|`HasMetadata`|`@(MyItem->HasMetadataValue("MetadataName")`|Retorna os itens que têm o nome de metadados especificado. A comparação não diferencia maiúsculas de minúsculas.|  
|`Metadata`|`@(MyItem->Metadata("MetadataName"))`|Retorna os valores dos metadados que têm o nome de metadados.|  
|`WithMetadataValue`|`@(MyItem->WithMetadataValue("MetadataName", "MetadataValue")`|Retorna os itens que têm o nome e o valor de metadados especificado. A comparação não diferencia maiúsculas de minúsculas.|  
  
 O exemplo a seguir mostra como usar funções intrínsecas de item.  
  
```  
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



