---
title: 'CA2202: Não descartar objetos várias vezes | Microsoft Docs'
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
- CA2202
- Do not dispose objects multiple times
- DoNotDisposeObjectsMultipleTimes
helpviewer_keywords:
- CA2202
ms.assetid: fa85349a-cf1e-42c8-a86b-eacae1f8bd96
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: de3bc29e6d843532e4c15db1e33673d4f63c5179
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49830711"
---
# <a name="ca2202-do-not-dispose-objects-multiple-times"></a>CA2202: não descartar objetos várias vezes
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|DoNotDisposeObjectsMultipleTimes|
|CheckId|CA2202|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Uma implementação do método contém caminhos de código que poderiam causar várias chamadas para <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> ou um equivalente de Dispose, como um método Close () em alguns tipos, no mesmo objeto.

## <a name="rule-description"></a>Descrição da Regra
 Um implementado corretamente <xref:System.IDisposable.Dispose%2A> método pode ser chamado várias vezes sem lançar uma exceção. No entanto, isso não é garantido e para evitar a geração de um <xref:System.ObjectDisposedException?displayProperty=fullName> você não deve chamar <xref:System.IDisposable.Dispose%2A> mais de uma vez em um objeto.

## <a name="related-rules"></a>Regras relacionadas
 [CA2000: descartar objetos antes de perder o escopo](../code-quality/ca2000-dispose-objects-before-losing-scope.md)

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere a implementação assim que independentemente do caminho do código, <xref:System.IDisposable.Dispose%2A> é chamado apenas uma vez para o objeto.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra. Mesmo se <xref:System.IDisposable.Dispose%2A> para o objeto é conhecido por ser com segurança que pode ser chamado várias vezes, a implementação pode ser alterado no futuro.

## <a name="example"></a>Exemplo
 Aninhado `using` instruções (`Using` no Visual Basic) pode causar violações do aviso CA2202. Se o recurso de IDisposable de aninhada interna `using` declaração contém o recurso de externo `using` instrução, o `Dispose` método do recurso aninhado libera o recurso contido. Quando essa situação ocorre, o `Dispose` método de externo `using` declaração tenta descartar seu recurso para uma segunda vez.

 No exemplo a seguir, uma <xref:System.IO.Stream> objeto que é criado em um externa usando a instrução é liberado no final do interno usando a instrução no método Dispose do <xref:System.IO.StreamWriter> objeto que contém o `stream` objeto. No final do externo `using` instrução, o `stream` o objeto é liberado uma segunda vez. A segunda versão é uma violação da CA2202.

```
using (Stream stream = new FileStream("file.txt", FileMode.OpenOrCreate))
{
    using (StreamWriter writer = new StreamWriter(stream))
    {
        // Use the writer object...
    }
}
```

## <a name="example"></a>Exemplo
 Para resolver esse problema, use uma `try` / `finally` bloco, em vez de externa `using` instrução. No `finally` bloquear, certifique-se de que o `stream` recurso não for nulo.

```
Stream stream = null;
try
{
    stream = new FileStream("file.txt", FileMode.OpenOrCreate);
    using (StreamWriter writer = new StreamWriter(stream))
    {
        stream = null;
        // Use the writer object...
    }
}
finally
{
    if(stream != null)
        stream.Dispose();
}
```

## <a name="see-also"></a>Consulte também
 <xref:System.IDisposable?displayProperty=fullName> [Padrão de descarte](http://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)



