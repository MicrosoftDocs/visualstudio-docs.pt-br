---
title: '&lt;&gt;elemento Description (desenvolvimento do Office no Visual Studio)'
titleSuffix: ''
ms.custom: secdec18
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- description element
- <description> element
- application manifests [Office development in Visual Studio], <description> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4c8b54f8ccf2181a053ae5d2fe221b49840cd72c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520261"
---
# <a name="ltdescriptiongt-element-office-development-in-visual-studio"></a>&lt;&gt;elemento Description (desenvolvimento do Office no Visual Studio)
  O `description` elemento do `vstov4` namespace armazena a descrição da solução do Office que aparece na caixa de diálogo suplementos de COM de Microsoft Office aplicativos.

## <a name="syntax"></a>Sintaxe

```xml
<description>
</description>
```

## <a name="elements-and-attributes"></a>Elementos e atributos
 Opcional. O `description` elemento está no `vstov4` namespace. Ele contém a descrição do suplemento que aparece na caixa de diálogo suplementos COM do Microsoft Office aplicativos.

 O `description` elemento não tem atributos ou elementos.

## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra o `description` elemento para uma solução em nível de aplicativo implantada usando o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] . Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

### <a name="code"></a>Código

```xml
<vstov4:description>
  ContosoOutlookAddIn - Outlook add-in
  created with Visual Studio Tools for Office
</vstov4:description>
```

## <a name="see-also"></a>Confira também

- [Manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)
- [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)