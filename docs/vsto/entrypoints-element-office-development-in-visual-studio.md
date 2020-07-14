---
title: '&lt;elemento entryPoints &gt; (desenvolvimento do Office no Visual Studio)'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <entryPoints> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a8e735cfabcc02a46ca83759a7ad53877bfb05f0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543566"
---
# <a name="ltentrypointsgt-element-office-development-in-visual-studio"></a>&lt;elemento entryPoints &gt; (desenvolvimento do Office no Visual Studio)
  O `entryPoints` elemento do `vstav3` namespace contém todos os `entryPoint` elementos associados a uma solução do Office.

## <a name="syntax"></a>Sintaxe

```xml
<entryPoints>
    <entryPoint>
    </entryPoint>
    <entryPoint>
    </entryPoint>
    <entryPoint>
    </entryPoint>
</entryPoints>
```

## <a name="elements-and-attributes"></a>Elementos e atributos
 O `entryPoints` elemento é obrigatório e está no `vstav3` namespace. Há um `entryPoints` elemento definido em um manifesto de aplicativo para cada solução do Office. Por exemplo, se você implantar três soluções do Office em uma implantação de vários projetos, haverá três `entryPoints` elementos no manifesto do aplicativo.

 O `entryPoints` elemento tem o atributo a seguir.

|Atributo|Descrição|
|---------------|-----------------|
|id|Necessário para implantação de vários projetos. O nome da solução do Office. A ID não pode conter o símbolo de igual (=).|

 `entryPoints`tem os elementos a seguir.

### <a name="entrypoint"></a>entryPoint
 Obrigatórios. A função do `entryPoint` elemento no `vstav3` namespace é definida no [elemento&#60;EntryPoint&#62; &#40;o desenvolvimento do Office no Visual Studio&#41;](../vsto/entrypoint-element-office-development-in-visual-studio.md).

## <a name="document-level-customization-example"></a>Exemplo de personalização no nível do documento

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra o `entryPoints` elemento em um manifesto de aplicativo para uma solução em nível de documento implantada usando o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] . Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

### <a name="code"></a>Código

```xml
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
```

## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra um `entryPoints` elemento em um manifesto de aplicativo para uma solução de nível de aplicativo implantada usando o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] . Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

### <a name="code"></a>Código

```xml
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
```

## <a name="multi-project-deployment-example"></a>Exemplo de implantação de vários projetos

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra o `entryPoints` elemento em um manifesto de aplicativo para uma implantação de vários projetos. Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

### <a name="code"></a>Código

```xml
<vstav3:entryPoints
  id="ContosoExcel">
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
<vstav3:entryPoints
  id="ContosoOutlook">
  <vstav3:entryPoint
    class="ContosoOutlookAddIn.ThisAddIn">
    <assemblyIdentity
      name="ContosoOutlookAddIn"
      version="1.0.0.0"
      language="neutral"
      processorArchitecture="msil" />
  </vstav3:entryPoint>
</vstav3:entryPoints>
```

## <a name="see-also"></a>Confira também

- [Manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)
- [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)