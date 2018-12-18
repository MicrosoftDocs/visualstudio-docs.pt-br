---
title: 'Como: editar um valor de registro | Microsoft Docs'
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
- vs.debug.register.edit
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- Registers window, editing register values
- register values
ms.assetid: e27b6bd8-e6d4-4f1d-8a86-9f4047bb1167
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c41b54ea075415dac7114413f9cdc15cc6a07a12
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51764754"
---
# <a name="how-to-edit-a-register-value"></a>Como editar um valor de registro
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

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





