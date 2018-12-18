---
title: '&lt;vstoRuntime&gt; elemento (desenvolvimento do Office no Visual Studio)'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <vstoRuntime> element
- <vstoRuntime> element
- vstoRuntime element
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: d21e097c0a05dfba2aa15bc41e37441ae02a63e4
ms.sourcegitcommit: 4cd4aef53e7035d23e7d1d0f66f51ac8480622a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34768060"
---
# <a name="ltvstoruntimegt-element-office-development-in-visual-studio"></a>&lt;vstoRuntime&gt; elemento (desenvolvimento do Office no Visual Studio)
  O `vstoRuntime` elemento o `vstav3` namespace contém uma versão com suporte do Visual Studio Tools para Office runtime para uma determinada solução do Office.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<vstoRuntime  
    release  
    version  
    supportUrl />  
```  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 O `vstoRuntime` elemento é necessário e está no `vstav3` namespace. Se uma solução do Office oferece suporte a duas versões do Visual Studio Tools para Office runtime, há dois `vstoRuntime` elementos no manifesto do aplicativo.  
  
 O `vstoRuntime` elemento tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`release`|Necessário. A versão de lançamento do Visual Studio Tools para Office runtime.|  
|`version`|Necessário. Número de versão do Visual Studio Tools para Office runtime.|  
|`supportUrl`|Opcional. Link para o local de instalação do Visual Studio Tools para Office runtime.|  
  
 `vstoRuntime` não tem elementos.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir ilustra o `vstoRuntime` elemento em um manifesto de aplicativo para uma solução do Office implantado usando [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]. Este exemplo de código é parte de um exemplo maior fornecido em [manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).  
  
```xml  
<vstav3:vstoRuntime  
    release="VSTOR40Beta1"  
    version="10.0.20303"  
    supportUrl="http://www.microsoft.com" />  
```  
  
## <a name="see-also"></a>Consulte também  
 [Manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)   
 [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)   
 [Manifesto do aplicativo ClickOnce](/visualstudio/deployment/clickonce-application-manifest)  
  
  