---
title: Referência do esquema de arquivo de projeto MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, file schema
ms.assetid: d9a68146-1f43-4621-ac78-2c8c3f400936
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0ed3fd3fc60e6c263d7363047ed36b2f0d891a76
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39078934"
---
# <a name="msbuild-project-file-schema-reference"></a>Referência de esquema de arquivos de projeto do MSBuild
Fornece uma tabela de todos os elementos [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] do esquema XML com elementos filho e atributos disponíveis.  
  
 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] usa arquivos de projeto para instruir o mecanismo de build sobre o que e como compilar. Os arquivos de projeto [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] são arquivos XML que seguem o esquema XML [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]. Esta seção documenta o arquivo de definição de esquema XML (*.xsd*) para o [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)].  
  
## <a name="msbuild-xml-schema-elements"></a>Elementos do esquema XML do MSBuild  
 A tabela a seguir lista todos os elementos [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] de esquema XML junto com seus atributos e elementos filho.  
  
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
|[Elemento Parameter](../msbuild/parameter-element.md)|--|Saída<br /><br /> ParameterType<br /><br /> Necessária|  
|[Elemento ParameterGroup](../msbuild/parametergroup-element.md)|*Parâmetro*|--|  
|[Elemento Project (MSBuild)](../msbuild/project-element-msbuild.md)|Escolha<br /><br /> Importar<br /><br /> ItemGroup<br /><br /> ProjectExtensions<br /><br /> GrupoPropriedade<br /><br /> Destino<br /><br /> UsingTask|DefaultTargets<br /><br /> InitialTargets<br /><br /> ToolsVersion<br /><br /> TreatAsLocalProperty<br /><br /> xmlns|  
|[Elemento ProjectExtensions (MSBuild)](../msbuild/projectextensions-element-msbuild.md)|--|--|  
|[Elemento Property (MSBuild)](../msbuild/property-element-msbuild.md)|--|Condição|  
|[Elemento PropertyGroup (MSBuild)](../msbuild/propertygroup-element-msbuild.md)|*Property*|Condição|  
|[Elemento Sdk (MSBuild)](../msbuild/sdk-element-msbuild.md)|--|Nome<br /><br /> Versão|  
|[Elemento Target (MSBuild)](../msbuild/target-element-msbuild.md)|OnError<br /><br /> *Tarefa*|AfterTargets<br /><br /> BeforeTargets<br /><br /> Condição<br /><br /> DependsOnTargets<br /><br /> Entradas<br /><br /> KeepDuplicateOutputs<br /><br /> Nome<br /><br /> Saídas<br /><br /> Retorna|  
|[Elemento Task (MSBuild)](../msbuild/task-element-msbuild.md)|Saída|Condição<br /><br /> ContinueOnError<br /><br /> *Parâmetro*|  
|[Elemento TaskBody (MSBuild)](../msbuild/taskbody-element-msbuild.md)|*Dados*|Avaliar o|  
|[Elemento UsingTask (MSBuild)](../msbuild/usingtask-element-msbuild.md)|ParameterGroup<br /><br /> TaskBody|AssemblyFile<br /><br /> AssemblyName<br /><br /> Condição<br /><br /> TaskFactory<br /><br /> TaskName|  
|[Elemento When (MSBuild)](../msbuild/when-element-msbuild.md)|Escolha<br /><br /> ItemGroup<br /><br /> GrupoPropriedade|Condição|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Condições](../msbuild/msbuild-conditions.md)   
 [Referência do MSBuild](../msbuild/msbuild-reference.md)  
 [MSBuild](../msbuild/msbuild.md)
