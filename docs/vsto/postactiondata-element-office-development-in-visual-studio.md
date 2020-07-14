---
title: '&lt;&gt;elemento postActionData (desenvolvimento do Office no Visual Studio)'
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- <postActionData> element
- application manifests [Office development in Visual Studio], <postActionData> element
- postActionData element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 104af55fdc11b6afae757eff95a964dad83418a6
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541863"
---
# <a name="ltpostactiondatagt-element-office-development-in-visual-studio"></a>&lt;&gt;elemento postActionData (desenvolvimento do Office no Visual Studio)
  O `postActionData` elemento do `vstav3` namespace Especifica os dados associados a qualquer ação pós-implantação que é executada Depois que as soluções do Office são instaladas.

## <a name="syntax"></a>Sintaxe

```xml
<postActionData>
</postActionData>
```

## <a name="elements-and-attributes"></a>Elementos e atributos
 O `postActionData` elemento é opcional e está no `vstav3` namespace. Há um `postActionData` elemento definido em um manifesto de aplicativo para cada ação pós-implantação.

 O `postActions` elemento não tem atributos.

 `postActions`Não tem nenhum elemento filho.

## <a name="post-deployment-action-example"></a>Exemplo de ação pós-implantação

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra o `postAction` elemento em um manifesto de aplicativo para uma solução do Office implantada usando o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] . Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

### <a name="code"></a>Código

```xml
<vstav3:postActionData>
  data in any format
</vstav3:postActionData>
```

## <a name="see-also"></a>Confira também

- [Manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)
- [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)
