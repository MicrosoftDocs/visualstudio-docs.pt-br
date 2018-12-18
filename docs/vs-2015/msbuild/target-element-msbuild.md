---
title: Elemento Target (MSBuild) | Microsoft Docs
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
- http://schemas.microsoft.com/developer/msbuild/2003#Target
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Target element [MSBuild]
- <Target> element [MSBuild]
ms.assetid: 350f6fc2-86b3-45f2-a31e-ece0e6bd4dca
caps.latest.revision: 38
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bc4224930782e24b20d3e9720c517304b0153f2d
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49173401"
---
# <a name="target-element-msbuild"></a>Elemento Target (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Contém um conjunto de tarefas para o [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] executar em sequência.  
  
 \<Project>  
 \<Target>  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<Target Name="Target Name"  
        Inputs="Inputs"  
        Outputs="Outputs"  
        Returns="Returns"  
        KeepDuplicateOutputs="true/false"  
        BeforeTargets="Targets"  
        AfterTargets="Targets"  
        DependsOnTargets="DependentTarget"  
        Condition="'String A' == 'String B'">  
        Label="Label">  
    <Task>... </Task>  
    <PropertyGroup>… </PropertyGroup>  
    <ItemGroup>… </ItemGroup>  
    <OnError... />  
</Target>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Name`|Atributo obrigatório.<br /><br /> O nome do destino.|  
|`Condition`|Atributo opcional.<br /><br /> A condição a ser avaliada. Se a condição for avaliada como `false`, o destino não executará o corpo dos destinos definidos no atributo `DependsOnTargets`. Para obter mais informações sobre condições, consulte [Condições](../msbuild/msbuild-conditions.md).|  
|`Inputs`|Atributo opcional.<br /><br /> Os arquivos que formam entradas nesse destino. Vários arquivos são separados por ponto e vírgula. Os carimbos de data/hora dos arquivos serão comparados com os dos arquivos em `Outputs` para determinar se o `Target` está atualizado. Para obter mais informações, consulte [Compilações incrementais](../msbuild/incremental-builds.md), [Como compilar de forma incremental](../msbuild/how-to-build-incrementally.md) e [Transformações](../msbuild/msbuild-transforms.md).|  
|`Outputs`|Atributo opcional.<br /><br /> Os arquivos que formam saídas nesse destino. Vários arquivos são separados por ponto e vírgula. Os carimbos de data/hora dos arquivos serão comparados com os dos arquivos em `Inputs` para determinar se o `Target` está atualizado. Para obter mais informações, consulte [Compilações incrementais](../msbuild/incremental-builds.md), [Como compilar de forma incremental](../msbuild/how-to-build-incrementally.md) e [Transformações](../msbuild/msbuild-transforms.md).|  
|`Returns`|Atributo opcional.<br /><br /> O conjunto de itens que será disponibilizado para tarefas que invocam esse destino, por exemplo, tarefas do MSBuild. Vários destinos são separados por ponto e vírgula. Se os destinos no arquivo não tiverem nenhum atributo `Returns`, os atributos de Saídas serão usados para essa finalidade.|  
|`KeepDuplicateOutputs`|Atributo booliano opcional.<br /><br /> Se for `true`, várias referências ao mesmo item nos Retornos do destino serão registradas.  Por padrão, esse atributo é `false`.|  
|`BeforeTargets`|Atributo opcional.<br /><br /> Uma lista separada por ponto e vírgula de nomes de destino.  Quando especificado, indica que esse destino deve ser executado antes dos destinos especificados. Isso permite que o autor do projeto estenda um conjunto existente de destinos sem modificá-los diretamente. Para obter mais informações, consulte [Target Build Order (Ordem de build de destino)](../msbuild/target-build-order.md).|  
|`AfterTargets`|Atributo opcional.<br /><br /> Uma lista separada por ponto e vírgula de nomes de destino. Quando especificado, indica que esse destino deve ser executado após os destinos especificados. Isso permite que o autor do projeto estenda um conjunto existente de destinos sem modificá-los diretamente. Para obter mais informações, consulte [Target Build Order (Ordem de build de destino)](../msbuild/target-build-order.md).|  
|`DependsOnTargets`|Atributo opcional.<br /><br /> Os destinos que devem ser executados antes que esse destino possa ser executado ou antes que a análise de dependência de nível superior possa ocorrer. Vários destinos são separados por ponto e vírgula.|  
|`Label`|Atributo opcional.<br /><br /> Um identificador que pode identificar ou ordenar os elementos do sistema e do usuário.|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Tarefa](../msbuild/task-element-msbuild.md)|Cria e executa uma instância de uma tarefa [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]. Pode haver zero ou mais tarefas em um destino.|  
|[PropertyGroup](../msbuild/propertygroup-element-msbuild.md)|Contém um conjunto de elementos `Property` definidos pelo usuário. A partir do .NET Framework 3.5, um elemento `Target` pode conter elementos `PropertyGroup`.|  
|[ItemGroup](../msbuild/itemgroup-element-msbuild.md)|Contém um conjunto de elementos `Item` definidos pelo usuário. A partir do .NET Framework 3.5, um elemento `Target` pode conter elementos `ItemGroup`. Para obter mais informações, consulte [Itens](../msbuild/msbuild-items.md).|  
|[OnError](../msbuild/onerror-element-msbuild.md)|Faz com que um ou mais destinos sejam executados se o atributo `ContinueOnError` é ErrorAndStop (ou `false`) para uma tarefa com falha. Pode haver zero ou mais elementos `OnError` em um destino. Se `OnError` elementos estiverem presentes, eles deverão ser os últimos elementos do elemento `Target`.<br /><br /> Para obter informações sobre o atributo `ContinueOnError`, consulte [Elemento Task (MSBuild)](../msbuild/task-element-msbuild.md).|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Projeto](../msbuild/project-element-msbuild.md)|Elemento raiz necessário de um arquivo de projeto [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)].|  
  
## <a name="remarks"></a>Comentários  
 O primeiro destino a ser executado é especificado em tempo de execução. Os destinos podem ter dependências em outros destinos. Por exemplo, um destino de implantação depende de um destino de compilação. O mecanismo [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] executa dependências na ordem em que aparecem no atributo `DependsOnTargets`, da esquerda para a direita. Para obter mais informações, consulte [Destinos](../msbuild/msbuild-targets.md).  
  
 Um destino é executado apenas uma vez durante um build, mesmo se mais de um destino tem uma dependência dele.  
  
 Se um destino for ignorado porque seu atributo `Condition` é avaliado como `false`, ele ainda poderá ser executado se for invocado posteriormente no build e se seu atributo `Condition` for avaliado como `true` nesse momento.  
  
 Antes do MSBuild 4, `Target` retornava todos os itens que eram especificados no atributo `Outputs`.  Para fazer isso, o MSBuild precisava registrar esses itens, caso tarefas posteriores no build os solicitassem. Como não havia nenhuma maneira de indicar quais destinos tinham saídas que seriam exigidas por chamadores, o MSBuild acumulou todos os itens de todos os `Outputs` em todos os `Target`s invocados. Isso leva a problemas de colocação em escala em compilações que tinham um grande número de itens de saída.  
  
 Se o usuário especificar um `Returns` em um elemento `Target` de um projeto, apenas esses `Target`s que têm um atributo `Returns` registrarão esses itens.  
  
 Um `Target` pode conter tanto um atributo `Outputs` quanto um atributo `Returns`.  `Outputs` é usado com `Inputs` para determinar se o destino está atualizado. `Returns`, se estiver presente, substitui o valor de `Outputs` para determinar quais itens são retornados aos chamadores.  Se `Returns` não estiver presente, `Outputs` será disponibilizado para os chamadores, exceto no caso descrito anteriormente.  
  
 Antes do MSBuild 4, sempre que um `Target` incluía várias referências ao mesmo item em seu `Outputs`, esses itens duplicados eram registrados. Em compilações muito grandes que tinham um grande número de saídas e várias interdependências de projeto, isso causava uma grande quantidade de memória gasta devido à inutilidade dos itens duplicados. Quando o atributo `KeepDuplicateOutputs` é definido como `true`, essas duplicatas são registradas.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir mostra um elemento `Target` que executa a tarefa `Csc`.  
  
```  
<Target Name="Compile" DependsOnTargets="Resources" Returns="$(TargetPath)">  
    <Csc Sources="@(CSFile)"  
          TargetType="library"  
          Resources="@(CompiledResources)"  
          EmitDebugInformation="$(includeDebugInformation)"  
          References="@(Reference)"  
          DebugType="$(debuggingType)" >  
        <Output TaskParameter="OutputAssembly"  
                  ItemName="FinalAssemblyName" />  
    </Csc>  
</Target>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Destinos](../msbuild/msbuild-targets.md)   
 [Referência do esquema de arquivos de projeto](../msbuild/msbuild-project-file-schema-reference.md)



