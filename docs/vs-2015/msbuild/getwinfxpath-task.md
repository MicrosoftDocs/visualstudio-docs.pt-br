---
title: Tarefa GetWinFXPath | Microsoft Docs
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
- getting the directory of the current .NET Framework runtime [WPF MSBuild]
- GetWinFXPath task [WPF MSBuild], parameters
- GetWinFXPath task [WPF MSBuild]
- obtaining the path to the current .NET Framework runtime [WPF MSBuild]
ms.assetid: b1dfb467-f3d3-47f3-83ef-af7b0e33a772
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ca9f7240e8f1f521d3eac9c3915f9a78e142bc1f
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49251999"
---
# <a name="getwinfxpath-task"></a>Tarefa GetWinFXPath
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
A tarefa <xref:Microsoft.Build.Tasks.Windows.GetWinFXPath> retorna o diretório do tempo de execução [!INCLUDE[TLA#tla_winfx](../includes/tlasharptla-winfx-md.md)] atual.  
  
## <a name="task-parameters"></a>Parâmetros da tarefa  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`WinFXPath`|Parâmetro de saída opcional **String**.<br /><br /> Especifica o caminho real para o tempo de execução de [!INCLUDE[TLA2#tla_winfx](../includes/tla2sharptla-winfx-md.md)].|  
|`WinFXNativePath`|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o caminho para o tempo de execução de [!INCLUDE[TLA2#tla_titlewinfx](../includes/tla2sharptla-titlewinfx-md.md)] nativo.|  
|`WinFXWowPath`|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o caminho para os assemblies de [!INCLUDE[TLA#tla_winfx](../includes/tlasharptla-winfx-md.md)] no módulo **Windows on Windows** de 32 bits em sistemas de 64 bits.|  
  
## <a name="remarks"></a>Comentários  
 Se a tarefa <xref:Microsoft.Build.Tasks.Windows.GetWinFXPath> está em execução em um processador de 64 bits, o parâmetro **WinFXPath** está definido como o caminho armazenado no parâmetro **WinFXWowPath**, caso contrário, o parâmetro **WinFXPath** é definido como o caminho armazenado no parâmetro **WinFXNativePath**.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar a tarefa **GetWinFXPath** para detectar o caminho nativo para o tempo de execução de [!INCLUDE[TLA2#tla_titlewinfx](../includes/tla2sharptla-titlewinfx-md.md)].  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <UsingTask   
    TaskName="Microsoft.Build.Tasks.Windows.GetWinFXPath"   
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />  
  <Target Name="GetWinFXPathTask">  
    <GetWinFXPath  
      WinFXNativePath="c:\WinFXNative"   
      WinFXWowPath="c:\WinFXWowNative" />  
  </Target>  
  <Import Project="$(MSBuildBinPath)\Microsoft.WinFX.targets" />  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência MSBuild do WPF](../msbuild/wpf-msbuild-reference.md)   
 [Referência de tarefas](../msbuild/wpf-msbuild-task-reference.md)   
 [Referência do MSBuild](../msbuild/msbuild-reference.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Como compilar um aplicativo WPF (WPF)](http://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c)



