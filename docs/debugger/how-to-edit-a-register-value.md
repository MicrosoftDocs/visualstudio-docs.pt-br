---
title: 'Como: Editar um valor de registro | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.register.edit
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- Registers window, editing register values
- register values
ms.assetid: e27b6bd8-e6d4-4f1d-8a86-9f4047bb1167
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 57ab8c2d173d5a5799d20bf50e0fd26716d163af
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54992744"
---
# <a name="how-to-edit-a-register-value-c-c-visual-basic-f"></a>Como: Editar um valor de registro (C#, C++, Visual Basic, F#)

A janela Registros só ficará disponível se a depuração do nível de endereços estiver habilitada na caixa de diálogo **Opções**, nó **Depuração**.  
  
### <a name="to-change-the-value-of-a-register"></a>Para alterar o valor de um registro  
  
1.  Na janela **Registros**, use a tecla TAB ou o mouse para mover o ponto de inserção para o valor que você deseja alterar. Quando você começa a digitar, o cursor deve estar localizado na frente do valor que você deseja substituir.  
  
2.  Digite o novo valor.  
  
    > [!CAUTION]
    >  Alterar valores do registro (principalmente nos registros de EIP e EBP) pode afetar a execução do programa.  
  
    > [!CAUTION]
    >  Editar valores de ponto flutuante pode resultar em imprecisões secundárias devido à conversão decimal-binária de componentes fracionários. Mesmo uma edição aparentemente inócua pode resultar em alterações em alguns bits menos significativos no registro de um ponto flutuante.  
  
## <a name="see-also"></a>Consulte também  
 [Como: Usar a janela Registros](../debugger/how-to-use-the-registers-window.md)