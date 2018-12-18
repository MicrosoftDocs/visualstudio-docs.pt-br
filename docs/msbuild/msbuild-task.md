---
title: Tarefa do MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#MSBuild
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild task [MSBuild]
- MSBuild, MSBuild task
ms.assetid: 76577f6c-7669-44ad-a840-363e37a04d34
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2a4d7a296902695007541e4c21c661f659fbbaab
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49861599"
---
# <a name="msbuild-task"></a>tarefa MSBuild
Compila projetos [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] de outro projeto [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)].  

## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `MSBuild`.  


| Parâmetro | Descrição |
|-----------------------------------| - |
| `BuildInParallel` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, os projetos especificados no parâmetro `Projects` serão criados em paralelo, se possível. O padrão é `false`. |
| `Projects` | Parâmetro <xref:Microsoft.Build.Framework.ITaskItem>`[]` obrigatório.<br /><br /> Especifica os arquivos de projeto para compilar. |
| `Properties` | Parâmetro `String` opcional.<br /><br /> Uma lista delimitada por ponto-e-vírgula de pares de nome/valor de propriedade para aplicar como propriedades globais para o projeto filho. Ao especificar esse parâmetro, ele será funcionalmente equivalente às propriedades de definição que têm o comutador **-property** quando você compila com [*MSBuild.exe*](../msbuild/msbuild-command-line-reference.md). Por exemplo:<br /><br /> `Properties="Configuration=Debug;Optimize=$(Optimize)"`<br /><br /> Ao passar propriedades para o projeto por meio do parâmetro `Properties`, [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] criará uma nova instância do projeto, mesmo se o arquivo de projeto já tiver sido carregado. Quando uma nova instância do projeto tiver sido criada, [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] a tratará como um projeto diferente que tem propriedades globais diferentes e que pode ser criado em paralelo com outras instâncias do projeto. Por exemplo, uma configuração de versão poderia ser compilada ao mesmo tempo como uma configuração de depuração. |
| `RebaseOutputs` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, os caminhos relativos dos itens de saída de destino de projetos de compilação terão seus caminhos ajustados para serem relativos ao projeto de chamada. O padrão é `false`. |
| `RemoveProperties` | Parâmetro `String` opcional.<br /><br /> Especifica o conjunto de propriedades globais para remover. |
| `RunEachTargetSeparately` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] chamará cada destino na lista passada para [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)], um de cada vez, em vez de ao mesmo tempo. Definir esse parâmetro como `true` garante que os destinos subsequentes sejam chamados mesmo se os destinos chamados anteriormente tiverem falhado. Caso contrário, um erro de build pararia a invocação de todos os destinos subsequentes. O padrão é `false`. |
| `SkipNonexistentProjects` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, os arquivos de projeto que não existem no disco serão ignorados. Caso contrário, esses projetos causarão um erro. |
| `StopOnFirstFailure` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, quando um dos projetos falhar em compilar, os projetos não serão mais compilados. Atualmente isso não tem suporte na criação em paralelo (com vários processadores). |
| `TargetAndPropertyListSeparators` | Parâmetro `String[]` opcional.<br /><br /> Especifica uma lista de destinos e de propriedades como metadados de item `Project`). Separadores não serão escapados antes do processamento. Por exemplo, %3B (um escape ';') será tratado como se não fosse escapado ';'. |
| `TargetOutputs` | Parâmetro <xref:Microsoft.Build.Framework.ITaskItem>`[]` de saída opcional somente leitura.<br /><br /> Retorna as saídas dos destinos compilados de todos os arquivos de projeto. Somente as saídas de destinos que foram especificados são retornadas, não as saídas que podem existir em destinos dos quais esses destinos dependem.<br /><br /> O parâmetro `TargetOutputs` também contém os metadados a seguir:<br /><br /> -   `MSBuildSourceProjectFile`: o arquivo de projeto [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] que contém o destino que defina as saídas.<br />-   `MSBuildSourceTargetName`: o destino que define as saídas. **Observação:** para identificar as saídas de cada arquivo de projeto ou destino separadamente, execute a tarefa `MSBuild` separadamente para cada arquivo de projeto ou destino. Se você executar a tarefa `MSBuild` apenas uma vez para compilar todos os arquivos de projeto, as saídas de todos os destinos serão coletadas em uma matriz. |
| `Targets` | Parâmetro `String` opcional.<br /><br /> Especifica o destino ou destinos para build nos arquivos de projeto. Use uma lista separada por ponto-e-vírgula de nomes de destino. Se nenhum destino for especificado na tarefa `MSBuild`, os destinos padrão especificados nos arquivos de projeto serão compilados. **Observação:** os destinos devem ocorrer em todos os arquivos de projeto. Caso contrário, ocorrerá um erro de build. |
| `ToolsVersion` | Parâmetro `String` opcional.<br /><br /> Especifica o `ToolsVersion` a ser usado ao compilar projetos passados para essa tarefa.<br /><br /> Permite que uma tarefa [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] compile um projeto que tem como alvo uma versão diferente de [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] do que a especificada no projeto. Os valores válidos são `2.0`, `3.0` e `3.5`. O valor padrão é `3.5`. |
| `UnloadProjectsOnCompletion` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, o projeto será descarregado quando a operação for concluída. |
| `UseResultsCache` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, o resultado em cache será retornado, se presente.<br /><br />  Se a tarefa do MSBuild for executada, o resultado será ser armazenado em cache em um escopo <br /><br /> (ProjectFileName, GlobalProperties)[TargetNames]<br /><br /> como uma lista de itens de build |

## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, confira [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  

 Em vez de usar a [tarefa Exec](../msbuild/exec-task.md) para iniciar o *MSBuild.exe*, essa tarefa usa o mesmo processo [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] para criar projetos filho. A lista de destinos já compilados que pode ser ignorada é compartilhada entre as compilações pai e filho. Essa tarefa também é mais rápida porque nenhum processo [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] novo é criado.  

 Essa tarefa pode processar não somente arquivos de projeto, mas também arquivos de solução.  

 Qualquer configuração que é exigida pelo [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] para habilitar projetos para build ao mesmo tempo, mesmo se a configuração envolve a infraestrutura remota (por exemplo, portas, protocolos, tempos limite, repetições e assim por diante), deverá ser feita configurável usando um arquivo de configuração. Quando possível, itens de configuração deverão ser capazes de ser especificados como parâmetros de tarefa na tarefa `MSBuild`.  

 A partir do [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 3.5, os projetos do Solution agora abrangem TargetOutputs de todos os subprojetos que ele compila.  

## <a name="pass-properties-to-projects"></a>Passar propriedades para projetos  
 Em versões do [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] anteriores ao [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 3.5, passar diferentes conjuntos de propriedades para diferentes projetos listados no item [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] era um desafio. Se você tiver usado o atributo de propriedades da [tarefa do MSBuild](../msbuild/msbuild-task.md), então essa configuração foi aplicada a todos os projetos que estão sendo criados, a menos que você tenha enviado em lote a [tarefa do MSBuild](../msbuild/msbuild-task.md) e fornecido condicionalmente propriedades diferentes para cada projeto na lista de itens.  

 O [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 3.5, no entanto, fornece dois novos itens de metadados reservados, Properties e AdditionalProperties, que oferecem uma maneira flexível de passar diferentes propriedades para diferentes projetos criados usando a [tarefa do MSBuild](../msbuild/msbuild-task.md).  

> [!NOTE]
>  Esses novos itens de metadados são aplicáveis apenas para itens que passaram no atributo de projetos da [tarefa do MSBuild](../msbuild/msbuild-task.md).  

## <a name="multi-processor-build-benefits"></a>Benefícios da compilação multiprocessador  
 Um dos principais benefícios de usar esses novos metadados ocorre quando você compila seus projetos em paralelo em um sistema com vários processadores. Os metadados permitem consolidar todos os projetos em uma única chamada da [tarefa do MSBuild](../msbuild/msbuild-task.md) sem ter que executar qualquer processamento em lotes ou tarefas [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] condicionais. E quando você chama uma única [tarefa do MSBuild](../msbuild/msbuild-task.md), todos os projetos listados no atributo de projetos são criados em paralelo. (Apenas, no entanto, se o atributo `BuildInParallel=true` estiver presente na [tarefa do MSBuild](../msbuild/msbuild-task.md)). Para saber mais, confira [Compilar vários projetos em paralelo](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md).  

## <a name="properties-metadata"></a>Metadados de propriedades  
 Um cenário comum é ao compilar vários arquivos de solução usando a [tarefa do MSBuild](../msbuild/msbuild-task.md), usar apenas configurações de build diferentes. Você pode querer compilar a solução a1 usando a configuração de depuração e compilar a solução a2 usando a configuração de versão. Em [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 2.0, esse arquivo de projeto seria semelhante ao seguinte:  

> [!NOTE]
>  No exemplo a seguir, "…" representa arquivos adicionais da solução.  

### <a name="aproj"></a>a.proj  

```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <Target Name="Build">  
        <MSBuild Projects="a1.sln..." Properties="Configuration=Debug"/>  
        <MSBuild Projects="a2.sln" Properties="Configuration=Release"/>  
    </Target>  
</Project>  
```  

 Usando os metadados de propriedades, no entanto, você pode simplificar isso para usar uma única [tarefa do MSBuild](../msbuild/msbuild-task.md), conforme mostrado a seguir:  

### <a name="aproj"></a>a.proj  

```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <ProjectToBuild Include="a1.sln...">  
            <Properties>Configuration=Debug</Properties>  
        </ProjectToBuild>  
        <ProjectToBuild Include="a2.sln">  
            <Properties>Configuration=Release</Properties>  
        </ProjectToBuild>  
    </ItemGroup>  
    <Target Name="Build">  
        <MSBuild Projects="@(ProjectToBuild)"/>  
    </Target>  
</Project>  
```  

 \- ou -  

```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <ProjectToBuild Include="a1.sln..."/>  
        <ProjectToBuild Include="a2.sln">  
            <Properties>Configuration=Release</Properties>  
        </ProjectToBuild>  
    </ItemGroup>  
    <Target Name="Build">  
        <MSBuild Projects="@(ProjectToBuild)"   
          Properties="Configuration=Debug"/>  
    </Target>  
</Project>  
```  

## <a name="additionalproperties-metadata"></a>Metadados de AdditionalProperties  
 Considere o seguinte cenário em que você está compilando dois arquivos de solução usando a [tarefa do MSBuild](../msbuild/msbuild-task.md), usando a configuração de versão, mas uma que usa a arquitetura x86 e outra usando a arquitetura ia64. No [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 2.0, você precisaria criar várias instâncias da [tarefa do MSBuild](../msbuild/msbuild-task.md): uma para compilar o projeto usando a configuração de versão com a arquitetura x86, a outra usando a configuração de versão com a arquitetura ia64. Seu arquivo de projeto seria semelhante ao seguinte:  

### <a name="aproj"></a>a.proj  

```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <Target Name="Build">  
        <MSBuild Projects="a1.sln..." Properties="Configuration=Release;   
          Architecture=x86"/>  
        <MSBuild Projects="a2.sln" Properties="Configuration=Release;   
          Architecture=ia64"/>  
    </Target>  
</Project>  
```  

 Usando os metadados AdditionalProperties, você pode simplificar isso para usar uma única [tarefa do MSBuild](../msbuild/msbuild-task.md), conforme mostrado a seguir:  

### <a name="aproj"></a>a.proj  

```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <ProjectToBuild Include="a1.sln...">  
            <AdditionalProperties>Architecture=x86  
              </AdditionalProperties>  
        </ProjectToBuild>  
        <ProjectToBuild Include="a2.sln">  
            <AdditionalProperties>Architecture=ia64  
              </AdditionalProperties>  
        </ProjectToBuild>  
    </ItemGroup>  
    <Target Name="Build">  
        <MSBuild Projects="@(ProjectToBuild)"   
          Properties="Configuration=Release"/>  
    </Target>  
</Project>  
```  

## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a tarefa `MSBuild` para compilar projetos especificados pela coleção de itens `ProjectReferences`. As saídas de destino resultantes são armazenadas na coleção de itens `AssembliesBuiltByChildProjects`.  

```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  

    <ItemGroup>  
        <ProjectReferences Include="*.*proj" />  
    </ItemGroup>  

    <Target Name="BuildOtherProjects">  
        <MSBuild  
            Projects="@(ProjectReferences)"  
            Targets="Build">  
            <Output  
                TaskParameter="TargetOutputs"  
                ItemName="AssembliesBuiltByChildProjects" />  
        </MSBuild>  
    </Target>  

</Project>  
```  

## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)