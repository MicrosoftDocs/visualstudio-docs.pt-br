---
title: 'CA1045: não passar tipos por referência'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1045
- DoNotPassTypesByReference
helpviewer_keywords:
- CA1045
- DoNotPassTypesByReference
ms.assetid: bcc3900a-e092-4bb8-896f-cb83f6289968
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6ee365dd36a3a88b896fe9ec6e2f676b4e29bf1e
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45547835"
---
# <a name="ca1045-do-not-pass-types-by-reference"></a>CA1045: não passar tipos por referência

|||
|-|-|
|NomeDoTipo|DoNotPassTypesByReference|
|CheckId|CA1045|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método público ou protegido em um tipo público tem um `ref` parâmetro que usa um tipo primitivo, um tipo de referência ou um tipo de valor que não é um dos tipos internos.

## <a name="rule-description"></a>Descrição da regra
 Passar tipos por referência (usando `out` ou `ref`) requer experiência com ponteiros, compreensão das diferem entre tipos de valor e tipos de referência e lidando com métodos que têm vários valores de retorno. Além disso, a diferença entre `out` e `ref` parâmetros não é amplamente compreendida.

 Quando um tipo de referência for passado "por referência", o método pretende usar o parâmetro para retornar uma instância diferente do objeto. (Passar um tipo de referência por referência é também conhecido como usando um ponteiro duplo, o ponteiro para um ponteiro ou indireção double.) Usando o padrão de convenção de chamada, que é passada "por valor", um parâmetro que usa um tipo de referência já recebe um ponteiro para o objeto. O ponteiro, não o objeto para o qual ele aponta, é passado por valor. Passagem por valor significa que o método não é possível alterar o ponteiro para que ele aponte para uma nova instância da referência de tipo, mas pode alterar o conteúdo do objeto para o qual ele aponta. Para a maioria dos aplicativos, isso é suficiente e produz o comportamento que você deseja.

 Se um método deve retornar uma instância diferente, use o valor de retorno do método para fazer isso. Consulte o <xref:System.String?displayProperty=fullName> classe para uma variedade de métodos que operam em cadeias de caracteres e retornam uma nova instância de uma cadeia de caracteres. Usando esse modelo, ela é deixada para o chamador para decidir se o objeto original é preservado.

 Embora os valores de retorno são comuns e usadas intensamente, a aplicação correta de `out` e `ref` parâmetros requer habilidades de codificação e design intermediário. Os arquitetos de bibliotecas que projetam para um público em geral não deve esperar que os usuários dominem o trabalho com `out` ou `ref` parâmetros.

> [!NOTE]
>  Quando você trabalha com parâmetros que são estruturas grandes, os recursos adicionais que são necessárias para copiar essas estruturas pode causar um efeito de desempenho quando você passa por valor. Nesses casos, você pode considerar o uso `ref` ou `out` parâmetros.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra que é causado por um tipo de valor, fazer com que o método retornar o objeto como seu valor de retorno. Se o método deve retornar vários valores, recrie-o para uma única instância de um objeto que contém os valores de retorno.

 Para corrigir uma violação dessa regra que é causado por um tipo de referência, certifique-se de que o comportamento desejado é para retornar uma nova instância da referência. Se for, o método deve usar seu valor de retorno para fazer isso.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra; No entanto, esse design pode causar problemas de usabilidade.

## <a name="example"></a>Exemplo
 A biblioteca a seguir mostra duas implementações de uma classe que gera respostas aos comentários do usuário. A primeira implementação (`BadRefAndOut`) força o usuário da biblioteca para gerenciar os três valores de retorno. A implementação de segundo (`RedesignedRefAndOut`) simplifica a experiência do usuário, retornando uma instância de uma classe de contêiner (`ReplyData`) que gerencia os dados como uma única unidade.

 [!code-csharp[FxCop.Design.NoRefOrOut#1](../code-quality/codesnippet/CSharp/ca1045-do-not-pass-types-by-reference_1.cs)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir ilustra a experiência do usuário. A chamada para a biblioteca reprojetada (`UseTheSimplifiedClass` método) é mais simples, e as informações que são retornadas pelo método é facilmente gerenciadas. A saída entre os dois métodos é idêntica.

 [!code-csharp[FxCop.Design.TestNoRefOrOut#1](../code-quality/codesnippet/CSharp/ca1045-do-not-pass-types-by-reference_2.cs)]

## <a name="example"></a>Exemplo
 A biblioteca de exemplo a seguir ilustra como `ref` parâmetros para tipos de referência são usados e mostra uma maneira melhor para implementar essa funcionalidade.

 [!code-csharp[FxCop.Design.RefByRefNo#1](../code-quality/codesnippet/CSharp/ca1045-do-not-pass-types-by-reference_3.cs)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir chama cada método na biblioteca para demonstrar o comportamento.

 [!code-csharp[FxCop.Design.TestRefByRefNo#1](../code-quality/codesnippet/CSharp/ca1045-do-not-pass-types-by-reference_4.cs)]

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

## <a name="related-rules"></a>Regras relacionadas
 [CA1021: evitar parâmetros de saída](../code-quality/ca1021-avoid-out-parameters.md)