---
title: '&lt;&gt;elemento AddIn (desenvolvimento do Office no Visual Studio)'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <addIn> element
- addin element
- <addin> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: cf922799301aef67ee70c480dd9e0823382cbd47
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543761"
---
# <a name="ltaddingt-element-office-development-in-visual-studio"></a>&lt;&gt;elemento AddIn (desenvolvimento do Office no Visual Studio)
  O elemento **AddIn** do `vstav3` namespace contém informações específicas para Microsoft Office suplementos do VSTO e personalizações em nível de documento desenvolvidas com o Visual Studio.

## <a name="syntax"></a>Sintaxe

```xml
<addIn>
  <entryPointsCollection>
    <entryPoints>
      <entryPoint>
      </entryPoint>
    </entryPoints>
  </entryPointsCollection>
  <update></update>
  <postActions>
    <postAction>
      <postActionData>
      </postActionData>
    <postAction>
  </postActions>
  <application>
    <customization>
    </customization>
  </application
</addIn>
```

## <a name="elements-and-attributes"></a>Elementos e atributos
 O elemento **AddIn** do `vstav3` namespace contém informações sobre a solução do Office e o aplicativo Microsoft Office. Esse elemento deve estar no seguinte namespace: `vstav3=urn:schemas-microsoft-com:vsta.v3` . Os elementos filho também devem estar nesse namespace.

 O `addin` elemento não tem atributos.

 O `addin` elemento tem os seguintes elementos filho.

### <a name="entrypoints"></a>entryPoints
 Obrigatórios. O elemento **entryPoints** é descrito em [&#60;entryPoints&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/entrypoints-element-office-development-in-visual-studio.md).

### <a name="update"></a>atualizar
 Obrigatórios. O elemento **Update** é descrito em [&#60;elemento&#62; de atualização &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/update-element-office-development-in-visual-studio.md).

### <a name="postactions"></a>Ações
 Opcional. O elemento de **ações** é descrito em [&#60;ações&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/postactions-element-office-development-in-visual-studio.md).

### <a name="application"></a>aplicativo
 Obrigatórios. O elemento **Application** é descrito em [&#60;elemento&#62; de aplicativo &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/application-element-office-development-in-visual-studio.md).

## <a name="document-level-customization-example"></a>Exemplo de personalização no nível do documento

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra o elemento **AddIn** em uma solução do Office de nível de documento que é implantada usando o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] . Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

### <a name="code"></a>Código

```xml
<vstav3:addIn
  xmlns:vstav3="urn:schemas-microsoft-com:vsta.v3">
  <vstav3:entryPointsCollection>
    <vstav3:entryPoints>
      <vstav3:entryPoint
        class="ContosoExcelWorkbook.ThisWorkbook">
        <assemblyIdentity
          name="ContosoExcelWorkbook"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
      <vstav3:entryPoint
        class="ContosoExcelWorkbook.Sheet1">
        <assemblyIdentity
          name="ContosoExcelWorkbook"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
      <vstav3:entryPoint
        class="ContosoExcelWorkbook.Sheet2">
        <assemblyIdentity
          name="ContosoExcelWorkbook"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
      <vstav3:entryPoint
        class="ContosoExcelWorkbook.Sheet3">
        <assemblyIdentity
          name="ContosoExcelWorkbook"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
    </vstav3:entryPoints>
  </vstav3:entryPointsCollection>
  <vstav3:update
    enabled="true">
    <vstav3:expiration
      maximumAge="7"
      unit="days" />
  </vstav3:update>
  <vstav3:application>
    <vstov4:customizations
      xmlns:vstov4="urn:schemas-microsoft-com:vsto.v4">
      <vstov4:customization>
        <vstov4:document
          solutionId="73e" />
      </vstov4:customization>
    </vstov4:customizations>
  </vstav3:application>
</vstav3:addIn>
```

## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra o elemento **AddIn** em uma solução do Office de nível de aplicativo que é implantada usando o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] . Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

### <a name="code"></a>Código

```xml
<vstav3:addIn
  xmlns:vstav3="urn:schemas-microsoft-com:vsta.v3">
  <vstav3:entryPointsCollection>
    <vstav3:entryPoints>
      <vstav3:entryPoint
        class="ContosoOutlookAddIn.ThisAddIn">
        <assemblyIdentity
          name="ContosoOutlookAddIn"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
    </vstav3:entryPoints>
  </vstav3:entryPointsCollection>
  <vstav3:update
    enabled="true">
    <vstav3:expiration
      maximumAge="7"
      unit="days" />
  </vstav3:update>
  <vstav3:application>
    <vstov4:customizations
      xmlns:vstov4="urn:schemas-microsoft-com:vsto.v4">
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
    </vstov4:customizations>
  </vstav3:application>
</vstav3:addIn>
```

## <a name="see-also"></a>Consulte também

- [Manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)
- [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)