---
title: 'Depurando F # | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Debugging [F#]
- F#, debugging
ms.assetid: 20bcd51c-2d06-4281-9a1e-ef2b91d1a779
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2b3bb2a9379dd6cd43bb0398ccda2b031b96d56e
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31473784"
---
# <a name="debugging-f"></a>Depurando F#
A depuração de F# é semelhante à depuração de qualquer linguagem gerenciada, com algumas exceções:  
  
-   O **Autos** janela não exibe variáveis de F #.  
  
-   Não há suporte para Editar e Continuar em F#. As edições ao código F# durante uma sessão de depuração são possíveis, mas devem ser evitadas. Como as alterações de código não são aplicadas durante a sessão de depuração, a edição do código F# durante a depuração causará uma incompatibilidade entre o código-fonte e o código que está sendo depurado.  
  
-   O depurador não reconhece expressões de F#. Para inserir uma expressão em uma janela ou uma caixa de diálogo do depurador durante a depuração de F#, você deve traduzir a expressão para a sintaxe do C#. Quando você traduzir uma expressão F# em C#, lembre-se de que o C# usa == como o operador de comparação para igualdade, enquanto o F# usa o = simples.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando código gerenciado](../debugger/debugging-managed-code.md)
