---
title: 'CA1021: evitar parâmetros de saída'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1021
- AvoidOutParameters
helpviewer_keywords:
- AvoidOutParameters
- CA1021
ms.assetid: 970f2304-842c-4fb7-9734-f3871da8d479
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1082aaef3422923e0f74e8bd5eb242f3ae8e6023
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45549489"
---
# <a name="ca1021-avoid-out-parameters"></a>CA1021: evitar parâmetros de saída

|||
|-|-|
|NomeDoTipo|AvoidOutParameters|
|CheckId|CA1021|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método público ou protegido em um tipo público tem um `out` parâmetro.

## <a name="rule-description"></a>Descrição da regra
 Passar tipos por referência (usando `out` ou `ref`) requer experiência com ponteiros, compreensão das diferem entre tipos de valor e tipos de referência e métodos de tratamento com vários valores de retorno. Além disso, a diferença entre `out` e `ref` parâmetros não é amplamente compreendida.

 Quando um tipo de referência for passado "por referência", o método pretende usar o parâmetro para retornar uma instância diferente do objeto. Passar um tipo de referência por referência também é conhecido como usando um ponteiro duplo, o ponteiro para um ponteiro ou indireção double. Usando o padrão de convenção de chamada, que é passada "por valor", um parâmetro que usa um tipo de referência já recebe um ponteiro para o objeto. O ponteiro, não o objeto para o qual ele aponta, é passado por valor. Passe por valor significa que o método não é possível alterar o ponteiro para que ele aponte para uma nova instância do tipo de referência. No entanto, ele pode alterar o conteúdo do objeto para o qual ele aponta. Para a maioria dos aplicativos, isso é suficiente e produz o comportamento desejado.

 Se um método deve retornar uma instância diferente, use o valor de retorno do método para fazer isso. Consulte o <xref:System.String?displayProperty=fullName> classe para uma variedade de métodos que operam em cadeias de caracteres e retornam uma nova instância de uma cadeia de caracteres. Quando esse modelo é usado, o chamador deve decidir se o objeto original é preservado.

 Embora os valores de retorno são comuns e usadas intensamente, a aplicação correta de `out` e `ref` parâmetros requer habilidades de codificação e design intermediário. Os arquitetos de bibliotecas que projetam para um público em geral não deve esperar que os usuários dominem o trabalho com `out` ou `ref` parâmetros.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra que é causado por um tipo de valor, fazer com que o método retornar o objeto como seu valor de retorno. Se o método deve retornar vários valores, recrie-o para uma única instância de um objeto que contém os valores de retorno.

 Para corrigir uma violação dessa regra que é causado por um tipo de referência, certifique-se de que o comportamento desejado é para retornar uma nova instância da referência. Se for, o método deve usar seu valor de retorno para fazer isso.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra. No entanto, esse design pode causar problemas de usabilidade.

## <a name="example"></a>Exemplo
 A biblioteca a seguir mostra duas implementações de uma classe que gera respostas aos comentários de um usuário. A primeira implementação (`BadRefAndOut`) força o usuário da biblioteca para gerenciar os três valores de retorno. A implementação de segundo (`RedesignedRefAndOut`) simplifica a experiência do usuário, retornando uma instância de uma classe de contêiner (`ReplyData`) que gerencia os dados como uma única unidade.

 [!code-csharp[FxCop.Design.NoRefOrOut#1](../code-quality/codesnippet/CSharp/ca1021-avoid-out-parameters_1.cs)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir ilustra a experiência do usuário. A chamada para a biblioteca reprojetada (`UseTheSimplifiedClass` método) é mais simples, e as informações retornadas pelo método é facilmente gerenciadas. A saída entre os dois métodos é idêntica.

 [!code-csharp[FxCop.Design.TestNoRefOrOut#1](../code-quality/codesnippet/CSharp/ca1021-avoid-out-parameters_2.cs)]

## <a name="example"></a>Exemplo
 A biblioteca de exemplo a seguir ilustra como `ref` parâmetros para tipos de referência são usados e mostra uma maneira melhor para implementar essa funcionalidade.

 [!code-csharp[FxCop.Design.RefByRefNo#1](../code-quality/codesnippet/CSharp/ca1021-avoid-out-parameters_3.cs)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir chama cada método na biblioteca para demonstrar o comportamento.

 [!code-csharp[FxCop.Design.TestRefByRefNo#1](../code-quality/codesnippet/CSharp/ca1021-avoid-out-parameters_4.cs)]

Este exemplo gera a seguinte saída:

```txt
Changing pointer - passed by value:
12345
12345
Changing pointer - passed by reference:
12345
12345 ABCDE
Passing by return value:
12345 ABCDE
```

## <a name="try-pattern-methods"></a>Tente os métodos padrão

### <a name="description"></a>Descrição
 Métodos que implementam o **tente\<algo >** padrão, tais como <xref:System.Int32.TryParse%2A?displayProperty=fullName>, não gere a essa violação. O exemplo a seguir mostra uma estrutura (tipo de valor) que implementa o <xref:System.Int32.TryParse%2A?displayProperty=fullName> método.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Design.TryPattern#1](../code-quality/codesnippet/CSharp/ca1021-avoid-out-parameters_5.cs)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1045: não passar tipos por referência](../code-quality/ca1045-do-not-pass-types-by-reference.md)