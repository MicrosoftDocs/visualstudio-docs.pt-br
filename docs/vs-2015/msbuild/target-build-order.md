---
title: Ordem de build de destinos | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- msbuild, build order
ms.assetid: f4a26339-9f9a-497a-9aa6-0797183d450d
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f5d619a18fa38c09b25f2d8367f3f767ac5bdc11
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59651076"
---
# <a name="target-build-order"></a>Ordem de build de destinos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

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
  
```  
<Project InitialTargets="Warm;Eject" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
```  
  
 Os projetos importados podem ter seus próprios atributos `InitialTargets`. Todos os destinos iniciais são agregados juntos e executados na ordem.  
  
 Para obter mais informações, confira [Como: Especificar o destino de Build primeiro](../msbuild/how-to-specify-which-target-to-build-first.md).  
  
## <a name="default-targets"></a>Destinos Padrão  
 O atributo `DefaultTargets` do elemento [Project](../msbuild/project-element-msbuild.md) especifica quais destinos serão compilados se um destino não for especificado explicitamente em uma linha de comando.  
  
 O valor do atributo `DefaultTargets` pode ser uma lista de destinos padrão, delimitada por ponto e vírgula. O exemplo a seguir especifica que o destino `Clean` é executado e, em seguida, que o destino `Build` é executado.  
  
```  
<Project DefaultTargets="Clean;Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
```  
  
 É possível substituir os destinos padrão usando a opção **/target** na linha de comando. O exemplo a seguir especifica que o destino `Build` é executado e, em seguida, que o destino `Report` é executado. Ao especificar destinos dessa forma, os destinos padrão são ignorados.  
  
 `msbuild /target:Build;Report`  
  
 Se forem especificados destinos iniciais e destinos padrão e nenhum destino de linha de comando for especificado, o MSBuild executará os destinos iniciais primeiro e, em seguida, os destinos padrão.  
  
 Os projetos importados podem ter seus próprios atributos `DefaultTargets`. O primeiro atributo `DefaultTargets` encontrado determina quais destinos padrão serão executados.  
  
 Para obter mais informações, confira [Como: Especificar o destino de Build primeiro](../msbuild/how-to-specify-which-target-to-build-first.md).  
  
## <a name="first-target"></a>Primeiro Destino  
 Se não houver nenhum destino inicial, destino padrão ou destino de linha de comando, o MSBuild executará o primeiro destino encontrado no arquivo de projeto ou nos arquivos de projeto importados.  
  
## <a name="target-dependencies"></a>Dependências de Destino  
 Os destinos podem descrever relações de dependência entre si. O atributo `DependsOnTargets` indica que um destino depende de outros destinos. Por exemplo,  
  
```  
<Target Name="Serve" DependsOnTargets="Chop;Cook" />  
```  
  
 informa ao MSBuild que o destino `Serve` depende dos destino `Chop` e `Cook`. O MSBuild executa o destino `Chop` e, em seguida, o destino `Cook` antes de executar o destino `Serve`.  
  
## <a name="beforetargets-and-after-targets"></a>Antes e depois dos destinos  
 No MSBuild 4.0, é possível especificar a ordem de destinos usando os atributos `BeforeTargets` e `AfterTargets`.  
  
 Considere o script a seguir.  
  
```  
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
  
```  
<Target Name="Optimize"   
    AfterTargets="Compile" BeforeTargets="Link">  
    <Message Text="Optimizing" />  
</Target>  
```  
  
## <a name="determining-the-target-build-order"></a>Determinando a Ordem de Compilação de Destino  
 O MSBuild determina a ordem de build de destinos da seguinte maneira:  
  
1.  Os destinos `InitialTargets` são executados.  
  
2.  Os destinos especificados na linha de comando pela opção **/target** são executados. Se você não especificar nenhum destino na linha de comando, os destinos `DefaultTargets` serão executados. Se nenhum deles estiver presente, o primeiro destino encontrado será executado.  
  
3.  O atributo `Condition` do destino é avaliado. Se o atributo `Condition` estiver presente e for avaliado como `false`, o destino não será executado e não terá nenhum efeito adicional no build.  
  
4.  Antes de um destino ser executado, seus destinos `DependsOnTargets` são executados.  
  
5.  Antes de um destino ser executado, qualquer destino que o lista em um atributo `BeforeTargets` é executado.  
  
6.  Antes de um destino ser executado, os atributos `Inputs` e `Outputs` são comparados. Se o MSBuild determinar que os arquivos de saída estão desatualizados em relação aos arquivos de entrada correspondentes, ele executará o destino. Caso contrário, o MSBuild ignorará o destino.  
  
7.  Depois que um destino é executado ou ignorado, qualquer destino que o lista em um atributo `AfterTargets` é executado.  
  
## <a name="see-also"></a>Consulte também  
 [Destinos](../msbuild/msbuild-targets.md)
