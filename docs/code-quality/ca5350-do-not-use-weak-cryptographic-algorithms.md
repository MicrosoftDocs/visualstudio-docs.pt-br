---
title: 'CA5350: não use algoritmos criptográficos fracos'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
ms.assetid: 4c51bb8a-fcfa-46aa-ab61-634be84c4a7a
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ba5e70505db86b1497e625b216da955bba677245
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45547848"
---
# <a name="ca5350-do-not-use-weak-cryptographic-algorithms"></a>CA5350: não use algoritmos criptográficos fracos

|||
|-|-|
|NomeDoTipo|DoNotUseWeakCryptographicAlgorithms|
|CheckId|CA5350|
|Categoria|Microsoft.Cryptography|
|Alteração Significativa|Não separável|

> [!NOTE]
> Esse aviso foi atualizado pela última vez em novembro de 2015.

## <a name="cause"></a>Causa

Algoritmos de criptografia, como <xref:System.Security.Cryptography.TripleDES> e, como os algoritmos de hash <xref:System.Security.Cryptography.SHA1> e <xref:System.Security.Cryptography.RIPEMD160> são considerados fracos.

Esses algoritmos de criptografia não oferecem tanta garantia de segurança como equivalentes mais modernas. Criptografia de algoritmos de hash <xref:System.Security.Cryptography.SHA1> e <xref:System.Security.Cryptography.RIPEMD160> fornecem menos resistência a colisão de mais moderno de algoritmos de hash. O algoritmo de criptografia <xref:System.Security.Cryptography.TripleDES> fornece menos bits de segurança que algoritmos de criptografia mais modernos.

## <a name="rule-description"></a>Descrição da regra

Algoritmos de criptografia fraca e funções de hash são usadas atualmente por uma série de motivos, mas não deve ser usados para garantir a confidencialidade dos dados que eles protegem.

A regra dispara quando ele localiza o 3DES, SHA1 ou RIPEMD160 algoritmos no código e gera um aviso ao usuário.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Use opções criptograficamente mais fortes:

- Para criptografia TripleDES, use <xref:System.Security.Cryptography.Aes> criptografia.

- Para funções de hash SHA1 ou RIPEMD160, use os dos [SHA-2](/windows/desktop/SecCrypto/hash-and-signature-algorithms) família (por exemplo, <xref:System.Security.Cryptography.SHA512>, <xref:System.Security.Cryptography.SHA384>, <xref:System.Security.Cryptography.SHA256>).

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Suprima um aviso nessa regra, quando o nível de proteção necessário para os dados não requer uma garantia de segurança.

## <a name="pseudo-code-examples"></a>Exemplos de código pseudo

No momento da redação deste artigo, o exemplo de pseudocódigo a seguir ilustra o padrão de detectadas por essa regra.

### <a name="sha-1-hashing-violation"></a>Violação de hash SHA-1

```csharp
using System.Security.Cryptography;
...
var hashAlg = SHA1.Create();
```

Solução:

```csharp
using System.Security.Cryptography;
...
var hashAlg = SHA256.Create();
```

### <a name="ripemd160-hashing-violation"></a>RIPEMD160 Violação de hash

```csharp
using System.Security.Cryptography;
...
var hashAlg = RIPEMD160Managed.Create();
```

Solução:

```csharp
using System.Security.Cryptography;
...
var hashAlg = SHA256.Create();
```

### <a name="tripledes-encryption-violation"></a>Violação de criptografia TripleDES

```csharp
using System.Security.Cryptography;
...
using (TripleDES encAlg = TripleDES.Create())
{
  ...
}
```

Solução:

```csharp
using System.Security.Cryptography;
...
using (AesManaged encAlg = new AesManaged())
{
  ...
}
```