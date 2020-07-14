---
title: 'CA5350: não use algoritmos de criptografia fracos | Microsoft Docs'
ms.date: 11/15/2016
ms.technology: vs-ide-code-analysis
ms.topic: reference
ms.assetid: 4c51bb8a-fcfa-46aa-ab61-634be84c4a7a
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: afadf41fc753051047e858758bfe0677987d726d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545061"
---
# <a name="ca5350-do-not-use-weak-cryptographic-algorithms"></a>CA5350: Não usar algoritmos de criptografia fracos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotUseWeakCryptographicAlgorithms|
|CheckId|CA5350|
|Categoria|Microsoft. Cryptography|
|Alteração Significativa|Sem interrupção|

> [!NOTE]
> Esse aviso foi atualizado pela última vez em 2015 de novembro.

## <a name="cause"></a>Causa
 Os algoritmos de criptografia, como <xref:System.Security.Cryptography.TripleDES> e os algoritmos de hash, como <xref:System.Security.Cryptography.SHA1> e <xref:System.Security.Cryptography.RIPEMD160> são considerados fracos.

 Esses algoritmos de criptografia não fornecem tanta garantia de segurança quanto as contrapartes mais modernas. Algoritmos de hash criptográfico <xref:System.Security.Cryptography.SHA1> e <xref:System.Security.Cryptography.RIPEMD160> fornecem menos resistência à colisão que os mais modernos algoritmos de hash. O algoritmo de criptografia <xref:System.Security.Cryptography.TripleDES> fornece menos bits de segurança do que mais algoritmos de criptografia modernos.

## <a name="rule-description"></a>Descrição da Regra
 Algoritmos de criptografia fracos e funções de hash são usados hoje por vários motivos, mas não devem ser usados para garantir a confidencialidade dos dados que eles protegem.

 A regra é disparada quando encontra algoritmos 3DES, SHA1 ou RIPEMD160 no código e gera um aviso para o usuário.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Use opções criptograficamente mais fortes:

- Para criptografia TripleDES, use <xref:System.Security.Cryptography.Aes> criptografia.

- Para funções de hash SHA1 ou RIPEMD160, use aquelas na família [SHA-2](https://msdn.microsoft.com/library/windows/desktop/aa382459.aspx) (por exemplo <xref:System.Security.Cryptography.SHA512> , <xref:System.Security.Cryptography.SHA384> , <xref:System.Security.Cryptography.SHA256> ).

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir um aviso dessa regra quando o nível de proteção necessário para os dados não exigir uma garantia de segurança.

## <a name="pseudo-code-example"></a>Exemplo de pseudo-código
 No momento da redação deste artigo, o exemplo de pseudocódigo a seguir ilustra o padrão detectado por essa regra.

### <a name="sha-1-hashing-violation"></a>Violação de hash SHA-1

```
using System.Security.Cryptography;
...
var hashAlg = SHA1.Create();

```

### <a name="solution"></a>Solução

```
using System.Security.Cryptography;
...
var hashAlg = SHA256.Create();

```

### <a name="ripemd160-br-br-hashing-violation"></a>RIPEMD160 <br /><br />Violação de hash

```
using System.Security.Cryptography;
...
var hashAlg = RIPEMD160Managed.Create();

```

### <a name="solution"></a>Solução

```
using System.Security.Cryptography;
...
var hashAlg = SHA256.Create();

```

### <a name="tripledes-encryption-violation"></a>Violação de criptografia TripleDES

```
using System.Security.Cryptography;
...
using (TripleDES encAlg = TripleDES.Create())
{
  ...
}
```

### <a name="solution"></a>Solução

```
using System.Security.Cryptography;
...
using (AesManaged encAlg = new AesManaged())
{
  ...
}
```