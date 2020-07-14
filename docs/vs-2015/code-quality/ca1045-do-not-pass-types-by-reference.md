---
title: 'CA1045: não passar tipos por referência | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1045
- DoNotPassTypesByReference
helpviewer_keywords:
- CA1045
- DoNotPassTypesByReference
ms.assetid: bcc3900a-e092-4bb8-896f-cb83f6289968
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: dad2f90a51a4247a4c111ef51e85a28ba1a118ce
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548467"
---
# <a name="ca1045-do-not-pass-types-by-reference"></a>CA1045: Não passar tipos por referência
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotPassTypesByReference|
|CheckId|CA1045|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método público ou protegido em um tipo público tem um `ref` parâmetro que usa um tipo primitivo, um tipo de referência ou um tipo de valor que não é um dos tipos internos.

## <a name="rule-description"></a>Descrição da Regra
 Passar tipos por referência (usando `out` ou `ref` ) requer experiência com ponteiros, compreendendo como tipos de valor e tipos de referência diferem e manipulando métodos que têm vários valores de retorno. Além disso, a diferença entre os `out` `ref` parâmetros e não é amplamente compreendida.

 Quando um tipo de referência é passado "por referência", o método pretende usar o parâmetro para retornar uma instância diferente do objeto. (Passar um tipo de referência por referência também é conhecido como usar um ponteiro duplo, um ponteiro para um ponteiro ou um indireção duplo.) Usando a Convenção de chamada padrão, que é Pass "por valor", um parâmetro que usa um tipo de referência já recebe um ponteiro para o objeto. O ponteiro, não o objeto ao qual ele aponta, é passado por valor. A passagem por valor significa que o método não pode alterar o ponteiro para que ele aponte para uma nova instância do tipo de referência, mas pode alterar o conteúdo do objeto para o qual ele aponta. Para a maioria dos aplicativos, isso é suficiente e produz o comportamento desejado.

 Se um método precisar retornar uma instância diferente, use o valor de retorno do método para fazer isso. Consulte a <xref:System.String?displayProperty=fullName> classe de uma variedade de métodos que operam em cadeias de caracteres e retornam uma nova instância de uma cadeia de caracteres. Ao usar esse modelo, ele é deixado para o chamador a fim de decidir se o objeto original é preservado.

 Embora os valores de retorno sejam comuns e usados intensamente, a aplicação e os parâmetros corretos `out` `ref` exigem design intermediário e habilidades de codificação. Os arquitetos de biblioteca que projetam um público geral não devem esperar que os usuários façam o mestre de trabalho com os `out` `ref` parâmetros ou.

> [!NOTE]
> Quando você trabalha com parâmetros que são estruturas grandes, os recursos adicionais necessários para copiar essas estruturas podem causar um efeito de desempenho quando você passa por valor. Nesses casos, você pode considerar o uso `ref` de `out` parâmetros ou.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra causada por um tipo de valor, faça com que o método retorne o objeto como seu valor de retorno. Se o método deve retornar vários valores, recrie-o para retornar uma única instância de um objeto que contém os valores.

 Para corrigir uma violação dessa regra que é causada por um tipo de referência, verifique se o comportamento desejado é retornar uma nova instância da referência. Se for, o método deve usar seu valor de retorno para fazer isso.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra; no entanto, esse design pode causar problemas de usabilidade.

## <a name="example"></a>Exemplo
 A biblioteca a seguir mostra duas implementações de uma classe que gera respostas para os comentários do usuário. A primeira implementação ( `BadRefAndOut` ) força o usuário da biblioteca a gerenciar três valores de retorno. A segunda implementação ( `RedesignedRefAndOut` ) simplifica a experiência do usuário retornando uma instância de uma classe de contêiner ( `ReplyData` ) que gerencia os dados como uma única unidade.

 [!code-csharp[FxCop.Design.NoRefOrOut#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NoRefOrOut/cs/FxCop.Design.NoRefOrOut.cs#1)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir ilustra a experiência do usuário. A chamada para a biblioteca remodelada ( `UseTheSimplifiedClass` método) é mais simples, e as informações retornadas pelo método são facilmente gerenciadas. A saída dos dois métodos é idêntica.

 [!code-csharp[FxCop.Design.TestNoRefOrOut#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestNoRefOrOut/cs/FxCop.Design.TestNoRefOrOut.cs#1)]

## <a name="example"></a>Exemplo
 A biblioteca de exemplo a seguir ilustra como os `ref` parâmetros para tipos de referência são usados e mostra uma maneira melhor de implementar essa funcionalidade.

 [!code-csharp[FxCop.Design.RefByRefNo#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.RefByRefNo/cs/FxCop.Design.RefByRefNo.cs#1)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir chama cada método na biblioteca para demonstrar o comportamento.

 [!code-csharp[FxCop.Design.TestRefByRefNo#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestRefByRefNo/cs/FxCop.Design.TestRefByRefNo.cs#1)]

 Este exemplo gerencia a seguinte saída.

 **Alterando ponteiro – aprovado por valor:** 
 **12345** 
 **12345** 
 **Alterando ponteiro – aprovado por referência:** 
 **12345** 
 **12345 abcde** 
 **Passando por valor de retorno:** 
 **12345 abcde**
## <a name="related-rules"></a>Regras relacionadas
 [CA1021: Evitar parâmetros out](../code-quality/ca1021-avoid-out-parameters.md)
