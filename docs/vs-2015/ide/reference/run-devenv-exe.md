---
title: -Run (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- /run Devenv
- run Devenv switch
- applications [Visual Studio], running
- /r Devenv switch
- Devenv, /run switch
- r Devenv switch (/r)
ms.assetid: b1f22f9d-39a5-4918-8a2a-4b5c1e872665
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 8f941aaff6b4f5f97a298549e91c29ffb19e84ea
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59667511"
---
# <a name="run-devenvexe"></a>/Run (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Compila e executa o projeto ou a solução especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
devenv {/run|/r} {SolutionName|ProjectName}  
```  
  
## <a name="arguments"></a>Arguments  
 `SolutionName`  
 Necessário. O caminho completo e o nome de um arquivo de solução.  
  
 `ProjectName`  
 Necessário. O caminho completo e o nome de um arquivo de projeto.  
  
## <a name="remarks"></a>Comentários  
 Compila e executa o projeto ou a solução especificada de acordo com as configurações especificadas para a configuração da solução ativa. Essa opção inicia o IDE (ambiente de desenvolvimento integrado) e o deixa ativo após o projeto ou a solução tiver concluído sua execução.  
  
-   Coloque as cadeias de caracteres que incluem espaços entre aspas duplas.  
  
-   As informações de resumo, incluindo erros, podem ser exibidas na janela **Comando** ou em qualquer arquivo de log especificado com a opção `/out`.  
  
## <a name="example"></a>Exemplo  
 Este exemplo executa a solução `MySolution` usando a configuração de implantação ativa.  
  
```  
devenv /run "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Opções de linha de comando devenv](../../ide/reference/devenv-command-line-switches.md)   
 [/Runexit (devenv.exe)](../../ide/reference/runexit-devenv-exe.md)   
 [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)   
 [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)   
 [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
