---
title: Tarefa GetWinFXPath | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c95e5ad882d7021b597d7ba0ad8c38177f4a5136
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56646923"
---
# <a name="getwinfxpath-task"></a>Tarefa GetWinFXPath
A tarefa <xref:Microsoft.Build.Tasks.Windows.GetWinFXPath> retorna o diretório do tempo de execução [!INCLUDE[TLA#tla_winfx](../msbuild/includes/tlasharptla_winfx_md.md)] atual.

## <a name="task-parameters"></a>Parâmetros de tarefa

| Parâmetro | Descrição |
|-------------------| - |
| `WinFXPath` | Parâmetro de saída opcional **String**.<br /><br /> Especifica o caminho real para o tempo de execução de [!INCLUDE[TLA2#tla_winfx](../msbuild/includes/tla2sharptla_winfx_md.md)]. |
| `WinFXNativePath` | Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o caminho para o tempo de execução de [!INCLUDE[TLA2#tla_titlewinfx](../msbuild/includes/tla2sharptla_titlewinfx_md.md)] nativo. |
| `WinFXWowPath` | Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o caminho para os assemblies de [!INCLUDE[TLA#tla_winfx](../msbuild/includes/tlasharptla_winfx_md.md)] no módulo **Windows on Windows** de 32 bits em sistemas de 64 bits. |

## <a name="remarks"></a>Comentários
 Se a tarefa <xref:Microsoft.Build.Tasks.Windows.GetWinFXPath> está em execução em um processador de 64 bits, o parâmetro **WinFXPath** está definido como o caminho armazenado no parâmetro **WinFXWowPath**, caso contrário, o parâmetro **WinFXPath** é definido como o caminho armazenado no parâmetro **WinFXNativePath**.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra como usar a tarefa **GetWinFXPath** para detectar o caminho nativo para o tempo de execução de [!INCLUDE[TLA2#tla_titlewinfx](../msbuild/includes/tla2sharptla_titlewinfx_md.md)].

```xml
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
- [Referência do WPF MSBuild](../msbuild/wpf-msbuild-reference.md)
- [Referência de tarefas](../msbuild/wpf-msbuild-task-reference.md)
- [Referência do MSBuild](../msbuild/msbuild-reference.md)
- [Referência de tarefas](../msbuild/msbuild-task-reference.md)
- [Compilar um aplicativo WPF](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)
