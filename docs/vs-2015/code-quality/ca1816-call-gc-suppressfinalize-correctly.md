---
title: 'CA1816: Chamar GC. SuppressFinalize corretamente | Microsoft Docs'
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
- CA1816
- DisposeMethodsShouldCallSuppressFinalize
helpviewer_keywords:
- DisposeMethodsShouldCallSuppressFinalize
- CA1816
ms.assetid: 47915fbb-103f-4333-b157-1da16bf49660
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: d859f8fe38d4b6efecb83b117f35cbf483467b6f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49913872"
---
# <a name="ca1816-call-gcsuppressfinalize-correctly"></a>CA1816: chamar GC.SuppressFinalize corretamente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|CallGCSuppressFinalizeCorrectly|
|CheckId|CA1816|
|Categoria|Microsoft. Uso|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa

-   Um método que é uma implementação de <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> não chama <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>.

-   Um método que não é uma implementação de <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> chamadas <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>.

-   Chama um método <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> e passa algo que não seja isso (Me no Visual Basic).

## <a name="rule-description"></a>Descrição da Regra
 O <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> método permite que os usuários liberar os recursos a qualquer momento antes do objeto ficarem disponíveis para a coleta de lixo. Se o <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> método é chamado, ele libera os recursos do objeto. Isso torna a finalização desnecessária. <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> deve chamar <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> para que o coletor de lixo não chamará o finalizador do objeto.

 Para impedir que os tipos derivados com finalizadores tenham reimplementar [System. IDisposable] (<!-- TODO: review code entity reference <xref:assetId:///System.IDisposable?qualifyHint=True&amp;autoUpgrade=False>  -->) e para chamá-lo, sem lacre tipos sem os finalizadores devem chamar ainda <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra:

 Se o método é uma implementação de <xref:System.IDisposable.Dispose%2A>, adicione uma chamada para <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>.

 Se o método não é uma implementação de <xref:System.IDisposable.Dispose%2A>, ou remova a chamada para <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> ou movê-lo para o tipo <xref:System.IDisposable.Dispose%2A> implementação.

 Alterar todas as chamadas para <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> passar isso (Me no Visual Basic).

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir um aviso nessa regra somente se você estiver deliberating usando <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> para controlar o tempo de vida de outros objetos. Não suprimir um aviso nessa regra se uma implementação de <xref:System.IDisposable.Dispose%2A> não chama <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>. Nessa situação, falhando suprimir a finalização degrada o desempenho e não fornecer nenhum benefício.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que incorretamente chamadas <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>.

 [!code-csharp[FxCop.Usage.CallGCSuppressFinalizeCorrectly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly/CS/FxCop.Usage.CallGCSuppressFinalizeCorrectly.cs#1)]
 [!code-vb[FxCop.Usage.CallGCSuppressFinalizeCorrectly#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly/VB/FxCop.Usage.CallGCSuppressFinalizeCorrectly.vb#1)]

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que corretamente chamadas <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>.

 [!code-csharp[FxCop.Usage.CallGCSuppressFinalizeCorrectly2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly2/CS/FxCop.Usage.CallGCSuppressFinalizeCorrectly2.cs#1)]
 [!code-vb[FxCop.Usage.CallGCSuppressFinalizeCorrectly2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly2/VB/FxCop.Usage.CallGCSuppressFinalizeCorrectly2.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2215: métodos Dispose devem chamar o descarte da classe base](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)

 [CA2216: os tipos descartáveis devem declarar o finalizador](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

## <a name="see-also"></a>Consulte também
 [Padrão de descarte](http://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)



