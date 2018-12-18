---
title: '&lt;appAddin&gt; elemento (desenvolvimento do Office no Visual Studio)'
titleSuffix: ''
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <appAddin> element
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: 3160f153bb6775cf5b2541abf4f75069c818f82b
ms.sourcegitcommit: 20c0991d737c540750c613c380cd4cf5bb07de51
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248066"
---
# <a name="ltappaddingt-element-office-development-in-visual-studio"></a>&lt;appAddin&gt; elemento (desenvolvimento do Office no Visual Studio)
  O **appAddin** elemento da `vstov4` namespace armazena informações de personalização específicas para suplementos do VSTO.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml 
<appAddin  
  application  
  loadBehavior  
  keyName>  
  <friendlyName>  
  <description>  
  <formRegions></formRegions>  
</appAddin>  
```  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 O **appAddin** elemento é necessário e está no `vstov4` namespace. Há apenas um **appAddin** elemento definido em um manifesto de aplicativo.  
  
 O **appAddin** elemento tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|**Aplicativo**|Necessário. Identifica o aplicativo do Microsoft Office. O valor pode ser um dos seguintes: Excel, InfoPath, Outlook, PowerPoint, Project, Visio ou Word.|  
|**LoadBehavior**|Opcional. Por padrão, o **loadBehavior** é habilitada ao definir esse valor como. Para depuração, o suplemento do VSTO pode ser desabilitado definindo o valor para dois. Para obter mais informações, consulte a tabela intitulada valores LoadBehavior [entradas do registro para suplementos VSTO](../vsto/registry-entries-for-vsto-add-ins.md).|  
|**keyName**|Necessário. Esse valor é o nome da chave do registro que será usado pelo aplicativo para carregar o suplemento do VSTO. Para obter mais informações, consulte [entradas do registro para suplementos VSTO](../vsto/registry-entries-for-vsto-add-ins.md).|  
  
 O **appAddin** elemento tem os seguintes elementos filho.  
  
### <a name="friendlyname"></a>Nome amigável  
 Opcional. O **friendlyName** elemento é explicado na [ &#60;friendlyName&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/friendlyname-element-office-development-in-visual-studio.md).  
  
### <a name="description"></a>descrição  
 Opcional. O **descrição** elemento é explicado na [ &#60;descrição&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/description-element-office-development-in-visual-studio.md).  
  
### <a name="formregions"></a>formRegions  
 Necessário apenas para Outlook suplementos do VSTO que incluem regiões de formulário. O **formRegions** elemento é explicado na [ &#60;formRegions&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/formregions-element-office-development-in-visual-studio.md).  
  
## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO  
  
### <a name="description"></a>Descrição  
 O exemplo de código a seguir ilustra **appAddin** elementos em uma solução do Outlook implantado usando [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]. Este exemplo de código é parte de um exemplo maior fornecido no [manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).  
  
### <a name="code"></a>Código  
  
```xml  
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
```  
  
## <a name="see-also"></a>Consulte também  
 [Manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)   
 [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)   
 [Manifesto do aplicativo ClickOnce](/visualstudio/deployment/clickonce-application-manifest)  
  
  