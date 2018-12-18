---
title: Arquivos .targets do MSBuild | Microsoft Docs
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
- .Targets files
- MSBuild, .Targets files
ms.assetid: f6d98eb4-d2fa-49b7-8e3c-bae1ca3cf596
caps.latest.revision: 20
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bec05a2947bad76b0be4e7cf339bbef98a27644e
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49274229"
---
# <a name="msbuild-targets-files"></a>Arquivos .targets do MSBuild
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] inclui vários arquivos .targets que contêm itens, propriedades, destinos e tarefas para cenários comuns. Esses arquivos são automaticamente importados para a maioria dos arquivos de projeto [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para simplificar a manutenção e a legibilidade.  
  
 Os projetos normalmente importam um ou mais arquivos .targets para definir o processo de build. Por exemplo, um projeto [!INCLUDE[csprcs](../includes/csprcs-md.md)] criado pelo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] importará Microsoft.CSharp.targets que importa Microsoft.Common.targets. O próprio projeto [!INCLUDE[csprcs](../includes/csprcs-md.md)] definirá os itens e propriedades específicos para esse projeto, mas as regras de build padrão para um projeto [!INCLUDE[csprcs](../includes/csprcs-md.md)] são definidas pelos arquivos .targets importados.  
  
 O valor `$(MSBuildToolsPath)` especifica o caminho desses arquivos .targets comuns. Se o `ToolsVersion` for 4.0, os arquivos estarão no seguinte local: `WindowsInstallationPath\Microsoft.NET\Framework\v4.0.30319\`  
  
> [!NOTE]
>  Para obter informações sobre como criar seus próprios destinos, consulte [Destinos](../msbuild/msbuild-targets.md). Para obter informações sobre como usar o elemento `Import` para inserir um arquivo de projeto em outro arquivo de projeto, consulte [Elemento Import (MSBuild)](../msbuild/import-element-msbuild.md) e [Como usar o mesmo destino em vários arquivos de projeto](../msbuild/how-to-use-the-same-target-in-multiple-project-files.md).  
  
## <a name="common-targets-files"></a>Arquivos .targets comuns  
  
|Arquivo .targets|Descrição|  
|-------------------|-----------------|  
|Microsoft.Common.targets|Define as etapas no processo de build padrão de projetos [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] e [!INCLUDE[csprcs](../includes/csprcs-md.md)].<br /><br /> Importado pelos arquivos Microsoft.CSharp.targets e Microsoft.VisualBasic.targets, quem incluem as seguintes instruções: `<Import Project="Microsoft.Common.targets" />`|  
|Microsoft.CSharp.targets|Define as etapas no processo de build padrão de projetos do Visual C#.<br /><br /> Importado pelos arquivos de projeto do Visual C# (.csproj), que incluem a seguinte instrução: `<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />`|  
|Microsoft.VisualBasic.targets|Define as etapas no processo de build padrão de projetos do Visual Basic.<br /><br /> Importado pelos arquivos de projeto do Visual Basic (.vbproj), que incluem a seguinte instrução: `<Import Project="$(MSBuildToolsPath)\Microsoft.VisualBasic.targets" />`|  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Import (MSBuild)](../msbuild/import-element-msbuild.md)   
 [Referência do MSBuild](../msbuild/msbuild-reference.md)  
 [MSBuild](msbuild.md)


