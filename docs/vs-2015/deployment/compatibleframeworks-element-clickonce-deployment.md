---
title: '&lt;compatibleFrameworks&gt; elemento (implantação do ClickOnce) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <compatibleFrameworks> element [ClickOnce deployment manifest]
ms.assetid: f6c3ee55-9e65-403d-8664-3ebde872c7d4
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 051fd3eea0ffab2a7c5f088538d7208c8286d1d6
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49176575"
---
# <a name="ltcompatibleframeworksgt-element-clickonce-deployment"></a>&lt;compatibleFrameworks&gt; elemento (implantação do ClickOnce)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Identifica as versões do .NET Framework em que este aplicativo pode instalar e executar.  
  
> [!NOTE]
>  [MageUI.exe](http://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14) não oferece suporte a `compatibleFrameworks` elemento ao salvar um manifesto de aplicativo que já foi assinado com um certificado usando [MageUI.exe](http://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14). Em vez disso, você deve usar [Mage.exe](http://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<compatibleFrameworks  
      SupportUrl>   
   <framework  
      targetVersion  
      profile  
      supportedRuntime  
   />   
</ compatibleFrameworks>  
```  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 O `compatibleFrameworks` elemento é necessário para manifestos de implantação que se destinam a [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] tempo de execução fornecido pelo [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] ou posterior. O `compatibleFrameworks` elemento contém um ou mais `framework` elementos que especificam as versões do .NET Framework em que esse aplicativo pode ser executado. O [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] tempo de execução executará o aplicativo na primeira disponível `framework` nessa lista.  
  
 A tabela a seguir lista o atributo que o `compatibleFrameworks` dá suporte ao elemento.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`S` `upportUrl`|Opcional. Especifica uma URL em que a versão do .NET Framework compatível preferida pode ser baixada.|  
  
## <a name="framework"></a>estrutura  
 Necessário. A tabela a seguir lista os atributos que o `framework` dá suporte ao elemento.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`targetVersion`|Necessário. Especifica o número de versão do .NET Framework de destino.|  
|`profile`|Necessário. Especifica o perfil de destino do .NET Framework.|  
|`supportedRuntime`|Necessário. Especifica o número de versão do tempo de execução associado com o .NET Framework de destino.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="example"></a>Exemplo  
 O seguinte exemplo de código mostra uma `compatibleFrameworks` elemento em um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifesto de implantação. Essa implantação pode ser executado no [!INCLUDE[net_client_v40_long](../includes/net-client-v40-long-md.md)]. Ele também pode ser executado nos [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] porque ele é um superconjunto do [!INCLUDE[net_client_v40_long](../includes/net-client-v40-long-md.md)].  
  
```  
<compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">  
  <framework   
      targetVersion="4.0"   
      profile="Client"   
      supportedRuntime="4.0.30319" />  
</compatibleFrameworks>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Manifesto de implantação do ClickOnce](../deployment/clickonce-deployment-manifest.md)



