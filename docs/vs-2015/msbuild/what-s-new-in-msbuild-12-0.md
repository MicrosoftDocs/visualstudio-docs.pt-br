---
title: Novidades do MSBuild 12.0 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9976a6ad-c052-4017-b848-35b5ae4a2f66
caps.latest.revision: 26
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3f10fa5496795947c041482d5ae5dc7b6112da67
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49247384"
---
# <a name="what39s-new-in-msbuild-120"></a>Novidades do MSBuild 12.0
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O MSBuild agora é instalado como parte do Visual Studio e não como parte do .NET Framework. O número de versão atual do MSBuild é 12.0. Se desejar instalar o MSBuild separadamente, baixe o pacote de instalação em [MSBuild Download](http://go.microsoft.com/fwlink/?LinkId=309745) (Download do MSBuild).  
  
## <a name="changed-path"></a>Caminho alterado  
 O MSBuild agora é instalado diretamente em *%ProgramFiles%*, por exemplo, em C:\Arquivos de Programas\MSBuild\\.  
  
## <a name="changed-properties"></a>Propriedades alteradas  
 As seguintes propriedades do MSBuild foram alteradas no novo número de versão:  
  
-   A `MSBuildToolsVersion` desta versão das ferramentas é 12.0.  
  
-   O `MSBuildToolsPath` agora é %ProgramFiles%\MSBuild\12.0\bin nos sistemas operacionais de 32 bits ou %ProgramFiles%\MSBuild\12.0\bin\amd64 nos sistemas operacionais de 64 bits.  
  
-   Os valores de `ToolsVersion` podem ser encontrados em HKLM\SOFTWARE\Microsoft\MSBuild\ToolsVersions\12.0 para os sistemas operacionais de 32 bits ou HKLM\SOFTWARE\Wow6432Node\Microsoft\MSBuild\ToolsVersions\12.0 para os sistemas operacionais de 64 bits.  
  
-   As propriedades `SDK35ToolsPath` e `SDK40ToolsPath` apontam para o SDK do .NET Framework que é fornecido no pacote desta versão do Visual Studio (por exemplo, 8.1A para as ferramentas 4.X).  
  
## <a name="new-properties"></a>Novas propriedades  
  
-   `MSBuildFrameworkToolsPath` é uma nova propriedade que tem um valor de %windir%\Microsoft.NET\Framework\v4.0.30319 nos sistemas operacionais de 32 bits ou %windir%\Microsoft.NET\Framework64\v4.0.30319 nos sistemas operacionais de 64 bits. Trata-se de uma substituição de `MSBuildToolsPath` que pode ser usada para apontar para as ferramentas e utilitários do .NET Framework.  
  
-   `MSBuildToolsPath` e `MSBuildFrameworkToolsPath` têm equivalentes de 32 bits – `MSBuildToolsPath32` e `MSBuildFrameworkToolsPath32`– que sempre apontam para o local de 32 bits, independentemente se está sendo usado o MSBuild de 32 bits ou o de 64 bits.

## <a name="see-also"></a>Consulte também
[MSBuild](msbuild.md)


