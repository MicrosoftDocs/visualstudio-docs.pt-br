---
title: Elemento UsingTask (MSBuild) | Microsoft Docs
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
- http://schemas.microsoft.com/developer/msbuild/2003#UsingTask
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- UsingTask element [MSBuild]
- <UsingTask> element [MSBuild]
ms.assetid: 20247902-9446-4a1f-8253-5c7a17e4fe43
caps.latest.revision: 27
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e412fce1169b0e68c6b2f924b95c5433728be3a7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49871934"
---
# <a name="usingtask-element-msbuild"></a>Elemento UsingTask (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Mapeia a tarefa que é referenciada em um elemento [Tarefa](../msbuild/task-element-msbuild.md) para o assembly que contém a implementação de tarefas.  
  
 \<Project>  
 \<UsingTask>  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<UsingTask TaskName="TaskName"  
    AssemblyName = "AssemblyName"   
    TaskFactory = "ClassName"  
    Condition="'String A'=='String B'" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`AssemblyName`|O atributo `AssemblyName` ou o `AssemblyFile` é necessário.<br /><br /> O nome do assembly a ser carregado. O atributo `AssemblyName` aceita os assemblies de nomes fortes, embora não seja necessário com nomes fortes. Usar esse atributo é equivalente a carregar um assembly usando o método <xref:System.Reflection.Assembly.Load%2A> no .NET.<br /><br /> Você não poderá usar esse atributo se o atributo `AssemblyFile` for usado.|  
|`AssemblyFile`|O atributo `AssemblyName` ou `AssemblyFile` é necessário.<br /><br /> O caminho do arquivo do assembly. Esse atributo aceita caminhos completos ou caminhos relativos. Caminhos relativos são relativos ao diretório do arquivo de projeto ou arquivo de destino no qual o elemento `UsingTask` é declarado. Usar esse atributo é equivalente a carregar um assembly usando o método <xref:System.Reflection.Assembly.LoadFrom%2A> no .NET.<br /><br /> Você não poderá usar esse atributo se o atributo `AssemblyName` for usado.|  
|`TaskFactory`|Atributo opcional.<br /><br /> Especifica a classe no assembly que é responsável por gerar instâncias do nome `Task` especificado.  O usuário também pode especificar um `TaskBody` como um elemento filho que a fábrica de tarefa recebe e usa para gerar a tarefa. O conteúdo de `TaskBody` é específico para a fábrica da tarefa.|  
|`TaskName`|Atributo obrigatório.<br /><br /> O nome da tarefa para referência de um assembly. Se for possível usar ambiguidades, esse atributo sempre deverá especificar namespaces completos. Se houver ambiguidades, o MSBuild escolherá uma correspondência arbitrária, que poderá produzir resultados inesperados.|  
|`Condition`|Atributo opcional.<br /><br /> A condição que será avaliada. Para obter mais informações, consulte [Condições](../msbuild/msbuild-conditions.md).|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[ParameterGroup](../msbuild/parametergroup-element.md)|O conjunto de parâmetros que aparecem na tarefa que é gerada pelo `TaskFactory` especificado.|  
|[Tarefa](../msbuild/task-element-msbuild.md)|Os dados que são passados para o `TaskFactory` para gerar uma instância da tarefa.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Projeto](../msbuild/project-element-msbuild.md)|Elemento raiz necessário de um arquivo de projeto [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)].|  
  
## <a name="remarks"></a>Comentários  
 Variáveis de ambiente, propriedades de linha de comando e propriedades de nível de projeto podem ser referenciadas em algum lugar do elemento `UsingTask` se ele aparecer no arquivo de projeto explicitamente ou por meio de um arquivo de projeto importado. Para obter mais informações, consulte [Tarefas](../msbuild/msbuild-tasks.md).  
  
> [!NOTE]
>  Propriedades de nível de projeto não têm significado se o elemento `UsingTask` for proveniente de um dos arquivos .tasks globalmente registrados com o mecanismo do MSBuild. Propriedades de nível de projeto não são globais para o MSBuild.  
  
 No MSBuild 4.0, usar tarefas pode ser carregado de arquivos .overridetask.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar o elemento `UsingTask` com um atributo `AssemblyName`.  
  
```  
<UsingTask TaskName="MyTask" AssemblyName="My.Assembly" TaskFactory="MyTaskFactory">  
       <ParameterGroup>  
              <Parameter1 ParameterType="System.String" Required="False" Output="False"/>  
              <Parameter2 ParameterType="System.Int" Required="True" Output="False"/>  
              ...  
</ParameterGroup>  
       <TaskBody>  
      ... Task factory-specific data ...  
       </TaskBody>  
</UsingTask>  
```  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar o elemento `UsingTask` com um atributo `AssemblyFile`.  
  
```  
<UsingTask TaskName="Email"  
              AssemblyFile="c:\myTasks\myTask.dll" />  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Referência do esquema de arquivos de projeto](../msbuild/msbuild-project-file-schema-reference.md)



