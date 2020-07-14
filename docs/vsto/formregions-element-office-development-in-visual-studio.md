---
title: '&lt;&gt;elemento FormRegions (desenvolvimento do Office no Visual Studio)'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- formRegions element
- <formRegions> element
- application manifests [Office development in Visual Studio], <formRegions> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6f98c74c2df998f0e79f5b95a316a7917304e029
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538353"
---
# <a name="ltformregionsgt-element-office-development-in-visual-studio"></a>&lt;&gt;elemento FormRegions (desenvolvimento do Office no Visual Studio)
  O `formRegions` elemento do `vstov4` namespace contém as Microsoft Office regiões de formulário do Outlook que estão associadas a um suplemento do VSTO.

## <a name="syntax"></a>Sintaxe

```xml
<formRegions>
  <formRegion>
  </formRegion>
</formRegions>
```

## <a name="elements-and-attributes"></a>Elementos e atributos
 O `formRegions` elemento do `vstov4` namespace contém todos os `formRegion` elementos para um suplemento do VSTO do Outlook. Ele é necessário apenas para suplementos do VSTO do Outlook que incluem regiões de formulário.

 Pode haver apenas um `formRegions` elemento definido em um manifesto do aplicativo.

 O `formRegions` elemento não tem atributos.

 O `formRegions` elemento tem o elemento a seguir.

### <a name="formregion"></a>formRegion
 Necessário para os suplementos do VSTO do Outlook que incluem regiões de formulário. O `formRegion` elemento é definido no [elemento&#60;formRegion&#62; &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/formregion-element-office-development-in-visual-studio.md).

## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra um `formRegions` elemento em um manifesto de aplicativo para uma solução do Office de nível de aplicativo implantada usando [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] . Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

### <a name="code"></a>Código

```xml
<vstov4:formRegions>
  <vstov4:formRegion
      name="OutlookAddIn1.FormRegion1">
    <vstov4:messageClass name="IPM.Note" />
    <vstov4:messageClass name="IPM.Contact" />
    <vstov4:messageClass name="IPM.Appointment" />
  </vstov4:formRegion>
</vstov4:formRegions>
```

## <a name="see-also"></a>Consulte também

- [Manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)
- [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)