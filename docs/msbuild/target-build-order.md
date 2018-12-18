---
title: Ordem de build de destinos | Microsoft Docs
ms.custom: ''
ms.date: 09/04/2018
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- msbuild, build order
ms.assetid: f4a26339-9f9a-497a-9aa6-0797183d450d
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 13405d197fc5ab64d4c7b7040580f073e36f98c7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49812654"
---
# <a name="target-build-order"></a>Ordem de build de destino
Os destinos deverão ser ordenados se a entrada para um destino depender da saída de outro. É possível usar esses atributos para especificar a ordem na qual os destinos são executados:  
  
- `InitialTargets`. Este atributo `Project` especifica os destinos que serão executados primeiro, mesmo se os destinos foram especificados na linha de comando ou no atributo `DefaultTargets`.  
  
- `DefaultTargets`. Este atributo `Project` especifica quais destinos serão executados se um destino não for especificado explicitamente na linha de comando.  
  
- `DependsOnTargets`. Este atributo `Target` especifica os destinos que devem ser executados antes que esse destino possa ser executado.  
  
- `BeforeTargets` e `AfterTargets`. Esses atributos `Target` especificam que esse destino deve ser executado antes ou após os destinos especificados (MSBuild 4.0).  
  
  Um destino nunca é executado duas vezes durante um build, mesmo se um destino posterior no build depende dele. Depois que um destino tiver sido executado, sua contribuição para o build será concluída.  
  
  Os destinos podem ter um atributo `Condition`. Se a condição especificada for avaliada como `false`, o destino não será executado e não terá nenhum efeito no build. Para obter mais informações sobre condições, consulte [Condições](../msbuild/msbuild-conditions.md).  
  
## <a name="initial-targets"></a>Destinos Iniciais  
 O atributo `InitialTargets` do elemento [Project](../msbuild/project-element-msbuild.md) especifica os destinos que serão executados primeiro, mesmo se os destinos forem especificados na linha de comando ou no atributo `DefaultTargets`. Normalmente, os destinos iniciais são usados para verificação de erros.  
  
 O valor do atributo `InitialTargets` pode ser uma lista ordenada de destinos, delimitada por ponto e vírgula. O exemplo a seguir especifica que o destino `Warm` é executado e, em seguida, que o destino `Eject` é executado.  
  
```xml  
<Project InitialTargets="Warm;Eject" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
```  
  
 Os projetos importados podem ter seus próprios atributos `InitialTargets`. Todos os destinos iniciais são agregados juntos e executados na ordem.  
  
 Para saber mais, consulte [Como especificar qual destino será compilado primeiro](../msbuild/how-to-specify-which-target-to-build-first.md).  
  
## <a name="default-targets"></a>Destinos padrão  
 O atributo `DefaultTargets` do elemento [Project](../msbuild/project-element-msbuild.md) especifica quais destinos serão compilados se um destino não for especificado explicitamente em uma linha de comando.  
  
 O valor do atributo `DefaultTargets` pode ser uma lista de destinos padrão, delimitada por ponto e vírgula. O exemplo a seguir especifica que o destino `Clean` é executado e, em seguida, que o destino `Build` é executado.  
  
```xml  
<Project DefaultTargets="Clean;Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
```  
  
 É possível substituir os destinos padrão usando a opção **–target** na linha de comando. O exemplo a seguir especifica que o destino `Build` é executado e, em seguida, que o destino `Report` é executado. Ao especificar destinos dessa forma, os destinos padrão são ignorados.  
  
 `msbuild -target:Build;Report`  
  
 Se forem especificados destinos iniciais e destinos padrão e nenhum destino de linha de comando for especificado, o MSBuild executará os destinos iniciais primeiro e, em seguida, os destinos padrão.  
  
 Os projetos importados podem ter seus próprios atributos `DefaultTargets`. O primeiro atributo `DefaultTargets` encontrado determina quais destinos padrão serão executados.  
  
 Para saber mais, consulte [Como especificar qual destino será compilado primeiro](../msbuild/how-to-specify-which-target-to-build-first.md).  
  
## <a name="first-target"></a>Primeiro destino  
 Se não houver nenhum destino inicial, destino padrão ou destino de linha de comando, o MSBuild executará o primeiro destino encontrado no arquivo de projeto ou nos arquivos de projeto importados.  
  
## <a name="target-dependencies"></a>Dependências de destino  
 Os destinos podem descrever relações de dependência entre si. O atributo `DependsOnTargets` indica que um destino depende de outros destinos. Por exemplo,  
  
```xml  
<Target Name="Serve" DependsOnTargets="Chop;Cook" />  
```  
  
 informa ao MSBuild que o destino `Serve` depende dos destino `Chop` e `Cook`. O MSBuild executa o destino `Chop` e, em seguida, o destino `Cook` antes de executar o destino `Serve`.  
  
## <a name="beforetargets-and-aftertargets"></a>BeforeTargets e AfterTargets  
 No MSBuild 4.0, é possível especificar a ordem de destinos usando os atributos `BeforeTargets` e `AfterTargets`.  
  
 Considere o script a seguir.  
  
```xml  
<Project DefaultTargets="Compile;Link" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <Target Name="Compile">  
        <Message Text="Compiling" />  
    </Target>  
    <Target Name="Link">  
        <Message Text="Linking" />  
    </Target>  
</Project>  
```  
  
 Para criar um destino intermediário `Optimize` que é executado após o destino `Compile`, mas antes do destino `Link`, adicione o destino a seguir em qualquer lugar do elemento `Project`.  
  
```xml  
<Target Name="Optimize"   
    AfterTargets="Compile" BeforeTargets="Link">  
    <Message Text="Optimizing" />  
</Target>  
```  
  
## <a name="determine-the-target-build-order"></a>Determinar a ordem de compilação de destino  
 O MSBuild determina a ordem de build de destinos da seguinte maneira:  
  
1.  Os destinos `InitialTargets` são executados.  
  
2.  Os destinos especificados na linha de comando pela opção **–target** são executados. Se você não especificar nenhum destino na linha de comando, os destinos `DefaultTargets` serão executados. Se nenhum deles estiver presente, o primeiro destino encontrado será executado.  
  
3.  O atributo `Condition` do destino é avaliado. Se o atributo `Condition` estiver presente e for avaliado como `false`, o destino não será executado e não terá nenhum efeito adicional no build.

    Destinos que listam o destino condicional em `BeforeTargets` ou `AfterTargets` ainda são executados na ordem prescrita
  
4.  Antes que um destino seja executado ou ignorado, se o atributo `Condition` estava ausente ou não foi avaliado para `false`, os destinos de `DependsOnTargets` serão executados.  
  
5.  Antes da execução de um destino, ou de ignorá-lo, qualquer destino que contiver um atributo `BeforeTargets` será executado.  
  
6.  Antes de um destino ser executado, os atributos `Inputs` e `Outputs` são comparados. Se o MSBuild determinar que os arquivos de saída estão desatualizados em relação aos arquivos de entrada correspondentes, ele executará o destino. Caso contrário, o MSBuild ignorará o destino.  
  
7.  Depois que um destino é executado ou ignorado, qualquer destino que o lista em um atributo `AfterTargets` é executado.  
  
## <a name="see-also"></a>Consulte também  
 [Destinos](../msbuild/msbuild-targets.md)
