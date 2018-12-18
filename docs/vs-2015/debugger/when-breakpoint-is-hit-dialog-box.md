---
title: Quando o ponto de interrupção é a caixa de diálogo ocorrências | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.whenbreakpointishit
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- SQL
- VB
- CSharp
- C++
ms.assetid: 476e3d98-cf35-4338-b124-cd0f3010d854
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ad979fa302a29f9d444579655e368db6da8b3e1f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51805405"
---
# <a name="when-breakpoint-is-hit-dialog-box"></a>Caixa de diálogo Ponto de Interrupção Quando Visitado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Com essa caixa de diálogo, você pode personalizar a ação que ocorre quando um ponto de interrupção é atingido.  
  
## <a name="uielement-list"></a>Lista UIElement  
 **Imprimir uma mensagem**  
 Imprime uma mensagem, usando a sintaxe do DebuggerDisplay. Para obter mais informações, consulte [usando o atributo DebuggerDisplay](../debugger/using-the-debuggerdisplay-attribute.md).  
  
 Essa caixa de texto também oferece suporte à palavras-chave especiais (como $ADDRESS) que podem ser usadas por si mesmas ou nas chaves de uma expressão do DebuggerDisplay. As palavras-chave disponíveis são listadas na caixa de diálogo.  
  
 **Continuar execução**  
 Esse controle será habilitado somente quando **imprimir uma mensagem** está selecionado. Com esse controle selecionado, você pode usar um ponto de interrupção como um tracepoint para rastrear a execução do programa, em vez de interrompê-lo quando o local for atingido.  
  
## <a name="see-also"></a>Consulte também  
 [Usando pontos de interrupção](../debugger/using-breakpoints.md)   
 [Usando o atributo DebuggerDisplay](../debugger/using-the-debuggerdisplay-attribute.md)



