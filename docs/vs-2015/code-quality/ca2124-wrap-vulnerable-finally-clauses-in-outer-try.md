---
title: 'CA2124: encapsular cláusulas finally vulneráveis na tentativa externa | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2124
- WrapVulnerableFinallyClausesInOuterTry
helpviewer_keywords:
- CA2124
- WrapVulnerableFinallyClausesInOuterTry
ms.assetid: 82efd224-9e60-4b88-a0f5-dfabcc49a254
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 4e191ca10456f133e1213961ca2d1ed9cb8e040b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544294"
---
# <a name="ca2124-wrap-vulnerable-finally-clauses-in-outer-try"></a>CA2124: Encapsular cláusulas finally vulneráveis em try externo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|WrapVulnerableFinallyClausesInOuterTry|
|CheckId|CA2124|
|Categoria|Microsoft.Security|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Nas versões 1,0 e 1,1 do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] , um método público ou protegido contém um `try` / `catch` / `finally` bloco. O `finally` bloco é exibido para redefinir o estado de segurança e não está incluído em um `finally` bloco.

## <a name="rule-description"></a>Descrição da Regra
 Essa regra localiza `try` / `finally` blocos no código que têm como destino as versões 1,0 e 1,1 do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] que podem estar vulneráveis a filtros de exceção mal-intencionada presentes na pilha de chamadas. Se operações confidenciais, como a representação ocorrerem no bloco try, e uma exceção for lançada, o filtro poderá ser executado antes do `finally` bloco. Para o exemplo de representação, isso significa que o filtro seria executado como o usuário representado. Atualmente, os filtros são implementados somente em Visual Basic.

> [!WARNING]
> Nas versões 2,0 e posteriores do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] , o tempo de execução protege automaticamente um `try` / `catch` /  `finally` bloco de filtros de exceção mal-intencionados, se a redefinição ocorrer diretamente dentro do método que contém o bloco de exceção.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Coloque o desencapsulado `try` / `finally` em um bloco try externo. Consulte o segundo exemplo a seguir. Isso força o `finally` a executar antes do código de filtro.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="pseudo-code-example"></a>Exemplo de pseudo-código

### <a name="description"></a>Descrição
 O pseudocódigo a seguir ilustra o padrão detectado por essa regra.

### <a name="code"></a>Código

```
try {
   // Do some work.
   Impersonator imp = new Impersonator("John Doe");
   imp.AddToCreditCardBalance(100);
}
finally {
   // Reset security state.
   imp.Revert();
}
```

## <a name="example"></a>Exemplo
 O pseudocódigo a seguir mostra o padrão que você pode usar para proteger seu código e atender a essa regra.

```
try {
     try {
        // Do some work.
     }
     finally {
        // Reset security state.
     }
}
catch()
{
    throw;
}
```
