---
title: CA5351 Não usar algoritmos de criptografia | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 483f51b3-e186-4433-b48e-5ca24a9a9c94
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 7067d1d08be6de121986c60ead67086a11548ea8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49889809"
---
# <a name="ca5351-do-not-use-broken-cryptographic-algorithms"></a>CA5351 não use algoritmos de criptografia desfeitos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||  
|-|-|  
|NomeDoTipo|DoNotUseBrokenCryptographicAlgorithms|  
|CheckId|CA5351|  
|Categoria|Microsoft.Cryptography|  
|Alteração Significativa|Não separável|  
  
> [!NOTE]
>  Esse aviso foi atualizado pela última vez em novembro de 2015.  
  
## <a name="cause"></a>Causa  
 Funções de hash, como <xref:System.Security.Cryptography.MD5> e algoritmos de criptografia, como <xref:System.Security.Cryptography.DES> e <xref:System.Security.Cryptography.RC2> pode expor um risco significativo e pode resultar na exposição de informações confidenciais por meio de técnicas de ataque trivial, como ataques de força bruta e colisões de hash.  
  
 A lista de algoritmos de criptografia a seguir estão sujeitos a ataques de criptografia conhecidos. O algoritmo de hash criptográfico <xref:System.Security.Cryptography.MD5> está sujeita a ataques de colisão de hash.  Dependendo do uso, uma colisão de hash pode levar a representação, violação ou outros tipos de ataques em sistemas que contam com a saída de criptografia exclusiva de uma função de hash. Os algoritmos de criptografia <xref:System.Security.Cryptography.DES> e <xref:System.Security.Cryptography.RC2> estão sujeitas a ataques de criptografia que pode resultar na divulgação não intencional de dados criptografados.  
  
## <a name="rule-description"></a>Descrição da Regra  
 Dividido criptográfico algoritmos não são considerados seguros e seu uso deve ser desencorajado. O algoritmo de hash MD5 é suscetível a ataques conhecidos de colisão, embora a vulnerabilidade específica variará com base no contexto de uso.  Algoritmos de hash usados para garantir a integridade de dados (por exemplo, a assinatura do arquivo ou o certificado digital) são especialmente vulneráveis.  Nesse contexto, os invasores poderiam gerar duas partes separadas de dados, de modo que os dados benignos podem ser substituídos com dados mal-intencionados, sem alterar o valor de hash ou invalidar uma assinatura digital associada.  
  
 Para os algoritmos de criptografia:  
  
- <xref:System.Security.Cryptography.DES> criptografia contém um pequeno tamanho de chave, que pode ser por força bruta em menos de um dia.  
  
- <xref:System.Security.Cryptography.RC2> a criptografia é suscetível a um ataque de chave relacionados, em que o invasor localiza matemáticas relações entre todos os valores de chave.  
  
  Essa regra dispara quando ele encontra qualquer uma das funções criptográficas acima no código-fonte e gera um aviso ao usuário.  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Use opções criptograficamente mais fortes:  
  
-   Para o MD5, use hashes na [SHA-2](https://msdn.microsoft.com/en-us/library/windows/desktop/aa382459.aspx) família (por exemplo, <xref:System.Security.Cryptography.SHA512>, <xref:System.Security.Cryptography.SHA384>, <xref:System.Security.Cryptography.SHA256>).  
  
-   Para DES e RC2, use <xref:System.Security.Cryptography.Aes> criptografia.  
  
## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos  
 Não suprima um aviso nessa regra, a menos que é examinada por um especialista em criptografia.  
  
## <a name="pseudo-code-example"></a>Exemplo de pseudocódigo  
 O exemplo de pseudocódigo a seguir ilustra o padrão detectado por essa regra e alternativas possíveis.  
  
### <a name="md5-hashing-violation"></a>MD5 Violação de hash  
  
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
  
### <a name="rc2-encryption-violation"></a>RC2 Violação de criptografia  
  
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