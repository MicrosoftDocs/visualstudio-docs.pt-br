---
title: '&lt;Assinatura&gt; elemento (implantação do ClickOnce) | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <Signature> element [ClickOnce deployment manifest]
ms.assetid: c99b07ad-e8ba-43f2-b0d6-3745e7a7c8b3
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ab91a8dea24c37c58fceddce32eadabca4e11e7d
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53858033"
---
# <a name="ltsignaturegt-element-clickonce-deployment"></a>&lt;Assinatura&gt; elemento (implantação do ClickOnce)
Contém as informações necessárias para assinar digitalmente o manifesto de implantação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
      <Signature>   
   XML signature information   
</Signature>  
```  
  
## <a name="remarks"></a>Comentários  
 Assinar um manifesto de implantação usando uma assinatura do envelope é opcional mas recomendado. Para obter mais informações sobre como assinar arquivos XML, consulte a World Wide Web Consortium recomendação, "Sintaxe e processamento de assinatura XML," descrita em [ http://www.w3.org/TR/xmldsig-core/ ](http://www.w3.org/TR/xmldsig-core/).  
  
 Se você desejar assinar seu manifesto, hashes devem ser fornecidos para todos os arquivos. Um manifesto com arquivos que não são transformadas em hash não pode ser assinado, porque os usuários não é possível verificar o conteúdo dos arquivos sem hash.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir ilustra uma `Signature` elemento em um manifesto de implantação usado em um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação.  
  
```xml  
<Signature xmlns="http://www.w3.org/2000/09/xmldsig#">  
  <SignedInfo>  
    <CanonicalizationMethod Algorithm=  
           "http://www.w3.org/TR/2001/REC-xml-c14n-20010315" />  
    <SignatureMethod Algorithm=  
           "http://www.w3.org/2000/09/xmldsig#rsa-sha1" />  
    <Reference URI="">  
      <Transforms>  
        <Transform Algorithm=  
           "http://www.w3.org/2000/09/xmldsig#enveloped-signature" />  
      </Transforms>  
      <DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />  
      <DigestValue>d2z5AE...</DigestValue>  
    </Reference>  
  </SignedInfo>  
  <SignatureValue>  
4PHj6SaopoLp...  
  </SignatureValue>  
  <KeyInfo>  
    <X509Data>  
      <X509Certificate>  
MIIHnTCCBoWgAwIBAgIKJY9+nwAHAAB...  
      </X509Certificate>  
    </X509Data>  
  </KeyInfo>  
</Signature>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Manifesto de implantação do ClickOnce](../deployment/clickonce-deployment-manifest.md)