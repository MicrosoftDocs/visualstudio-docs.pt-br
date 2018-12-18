---
title: 'Como: examinar o código do sistema após uma exceção | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging, exceptions
- exceptions, debugging
ms.assetid: a38ad49b-7cf3-483d-91c4-eb3116eba50c
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8cbaff38cdd6d769140f135d319a88d6098f294b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51729046"
---
# <a name="how-to-examine-system-code-after-an-exception"></a>Como examinar um código de sistema após uma exceção
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando uma exceção ocorre, você poderá precisar examinar o código dentro de uma chamada do sistema para determinar a causa da exceção. O procedimento a seguir explica como fazer isso se você não tiver os símbolos carregados para o código do sistema ou se Just My Code estiver habilitado.  
  
### <a name="to-examine-system-code-following-an-exception"></a>Para examinar o código do sistema após uma exceção  
  
1.  No **pilha de chamadas** janela, o botão direito do mouse, em seguida, clique em **Mostrar código externo**.  
  
     Se Just My Code não estiver habilitado, essa opção não estará disponível no menu de atalho e o código do sistema será mostrado por padrão.  
  
2.  Os quadros de código externo que agora são exibidos no botão direito do mouse a **pilha de chamadas** janela.  
  
3.  Aponte para **carregar símbolos de** e, em seguida, clique em **servidores de símbolo Microsoft**.  
  
    1.  Se Just My Code tiver sido habilitado, uma caixa de diálogo será exibida. Indica que Just My Code agora foi desabilitado. Isso é necessário para entrar em chamadas do sistema.  
  
    2.  O **Baixando símbolos públicos** caixa de diálogo é exibida. Ela desaparecerá quando o download for concluído.  
  
4.  Agora você pode examinar o código do sistema na **pilha de chamadas** janela e outras janelas. Por exemplo, você pode clique duas vezes em um quadro de pilha de chamadas para exibir o código em uma fonte ou **desmontagem** janela.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando exceções com o depurador](../debugger/managing-exceptions-with-the-debugger.md)





