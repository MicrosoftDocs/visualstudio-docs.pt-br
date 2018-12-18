---
title: '&lt;publisherIdentity&gt; elemento (implantação do ClickOnce) | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- publisherIdentity Element [ClickOnce deployment manifest], introduction
- required element for signed manifests [ClickOnce], publisherIdentity Element
- publisherIdentity Element [ClickOnce deployment manifest], syntax, elements, and attributes
ms.assetid: 34c579db-d2f2-4b66-b9c8-47207f33d950
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f33772a35e8e47a77e0fdaddd28b7471ef5abcce
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39081404"
---
# <a name="ltpublisheridentitygt-element-clickonce-deployment"></a>&lt;publisherIdentity&gt; elemento (implantação do ClickOnce)
Contém informações sobre o editor que assinou o manifesto de implantação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<publisherIdentity  
   name  
   issuerKeyHash  
/>  
```  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 O `publisherIdentity` elemento é necessário para manifestos assinados. A tabela a seguir mostra os atributos que o `publisherIdentity` dá suporte ao elemento.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`name`|Necessário. Descreve a identidade da parte que publicou este aplicativo.|  
|`issuerKeyHash`|Necessário. Contém o hash SHA-1 da chave pública do emissor do certificado.|  
  
#### <a name="parameters"></a>Parâmetros  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/valor retornado  
  
## <a name="exceptions"></a>Exceções  
  
## <a name="remarks"></a>Comentários  
  
## <a name="requirements"></a>Requisitos  
  
## <a name="subhead"></a>Subtítulo