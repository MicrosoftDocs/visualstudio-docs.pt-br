---
title: Referência do esquema de arquivo de projeto MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, file schema
ms.assetid: d9a68146-1f43-4621-ac78-2c8c3f400936
caps.latest.revision: 22
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cd1add4f68bb2e0648cf3cf08b72b1bc6f592595
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49305975"
---
# <a name="msbuild-project-file-schema-reference"></a>Referência do esquema de arquivos de projeto do MSBuild
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Fornece uma tabela de todos os elementos [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] do esquema XML com elementos filho e atributos disponíveis.  
  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] usa arquivos de projeto para instruir o mecanismo de build sobre o que e como compilar. Os arquivos de projeto [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] são arquivos XML que seguem o esquema XML [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]. Esta seção documenta o arquivo de definição do esquema XML (.xsd) para [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)].  
  
## <a name="msbuild-xml-schema-elements"></a>Elementos do esquema XML do MSBuild  
 A tabela a seguir lista todos os elementos [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] de esquema XML junto com seus atributos e elementos filho.  
  
|Elemento|Elementos filho|Atributos|  
|-------------|--------------------|----------------|  
|[Elemento Choose (MSBuild)](../msbuild/choose-element-msbuild.md)|Otherwise<br /><br /> When|--|  
|[Elemento Import (MSBuild)](../msbuild/import-element-msbuild.md)|--|Condição<br /><br /> Projeto|  
|[Elemento ImportGroup](../msbuild/importgroup-element.md)|Importar|Condição|  
|[Elemento Item (MSBuild)](../msbuild/item-element-msbuild.md)|*ItemMetaData*|Condição<br /><br /> Excluir<br /><br /> Incluir<br /><br /> Remover|  
|[Elemento ItemDefinitionGroup (MSBuild)](../msbuild/itemdefinitiongroup-element-msbuild.md)|*Item*|Condição|  
|[Elemento ItemGroup (MSBuild)](../msbuild/itemgroup-element-msbuild.md)|*Item*|Condição|  
|[Elemento ItemMetadata (MSBuild)](../msbuild/itemmetadata-element-msbuild.md)|*Item*|Condição|  
|[Elemento OnError (MSBuild)](../msbuild/onerror-element-msbuild.md)|--|Condição<br /><br /> ExecuteTargets|  
|[Elemento Otherwise (MSBuild)](../msbuild/otherwise-element-msbuild.md)|Escolha<br /><br /> ItemGroup<br /><br /> GrupoPropriedade|--|  
|[Elemento Output (MSBuild)](../msbuild/output-element-msbuild.md)|--|Condição<br /><br /> NomeItem<br /><br /> PropertyName<br /><br /> TaskParameter|  
|[Elemento de Parâmetro](../msbuild/parameter-element.md)|--|Saída<br /><br /> ParameterType<br /><br /> Necessária|  
|[Elemento ParameterGroup](../msbuild/parametergroup-element.md)|*Parâmetro*|--|  
|[Elemento Project (MSBuild)](../msbuild/project-element-msbuild.md)|Escolha<br /><br /> Importar<br /><br /> ItemGroup<br /><br /> ProjectExtensions<br /><br /> GrupoPropriedade<br /><br /> Destino<br /><br /> UsingTask|DefaultTargets<br /><br /> InitialTargets<br /><br /> ToolsVersion<br /><br /> TreatAsLocalProperty<br /><br /> xmlns|  
|[Elemento ProjectExtensions (MSBuild)](../msbuild/projectextensions-element-msbuild.md)|--|--|  
|[Elemento Property (MSBuild)](../msbuild/property-element-msbuild.md)|--|Condição|  
|[Elemento PropertyGroup (MSBuild)](../msbuild/propertygroup-element-msbuild.md)|*Property*|Condição|  
|[Elemento Target (MSBuild)](../msbuild/target-element-msbuild.md)|OnError<br /><br /> *Tarefa*|AfterTargets<br /><br /> BeforeTargets<br /><br /> Condição<br /><br /> DependsOnTargets<br /><br /> Entradas<br /><br /> KeepDuplicateOutputs<br /><br /> Nome<br /><br /> Saídas<br /><br /> Retorna|  
|[Elemento Task (MSBuild)](../msbuild/task-element-msbuild.md)|Saída|Condição<br /><br /> ContinueOnError<br /><br /> *Parâmetro*|  
|[Elemento TaskBody (MSBuild)](../msbuild/taskbody-element-msbuild.md)|*Dados*|Avaliar o|  
|[Elemento UsingTask (MSBuild)](../msbuild/usingtask-element-msbuild.md)|ParameterGroup<br /><br /> TaskBody|AssemblyFile<br /><br /> AssemblyName<br /><br /> Condição<br /><br /> TaskFactory<br /><br /> TaskName|  
|[Elemento When (MSBuild)](../msbuild/when-element-msbuild.md)|Escolha<br /><br /> ItemGroup<br /><br /> GrupoPropriedade|Condição|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Condições](../msbuild/msbuild-conditions.md)   
 [Referência do MSBuild](../msbuild/msbuild-reference.md)  
 [MSBuild](msbuild.md)


