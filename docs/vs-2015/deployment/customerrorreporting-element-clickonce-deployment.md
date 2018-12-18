---
title: '&lt;customErrorReporting&gt; elemento (implantação do ClickOnce) | Microsoft Docs'
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
- <customErrorReporting> element [ClickOnce deployment manifest]
ms.assetid: 7d31816e-c692-46b5-9cc9-753284b3bcda
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: cf4a723fe5986287859134d0f97868a19956f5a9
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49252012"
---
# <a name="ltcustomerrorreportinggt-element-clickonce-deployment"></a>&lt;customErrorReporting&gt; elemento (implantação do ClickOnce)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Especifica um URI para mostrar quando ocorre um erro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<customErrorReporting  
   uri  
/>  
```  
  
## <a name="remarks"></a>Comentários  
 Esse elemento é opcional. Sem ele, [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] exibe uma caixa de diálogo de erro que mostra a pilha de exceção. Se o `customErrorReporting` elemento estiver presente, [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] em vez disso, exibirá o URI indicado pelo `uri` parâmetro. O URI de destino incluirá a classe de exceção externa, a classe de exceção interna e a mensagem de exceção interna como parâmetros.  
  
 Use esse elemento para adicionar funcionalidade ao seu aplicativo de relatório de erros. Uma vez que o URI gerado inclui informações sobre o tipo de erro, seu site da Web pode analisar esse informações e exibição, por exemplo, uma tela de solução de problemas apropriada.  
  
## <a name="example"></a>Exemplo  
 O trecho de código a seguir mostra o `customErrorReporting` elemento, junto com o URI gerado, ele pode produzir.  
  
```  
<customErrorReporting uri=http://www.contoso.com/applications/error.asp />  
  
Example Generated Error:  
http://www.contoso.com/applications/error.asp? outer=System.Deployment.Application.InvalidDeploymentException&&inner=System.Deployment.Application.InvalidDeploymentException&&msg=The%20application%20manifest%20is%20signed,%20but%20the%20deployment%20manifest%20is%20unsigned.%20Both%20manifests%20must%20be%20either%20signed%20or%20unsigned.  
```  
  
## <a name="see-also"></a>Consulte também  
 [Manifesto de implantação do ClickOnce](../deployment/clickonce-deployment-manifest.md)



