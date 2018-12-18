---
title: Definições de Itens | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- msbuild, item definitions
ms.assetid: 8e3dc223-f9e5-4974-aa0e-5dc7967419cb
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0c267c8a0d76fdda08112e428c0fc7403daa1f30
ms.sourcegitcommit: 5b767247b3d819a99deb0dbce729a0562b9654ba
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39178556"
---
# <a name="item-definitions"></a>Definições de item
O [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 2.0 permite a declaração estática de itens em arquivos de projeto usando o elemento [ItemGroup](../msbuild/itemgroup-element-msbuild.md). No entanto, metadados podem ser adicionados somente no nível de item, mesmo que os metadados sejam idênticos para todos os itens. Do [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 3.5 em diante, um elemento de projeto chamado [ItemDefinitionGroup](../msbuild/itemdefinitiongroup-element-msbuild.md) supera essa limitação. *ItemDefinitionGroup* permite que você defina um conjunto de definições de item, que adicionam valores de metadados padrão a todos os itens no tipo de item nomeado.  
  
 O elemento *ItemDefinitionGroup* aparece logo após o elemento [Project](../msbuild/project-element-msbuild.md) do arquivo de projeto. Definições de item fornecem a seguinte funcionalidade:  
  
-   Você pode definir metadados globais padrão para itens fora de um destino. Ou seja, os mesmos metadados se aplicam a todos os itens do tipo especificado.  
  
-   Tipos de item podem ter várias definições. Quando as especificações de metadados adicionais são adicionadas ao tipo, a última especificação tem precedência. \(Os metadados seguem a mesma ordem de importação das propriedades a seguir.\)  
  
-   Os metadados podem ser aditivos. Por exemplo, valores de CDefines são acumulados condicionalmente, dependendo das propriedades sendo definidas. Por exemplo, `MT;STD_CALL;DEBUG;UNICODE`.  
  
-   Os metadados podem ser removidos.  
  
-   É possível usar Conditions para controlar a inclusão de metadados.  
  
## <a name="item-metadata-default-values"></a>Valores padrão de metadados de item  
 Metadados do item que são definido em um ItemDefinitionGroup são apenas uma declaração de metadados padrão. Os metadados não se aplicam a menos que você defina um Item que use um ItemGroup para conter os valores de metadados.  
  
> [!NOTE]
>  Em muitos dos exemplos neste tópico, um elemento ItemDefinitionGroup é mostrado mas sua definição de ItemGroup correspondente é omitida para fins de clareza.  
  
 Os metadados definidos explicitamente em um ItemGroup têm precedência sobre metadados em ItemDefinitionGroup. Os metadados em ItemDefinitionGroup são aplicados somente a metadados indefinidos em um ItemGroup. Por exemplo:  
  
```xml  
<ItemDefinitionGroup>  
    <i>  
        <m>m1</m>  
        <n>n1</n>  
    </i>        
</ItemDefinitionGroup>  
<ItemGroup>  
    <i Include="a">  
        <o>o1</o>  
        <n>n2</n>  
    </i>  
</ItemGroup>  
```  
  
 Nesse exemplo, os metadados padrão "m" são aplicados ao Item "i" porque os metadados "m" não estão explicitamente definidos pelo Item "i". No entanto, os metadados padrão "n" não são aplicados ao Item "i" porque os metadados "n" já estão definidos pelo Item "i".  
  
> [!NOTE]
>  Nomes de parâmetro e de elemento XML diferenciam maiúsculas e minúsculas. Nomes de metadados de item e de propriedades de item não diferenciam maiúsculas e minúsculas. Portanto, itens ItemDefinitionGroup que têm nomes que diferem somente por maiúsculas e minúsculas devem ser tratados como o mesmo ItemGroup.  
  
## <a name="value-sources"></a>Fontes de valor  
 Os valores dos metadados definidos em um ItemDefinitionGroup podem vir de várias fontes diferentes, da seguinte maneira:  
  
-   Propriedade PropertyGroup  
  
-   Item de um ItemDefinitionGroup  
  
-   Transformação de item em um Item ItemDefinitionGroup  
  
-   Variável de ambiente  
  
-   Propriedade global (na linha de comando *MSBuild.exe*)  
  
-   Propriedade reservada  
  
-   Metadados conhecidos em um Item de um ItemDefinitionGroup  
  
-   Seção CDATA \<\!\[CDATA\[qualquer conteúdo presente aqui não será analisado\]\]\>  
  
> [!NOTE]
>  Metadados de item de um ItemGroup não são úteis em uma declaração de metadados de ItemDefinitionGroup porque elementos de ItemDefinitionGroup são processados antes de elementos de ItemGroup.  
  
## <a name="additive-and-multiple-definitions"></a>Definições aditivas e várias definições  
 Quando você adicionar definições ou usar vários ItemDefinitionGroups, lembre-se do seguinte:  
  
-   A especificação de metadados adicionais é adicionada ao tipo.  
  
-   A última especificação tem precedência.  
  
Quando você tem vários ItemDefinitionGroups, cada especificação subsequente adiciona seus metadados à definição anterior. Por exemplo:  
  
```xml  
<ItemDefinitionGroup>  
    <i>  
        <m>m1</m>  
        <n>n1</n>  
    </i>  
</ItemDefinitionGroup>  
<ItemDefinitionGroup>  
    <i>  
        <o>o1</o>  
    </i>  
</ItemDefinitionGroup>  
```  
  
Neste exemplo, os metadados "o" são adicionados a "m" e "n".  
  
Além disso, valores de metadados definidos anteriormente também podem ser adicionados. Por exemplo:  
  
```xml  
<ItemDefinitionGroup>  
    <i>  
        <m>m1</m>  
    </i>  
</ItemDefinitionGroup>  
<ItemDefinitionGroup>  
    <i>  
        <m>%(m);m2</m>  
    </i>  
</ItemDefinitionGroup>    
```  
  
Neste exemplo, o valor \(m1\) definido anteriormente para metadados "m" é adicionado ao novo valor \(m2\), de modo que o valor final é "m1; m2".  
  
> [!NOTE]
>  Isso também pode ocorrer no mesmo ItemDefinitionGroup.  
  
Quando você substituir os metadados definidos anteriormente, a última especificação terá precedência. No exemplo a seguir, o valor final de metadados "m" muda de "m1" para "m1a".  
  
```xml  
<ItemDefinitionGroup>  
    <i>  
        <m>m1</m>  
    </i>  
</ItemDefinitionGroup>  
<ItemDefinitionGroup>  
    <i>  
        <m>m1a</m>  
    </i>  
</ItemDefinitionGroup>    
```  
  
## <a name="use-conditions-in-an-itemdefinitiongroup"></a>Usar condições em um ItemDefinitionGroup  
 Você pode usar condições em um ItemDefinitionGroup para controlar a inclusão de metadados. Por exemplo:  
  
```xml  
<ItemDefinitionGroup Condition="'$(Configuration)'=='Debug'">  
    <i>  
        <m>m1</m>  
    </i>  
</ItemDefinitionGroup>  
```  
  
Nesse caso, os metadados padrão "m1" no item "i" são incluídos somente se o valor da propriedade "Configuration" é "Debug".  
  
> [!NOTE]
>  Somente as referências de metadados locais têm suporte em condições.  
  
Referências a metadados definidos em um ItemDefinitionGroup anterior são locais para o item, não para o grupo de definição. Ou seja, o escopo das referências é específico de um item. Por exemplo:  
  
```xml  
<ItemDefinitionGroup>  
    <test>  
        <yes>1</yes>  
    </test>  
    <i> 
        <m>m0</m>
        <m Condition="'%(test.yes)'=='1'">m1</m>  
    </i>  
</ItemDefinitionGroup>  
  
```  
  
No exemplo acima, item "i" faz referência ao item "test" em sua Condition. Essa Condition nunca será true porque o MSBuild interpreta uma referência aos metadados de outro item em um ItemDefinitionGroup como a cadeia de caracteres vazia. Assim, "m" seria definido como "m0."
 
```xml 
  <ItemDefinitionGroup>
    <i>
      <m>m0</m>
      <yes>1</yes>
      <m Condition="'%(i.yes)'=='1'">m1</m>
    </i>
  </ItemDefinitionGroup>

```

No exemplo acima, "m" seria definido para o valor "m1" conforme a Condition faz referência ao valor de metadados do item "i" para o item "yes". 
  
## <a name="override-and-delete-metadata"></a>Substituir e excluir metadados  
 Metadados definidos em um elemento ItemDefinitionGroup podem ser substituídos em um elemento ItemDefinitionGroup posterior, definindo-se o valor dos metadados como em branco. Você também pode excluir efetivamente um item de metadados configurando seu valor como vazio. Por exemplo:  
  
```xml  
<ItemDefinitionGroup>  
    <i>  
        <m>m1</m>  
    </i>  
</ItemDefinitionGroup>  
<ItemDefinitionGroup>  
    <i>  
        <m></m>  
    </i>  
</ItemDefinitionGroup>  
```  
  
O item "i" ainda contém metadados "m", mas seu valor agora está vazio.  
  
## <a name="scope-of-metadata"></a>Escopo dos metadados  
 Os ItemDefinitionGroups têm escopo global nas propriedades globais e definidas, onde quer que estejam definidas. As definições de metadados padrão em um ItemDefinitionGroup podem ser autorreferenciais. Por exemplo, o código a seguir usa uma referência de metadados simples:  
  
```xml  
<ItemDefinitionGroup>  
    <i>  
        <m>m1</m>  
        <m>%(m);m2</m>  
    </i>  
</ItemDefinitionGroup>  
```  
  
Uma referência de metadados qualificados também pode ser usada:  
  
```xml  
<ItemDefinitionGroup>  
    <i>  
      <m>m1</m>  
      <m>%(i.m);m2</m>  
    </i>  
</ItemDefinitionGroup>  
```  
  
No entanto, o seguinte não é válido:  
  
```xml  
<ItemDefinitionGroup>  
    <i>  
        <m>m1</m>  
        <m>@(x)</m>  
    </i>  
</ItemDefinitionGroup>  
```  
  
A partir do [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 3.5, ItemGroups também podem ser autorreferenciais. Por exemplo:  
  
```xml  
<ItemGroup>  
    <item Include="a">  
        <m>m1</m>  
        <m>%(m);m2</m>  
    </item>  
</ItemGroup>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Envio em lote](../msbuild/msbuild-batching.md)
