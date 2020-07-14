---
title: Não é possível atribuir a ' this ' | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5000
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: ba2b0a2b-f0f8-4698-b335-a4ab6c166671
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f5c52153da64ff477d89b09d4af17169da18e4e1
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817314"
---
# <a name="cannot-assign-to-this"></a>Não é possível designar a "isso"
Você tentou atribuir um valor a **isso**. **essa** é uma [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] palavra-chave que se refere a:

- o objeto atualmente executando um método,

- o objeto global se não houver nenhum método atual (ou o método não pertencer a nenhum outro objeto).

Um método é uma [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] função que é invocada por meio de um objeto. Dentro de um método, a palavra-chave **this** é uma referência ao objeto para o qual o método foi invocado (que, por acaso, é o objeto criado invocando o construtor de classe com o **novo** operador).

Dentro de um método, você pode usar **isso** para fazer referência ao objeto atual, mas não pode atribuir um novo valor a **isso**.

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Não tente atribuir a **isso**. Para acessar uma propriedade ou um método de um objeto instanciado, use o operador ponto (por exemplo, **Circle. RADIUS**).

  > [!NOTE]
  > Você não pode nomear **uma variável criada**pelo usuário; é uma [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] palavra reservada.

## <a name="see-also"></a>Veja também

- [Esta instrução](../../javascript/reference/this-statement-javascript.md)
- [Solucionar problemas com scripts](../../javascript/advanced/troubleshooting-your-scripts-javascript.md)