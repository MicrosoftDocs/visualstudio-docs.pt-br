---
title: 'CA1806: não ignore resultados do método'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1806
- DoNotIgnoreMethodResults
helpviewer_keywords:
- CA1806
- DoNotIgnoreMethodResults
ms.assetid: fd805687-0817-481e-804e-b62cfb3b1076
author: gewarren
ms.author: gewarren
dev_langs:
- CPP
- CSharp
- VB
manager: douge
ms.openlocfilehash: ebbad9eb48a448aa756f580ade794ba70eb25611
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45546831"
---
# <a name="ca1806-do-not-ignore-method-results"></a>CA1806: não ignore resultados do método

|||
|-|-|
|NomeDoTipo|DoNotIgnoreMethodResults|
|CheckId|CA1806|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa

Há várias razões possíveis para esse aviso:

- Um novo objeto é criado, mas nunca usado.

- Um método que cria e retorna uma nova cadeia de caracteres é chamado e a nova cadeia de caracteres nunca é usada.

- Um método COM ou P/Invoke que retorna um código de erro ou HRESULT que nunca é usado. Descrição da Regra

Criação do objeto desnecessário e a coleta de lixo associado do objeto não utilizado degradar o desempenho.

Cadeias de caracteres são imutáveis e métodos, como string. ToUpper retorna uma nova instância de uma cadeia de caracteres em vez de modificar a instância da cadeia de caracteres no método de chamada.

Ignorar o código de erro ou HRESULT pode levar a um comportamento inesperado em condições de erro ou a condições de poucos recursos.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Se o método um cria uma nova instância do objeto B que nunca é usado, passe a instância como um argumento para outro método ou atribua a instância a uma variável. Se a criação do objeto é desnecessária, remova o proprietário.- ou -

 Se o método um chama o método B, mas não usa a nova instância de cadeia de caracteres que o método B retorna. Passe a instância como um argumento para outro método, atribua a instância a uma variável. Ou remova a chamada se ela for desnecessária.

 -ou-

 Se o método um chama o método B, mas não usa o HRESULT ou código de erro que o método retorna. Use o resultado em uma instrução condicional, atribua o resultado a uma variável ou passá-lo como um argumento para outro método.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra, a menos que o ato de criar o objeto tem alguma finalidade.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma classe que ignora o resultado da chamada String. trim.

 [!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults3#1](../code-quality/codesnippet/CSharp/ca1806-do-not-ignore-method-results_1.cs)]
 [!code-vb[FxCop.Usage.DoNotIgnoreMethodResults3#1](../code-quality/codesnippet/VisualBasic/ca1806-do-not-ignore-method-results_1.vb)]
 [!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults3#1](../code-quality/codesnippet/CPP/ca1806-do-not-ignore-method-results_1.cpp)]

## <a name="example"></a>Exemplo
 O exemplo a seguir corrige a violação anterior atribuindo o resultado de String. Trim novamente para a variável que foi chamado.

 [!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults4#1](../code-quality/codesnippet/CSharp/ca1806-do-not-ignore-method-results_2.cs)]
 [!code-vb[FxCop.Usage.DoNotIgnoreMethodResults4#1](../code-quality/codesnippet/VisualBasic/ca1806-do-not-ignore-method-results_2.vb)]
 [!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults4#1](../code-quality/codesnippet/CPP/ca1806-do-not-ignore-method-results_2.cpp)]

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que não usa um objeto que ele cria.

> [!NOTE]
> Essa violação não pode ser reproduzida no Visual Basic.

 [!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults5#1](../code-quality/codesnippet/CPP/ca1806-do-not-ignore-method-results_3.cpp)]
 [!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults5#1](../code-quality/codesnippet/CSharp/ca1806-do-not-ignore-method-results_3.cs)]

## <a name="example"></a>Exemplo
 O exemplo a seguir corrige a violação anterior, removendo a criação desnecessária de um objeto.

 [!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults6#1](../code-quality/codesnippet/CSharp/ca1806-do-not-ignore-method-results_4.cs)]
 [!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults6#1](../code-quality/codesnippet/CPP/ca1806-do-not-ignore-method-results_4.cpp)]

<!-- Examples don't exist for the below... -->
<!--
## Example
 The following example shows a method that ignores the error code that the native method GetShortPathName returns.

## Example
 The following example fixes the previous violation by checking the error code and throwing an exception when the call fails.
-->