---
title: '&lt;&gt;elemento Customization (desenvolvimento do Office no Visual Studio)'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <customization> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1239c6749f25bf4bce7a1f5cc89a2a8430c98a4d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544866"
---
# <a name="ltcustomizationgt-element-office-development-in-visual-studio"></a>&lt;&gt;elemento Customization (desenvolvimento do Office no Visual Studio)
  O `customization` elemento do `vstov4` namespace descreve uma solução específica do Office. Os elementos filho são diferentes para as personalizações em nível de documento e os suplementos do VSTO.

## <a name="syntax-for-document-level-customizations"></a>Sintaxe para personalizações em nível de documento

```xml
<customization
  id
  <document
    solutionId
  />
</customization>
```

## <a name="syntax-for-vsto-add-ins"></a>Sintaxe para suplementos do VSTO

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
 O `customization` elemento contém informações específicas de personalização. Esse elemento deve estar no seguinte namespace: `vstov4=urn:schemas-microsoft-com:vsto.v4` . Há um `customization` elemento para cada solução do Office. Por exemplo, se você implantar três soluções do Office em uma implantação de vários projetos, haverá três `customization` elementos no manifesto do aplicativo.

 Os elementos filho do assembly também devem estar nesse namespace.

 O `customization` elemento tem o atributo a seguir.

|Atributo|Descrição|
|---------------|-----------------|
|`id`|Necessário para implantação de vários projetos. O `id` elemento identifica exclusivamente uma solução do Office.|

### <a name="document-level-customizations"></a>Personalizações em nível de documento
 O `customization` elemento tem o seguinte elemento filho.

#### <a name="document"></a>documento
 O `document` elemento no `vstov4` namespace é definido em [&#60;elemento&#62; de documento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/document-element-office-development-in-visual-studio.md).

### <a name="vsto-add-ins"></a>Suplementos do VSTO
 O `customization` elemento tem o seguinte elemento filho.

#### <a name="appaddin"></a>appAddin
 O `appAddin` elemento no `vstov4` namespace é definido no [elemento&#60;appAddin&#62; &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/appaddin-element-office-development-in-visual-studio.md).

## <a name="example-of-a-document-level-customization"></a>Exemplo de uma personalização no nível do documento

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra o `customization` elemento para uma personalização em nível de documento. Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

### <a name="code"></a>Código

```xml
<vstov4:customization>
  <vstov4:document
    solutionId="73e" />
</vstov4:customization>
```

## <a name="example-of-a-vsto-add-in"></a>Exemplo de um suplemento do VSTO

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra o `customization` elemento para um suplemento do VSTO. Este é um suplemento do VSTO do Outlook que inclui regiões de formulário. Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

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

- [Manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)
- [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)