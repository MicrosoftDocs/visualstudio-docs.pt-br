---
title: '&lt;assemblyIdentity&gt; elemento (implantação do ClickOnce) | Microsoft Docs'
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
- urn:schemas-microsoft-com:asm.v2#assemblyIdentity
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <assemblyIdentity> element [ClickOnce deployment manifest]
ms.assetid: f4a3bb83-c800-47d0-9905-9a5ae2486838
caps.latest.revision: 25
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 157ad7bb43ae7eb164d7c58edb79f51df3da5dcd
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49195098"
---
# <a name="ltassemblyidentitygt-element-clickonce-deployment"></a>&lt;assemblyIdentity&gt; elemento (implantação do ClickOnce)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Identifica o assembly principal da [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
      <assemblyIdentity    
   name   
   version  
   publicKeyToken  
   processorArchitecture  
    type  
/>  
```  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 O `assemblyIdentity` elemento é necessário. Ele não contém nenhum elemento filho e tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`name`|Necessário. Identifica o nome legível por humanos da implantação para fins informativos.<br /><br /> Se `name` contiver caracteres especiais, como aspas simples ou duplas, o aplicativo poderá falhar ao ativar.|  
|`version`|Necessário. Especifica o número de versão do assembly, no seguinte formato: `major.minor.build.revision`.<br /><br /> Esse valor deve ser incrementado em um manifesto atualizado para disparar uma atualização de aplicativo.|  
|`publicKeyToken`|Necessário. Especifica uma cadeia hexadecimal de 16 caracteres que representa os últimos 8 bytes do valor de hash SHA-1 da chave pública sob a qual o manifesto de implantação é assinado. A chave pública que é usada para assinar deve ser de 2048 bits ou superior.<br /><br /> Embora a assinar um assembly é opcional mas recomendado, esse atributo é necessário. Se um assembly estiver assinado, você deve copiar um valor de um assembly autoassinado ou use um valor "fictício" de todos os zeros.|  
|`processorArchitecture`|Necessário. Especifica o processador. Os valores válidos são `msil` de todos os processadores, `x86` para Windows de 32 bits `IA64` para Windows de 64 bits, e `Itanium` para processadores de 64 bits Intel Itanium.|  
|`type`|Necessário. Para compatibilidade com a tecnologia de instalação lado a lado do Windows. O único valor permitido é `win32`.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir ilustra uma `assemblyIdentity` elemento em um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifesto de implantação. Este exemplo de código é parte de um exemplo maior fornecido para o [manifesto de implantação do ClickOnce](../deployment/clickonce-deployment-manifest.md) tópico.  
  
```  
<!-- Identify the deployment. -->  
<assemblyIdentity   
  name="My Application Deployment.app"  
  version="1.0.0.0"  
  publicKeyToken="43cb1e8e7a352766"  
  language="neutral"  
  processorArchitecture="x86"  
  xmlns="urn:schemas-microsoft-com:asm.v1" />  
```  
  
## <a name="see-also"></a>Consulte também  
 [Manifesto de implantação do ClickOnce](../deployment/clickonce-deployment-manifest.md)   
 [\<assemblyIdentity > elemento](../deployment/assemblyidentity-element-clickonce-application.md)



