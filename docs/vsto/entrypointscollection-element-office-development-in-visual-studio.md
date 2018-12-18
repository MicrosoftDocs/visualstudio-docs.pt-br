---
title: '&lt;entryPointsCollection&gt; elemento (desenvolvimento do Office no Visual Studio)'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- <entryPointsCollection> element
- application manifests [Office development in Visual Studio], <entryPointsCollection> element
- entryPointsCollection element
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 119cff9135b2b65f09d265aed2af3a7e2d500d60
ms.sourcegitcommit: 1466ac0f49ebf7448ea4507ae3f79acb25d51d3e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34447899"
---
# <a name="ltentrypointscollectiongt-element-office-development-in-visual-studio"></a>&lt;entryPointsCollection&gt; elemento (desenvolvimento do Office no Visual Studio)
  O `entryPointsCollection` elemento do `vstav3` namespace contém tudo o `entryPoints` elementos associados a soluções do Office.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<entryPointsCollection>  
  <entryPoints>  
    <entryPoint>  
    </entryPoint>  
    <entryPoint>  
    </entryPoint>  
    <entryPoint>  
    </entryPoint>  
  </entryPoints>  
</entryPointsCollection>  
```  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 O `entryPointsCollection` elemento é necessário e está no `vstav3` namespace. Elementos filho também devem ser neste namespace. Há apenas um `entryPointsCollection` elemento definido em um manifesto de aplicativo.  
  
 O `entryPointsCollection` elemento não tem atributos.  
  
 `entryPointsCollection` tem os seguintes elementos.  
  
### <a name="entrypoints"></a>Pontos  
 Necessário. A função da `entryPoints` elemento o `vstav3` namespace está definido em [ &#60;pontos&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/entrypoints-element-office-development-in-visual-studio.md).  
  
## <a name="document-level-customization-example"></a>Exemplo de personalização de nível de documento  
  
### <a name="description"></a>Descrição  
 O exemplo de código a seguir ilustra o `entryPointsCollection` elemento em um manifesto de aplicativo para uma solução de nível de documento implantado usando [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]. Este exemplo de código é parte de um exemplo maior fornecido em [manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).  
  
### <a name="code"></a>Código  
  
```xml  
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
```  
  
## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO  
  
### <a name="description"></a>Descrição  
 O exemplo de código a seguir ilustra uma `entryPointsCollection` elemento em um manifesto de aplicativo para uma solução de nível de aplicativo implantado usando [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]. Este exemplo de código é parte de um exemplo maior fornecido em [manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).  
  
### <a name="code"></a>Código  
  
```xml  
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
```  
  
## <a name="multi-project-deployment-example"></a>Exemplo de implantação de multiprojeto  
  
### <a name="description"></a>Descrição  
 O exemplo de código a seguir ilustra um `entryPointsCollection` elemento em um manifesto de aplicativo para implantação de vários projeto com duas soluções do Office. Este exemplo de código é parte de um exemplo maior fornecido em [manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).  
  
### <a name="code"></a>Código  
  
```xml  
<vstav3:entryPointsCollection>  
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
    </vstav3:entryPointsCollection>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)   
 [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)   
 [Manifesto do aplicativo ClickOnce](/visualstudio/deployment/clickonce-application-manifest)  
  
  