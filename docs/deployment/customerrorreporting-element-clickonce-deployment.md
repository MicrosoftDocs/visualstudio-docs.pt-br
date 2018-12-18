---
title: '&lt;customErrorReporting&gt; elemento (implantação do ClickOnce) | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <customErrorReporting> element [ClickOnce deployment manifest]
ms.assetid: 7d31816e-c692-46b5-9cc9-753284b3bcda
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c060c419fa72bb5914491a8ee666a9b1a2c6a622
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39080347"
---
# <a name="ltcustomerrorreportinggt-element-clickonce-deployment"></a>&lt;customErrorReporting&gt; elemento (implantação do ClickOnce)
Especifica um URI para mostrar quando ocorre um erro.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<customErrorReporting  
   uri  
/>  
```  
  
## <a name="remarks"></a>Comentários  
 Esse elemento é opcional. Sem ele, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] exibe uma caixa de diálogo de erro que mostra a pilha de exceção. Se o `customErrorReporting` elemento estiver presente, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] em vez disso, exibirá o URI indicado pelo `uri` parâmetro. O URI de destino incluirá a classe de exceção externa, a classe de exceção interna e a mensagem de exceção interna como parâmetros.  
  
 Use esse elemento para adicionar funcionalidade ao seu aplicativo de relatório de erros. Uma vez que o URI gerado inclui informações sobre o tipo de erro, seu site da Web pode analisar esse informações e exibição, por exemplo, uma tela de solução de problemas apropriada.  
  
## <a name="example"></a>Exemplo  
 O trecho de código a seguir mostra o `customErrorReporting` elemento, junto com o URI gerado, ele pode produzir.  
  
```xml
<customErrorReporting uri=http://www.contoso.com/applications/error.asp />  
  
Example Generated Error:  
http://www.contoso.com/applications/error.asp? outer=System.Deployment.Application.InvalidDeploymentException&&inner=System.Deployment.Application.InvalidDeploymentException&&msg=The%20application%20manifest%20is%20signed,%20but%20the%20deployment%20manifest%20is%20unsigned.%20Both%20manifests%20must%20be%20either%20signed%20or%20unsigned.  
```  
  
## <a name="see-also"></a>Consulte também  
 [Manifesto de implantação do ClickOnce](../deployment/clickonce-deployment-manifest.md)