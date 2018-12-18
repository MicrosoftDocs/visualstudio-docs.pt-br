---
title: 'CA1001: Tipos que possuem campos descartáveis devem ser descartáveis | Microsoft Docs'
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
- CA1001
- TypesThatOwnDisposableFieldsShouldBeDisposable
helpviewer_keywords:
- CA1001
- TypesThatOwnDisposableFieldsShouldBeDisposable
ms.assetid: c85c126c-2b16-4505-940a-b5ddf873fb22
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: a4bde7f20d1e7c93aec7a4a1a3abf44c21659b6e
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49176443"
---
# <a name="ca1001-types-that-own-disposable-fields-should-be-disposable"></a>CA1001: tipos que tenham campos descartáveis devem ser descartáveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||  
|-|-|  
|NomeDoTipo|TypesThatOwnDisposableFieldsShouldBeDisposable|  
|CheckId|CA1001|  
|Categoria|Microsoft.Design|  
|Alteração Significativa|Sem quebra - se o tipo não é visível fora do assembly.<br /><br /> Quebrando - se o tipo é visível fora do assembly.|  
  
## <a name="cause"></a>Causa  
 Uma classe declara e implementa um campo de instância que é um <xref:System.IDisposable?displayProperty=fullName> tipo e a classe não implementa <xref:System.IDisposable>.  
  
## <a name="rule-description"></a>Descrição da Regra  
 Uma classe implementa o <xref:System.IDisposable> interface para descartar os recursos não gerenciados que ele possui. Um campo de instância que é um <xref:System.IDisposable> tipo indica se o campo tem um recurso não gerenciado. Uma classe que declara um <xref:System.IDisposable> campo indiretamente possui um recurso não gerenciado e deve implementar o <xref:System.IDisposable> interface. Se a classe possui diretamente quaisquer recursos não gerenciados, ele não deve implementar um finalizador.  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Para corrigir uma violação dessa regra, implemente <xref:System.IDisposable> e para o <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> chamada de método a <xref:System.IDisposable.Dispose%2A> método do campo.  
  
## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos  
 Não suprima um aviso nessa regra.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra uma classe que viola a regra e uma classe que satisfaz a regra com a implementação de <xref:System.IDisposable>. A classe não implementa um finalizador porque a classe não possui diretamente quaisquer recursos não gerenciados.  
  
 [!code-csharp[FxCop.Design.DisposableFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.DisposableFields/cs/FxCop.Design.DisposableFields.cs#1)]
 [!code-vb[FxCop.Design.DisposableFields#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.DisposableFields/vb/FxCop.Design.DisposableFields.vb#1)]  
  
## <a name="related-rules"></a>Regras relacionadas  
 [CA2213: os campos descartáveis devem ser descartados](../code-quality/ca2213-disposable-fields-should-be-disposed.md)  
  
 [CA2216: os tipos descartáveis devem declarar o finalizador](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)  
  
 [CA2215: métodos Dispose devem chamar o descarte da classe base](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)  
  
 [CA1049: tipos que tenham recursos nativos devem ser descartáveis](../code-quality/ca1049-types-that-own-native-resources-should-be-disposable.md)

