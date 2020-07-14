---
title: Continuando a execução após uma exceção | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- managed exceptions, continuing execution after
- exceptions, continuing execution after
- debugger, exceptions
- managed code, exception handling
- exception handling, continuing execution after
- execution, continuing after an exception
- program execution
- threading [Visual Studio], continuing execution after exceptions
- Exceptions dialog box
- programs, executing
ms.assetid: 6fe97aac-2131-4615-bd92-d3afee741558
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2e94867d845988b787247c32d32afd35af946972
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350674"
---
# <a name="continuing-execution-after-an-exception"></a>Continuando a execução depois de uma exceção
Quando o depurador interromper a execução devido a uma exceção, você verá o **auxiliar de exceção**, por padrão. Se você tiver desabilitado **o auxiliar de exceção** na caixa de diálogo **Opções** , verá o **Assistente de exceção** (C# ou Visual Basic) ou a caixa de diálogo de **exceção** (C++).

 Quando o **auxiliar de exceção** for exibido, você poderá tentar corrigir o problema que causou a exceção.

## <a name="managed-and-native-code"></a>Código gerenciado e nativo
 Em código gerenciado e nativo, você pode continuar a execução no mesmo thread após uma exceção sem tratamento. O **auxiliar de exceção** desenrola a pilha de chamadas até o ponto em que a exceção foi gerada.

## <a name="mixed-code"></a>Código misto
 Se você atinge uma exceção não tratada ao depurar um código nativo misto e gerenciado, as restrições do sistema operacional impedem o desenrolar da pilha de chamadas. Se você tentar voltar a pilha de chamadas usando o menu de atalho, uma mensagem de erro explicará que o depurador não pode desenrolar de uma exceção não tratada exceto durante a depuração de código misto.

## <a name="see-also"></a>Veja também

- [Gerenciando exceções com o depurador](../debugger/managing-exceptions-with-the-debugger.md)