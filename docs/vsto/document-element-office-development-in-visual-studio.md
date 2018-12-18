---
title: '&lt;documento&gt; elemento (desenvolvimento do Office no Visual Studio)'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- document element
- application manifests [Office development in Visual Studio], <document> element
- <document> element
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 07d8172ec4e56352c2244aef02d947ac48833ab7
ms.sourcegitcommit: 1466ac0f49ebf7448ea4507ae3f79acb25d51d3e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34447329"
---
# <a name="ltdocumentgt-element-office-development-in-visual-studio"></a>&lt;documento&gt; elemento (desenvolvimento do Office no Visual Studio)
  O `document` elemento o `vstov4` namespace armazena informações específicas de personalização para personalizações no nível do documento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<document solutionId />  
```  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 Necessário apenas para personalizações no nível do documento. O `document` elemento o `vstov4` namespace. O `document` elemento tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`solutionId`|Necessário. O GUID usado pelo Visual Studio Tools para Office runtime para identificar exclusivamente uma solução de nível de documento. Esse valor é armazenado como propriedade assemblylocation personalizada de documento. Para obter mais informações, consulte [visão geral de propriedades de documento personalizadas](../vsto/custom-document-properties-overview.md).|  
  
 `document` não possui elementos filho.  
  
## <a name="document-level-customization-example"></a>Exemplo de personalização de nível de documento  
  
### <a name="description"></a>Descrição  
 O exemplo de código a seguir ilustra o `document` elemento em uma solução de nível de documento implantado usando [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]. Este exemplo de código é parte de um exemplo maior fornecido em [manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).  
  
### <a name="code"></a>Código  
  
```xml
<vstov4:document   
  solutionId="73e" />  
```  
  
## <a name="see-also"></a>Consulte também  
 [Manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)   
 [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)   
 [Manifesto do aplicativo ClickOnce](/visualstudio/deployment/clickonce-application-manifest)  
  
  