---
title: Quando o ponto de interrupção é a caixa de diálogo ocorrências | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.whenbreakpointishit
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
ms.assetid: 476e3d98-cf35-4338-b124-cd0f3010d854
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2d2d0940764e64f9179eb8346c271afa6136b72f
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31475032"
---
# <a name="when-breakpoint-is-hit-dialog-box"></a>Caixa de diálogo Ponto de Interrupção Quando Visitado
Com essa caixa de diálogo, você pode personalizar a ação que ocorre quando um ponto de interrupção é atingido.  
  
## <a name="uielement-list"></a>Lista UIElement  
 **Imprimir uma mensagem**  
 Imprime uma mensagem, usando a sintaxe do DebuggerDisplay. Para obter mais informações, consulte [usando o atributo DebuggerDisplay](../debugger/using-the-debuggerdisplay-attribute.md).  
  
 Essa caixa de texto também oferece suporte à palavras-chave especiais (como $ADDRESS) que podem ser usadas por si mesmas ou nas chaves de uma expressão do DebuggerDisplay. As palavras-chave disponíveis são listadas na caixa de diálogo.  
  
 **Continuar em execução**  
 Esse controle é habilitado apenas quando **imprimir uma mensagem** está selecionado. Com esse controle selecionado, você pode usar um ponto de interrupção como um tracepoint para rastrear a execução do programa, em vez de interrompê-lo quando o local for atingido.  
  
## <a name="see-also"></a>Consulte também  
 [Usando pontos de interrupção](../debugger/using-breakpoints.md)   
 [Usando o atributo DebuggerDisplay](../debugger/using-the-debuggerdisplay-attribute.md)