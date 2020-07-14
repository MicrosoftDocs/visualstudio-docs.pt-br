---
title: 'CA1810: inicializar campos estáticos de tipo de referência em linha | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- InitializeReferenceTypeStaticFieldsInline
- CA1810
helpviewer_keywords:
- InitializeReferenceTypeStaticFieldsInline
- CA1810
ms.assetid: e9693118-a914-4efb-9550-ec659d8d97d2
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c4ad2f4db9290430bb8a378bd264078370ca7b66
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543826"
---
# <a name="ca1810-initialize-reference-type-static-fields-inline"></a>CA1810: Inicializar campos estáticos de tipo de referência em linha
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|InitializeReferenceTypeStaticFieldsInline|
|CheckId|CA1810|
|Categoria|Microsoft. performance|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo de referência declara um construtor estático explícito.

## <a name="rule-description"></a>Descrição da Regra
 Quando um tipo declara um construtor estático explícito, o compilador JIT (just-in-time) adiciona uma verificação a cada método estático e construtor de instância do tipo para garantir que o construtor estático tenha sido chamado anteriormente. A inicialização estática é disparada quando qualquer membro estático é acessado ou quando uma instância do tipo é criada. No entanto, a inicialização estática não será disparada se você declarar uma variável do tipo, mas não a usar, o que pode ser importante se a inicialização alterar o estado global.

 Quando todos os dados estáticos são inicializados embutidos e um construtor estático explícito não é declarado, os compiladores MSIL (Microsoft Intermediate Language) adicionam o `beforefieldinit` sinalizador e um construtor estático implícito, que inicializa os dados estáticos para a definição do tipo MSIL. Quando o compilador JIT encontra o `beforefieldinit` sinalizador, na maioria das vezes as verificações de Construtor estáticos não são adicionadas. É garantido que a inicialização estática ocorra em algum momento antes de qualquer campo estático ser acessado, mas não antes que um método estático ou construtor de instância seja invocado. Observe que a inicialização estática pode ocorrer a qualquer momento depois que uma variável do tipo é declarada.

 As verificações de construtor estático podem diminuir o desempenho. Geralmente, um construtor estático é usado apenas para inicializar campos estáticos; nesse caso, você só deve garantir que a inicialização estática ocorra antes do primeiro acesso de um campo estático. O `beforefieldinit` comportamento é apropriado para esses e a maioria dos outros tipos. Só é inadequado quando a inicialização estática afeta o estado global e uma das seguintes opções é verdadeira:

- O efeito no estado global será caro e não será necessário se o tipo não for usado.

- Os efeitos de estado global podem ser acessados sem acessar nenhum campo estático do tipo.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, inicialize todos os dados estáticos quando declarados e remova o construtor estático.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se o desempenho não for um problema; ou se as alterações de estado global causadas pela inicialização estática forem caras ou precisarem ter a garantia de ocorrer antes que um método estático do tipo seja chamado ou uma instância do tipo seja criada.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo, `StaticConstructor` , que viola a regra e um tipo, `NoStaticConstructor` , que substitui o construtor estático por inicialização embutida para satisfazer a regra.

 [!code-csharp[FxCop.Performance.RefTypeStaticCtor#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.RefTypeStaticCtor/cs/FxCop.Performance.RefTypeStaticCtor.cs#1)]
 [!code-vb[FxCop.Performance.RefTypeStaticCtor#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.RefTypeStaticCtor/vb/FxCop.Performance.RefTypeStaticCtor.vb#1)]

 Observe a adição do `beforefieldinit` sinalizador na definição da MSIL para a `NoStaticConstructor` classe.

 **. classe pública ANSI auto StaticConstructor** **estende [mscorlib] System. Object** 
 **{** 
 **}//fim da classe StaticConstructor** 
 **. Class pública auto ANSI beforefieldinit NoStaticConstructor** **estende [mscorlib] System. Object** 
 **{** 
 **}//fim da classe NoStaticConstructor**
## <a name="related-rules"></a>Regras relacionadas
 [CA2207: Inicializar campos estáticos de tipo de valor em linha](../code-quality/ca2207-initialize-value-type-static-fields-inline.md)
