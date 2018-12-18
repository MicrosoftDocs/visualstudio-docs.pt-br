---
title: Como estender o processo de build do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, overriding predefined targets
- MSBuild, overriding DependsOn properties
- MSBuild, extending Visual Studio builds
- MSBuild, DependsOn properties
ms.assetid: cb077613-4a59-41b7-96ec-d8516689163c
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 777c2c4ecb5ea8561a43a12f1897c2260d6638d0
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39081547"
---
# <a name="how-to-extend-the-visual-studio-build-process"></a>Como estender o processo de build do Visual Studio
O processo de build do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] é definido por uma série de arquivos *.targets* do [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] que são importados para o arquivo de projeto. Um desses arquivos importados, *Microsoft.Common.targets*, pode ser estendido para permitir a execução de tarefas personalizadas em vários pontos no processo de build. Este artigo explica os dois métodos que você pode usar para estender o processo de build do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]:  
  
-   Substituindo destinos predefinidos específicos definidos em *Microsoft.Common.targets*.  
  
-   Substituindo as propriedades "DependsOn" definidas em *Microsoft.Common.targets*.  
  
## <a name="override-predefined-targets"></a>Substituir destinos predefinidos  
 O arquivo *Microsoft.Common.targets* contém um conjunto de destinos vazios predefinidos que é chamado antes e depois de alguns dos principais destinos no processo de build. Por exemplo, [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] chama o destino `BeforeBuild` antes do destino `CoreBuild` principal e o destino `AfterBuild` após o destino `CoreBuild`. Por padrão, os destinos vazios em *Microsoft.Common.targets* não tem nenhum efeito, mas você pode substituir o comportamento padrão definindo os destinos desejados em um arquivo de projeto que importa *Microsoft.Common.targets*. Substituindo destinos predefinidos, você pode usar tarefas do [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] para obter mais controle sobre o processo de build.  
  
#### <a name="to-override-a-predefined-target"></a>Para substituir um destino predefinido  
  
1.  Identifique um destino predefinido em *Microsoft.Common.targets* que você deseja substituir. Consulte a tabela abaixo para obter uma lista completa de destinos que você pode substituir com segurança.  
  
2.  Defina o destino ou destinos no final do arquivo de projeto, imediatamente antes da marca `</Project>`. Por exemplo:  
  
    ```xml  
    <Project>  
        ...  
        <Target Name="BeforeBuild">  
            <!-- Insert tasks to run before build here -->  
        </Target>  
        <Target Name="AfterBuild">  
            <!-- Insert tasks to run after build here -->  
        </Target>  
    </Project>  
    ```  
  
3.  Compile o arquivo de projeto.  

A tabela a seguir mostra todos os destinos em *Microsoft.Common.targets* que você pode substituir com segurança.  
  
|Nome de destino|Descrição|  
|-----------------|-----------------|  
|`BeforeCompile`, `AfterCompile`|As tarefas inseridas em um desses destinos são executadas antes ou após a conclusão da compilação principal. A maioria das personalizações é realizada em um desses dois destinos.|  
|`BeforeBuild`, `AfterBuild`|As tarefas inseridas em um desses destinos serão executadas antes ou depois de todo o resto no build. **Observação:** os destinos `BeforeBuild` e `AfterBuild` já estão definidos nos comentários ao final da maioria dos arquivos de projeto, permitindo que você adicione com facilidade eventos de pré e pós-build ao arquivo de projeto.|  
|`BeforeRebuild`, `AfterRebuild`|As tarefas inseridas em um desses destinos são executadas antes ou após a invocação da funcionalidade de recompilação principal. A ordem de execução de destino em *Microsoft.Common.targets* é: `BeforeRebuild`, `Clean`, `Build` e, em seguida, `AfterRebuild`.|  
|`BeforeClean`, `AfterClean`|As tarefas inseridas em um desses destinos são executadas antes ou após a invocação da funcionalidade de limpeza principal.|  
|`BeforePublish`, `AfterPublish`|As tarefas inseridas em um desses destinos são executadas antes ou após a invocação da funcionalidade de publicação principal.|  
|`BeforeResolveReference`, `AfterResolveReferences`|As tarefas inseridas em um desses destinos são executadas antes ou após a resolução das referências de assembly.|  
|`BeforeResGen`, `AfterResGen`|As tarefas inseridas em um desses destinos são executadas antes ou após a geração de recursos.|  
  
## <a name="override-dependson-properties"></a>Substituir propriedades DependsOn  
 Substituir destinos predefinidos é uma maneira fácil de estender o processo de build, mas, como [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] avalia a definição de destinos sequencialmente, não há nenhuma maneira de impedir que outro projeto que importa seu projeto substitua os destinos que você já substituiu. Dessa forma, por exemplo, o último destino `AfterBuild` no arquivo de projeto, depois que todos os outros projetos foram importados, será aquele usado durante o build.  
  
 Você pode se proteger contra substituições indesejadas de destinos substituindo as propriedades DependsOn usadas em atributos `DependsOnTargets` em todo o arquivo *Microsoft.Common.targets*. Por exemplo, o destino `Build` contém um valor de atributo `DependsOnTargets` de `"$(BuildDependsOn)"`. Considere:  
  
```xml  
<Target Name="Build" DependsOnTargets="$(BuildDependsOn)"/>  
```  
  
 Este trecho de XML indica que, antes de poder executar o destino `Build`, todos os destinos especificados na propriedade `BuildDependsOn` devem ser executados primeiro. A propriedade `BuildDependsOn` está definida como:  
  
```xml  
<PropertyGroup>  
    <BuildDependsOn>  
        BeforeBuild;  
        CoreBuild;  
        AfterBuild  
    </BuildDependsOn>  
</PropertyGroup>  
```  
  
 Você pode substituir esse valor da propriedade declarando outra propriedade denominada `BuildDependsOn` no final do seu arquivo de projeto. Incluindo a propriedade `BuildDependsOn` anterior na nova propriedade, você pode adicionar novos destinos no início e fim da lista de destinos. Por exemplo:  
  
```xml  
<PropertyGroup>  
    <BuildDependsOn>  
        MyCustomTarget1;  
        $(BuildDependsOn);  
        MyCustomTarget2  
    </BuildDependsOn>  
</PropertyGroup>  
  
<Target Name="MyCustomTarget1">  
    <Message Text="Running MyCustomTarget1..."/>  
</Target>  
<Target Name="MyCustomTarget2">  
    <Message Text="Running MyCustomTarget2..."/>  
</Target>  
```  
  
 Projetos que importam seus arquivos de projeto podem substituir essas propriedades sem substituir as personalizações que você fez.  
  
#### <a name="to-override-a-dependson-property"></a>Para substituir uma propriedade DependsOn  
  
1.  Identifique uma propriedade DependsOn predefinida em *Microsoft.Common.targets* que você deseja substituir. Confira a tabela abaixo para obter uma lista das propriedades DependsOn geralmente substituídas.  
  
2.  Defina outra instância da propriedade ou propriedades no final do seu arquivo de projeto. Inclua a propriedade original, por exemplo `$(BuildDependsOn)`, na nova propriedade.  
  
3.  Defina seus destinos personalizados antes ou após a definição da propriedade.  
  
4.  Compile o arquivo de projeto.  
  
### <a name="commonly-overridden-dependson-properties"></a>Propriedades DependsOn geralmente substituídas  
  
|Property name|Descrição|  
|-------------------|-----------------|  
|`BuildDependsOn`|A propriedade a ser substituída se você quiser inserir destinos personalizados antes ou após o processo inteiro de build.|  
|`CleanDependsOn`|A propriedade a ser substituída você quiser limpar a saída do seu processo de build personalizado.|  
|`CompileDependsOn`|A propriedade a ser substituída se você quiser inserir processos personalizados antes ou após a etapa de compilação.|  
  
## <a name="see-also"></a>Consulte também  
 [Integração com o Visual Studio](../msbuild/visual-studio-integration-msbuild.md)   
 [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)   
 [Arquivos .targets](../msbuild/msbuild-dot-targets-files.md)