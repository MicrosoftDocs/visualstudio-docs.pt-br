---
title: CA5351 não usam algoritmos de criptografia desfeitos | Microsoft Docs
ms.date: 11/15/2016
ms.technology: vs-ide-code-analysis
ms.topic: reference
ms.assetid: 483f51b3-e186-4433-b48e-5ca24a9a9c94
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ad4698fe469176ae8ed590c44b4efbb4ccf39de2
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545048"
---
# <a name="ca5351-do-not-use-broken-cryptographic-algorithms"></a>CA5351 não use algoritmos de criptografia desfeitos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotUseBrokenCryptographicAlgorithms|
|CheckId|CA5351|
|Categoria|Microsoft. Cryptography|
|Alteração Significativa|Sem interrupção|

> [!NOTE]
> Esse aviso foi atualizado pela última vez em 2015 de novembro.

## <a name="cause"></a>Causa
 Funções de hash, como <xref:System.Security.Cryptography.MD5> e algoritmos de criptografia, como <xref:System.Security.Cryptography.DES> e <xref:System.Security.Cryptography.RC2> podem expor um risco significativo e podem resultar na exposição de informações confidenciais por meio de técnicas de ataque triviais, como ataques de força bruta e colisões de hash.

 A lista de algoritmos criptográficos a seguir está sujeita a ataques criptográficos conhecidos. O algoritmo de hash criptográfico <xref:System.Security.Cryptography.MD5> está sujeito a ataques de colisão de hash.  Dependendo do uso, uma colisão de hash pode levar à representação, violação ou outros tipos de ataques em sistemas que dependem da saída criptográfica exclusiva de uma função de hash. Os algoritmos de criptografia <xref:System.Security.Cryptography.DES> e <xref:System.Security.Cryptography.RC2> estão sujeitos a ataques criptográficos que podem resultar na divulgação não intencional de dados criptografados.

## <a name="rule-description"></a>Descrição da Regra
 Os algoritmos de criptografia desfeitos não são considerados seguros e seu uso deve ser desencorajado. O algoritmo de hash MD5 é suscetível a ataques de colisão conhecidos, embora a vulnerabilidade específica varie de acordo com o contexto de uso.  Os algoritmos de hash usados para garantir a integridade dos dados (por exemplo, assinatura de arquivo ou certificado digital) são particularmente vulneráveis.  Nesse contexto, os invasores poderiam gerar duas partes separadas de dados, de modo que os dados benignos possam ser substituídos por dados mal-intencionados, sem alterar o valor de hash ou invalidar uma assinatura digital associada.

 Para algoritmos de criptografia:

- <xref:System.Security.Cryptography.DES>a criptografia contém um tamanho de chave pequeno, que pode ser forçado por uma força bruta em menos de um dia.

- <xref:System.Security.Cryptography.RC2>a criptografia é suscetível a um ataque de chave relacionada, em que o invasor encontra relações matemáticas entre todos os valores de chave.

  Essa regra é disparada quando encontra qualquer uma das funções criptográficas acima no código-fonte e gera um aviso ao usuário.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Use opções criptograficamente mais fortes:

- Para MD5, use hashes na família [SHA-2](https://msdn.microsoft.com/library/windows/desktop/aa382459.aspx) (por exemplo <xref:System.Security.Cryptography.SHA512> ,, <xref:System.Security.Cryptography.SHA384> <xref:System.Security.Cryptography.SHA256> ).

- Para DES e RC2, use <xref:System.Security.Cryptography.Aes> criptografia.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprimir um aviso desta regra, a menos que ela tenha sido revisada por um especialista em criptografia.

## <a name="pseudo-code-example"></a>Exemplo de pseudo-código
 O exemplo de pseudocódigo a seguir ilustra o padrão detectado por essa regra e possíveis alternativas.

### <a name="md5-hashing-violation"></a>Violação de hash MD5

```
using System.Security.Cryptography;
...
var hashAlg = MD5.Create();

```

### <a name="solution"></a>Solução

```
using System.Security.Cryptography;
...
var hashAlg = SHA256.Create();

```

### <a name="rc2-encryption-violation"></a>Violação de criptografia RC2

```
using System.Security.Cryptography;
...
RC2 encAlg = RC2.Create();

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

### <a name="des-br-br-encryption-violation"></a>DES <br /><br />Violação de criptografia

```
using System.Security.Cryptography;
...
DES encAlg = DES.Create();

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