---
title: Elemento OnError (MSBuild) | Microsoft Docs
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
- http://schemas.microsoft.com/developer/msbuild/2003#OnError
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- OnError Element [MSBuild]
- <OnError Element [MSBuild]
ms.assetid: 765767d3-ecb7-4cd9-ba1e-d9468964dddc
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 10f89d21441418ae0b5c267c0fea7e8451115afe
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49228703"
---
# <a name="onerror-element-msbuild"></a>Elemento OnError (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Faz com que um ou mais destinos sejam executados se o atributo `ContinueOnError` for `false` para uma tarefa com falha.  
  
 \<Project>  
 \<Target>  
 \<OnError>  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<OnError ExecuteTargets="TargetName"  
    Condition="'String A'=='String B'" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Condition`|Atributo opcional.<br /><br /> Condição a ser avaliada. Para obter mais informações, consulte [Condições](../msbuild/msbuild-conditions.md).|  
|`ExecuteTargets`|Atributo obrigatório.<br /><br /> Os destinos que serão executados se uma tarefa falhar. Separe vários destinos com ponto e vírgula. Vários destinos são executados na ordem especificada.|  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Target](../msbuild/target-element-msbuild.md)|Elemento contêiner para tarefas [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)].|  
  
## <a name="remarks"></a>Comentários  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] executa o elemento `OnError` se uma das tarefas do elemento `Target` falha com o atributo `ContinueOnError` definido como `ErrorAndStop` (ou `false`). Quando a tarefa falhar, os destinos especificados no atributo `ExecuteTargets` serão executados. Se houver mais de um elemento `OnError` no destino, os elementos `OnError` serão executados sequencialmente quando a tarefa falhar.  
  
 Para obter informações sobre o atributo `ContinueOnError`, consulte [Elemento Task (MSBuild)](../msbuild/task-element-msbuild.md). Para obter mais informações sobre os destinos, consulte [Destinos](../msbuild/msbuild-targets.md).  
  
## <a name="example"></a>Exemplo  
 O código a seguir executa as tarefas `TaskOne` e `TaskTwo`. Se `TaskOne` falhar, [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] avaliará o elemento `OnError` e executará o destino `OtherTarget`.  
  
```  
<Target Name="ThisTarget">  
    <TaskOne ContinueOnError="ErrorAndStop">  
    </TaskOne>  
    <TaskTwo>  
    </TaskTwo>  
    <OnError ExecuteTargets="OtherTarget" />  
</Target>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência do esquema de arquivos de projeto](../msbuild/msbuild-project-file-schema-reference.md)   
 [Destinos](../msbuild/msbuild-targets.md)



