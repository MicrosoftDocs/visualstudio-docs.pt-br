---
title: Elemento TaskBody (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- TaskBody element [MSBuild]
- <TaskBody> element [MSBuild]
ms.assetid: 49d8741b-f1ea-4470-94fd-a1ac27341a6a
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6b02616b54c0697f824d53eab978142679e8a358
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 02/19/2019
ms.locfileid: "54752385"
---
# <a name="taskbody-element-msbuild"></a>Elemento TaskBody (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Contém os dados que são passados para um `UsingTask``TaskFactory`. Para obter mais informações, consulte [Elemento UsingTask (MSBuild)](../msbuild/usingtask-element-msbuild.md).  
  
 \<Project>  
 \<UsingTask>  
 \<TaskBody>  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<TaskBody Evaluate="true/false" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Evaluate`|Atributo booliano opcional.<br /><br /> Se `true`, MSBuild avalia todos os elementos internos e expande os itens e propriedades antes de transmitir as informações para o `TaskFactory`, quando a tarefa é instanciada.|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|Dados|O texto entre as `TaskBody` marcas é enviada textual para `TaskFactory`.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[UsingTask](../msbuild/usingtask-element-msbuild.md)|Fornece uma maneira para registrar tarefas em [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]. Pode ser que não haja nenhum ou mais de um elemento `UsingTask` em um projeto.|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar o elemento `TaskBody` com um atributo `Evaluate`.  
  
```  
<UsingTask TaskName="MyTask" AssemblyName="My.Assembly" TaskFactory="MyTaskFactory">  
       <ParameterGroup>  
              <Parameter1 ParameterType="System.String" Required="False" Output="False"/>  
              <Parameter2 ParameterType="System.Int" Required="True" Output="False"/>  
              ...  
</ParameterGroup>  
       <TaskBody Evaluate="true">  
      ... Task factory-specific data ...  
       </TaskBody>  
</UsingTask>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Referência do esquema de arquivos de projeto](../msbuild/msbuild-project-file-schema-reference.md)
