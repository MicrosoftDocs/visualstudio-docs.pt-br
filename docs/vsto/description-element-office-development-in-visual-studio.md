---
title: '&lt;Descrição&gt; elemento (desenvolvimento do Office no Visual Studio)'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- description element
- <description> element
- application manifests [Office development in Visual Studio], <description> element
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9fcdac1e950d98394b5703322f40dd1823b246f6
ms.sourcegitcommit: 209c2c068ff0975994ed892b62aa9b834a7f6077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34265109"
---
# <a name="ltdescriptiongt-element-office-development-in-visual-studio"></a>&lt;Descrição&gt; elemento (desenvolvimento do Office no Visual Studio)
  O `description` elemento o `vstov4` namespace armazena a descrição para a solução do Office que aparece na caixa de diálogo COM os suplementos de aplicativos do Microsoft Office.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<description>  
</description>  
```  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 Opcional. O `description` elemento o `vstov4` namespace. Ele contém a descrição do que o suplemento que aparece na caixa de diálogo COM os suplementos de aplicativos do Microsoft Office.  
  
 O `description` elemento não tem atributos ou elementos.  
  
## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO  
  
### <a name="description"></a>Descrição  
 O exemplo de código a seguir ilustra o `description` elemento para uma solução de nível de aplicativo implantado usando [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]. Este exemplo de código é parte de um exemplo maior fornecido em [manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).  
  
### <a name="code"></a>Código  
  
```xml  
<vstov4:description>  
  ContosoOutlookAddIn - Outlook add-in   
  created with Visual Studio Tools for Office  
</vstov4:description>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)   
 [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)   
 [Manifesto do aplicativo ClickOnce](/visualstudio/deployment/clickonce-application-manifest)  
  
  