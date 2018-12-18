---
title: 'Como: editar um valor de registro | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0d0337f7c77d1ed601c7a6c13c702f4758cbfdbd
ms.sourcegitcommit: a7de99f36e9ead7ea9e9bac23c88d05ddfc38b00
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52257064"
---
# <a name="how-to-edit-a-register-value-c-c-visual-basic-f"></a>Como: editar um valor de registro (C#, C++, Visual Basic, F#)

A janela registros estará disponível somente se a depuração do nível de endereços estiver habilitada na **opções** caixa de diálogo **depuração** nó.  
  
### <a name="to-change-the-value-of-a-register"></a>Para alterar o valor de um registro  
  
1.  No **registra** janela, use a tecla TAB ou o mouse para mover a inserção de ponto para o valor que você deseja alterar. Quando você começa a digitar, o cursor deve estar localizado na frente do valor que você deseja substituir.  
  
2.  Digite o novo valor.  
  
    > [!CAUTION]
    >  Alterar valores do registro (principalmente nos registros de EIP e EBP) pode afetar a execução do programa.  
  
    > [!CAUTION]
    >  Editar valores de ponto flutuante pode resultar em imprecisões secundárias devido à conversão decimal-binária de componentes fracionários. Mesmo uma edição aparentemente inócua pode resultar em alterações em alguns bits menos significativos no registro de um ponto flutuante.  
  
## <a name="see-also"></a>Consulte também  
 [Como usar a janela Registros](../debugger/how-to-use-the-registers-window.md)