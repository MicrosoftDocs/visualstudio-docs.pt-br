---
title: Metadados de itens na separação de destinos em lotes | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- batching [MSBuild]
- MSBuild, target batching
- target batching [MSBuild]
ms.assetid: f3cc4186-6a4c-4161-bbe5-1ec638b4925b
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 486169788ad4533f5d45bf48c979ce3d0f5f7920
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39081053"
---
# <a name="item-metadata-in-target-batching"></a>Metadados de item no envio de destinos em lote
[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] tem a capacidade de executar a análise de dependência em entradas e saídas de um destino de build. Se for determinado que as entradas ou as saídas do destino estão atualizadas, o destino será ignorado e o build continuará. Elementos `Target` usam os atributos `Inputs` e `Outputs` para especificar os itens a fim de inspecionar durante a análise de dependência.  
  
 Se um destino contiver uma tarefa que usa itens em lotes como entradas ou saídas, o elemento `Target` do destino deve usar o envio em lote nos aributos `Inputs` ou `Outputs` para habilitar [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] a ignorar lotes de itens que já estão atualizados.  
  
## <a name="batch-targets"></a>Destinos em lotes  
 O exemplo a seguir contém uma lista de item nomeada `Res` que é dividida em dois lotes baseados nos metadados de item `Culture`. Cada um desses lotes é passada para a tarefa `AL`, que cria um assembly de saída para cada lote. Ao usar o envio em lote no atributo `Outputs` do elemento `Target`, [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] pode determinar se cada um dos lotes individuais está atualizado antes de executar o destino. Sem o uso do envio em lote de destino, ambos os lotes de itens seriam executados pela tarefa toda vez que o destino fosse executado.  
  
```xml  
<Project  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <Res Include="Strings.fr.resources">  
            <Culture>fr</Culture>  
        </Res>  
        <Res Include="Strings.jp.resources">  
            <Culture>jp</Culture>  
        </Res>  
        <Res Include="Menus.fr.resources">  
            <Culture>fr</Culture>  
        </Res>  
        <Res Include="Dialogs.fr.resources">  
            <Culture>fr</Culture>  
        </Res>  
        <Res Include="Dialogs.jp.resources">  
            <Culture>jp</Culture>  
        </Res>  
        <Res Include="Menus.jp.resources">  
            <Culture>jp</Culture>  
        </Res>  
    </ItemGroup>  
  
    <Target Name="Build"  
        Inputs="@(Res)"  
        Outputs="%(Culture)\MyApp.resources.dll">  
  
        <AL Resources="@(Res)"  
            TargetType="library"  
            OutputAssembly="%(Culture)\MyApp.resources.dll"  
  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Como criar de forma incremental](../msbuild/how-to-build-incrementally.md)   
 [Envio em lote](../msbuild/msbuild-batching.md)   
 [Elemento Target (MSBuild)](../msbuild/target-element-msbuild.md)   
 [Metadados de item no envio de tarefas em lote](../msbuild/item-metadata-in-task-batching.md)