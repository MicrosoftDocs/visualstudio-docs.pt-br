---
title: Comando de caminho de símbolo | Microsoft Docs
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
- debug.symbolpath
helpviewer_keywords:
- symbol path command
- Debug.SymbolPath command
- SymbolPath command
ms.assetid: b697ef2d-3f5d-40df-b113-7068a5bec0d4
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 343b45f4a8aef0fdeef5aef7653a5dbb1c7c5582
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49189157"
---
# <a name="symbol-path-command"></a>Comando demarcador do Símbolo
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Define a lista de diretórios para o depurador pesquisar símbolos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Debug.SymbolPath pathname1;pathname2;... pathnameN  
```  
  
## <a name="arguments"></a>Arguments  
 `pathname`  
 Opcional. Uma lista de caminhos delimitada por ponto-e-vírgula para que o depurador pesquise símbolos.  
  
## <a name="remarks"></a>Comentários  
 Se nenhum `pathname` for especificado, o comando listará os caminhos de símbolo atual.  
  
## <a name="example"></a>Exemplo  
 Este exemplo adiciona dois caminhos à lista de diretórios de símbolo.  
  
```  
Debug.SymbolPath C:\Symbol Path 1;C:\Symbol Path 2  
```  
  
## <a name="example"></a>Exemplo  
 Este exemplo exibe uma lista delimitada por ponto-e-vírgula dos caminhos de símbolo atuais.  
  
```  
Debug.SymbolPath  
```  
  
## <a name="see-also"></a>Consulte também  
 [Janela Comando](../../ide/reference/command-window.md)   
 [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)



