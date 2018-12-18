---
title: Comando Ir para | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- edit.goto
helpviewer_keywords:
- Debug.Goto command
- Go To command
ms.assetid: 201e1dd2-6701-467d-8cc1-faec2ef20511
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: d23f7b9961f8386fb023fa747a647c14c9cd5db1
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49303466"
---
# <a name="go-to-command"></a>Comando Ir para
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Move o cursor para a linha especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Edit.GoTo [linenumber]  
```  
  
## <a name="arguments"></a>Arguments  
 `linenumber`  
 Opcional. Um inteiro que representa o número da linha para a qual ir.  
  
## <a name="remarks"></a>Comentários  
 A numeração de linha começa em um. Se o valor de `linenumber` for menor que um, a primeira linha será exibida. Se o valor de `linenumber` for maior que o número da última linha, a última linha será exibida.  
  
 Se um valor para `linenumber` não for especificado, a caixa de diálogo **Ir para a Linha** será exibida.  
  
 O alias para esse comando é GoToLn.  
  
## <a name="example"></a>Exemplo  
  
```  
>Edit.GoTo 125  
```  
  
## <a name="see-also"></a>Consulte também  
 [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)   
 [Janela Comando](../../ide/reference/command-window.md)   
 [Caixa Localizar/Comando](../../ide/find-command-box.md)   
 [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)



