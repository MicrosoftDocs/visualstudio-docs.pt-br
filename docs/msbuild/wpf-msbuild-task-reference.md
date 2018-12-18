---
title: Referência da Tarefa do WPF MSBuild | Microsoft Docs
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
- WPF MSBuild task reference [WPF MSBuild], term/definition table
- build tasks [WPF MSBuild], Microsoft build engine
- build tasks using the Microsoft build engine [WPF MSBuild], compile markup and process resources
- WPF MSBuild task reference [WPF MSBuild]
ms.assetid: 96df0370-e50f-4ffc-9771-b12fb8721143
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 53f723644744001e39967186d0eeec74bf7d3bd7
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39153794"
---
# <a name="wpf-msbuild-task-reference"></a>Referência de tarefas do WPF MSBuild
O processo de build do Windows Presentation Foundation (WPF) estende o Microsoft Build Engine (MSBuild) com um conjunto adicional de tarefas de build, incluindo tarefas para compilar recursos de marcação e o processo.  
  
## <a name="in-this-section"></a>Nesta seção  
 [FileClassifier](../msbuild/fileclassifier-task.md)  
 Classifica um conjunto de recursos de origem que será inserido em um assembly. Se um recurso não for localizável, ele será inserido no assembly principal do aplicativo; caso contrário, ele será inserido em um assembly satélite.  
  
 [GenerateTemporaryTargetAssembly](../msbuild/generatetemporarytargetassembly-task.md)  
 Gera um assembly se pelo menos uma página [!INCLUDE[TLA#tla_xaml](../msbuild/includes/tlasharptla_xaml_md.md)] em um projeto referencia um tipo declarado localmente no projeto. O assembly gerado será removido após concluir o processo de build ou se o processo de build falhar.  
  
 [GetWinFXPath](../msbuild/getwinfxpath-task.md)  
 Retorna o diretório do tempo de execução [!INCLUDE[TLA#tla_winfx](../msbuild/includes/tlasharptla_winfx_md.md)] atual.  
  
 [MarkupCompilePass1](../msbuild/markupcompilepass1-task.md)  
 Converte arquivos de projeto [!INCLUDE[TLA#tla_xaml](../msbuild/includes/tlasharptla_xaml_md.md)] não localizáveis para o formato binário compilado.  
  
 [MarkupCompilePass2](../msbuild/markupcompilepass2-task.md)  
 Executa a compilação de marcação de segunda passagem em [!INCLUDE[TLA#tla_xaml](../msbuild/includes/tlasharptla_xaml_md.md)] arquivos que fazem referência a tipos no mesmo projeto.  
  
 [MergeLocalizationDirectives](../msbuild/mergelocalizationdirectives-task.md)  
 Mescla os atributos de localização e comentários de um ou mais [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] arquivos de formato binário em um único arquivo para todo o assembly.  
  
 [ResourcesGenerator](../msbuild/resourcesgenerator-task.md)  
 Insere um ou mais recursos (*.jpg*, *.ico*, *.bmp*, [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] em formato binário e outros tipos de extensão) em um arquivo *.resources*.  
  
 [UidManager](../msbuild/uidmanager-task.md)  
 Verifica, atualiza ou remove identificadores exclusivos (UIDs), para localizar todos os [!INCLUDE[TLA#tla_xaml](../msbuild/includes/tlasharptla_xaml_md.md)] elementos que são incluídos na fonte de [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] arquivos.  
  
 [UpdateManifestForBrowserApplication](../msbuild/updatemanifestforbrowserapplication-task.md)  
 Adiciona o elemento **\<hostInBrowser / >** para o manifesto do aplicativo (*\<projectname.exe.manifest*) quando um projeto de [!INCLUDE[TLA#tla_xbap](../msbuild/includes/tlasharptla_xbap_md.md)] é compilado.  
  
## <a name="see-also"></a>Consulte também  
 [MSBuild](../msbuild/msbuild.md)