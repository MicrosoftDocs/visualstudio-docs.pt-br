---
title: -Deploy (devenv.exe) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Devenv, /deploy switch
- deploy Devenv switch
- deploying applications [Visual Studio], after build
- /deploy Devenv switch
ms.assetid: e47c8723-df08-4645-aa2d-0c956e7ccca2
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: f3883cac01795f4dc5a1e3b0a3d9b58adc176c06
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49172179"
---
# <a name="deploy-devenvexe"></a>/Deploy (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Implanta uma solução após um build ou recompilação. Aplica-se somente a projetos de código gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
devenv SolutionName /deploy SolnConfigName [/project ProjName] [/projectconfig ProjConfigName] [/out LogFileName]  
```  
  
## <a name="arguments"></a>Arguments  
 `SolnConfigName`  
 Necessário. O nome da configuração de solução que será usada para compilar a solução nomeada no `SolutionName`.  
  
 `SolutionName`  
 Necessário. O caminho completo e o nome do arquivo de solução.  
  
 /project `ProjName`  
 Opcional. O caminho e o nome de um arquivo de projeto na solução. É possível inserir um caminho relativo da pasta `SolutionName` para o arquivo de projeto ou o nome de exibição do projeto ou o caminho completo e o nome do arquivo de projeto.  
  
 /projectconfig `ProjConfigName`  
 Opcional. O nome de uma configuração de build de projeto a ser usada ao compilar o `/project` nomeado.  
  
## <a name="remarks"></a>Comentários  
 O projeto especificado deve ser um projeto de implantação. Se o projeto especificado não for um projeto de implantação, quando o projeto que tiver sido compilado for passado para ser implantado, ele falhará com um erro.  
  
 Coloque as cadeias de caracteres que incluem espaços entre aspas duplas.  
  
 As informações de resumo para builds, incluindo erros, podem ser exibidas na janela **Comando** ou em qualquer arquivo de log especificado com a opção `/out`.  
  
## <a name="example"></a>Exemplo  
 Este exemplo implanta o projeto `CSharpConsoleApp`, usando a configuração de build de projeto `Release` dentro da configuração da solução `Release` de `MySolution`.  
  
```  
devenv "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln" /deploy Release /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Release   
```  
  
## <a name="see-also"></a>Consulte também  
 [Opções de linha de comando devenv](../../ide/reference/devenv-command-line-switches.md)   
 [/Project (devenv.exe)](../../ide/reference/project-devenv-exe.md)   
 [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)   
 [/Clean (devenv.exe)](../../ide/reference/clean-devenv-exe.md)   
 [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)   
 [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)



