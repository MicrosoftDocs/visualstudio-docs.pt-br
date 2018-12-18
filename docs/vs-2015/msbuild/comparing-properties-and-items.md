---
title: Comparando propriedades e itens | Microsoft Docs
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
- msbuild, msbuild properties
ms.assetid: b9da45ae-d6a6-4399-8628-397deed31486
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9d42cc8fb4e5ba0783ad24aedc0edf7a323db4d9
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49878577"
---
# <a name="comparing-properties-and-items"></a>Comparando propriedades e itens
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Itens e propriedades do MSBuild são usados para passar informações para tarefas, avaliar condições e armazenar os valores que podem ser referenciadas em todo o arquivo de projeto.  
  
-   Propriedades são pares nome-valor. Para mais informações, consulte [Propriedades do MSBuild](msbuild-properties1.md).  
  
-   Itens são objetos que normalmente representam arquivos. Objetos de item podem ter coleções de metadados associadas. Metadados são pares nome-valor. Para obter mais informações, consulte [Itens](../msbuild/msbuild-items.md).  
  
## <a name="scalars-and-vectors"></a>Escalares e vetores  
 Como as propriedades do MSBuild são pares nome-valor que têm apenas um valor de cadeia de caracteres, eles geralmente são descritos como *escalar*. Como os tipos de item do MSBuild são listas de itens, eles geralmente são descritos como *vetor*. No entanto, na prática, as propriedades podem representar vários valores e os tipos de item podem ter zero ou um item.  
  
### <a name="target-dependency-injection"></a>Injeção de dependência de destino  
 Para ver como as propriedades podem representar vários valores, considere um padrão de uso comum para adicionar um destino a uma lista de destinos a ser criada. Normalmente, essa lista é representada por um valor da propriedade com os nomes de destino separados por ponto-e-vírgula.  
  
```  
<PropertyGroup>  
    <BuildDependsOn>  
        BeforeBuild;  
        CoreBuild;  
        AfterBuild  
    </BuildDependsOn>  
</PropertyGroup>  
```  
  
 A propriedade `BuildDependsOn` normalmente é usada como o argumento de um atributo `DependsOnTargets` de destino, convertendo-o efetivamente em uma lista de itens. Essa propriedade pode ser substituída para adicionar um destino ou para alterar a ordem de execução de destino. Por exemplo,  
  
```  
<PropertyGroup>  
    <BuildDependsOn>  
        $(BuildDependsOn);  
        CustomBuild;  
    </BuildDependsOn>  
</PropertyGroup>  
```  
  
 adiciona o destino CustomBuild à lista de destinos, dando a `BuildDependsOn` o valor `BeforeBuild;CoreBuild;AfterBuild;CustomBuild`.  
  
 A partir do MSBuild 4.0, a injeção de dependência de destino é preterida. Em vez disso, use os atributos `AfterTargets` e `BeforeTargets`. Para obter mais informações, consulte [Target Build Order (Ordem de build de destino)](../msbuild/target-build-order.md).  
  
### <a name="conversions-between-strings-and-item-lists"></a>Conversões entre cadeias de caracteres e listas de itens  
 O MSBuild executa conversões em e de tipos de item e valores de cadeias de caracteres conforme necessário. Para ver como uma lista de itens pode se tornar um valor de cadeia de caracteres, considere o que acontece quando um tipo de item é usado como o valor de uma propriedade do MSBuild:  
  
```  
<ItemGroup>  
    <OutputDir Include="KeyFiles\;Certificates\" />  
  </ItemGroup>  
<PropertyGroup>  
    <OutputDirList>@(OutputDir)</OutputDirList>  
</PropertyGroup>  
```  
  
 O tipo de item OutputDir tem um atributo `Include` com o valor "KeyFiles\\;Certificates\\". O MSBuild analisa essa cadeia de caracteres em dois itens: KeyFiles e Certificates\\. Quando o tipo de item OutputDir é usado como o valor da propriedade OutputDirList, o MSBuild converte ou mescla o tipo de item na cadeia de caracteres separados por ponto-e-vírgula "KeyFiles\\;Certificates\\".  
  
## <a name="properties-and-items-in-tasks"></a>Propriedades e itens em Tarefas  
 As propriedades e os itens são usados como entradas e saídas para tarefas do MSBuild. Para obter mais informações, consulte [Tarefas](../msbuild/msbuild-tasks.md).  
  
 Propriedades são passadas para tarefas como atributos. Dentro da tarefa, uma propriedade do MSBuild é representada por um tipo de propriedade cujo valor pode ser convertido em ou de uma cadeia de caracteres. Os tipos de propriedade compatíveis incluem `bool`, `char`, `DateTime`, `Decimal`, `Double`, `int`, `string` e qualquer tipo que <xref:System.Convert.ChangeType%2A> possa manipular.  
  
 Os itens são passados para tarefas como objetos <xref:Microsoft.Build.Framework.ITaskItem>. Dentro da tarefa, o <xref:Microsoft.Build.Framework.ITaskItem.ItemSpec%2A> representa o valor do item e <xref:Microsoft.Build.Framework.ITaskItem.GetMetadata%2A> recupera os metadados.  
  
 A lista de itens de um tipo de item pode ser passada como uma matriz de objetos `ITaskItem`. A partir do .NET Framework 3.5, os itens podem ser removidos de uma lista de itens em um destino usando o atributo `Remove`. Como os itens podem ser removidos de uma lista de itens, é possível que um tipo de item tenha zero itens. Se uma lista de itens é passada para uma tarefa, o código na tarefa deve verificar essa possibilidade.  
  
## <a name="property-and-item-evaluation-order"></a>Ordem de avaliação de itens e propriedades  
 Durante a fase de avaliação de um build, os arquivos importados são incorporados ao build na ordem em que são exibidos. As propriedades e os itens são definidos em três passos na seguinte ordem:  
  
- As propriedades são definidas e modificadas na ordem em que são exibidas.  
  
- As definições de itens são realizadas e modificadas na ordem em que são exibidas.  
  
- Os itens são definidos e modificados na ordem em que são exibidos.  
  
  Durante a fase de execução de um build, as propriedades e os itens definidos dentro dos destinos são avaliados juntamente em uma única fase na ordem na qual são exibidos.  
  
  No entanto, essa não é a história completa. Quando uma propriedade, definição de item ou o item é definido, seu valor é avaliado. O avaliador de expressão expande a cadeia de caracteres que especifica o valor. A expansão de cadeia de caracteres depende da fase do build. Abaixo, há uma ordem de avaliação de itens e propriedades mais detalhada:  
  
- Durante a fase de avaliação de um build:  
  
  -   As propriedades são definidas e modificadas na ordem em que são exibidas. As funções de propriedade são executadas. Os valores da propriedade na forma $(PropertyName) são expandidos dentro de expressões. O valor da propriedade é definido como a expressão expandida.  
  
  -   As definições de itens são realizadas e modificadas na ordem em que são exibidas. As funções da propriedade já foram expandidas dentro das expressões. Os valores de metadados são definidos como as expressões expandidas.  
  
  -   Os tipos de item são definidos e modificados na ordem em que são exibidos. Os valores de item na forma @(ItemType) são expandidos. As transformações de item também são expandidas. As funções e valores de propriedade já foram expandidos dentro das expressões. Os valores da lista de itens e de metadados são definidos como as expressões expandidas.  
  
- Durante a fase de execução de um build:  
  
  -   As propriedades e os itens definidos dentro dos destinos são avaliados em conjunto na ordem em que são exibidos. As funções de propriedade são executadas e os valores da propriedade são expandidos dentro das expressões. Os valores e as transformações de item também são expandidas. Os valores da propriedade, de tipo de item e de metadados são definidos como as expressões expandidas.  
  
### <a name="subtle-effects-of-the-evaluation-order"></a>Efeitos sutis da ordem de avaliação  
 Na fase de avaliação de um build, a avaliação da propriedade precede a avaliação do item. No entanto, as propriedades podem ter valores que parecem depender de valores de item. Considere o script a seguir.  
  
```  
<ItemGroup>  
    <KeyFile Include="KeyFile.cs">  
        <Version>1.0.0.3</Version>  
    </KeyFile>  
</ItemGroup>  
<PropertyGroup>  
    <KeyFileVersion>@(KeyFile->'%(Version)')</KeyFileVersion>  
</PropertyGroup>  
<Target Name="AfterBuild">  
    <Message Text="KeyFileVersion: $(KeyFileVersion)" />  
</Target>  
```  
  
 Executar a tarefa Mensagem exibe esta mensagem:  
  
```  
KeyFileVersion: 1.0.0.3  
```  
  
 Isso ocorre porque o valor de `KeyFileVersion` é, na verdade, a cadeia de caracteres "@(KeyFile->'%(Version)')". O item e as transformações de item não foram expandidos quando a propriedade foi definida pela primeira vez. Portanto, a propriedade `KeyFileVersion` recebeu o valor da cadeia de caracteres não expandida.  
  
 Durante a fase de execução do build, quando ele processa a tarefa Mensagem, o MSBuild expande a cadeia de caracteres "@(KeyFile->'%(Version)')" para produzir "1.0.0.3".  
  
 Observe que a mesma mensagem seria exibida mesmo se os grupos de propriedade e de item fossem invertidos em ordem.  
  
 Como um segundo exemplo, considere o que pode acontecer quando grupos de propriedade e de item estão localizados dentro dos destinos:  
  
```  
<Target Name="AfterBuild">  
    <PropertyGroup>  
        <KeyFileVersion>@(KeyFile->'%(Version)')</KeyFileVersion>  
    </PropertyGroup>  
    <ItemGroup>  
        <KeyFile Include="KeyFile.cs">  
            <Version>1.0.0.3</Version>  
        </KeyFile>  
    </ItemGroup>  
    <Message Text="KeyFileVersion: $(KeyFileVersion)" />  
</Target>  
```  
  
 A tarefa de mensagem exibe esta mensagem:  
  
```  
KeyFileVersion:   
```  
  
 Isso ocorre porque, durante a fase de execução do build, os grupos de propriedade e de item definidos dentro dos destinos são avaliados de cima para baixo ao mesmo tempo. Quando `KeyFileVersion` é definido, `KeyFile` é desconhecido. Portanto, a transformação de item é expandida para uma cadeia de caracteres vazia.  
  
 Nesse caso, inverter a ordem dos grupos de item e de propriedade restaura a mensagem original:  
  
```  
<Target Name="AfterBuild">  
    <ItemGroup>  
        <KeyFile Include="KeyFile.cs">  
            <Version>1.0.0.3</Version>  
        </KeyFile>  
    </ItemGroup>  
    <PropertyGroup>  
        <KeyFileVersion>@(KeyFile->'%(Version)')</KeyFileVersion>  
    </PropertyGroup>  
    <Message Text="KeyFileVersion: $(KeyFileVersion)" />  
</Target>  
```  
  
 O valor de `KeyFileVersion` é definido como "1.0.0.3" e não como "@(KeyFile->'%(Version)')". A tarefa de mensagem exibe esta mensagem:  
  
```  
KeyFileVersion: 1.0.0.3  
```  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos avançados](../msbuild/msbuild-advanced-concepts.md)



