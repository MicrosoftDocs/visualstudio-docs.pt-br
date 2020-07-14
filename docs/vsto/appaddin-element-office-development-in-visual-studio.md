---
title: '&lt;&gt;elemento appAddin (desenvolvimento do Office no Visual Studio)'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <appAddin> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1bf9ea990d12bd24adee3f6a24a39fa43c74fb71
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85531632"
---
# <a name="ltappaddingt-element-office-development-in-visual-studio"></a>&lt;&gt;elemento appAddin (desenvolvimento do Office no Visual Studio)
  O elemento **appAddin** do `vstov4` namespace armazena informações específicas de personalização para suplementos do VSTO.

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
 O elemento **appAddin** é necessário e está no `vstov4` namespace. Há apenas um elemento **appAddin** definido em um manifesto do aplicativo.

 O elemento **appAddin** tem os atributos a seguir.

|Atributo|Descrição|
|---------------|-----------------|
|**aplicativo**|Obrigatórios. Identifica o aplicativo Microsoft Office. O valor pode ser um dos seguintes: Excel, InfoPath, Outlook, PowerPoint, Project, Visio ou Word.|
|**LoadBehavior**|Opcional. Por padrão, o **LoadBehavior** é habilitado definindo esse valor como. Para depuração, o suplemento do VSTO pode ser desabilitado definindo o valor como dois. Para obter mais informações, consulte a tabela denominada valores de LoadBehavior em [entradas do registro para suplementos do VSTO](../vsto/registry-entries-for-vsto-add-ins.md).|
|**keyName**|Obrigatórios. Esse valor é o nome da chave do registro que será usado pelo aplicativo para carregar o suplemento do VSTO. Para obter mais informações, consulte [entradas do registro para suplementos do VSTO](../vsto/registry-entries-for-vsto-add-ins.md).|

 O elemento **appAddin** tem os seguintes elementos filho.

### <a name="friendlyname"></a>friendlyName
 Opcional. O elemento **FriendlyName** é explicado no [elemento&#60;friendlyname&#62; &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/friendlyname-element-office-development-in-visual-studio.md).

### <a name="description"></a>descrição
 Opcional. O elemento **Description** é explicado em [&#60;descrição&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/description-element-office-development-in-visual-studio.md).

### <a name="formregions"></a>formRegions
 Necessário apenas para os suplementos do VSTO do Outlook que incluem regiões de formulário. O elemento **FormRegions** é explicado no [elemento&#60;FormRegions&#62; &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/formregions-element-office-development-in-visual-studio.md).

## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra os elementos **appAddin** em uma solução do Outlook implantada usando o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] . Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

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

## <a name="see-also"></a>Confira também

- [Manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)
- [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)