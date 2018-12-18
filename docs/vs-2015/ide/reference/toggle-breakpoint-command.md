---
title: Comando Ativar/desativar ponto de interrupção | Microsoft Docs
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
- debug.togglebreakpoint
helpviewer_keywords:
- ToggleBreakpoint command
- Debug.ToggleBreakPoint command
- Toggle Breakpoint command
ms.assetid: d50dfadb-ce79-4d5e-9c09-1cfddd57876d
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: f993d9a0377531b155301bed235c00bf8e6667c4
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49223152"
---
# <a name="toggle-breakpoint-command"></a>Comando Ativar/Desativar Ponto de Interrupção
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Ativa ou desativa o ponto de interrupção dependendo de seu estado atual, no local atual do arquivo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Debug.ToggleBreakpoint [text]  
```  
  
## <a name="arguments"></a>Arguments  
 `text`  
 Opcional. Se o texto for especificado, a linha será marcada como um ponto de interrupção nomeado. Caso contrário, a linha será marcada como um ponto de interrupção sem nome, semelhante ao que acontece quando você pressiona F9.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ativa/desativa o ponto de interrupção atual.  
  
```  
>Debug.ToggleBreakpoint  
```  
  
## <a name="see-also"></a>Consulte também  
 [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)   
 [Janela Comando](../../ide/reference/command-window.md)   
 [Caixa Localizar/Comando](../../ide/find-command-box.md)   
 [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)



