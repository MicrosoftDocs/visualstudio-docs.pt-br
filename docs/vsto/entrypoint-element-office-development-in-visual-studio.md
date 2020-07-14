---
title: '&lt;&gt;elemento EntryPoint (desenvolvimento do Office no Visual Studio)'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <entryPoint> element
- <entryPoint> element
- entryPoint element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 17f57b90b7c6aa4c254b2b55ee838a3086193ef7
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543592"
---
# <a name="ltentrypointgt-element-office-development-in-visual-studio"></a>&lt;&gt;elemento EntryPoint (desenvolvimento do Office no Visual Studio)
  Cada `entryPoint` elemento do `vstav3` namespace identifica um assembly de personalização que deve ser executado quando esse [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] aplicativo é instalado.

## <a name="syntax"></a>Sintaxe

```xml
<entryPoint class>
    <assemblyIdentity />
</entryPoint>
```

## <a name="elements-and-attributes"></a>Elementos e atributos
 O `entryPoint` elemento é obrigatório e está no `vstav3` namespace.

 Cada `entryPoint` elemento pode conter apenas um assembly de personalização. Pode haver vários `entryPoint` elementos definidos em um manifesto do aplicativo.

 O `entryPoint` elemento tem os atributos a seguir.

|Atributo|Descrição|
|---------------|-----------------|
|`class`|Obrigatórios. Identifica um assembly de personalização a ser executado. A sintaxe para esse atributo é *NamespaceName. ClassName*.|

 `entryPoint`tem o seguinte elemento.

### <a name="assemblyidentity"></a>assemblyIdentity
 Obrigatórios. O `assemblyIdentity` elemento no `vstav3` namespace refere-se a um `assemblyIdentity` elemento existente no [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] manifesto do aplicativo.

 A função `assemblyIdentity` e seus atributos são definidos no [elemento&#60;assemblyIdentity&#62; &#40;aplicativo ClickOnce&#41;](../deployment/assemblyidentity-element-clickonce-application.md).

## <a name="document-level-customization-example"></a>Exemplo de personalização no nível do documento

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra os `entryPoint` elementos em um manifesto de aplicativo para uma solução do Office de nível de documento implantada usando o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] . Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

### <a name="code"></a>Código

```xml
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
```

## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra um `entryPoint` elemento em um manifesto de aplicativo para uma solução do Office de nível de aplicativo implantada usando [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] . Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

### <a name="code"></a>Código

```xml
<vstav3:entryPoint
  class="ContosoOutlookAddIn.ThisAddIn">
  <assemblyIdentity
    name="ContosoOutlookAddIn"
    version="1.0.0.0"
    language="neutral"
    processorArchitecture="msil" />
</vstav3:entryPoint>
```

## <a name="see-also"></a>Confira também

- [Manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)
- [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)