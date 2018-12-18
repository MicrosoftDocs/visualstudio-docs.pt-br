---
title: '&lt;personalização&gt; elemento (desenvolvimento do Office no Visual Studio)'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <customization> element
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 1f1344b69aaf098f766aeafddfd23cea84d1a981
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669957"
---
# <a name="ltcustomizationgt-element-office-development-in-visual-studio"></a>&lt;personalização&gt; elemento (desenvolvimento do Office no Visual Studio)
  O `customization` elemento o `vstov4` namespace descreve uma solução específica do Office. Os elementos filho são diferentes para personalizações no nível de documento e suplementos do VSTO.  
  
## <a name="syntax-for-document-level-customizations"></a>Sintaxe para personalizações no nível do documento  
  
```xml
<customization  
  id  
  <document  
    solutionId  
  />  
</customization>  
```  
  
## <a name="syntax-for-vsto-add-ins"></a>Sintaxe para suplementos VSTO  
  
```xml
<customization  
  id  
  <appAddin  
    application  
    loadBehavior  
    keyName>  
  <friendlyName></friendlyName>  
  <description></description>  
  <formRegions></formRegions>  
</customization>  
```  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 O `customization` elemento contém informações específicas de personalização. Esse elemento deve estar no seguinte namespace: `vstov4=urn:schemas-microsoft-com:vsto.v4`. Há um `customization` elemento para cada solução do Office. Por exemplo, se você implantar três soluções do Office em uma implantação de vários projeto, há três `customization` elementos no manifesto do aplicativo.  
  
 Elementos filho do assembly devem ser também neste namespace.  
  
 O `customization` elemento tem o seguinte atributo.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`id`|Necessário para a implantação de vários projeto. O `id` elemento identifica exclusivamente uma solução do Office.|  
  
### <a name="document-level-customizations"></a>Personalizações no nível do documento  
 O `customization` elemento tem o seguinte elemento filho.  
  
#### <a name="document"></a>documento  
 O `document` elemento na `vstov4` namespace está definido no [ &#60;documentos&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/document-element-office-development-in-visual-studio.md).  
  
### <a name="vsto-add-ins"></a>Suplementos do VSTO  
 O `customization` elemento tem o seguinte elemento filho.  
  
#### <a name="appaddin"></a>appAddin  
 O `appAddin` elemento na `vstov4` namespace está definido no [ &#60;appAddin&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/appaddin-element-office-development-in-visual-studio.md).  
  
## <a name="example-of-a-document-level-customization"></a>Exemplo de uma personalização no nível de documento  
  
### <a name="description"></a>Descrição  
 O exemplo de código a seguir ilustra o `customization` elemento para uma personalização no nível de documento. Este exemplo de código é parte de um exemplo maior fornecido no [manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).  
  
### <a name="code"></a>Código  
  
```xml
<vstov4:customization>  
  <vstov4:document   
    solutionId="73e" />  
</vstov4:customization>  
```  
  
## <a name="example-of-a-vsto-add-in"></a>Exemplo de um suplemento do VSTO  
  
### <a name="description"></a>Descrição  
 O exemplo de código a seguir ilustra o `customization` elemento para um suplemento do VSTO. Isso é um Add-in do VSTO do Outlook que inclui as regiões do formulário. Este exemplo de código é parte de um exemplo maior fornecido no [manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).  
  
### <a name="code"></a>Código  
  
```xml  
<vstov4:customization>  
  <vstov4:appAddIn   
    application="Outlook"   
    loadBehavior="3"   
    keyName="ContosoOutlookAddIn">  
    <vstov4:friendlyName>  
      ContosoOutlookAddIn  
    </vstov4:friendlyName>  
    <vstov4:description>  
      ContosoOutlookAddIn - Outlook VSTO Add-in   
      created with Visual Studio Tools for Office  
    </vstov4:description>  
    <vstov4:formRegions>  
      <vstov4:formRegion  
          name="OutlookAddIn1.FormRegion1">  
        <vstov4:messageClass name="IPM.Note" />  
        <vstov4:messageClass name="IPM.Contact" />  
        <vstov4:messageClass name="IPM.Appointment" />  
      </vstov4:formRegion>  
    </vstov4:formRegions>  
  </vstov4:appAddIn>  
</vstov4:customization>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)   
 [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)   
 [Manifesto do aplicativo ClickOnce](/visualstudio/deployment/clickonce-application-manifest)  
  
  