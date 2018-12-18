---
title: Utilitário CreatePkgDef | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- package definition
- create pkgdef
- pkgdef
- createpkgdef
ms.assetid: c745cb76-47a6-49ff-9eed-16af0f748e35
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 492e34c92019de7f3c0921b853d103252e09b996
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51782642"
---
# <a name="createpkgdef-utility"></a>Utilitário CreatePkgDef
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Usa um arquivo. dll para uma extensão do Visual Studio como um parâmetro e cria um arquivo. pkgdef para acompanhar o arquivo. dll. O arquivo. pkgdef contém todas as informações que, caso contrário, seriam gravadas no registro do sistema quando a extensão está instalada.  
  
> [!NOTE]
>  A maioria dos modelos de projeto que estão incluídos no SDK do Visual Studio automaticamente cria arquivos. pkgdef como parte do processo de compilação. Este documento destina-se para aqueles que desejam criar pacotes manualmente ou converter pacotes existentes para usar a implantação. pkgdef.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CreatePkgDef /out=FileName [/codebase] [/assembly] AssemblyPath  
```  
  
## <a name="arguments"></a>Arguments  
 / out =`FileName`  
 Necessário. Define o nome do arquivo de saída. pkgdef para`FileName`.  
  
 /codebase  
 Opcional. Registro de forças com o utilitário de base de código.  
  
 /assembly  
 Registro de forças com o utilitário de Assembly.  
  
 `AssemblyPath`  
 O caminho do arquivo. dll do qual você deseja gerar o. pkgdef.  
  
## <a name="remarks"></a>Comentários  
 Implantação de extensão por meio de arquivos. pkgdef substituirá os requisitos de registro de versões anteriores do Visual Studio.  
  
 Os arquivos. pkgdef devem ser instalados em um dos seguintes locais: %localappdata%\Microsoft\Visual Studio\14.0\Extensions\ ou %vsinstalldir%\Common7\IDE\Extensions\\. Se a pasta de instalação é %localappdata%\Microsoft\Visual Studio\14.0\Extensions\\, a extensão será reconhecida pelo Visual Studio, mas será desabilitada por padrão. O usuário pode habilitar a extensão usando **extensões e atualizações**. Se a pasta de instalação é %vsinstalldir%\Common7\IDE\Extensions\\, a extensão está habilitada por padrão.  
  
> [!NOTE]
>  O **extensões e atualizações** ferramenta não pode ser usada para acessar uma extensão, a menos que ele é instalado como parte de um pacote VSIX.  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário CreateExpInstance](../../extensibility/internals/createexpinstance-utility.md)

