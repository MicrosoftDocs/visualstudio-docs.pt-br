---
title: Métodos e classes assert de MSTest
ms.date: 06/07/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: reference
helpviewer_keywords:
- Assert classes
- Assert methods
- unit tests, Assert classes
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 91198e9b7048b384bf2095840abbd012042025ed
ms.sourcegitcommit: ce154aee5b403d5c1c41da42302b896ad3cf8d82
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34844248"
---
# <a name="use-assert-classes-for-unit-testing"></a>Use as classes Assert para teste de unidade

Use as classes Assert do namespace <xref:Microsoft.VisualStudio.TestTools.UnitTesting> para verificar uma funcionalidade específica. Um método de teste de unidade executa o código de um método no código do aplicativo, mas relata a exatidão do comportamento do código somente quando você inclui instruções Assert.

## <a name="kinds-of-asserts"></a>Tipos de asserts

O namespace <xref:Microsoft.VisualStudio.TestTools.UnitTesting> fornece vários tipos de classes Assert.

No método de teste, é possível chamar qualquer método da classe <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert?displayProperty=fullName>, como <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A?displayProperty=nameWithType>. A classe <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> tem vários métodos disponíveis e muitos deles têm várias sobrecargas.

### <a name="compare-strings-and-collections"></a>Comparar cadeias de caracteres e coleções

Use a classe <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CollectionAssert> para comparar coleções de objetos ou verificar o estado de uma ou mais coleções.

Use a classe <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert> para comparar e examinar cadeias de caracteres. Essa classe contém uma variedade de métodos úteis, como <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert.Contains%2A?displayProperty=nameWithType>, <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert.Matches%2A?displayProperty=nameWithType> e <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert.StartsWith%2A?displayProperty=nameWithType>.

### <a name="exceptions"></a>Exceções

A exceção <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssertFailedException> é gerada sempre que um teste falha. Um teste falha quando seu tempo limite é atingido, quando gera uma exceção inesperada ou quando contém uma instrução assert que produz um resultado **Com falha**.

A <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssertInconclusiveException> é gerada sempre que um teste produz um resultado **Inconclusivo**. Normalmente, você adiciona uma instrução <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.Inconclusive%2A?displayProperty=nameWithType> a um teste no qual ainda está trabalhando, para indicar que ele ainda não está pronto para ser executado.

> [!NOTE]
> Uma estratégia alternativa é marcar um teste que não está pronto para ser executado com o atributo <xref:Microsoft.VisualStudio.TestTools.UnitTesting.IgnoreAttribute>. No entanto, a desvantagem é que não é fácil gerar um relatório sobre o número de testes que ainda não foram implementados.

Se você gravar uma nova classe de exceção assert, herde da classe base <xref:Microsoft.VisualStudio.TestTools.UnitTesting.UnitTestAssertException> para facilitar a identificação da exceção como uma falha de asserção em vez de uma exceção inesperada gerada pelo código de teste ou de produção.

Decore um método de teste com o atributo <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ExpectedExceptionAttribute> quando desejar que o método de teste verifique se uma exceção que você espera que seja gerada por um método no código do aplicativo, realmente é gerada.

## <a name="see-also"></a>Consulte também

- [Efetuar teste de unidade em seu código](../test/unit-test-your-code.md)