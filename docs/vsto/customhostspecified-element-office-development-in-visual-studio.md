---
title: '&lt;&gt;elemento customHostSpecified (desenvolvimento do Office no Visual Studio)'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <customHostSpecified> element
- <customHostSpecified> element
- customHostSpecified element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 689848f14b4540a54489b4ea5bbad67e493fe276
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544905"
---
# <a name="ltcustomhostspecifiedgt-element-office-development-in-visual-studio"></a>&lt;&gt;elemento customHostSpecified (desenvolvimento do Office no Visual Studio)
  O `customHostSpecified` elemento indica que essa solução não é um aplicativo autônomo. As soluções do Office contêm componentes que são hospedados dentro de Microsoft Office aplicativos.

## <a name="syntax"></a>Sintaxe

```xml
<customHostSpecified />
```

## <a name="elements-and-attributes"></a>Elementos e atributos
 O `customHostSpecified` elemento é necessário para as soluções do Office. Esse elemento está no `co.v1` namespace e especifica que essa implantação contém um componente que será implantado dentro de um host personalizado e não é um aplicativo autônomo.

 Esse elemento é um filho do primeiro `<entrypoint>` elemento no manifesto do aplicativo. Não pode haver nenhum outro elemento filho nesse `<entrypoint>` elemento ou [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] gerará um erro de validação durante a instalação.

 Este elemento não tem atributos nem elementos filho.

## <a name="example"></a>Exemplo
 O exemplo de código a seguir ilustra o `customHostSpecified` elemento em um manifesto de aplicativo para uma solução do Office. Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

```xml
<entryPoint>
    <co.v1:customHostSpecified />
</entryPoint>
```

## <a name="see-also"></a>Consulte também

- [Manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)
- [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)