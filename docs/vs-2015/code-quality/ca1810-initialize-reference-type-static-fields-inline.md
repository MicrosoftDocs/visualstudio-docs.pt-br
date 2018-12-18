---
title: 'CA1810: Tipo de referência inicializar campos estáticos embutido | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- InitializeReferenceTypeStaticFieldsInline
- CA1810
helpviewer_keywords:
- InitializeReferenceTypeStaticFieldsInline
- CA1810
ms.assetid: e9693118-a914-4efb-9550-ec659d8d97d2
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: e4d7ffbe4fc821ffd70b0bb299b2a4738d63873b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49862678"
---
# <a name="ca1810-initialize-reference-type-static-fields-inline"></a>CA1810: inicializar campos estáticos de tipo de referência embutido
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|InitializeReferenceTypeStaticFieldsInline|
|CheckId|CA1810|
|Categoria|Microsoft.Performance|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um tipo de referência declara um construtor estático explícito.

## <a name="rule-description"></a>Descrição da Regra
 Quando um tipo declara um construtor estático explícito, o compilador JIT (just-in-time) adiciona uma verificação a cada método estático e construtor de instância do tipo para garantir que o construtor estático tenha sido chamado anteriormente. Inicialização estática é acionada quando qualquer membro estático ser acessado ou quando uma instância do tipo é criada. No entanto, a inicialização estática não será acionada se você declara uma variável do tipo, mas não usá-lo, que pode ser importante se a inicialização altera o estado global.

 Quando todos os dados estáticos é inicializado embutido e não está declarado como um construtor estático explícito, os compiladores do Microsoft intermediate language (MSIL) adicionar o `beforefieldinit` sinalizador e um construtor estático implícito, que inicializa os dados estáticos, para o tipo MSIL definição. Quando o compilador JIT encontra o `beforefieldinit` sinalizar, a maioria das vezes, as verificações de construtor estático não são adicionadas. Inicialização estática é garantido que ocorrem em algum momento antes de qualquer campo estático é acessado, mas não antes de um construtor de instância ou método estático é invocado. Observe que a inicialização estática pode ocorrer a qualquer momento depois que uma variável do tipo é declarada.

 As verificações de construtor estático podem diminuir o desempenho. Geralmente, um construtor estático é usado somente para inicializar campos estáticos, na qual o caso, apenas certifique-se de que a inicialização estática ocorre antes do primeiro acesso de um campo estático. O `beforefieldinit` comportamento é apropriado para eles e a maioria dos outros tipos. Só é inadequado ao estado global afeta a inicialização estática e uma das seguintes opções for verdadeira:

-   O efeito sobre o estado global é caro e não será necessário se o tipo não é usado.

-   Os efeitos de estado global podem ser acessados sem acessar qualquer campo estático do tipo.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, inicialize todos os dados estáticos quando declarados e remova o construtor estático.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, se o desempenho não for uma preocupação; ou se as alterações de estado global que são causadas por inicialização estática são caras ou devem ser garantida para ocorrer antes que um método estático do tipo é chamado ou uma instância do tipo é criada.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo `StaticConstructor`, que viola a regra e um tipo, `NoStaticConstructor`, que substitui o construtor estático com inicialização embutida para satisfazer a regra.

 [!code-csharp[FxCop.Performance.RefTypeStaticCtor#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.RefTypeStaticCtor/cs/FxCop.Performance.RefTypeStaticCtor.cs#1)]
 [!code-vb[FxCop.Performance.RefTypeStaticCtor#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.RefTypeStaticCtor/vb/FxCop.Performance.RefTypeStaticCtor.vb#1)]

 Observe a adição do `beforefieldinit` sinalizador na definição do MSIL para o `NoStaticConstructor` classe.

 **. class pública auto ansi StaticConstructor** **estende [mscorlib]System.Object**
 **{**
 **} / / fim da classe StaticConstructor** 
 **. class pública automática ansi beforefieldinit NoStaticConstructor** **estende [mscorlib]System.Object**
 **{** 
 **} / / fim da classe NoStaticConstructor**
## <a name="related-rules"></a>Regras relacionadas
 [CA2207: inicializar campos estáticos de tipo de valor embutido](../code-quality/ca2207-initialize-value-type-static-fields-inline.md)



