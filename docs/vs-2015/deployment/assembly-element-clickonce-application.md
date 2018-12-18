---
title: '&lt;assembly&gt; elemento (aplicativo ClickOnce) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#assembly
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <assembly> element [ClickOnce application manifest]
ms.assetid: 51410569-10f9-4c0a-96b5-d39185edbefc
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 44437c0ff78c5f957a0d774530e8911513ba0fd6
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49191770"
---
# <a name="ltassemblygt-element-clickonce-application"></a>&lt;assembly&gt; elemento (aplicativo ClickOnce)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O elemento de nível superior para o manifesto do aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
      <assembly  
   manifestVersion  
/>  
```  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 O `assembly` elemento é o elemento raiz e é necessário. O primeiro elemento independente deve ser um `assemblyIdentity` elemento. Os elementos do manifesto devem estar em um dos seguintes namespaces:  
  
 `urn:schemas-microsoft-com:asm.v1`  
  
 `urn:schemas-microsoft-com:asm.v2`  
  
 `http://www.w3.org/2000/09/xmldsig#`  
  
 Elementos filho do assembly também devem ser nesses namespaces, por herança ou marcação.  
  
 O `assembly` elemento tem o seguinte atributo.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`manifestVersion`|Necessário. O `manifestVersion` atributo deve ser definido como `1.0`.|  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir ilustra uma `assembly` elemento em um manifesto de aplicativo para um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo. Este exemplo de código é parte de um exemplo maior fornecido no [manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md).  
  
```  
<asmv1:assembly   
  xsi:schemaLocation="urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd"   
  manifestVersion="1.0"   
  xmlns:asmv3="urn:schemas-microsoft-com:asm.v3"  
  xmlns:dsig=http://www.w3.org/2000/09/xmldsig#  
  xmlns:co.v2="urn:schemas-microsoft-com:clickonce.v2"  
  xmlns="urn:schemas-microsoft-com:asm.v2"  
  xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"  
  xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"  
  xmlns:xsi=http://www.w3.org/2001/XMLSchema-instance  
  xmlns:co.v1="urn:schemas-microsoft-com:clickonce.v1">  
```  
  
## <a name="see-also"></a>Consulte também  
 [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)   
 [\<assembly > elemento](../deployment/assembly-element-clickonce-deployment.md)



