---
title: Examinar o código do sistema após uma exceção | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging, exceptions
- exceptions, debugging
ms.assetid: a38ad49b-7cf3-483d-91c4-eb3116eba50c
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f2e3de04d07ffe1bf2853113cb003a273fa9e5a7
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53050986"
---
# <a name="how-to-examine-system-code-after-an-exception"></a>Como: Examinar o código do sistema após uma exceção
Quando uma exceção ocorre, você poderá precisar examinar o código dentro de uma chamada do sistema para determinar a causa da exceção. O procedimento a seguir explica como fazer isso se você não tiver os símbolos carregados para o código do sistema ou se Just My Code estiver habilitado.  
  
### <a name="to-examine-system-code-following-an-exception"></a>Para examinar o código do sistema após uma exceção  
  
1.  Na janela **Pilha de Chamadas**, clique com o botão direito do mouse, em seguida, clique em **Mostrar Código Externo**.  
  
     Se Just My Code não estiver habilitado, essa opção não estará disponível no menu de atalho e o código do sistema será mostrado por padrão.  
  
2.  Clique com o botão direito do mouse nos quadros de código externos que agora são exibidos na janela **Pilha de Chamadas**.  
  
3.  Aponte para **Carregar Símbolos de** e, em seguida, clique em **Servidores de Símbolo da Microsoft**.  
  
    1.  Se Just My Code tiver sido habilitado, uma caixa de diálogo será exibida. Indica que Just My Code agora foi desabilitado. Isso é necessário para entrar em chamadas do sistema.  
  
    2.  A caixa de diálogo **Baixando símbolos públicos** é exibida. Ela desaparecerá quando o download for concluído.  
  
4.  Agora você pode examinar o código do sistema na janela **Pilha de Chamadas** e em outras janelas. Por exemplo, você pode clicar duas vezes em um registro de ativação de chamadas para exibir o código em uma fonte ou na janela **Desmontagem**.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando exceções com o depurador](../debugger/managing-exceptions-with-the-debugger.md)