---
title: 'CA1806: não ignorar os resultados do método | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1806
- DoNotIgnoreMethodResults
helpviewer_keywords:
- CA1806
- DoNotIgnoreMethodResults
ms.assetid: fd805687-0817-481e-804e-b62cfb3b1076
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 726cde42eb08ee5508481887fae2e9d2b059256c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543865"
---
# <a name="ca1806-do-not-ignore-method-results"></a>CA1806: Não ignorar resultados do método
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotIgnoreMethodResults|
|CheckId|CA1806|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Há vários motivos possíveis para esse aviso:

- Um novo objeto é criado, mas nunca é usado.

- Um método que cria e retorna uma nova cadeia de caracteres é chamado e a nova cadeia de caracteres nunca é usada.

- Um método COM ou P/Invoke que retorna um HRESULT ou um código de erro que nunca é usado. Descrição da Regra

  Criação de objeto desnecessária e a coleta de lixo associada do desempenho degradado do objeto não utilizado.

  As cadeias de caracteres são imutáveis e métodos como String. ToUpper retorna uma nova instância de uma cadeia de caracteres em vez de modificar a instância da cadeia de caracteres no método de chamada.

  Ignorar HRESULT ou código de erro pode levar a um comportamento inesperado em condições de erro ou a condições de poucos recursos.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Se o método A cria uma nova instância do objeto B que nunca é usado, passe a instância como um argumento para outro método ou atribua a instância a uma variável. Se a criação do objeto for desnecessária, remova-o.-ou-

 Se o método A chama o método B, mas não usa a nova instância de cadeia de caracteres que o método B retorna. Passe a instância como um argumento para outro método, atribua a instância a uma variável. Ou remova a chamada se ela for desnecessária.

 -ou-

 Se o método A chama o método B, mas não usa o HRESULT ou o código de erro retornado pelo método. Use o resultado em uma instrução condicional, atribua o resultado a uma variável ou passe-o como um argumento para outro método.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprimir um aviso dessa regra, a menos que o ato de criar o objeto atenda a alguma finalidade.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma classe que ignora o resultado da chamada de String. Trim.

<!-- TODO: review snippet reference  [!CODE [FxCop.Usage.DoNotIgnoreMethodResults#1](FxCop.Usage.DoNotIgnoreMethodResults#1)]  -->

## <a name="example"></a>Exemplo
 O exemplo a seguir corrige a violação anterior, atribuindo o resultado de String. Trim de volta à variável em que foi chamada.

<!-- TODO: review snippet reference  [!CODE [FxCop.Usage.DoNotIgnoreMethodResults2#1](FxCop.Usage.DoNotIgnoreMethodResults2#1)]  -->

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que não usa um objeto que ele cria.

> [!NOTE]
> Essa violação não pode ser reproduzida no Visual Basic.

 [!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults3#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults3/cpp/FxCop.Usage.DoNotIgnoreMethodResults3.cpp#1)]
 [!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults3#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults3/cs/FxCop.Usage.DoNotIgnoreMethodResults3.cs#1)]
 [!code-vb[FxCop.Usage.DoNotIgnoreMethodResults3#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults3/vb/FxCop.Usage.DoNotIgnoreMethodResults3.vb#1)]

## <a name="example"></a>Exemplo
 O exemplo a seguir corrige a violação anterior, removendo a criação desnecessária de um objeto.

 [!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults4#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults4/cpp/FxCop.Usage.DoNotIgnoreMethodResults4.cpp#1)]
 [!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults4#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults4/cs/FxCop.Usage.DoNotIgnoreMethodResults4.cs#1)]
 [!code-vb[FxCop.Usage.DoNotIgnoreMethodResults4#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults4/vb/FxCop.Usage.DoNotIgnoreMethodResults4.vb#1)]

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que ignora o código de erro que o método nativo GetShortPathName retorna.

 [!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults5#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults5/cpp/FxCop.Usage.DoNotIgnoreMethodResults5.cpp#1)]
 [!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults5#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults5/cs/FxCop.Usage.DoNotIgnoreMethodResults5.cs#1)]

## <a name="example"></a>Exemplo
 O exemplo a seguir corrige a violação anterior, verificando o código de erro e gerando uma exceção quando a chamada falha.

 [!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults6#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults6/cpp/FxCop.Usage.DoNotIgnoreMethodResults6.cpp#1)]
 [!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults6#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults6/cs/FxCop.Usage.DoNotIgnoreMethodResults6.cs#1)]