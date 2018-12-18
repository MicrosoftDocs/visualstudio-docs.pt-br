---
title: '&lt;assemblyIdentity&gt; elemento (aplicativo ClickOnce) | Microsoft Docs'
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
- <assemblyIdentity> element [ClickOnce application manifest]
ms.assetid: f48e9531-efac-4d11-8166-f63a5ece1ac5
caps.latest.revision: 22
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: d16fdf182845eb2ae916da95b7677112b968b60f
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49249035"
---
# <a name="ltassemblyidentitygt-element-clickonce-application"></a>&lt;assemblyIdentity&gt; elemento (aplicativo ClickOnce)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Identifica o aplicativo implantado em um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
      <assemblyIdentity   
   name  
   version  
   publicKeyToken  
   processorArchitecture  
   language  
/>  
```  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 O `assemblyIdentity` elemento é necessário. Ele não contém nenhum elemento filho e tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Name`|Necessário. Identifica o nome do aplicativo.<br /><br /> Se `Name` contiver caracteres especiais, como aspas simples ou duplas, o aplicativo poderá falhar ao ativar.|  
|`Version`|Necessário. Especifica o número de versão do aplicativo no seguinte formato: `major.minor.build.revision`|  
|`publicKeyToken`|Opcional. Especifica uma cadeia hexadecimal de 16 caracteres que representa os últimos 8 bytes do `SHA-1` valor de hash da chave pública sob a qual o aplicativo ou assembly é assinado. A chave pública que é usada para assinar o catálogo deve ser de 2048 bits ou superior.<br /><br /> Embora a assinar um assembly é opcional mas recomendado, esse atributo é necessário. Se um assembly estiver assinado, você deve copiar um valor de um assembly autoassinado ou use um valor "fictício" de todos os zeros.|  
|`processorArchitecture`|Necessário. Especifica o processador. Os valores válidos são `msil` de todos os processadores, `x86` para Windows de 32 bits `IA64` para Windows de 64 bits, e `Itanium` para processadores de 64 bits Intel Itanium.|  
|`language`|Necessário. Identifica os códigos de idioma de duas partes (por exemplo, `en-US`) do assembly. Elemento o `asmv2` namespace. Se não for especificado, o padrão é `neutral`.|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="description"></a>Descrição  
 O exemplo de código a seguir ilustra uma `assemblyIdentity` elemento em um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifesto do aplicativo. Este exemplo de código é parte de um exemplo maior fornecido no [manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md).  
  
### <a name="code"></a>Código  
  
```  
<asmv1:assemblyIdentity   
  name="My Application Deployment.exe"   
  version="1.0.0.0"   
  publicKeyToken="43cb1e8e7a352766"   
  language="neutral"   
  processorArchitecture="x86"   
  type="win32" />  
```  
  
## <a name="see-also"></a>Consulte também  
 [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)   
 [\<assemblyIdentity > elemento](../deployment/assemblyidentity-element-clickonce-deployment.md)



