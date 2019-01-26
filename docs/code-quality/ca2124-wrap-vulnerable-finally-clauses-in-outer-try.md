---
title: 'CA2124: Encapsular cláusulas finally vulneráveis em try externo'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: reference
f1_keywords:
- CA2124
- WrapVulnerableFinallyClausesInOuterTry
helpviewer_keywords:
- CA2124
- WrapVulnerableFinallyClausesInOuterTry
ms.assetid: 82efd224-9e60-4b88-a0f5-dfabcc49a254
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8773df5d309d72ef7e1a5298230b6cce63f23ee8
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54958830"
---
# <a name="ca2124-wrap-vulnerable-finally-clauses-in-outer-try"></a>CA2124: Encapsular cláusulas finally vulneráveis em try externo

|||
|-|-|
|NomeDoTipo|WrapVulnerableFinallyClausesInOuterTry|
|CheckId|CA2124|
|Categoria|Microsoft.Security|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Nas versões 1.0 e 1.1 do .NET Framework, um método público ou protegido contém um `try` / `catch` / `finally` bloco. O `finally` bloco aparece para redefinir o estado de segurança e não é colocado um `finally` bloco.

## <a name="rule-description"></a>Descrição da regra
 Essa regra localiza `try` / `finally` bloqueia no código que tem como alvo as versões 1.0 e 1.1 do .NET Framework que podem ser vulneráveis a filtros de exceção mal-intencionados presentes na pilha de chamadas. Se operações confidenciais como representação ocorrerem no bloco try, e uma exceção é lançada, o filtro pode ser executado antes de `finally` bloco. No exemplo de representação, isso significa que o filtro seria executado como o usuário representado. Os filtros são implementável atualmente apenas no Visual Basic.

> [!NOTE]
> Nas versões 2.0 e posteriores do .NET Framework, o tempo de execução protege automaticamente um `try` / `catch` /  `finally` bloquear de filtros de exceção mal-intencionados, se a reinicialização ocorrer diretamente dentro do método que contém o bloco de exceção.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Coloque o desencapsulamento `try` / `finally` em um bloco try externo. Consulte o segundo exemplo que segue. Isso força o `finally` seja executado antes do código de filtro.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="pseudo-code-example"></a>Exemplo de pseudocódigo

### <a name="description"></a>Descrição

O pseudocódigo a seguir ilustra o padrão detectado por essa regra.

```csharp
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

O pseudocódigo a seguir mostra o padrão que você pode usar para proteger seu código e atender a essa regra.

```csharp
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