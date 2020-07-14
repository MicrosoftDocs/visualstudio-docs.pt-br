---
title: '&lt;&gt;elemento de ações (desenvolvimento do Office no Visual Studio)'
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <postActions> element
- postActions element
- <postActions> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: bfe9ae171f0f6fac1c2b5add5340de1c11f3da0f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544411"
---
# <a name="ltpostactionsgt-element-office-development-in-visual-studio"></a>&lt;&gt;elemento de ações (desenvolvimento do Office no Visual Studio)
  O `postActions` elemento do `vstav3` namespace contém todos os `postAction` elementos que descrevem as ações pós-implantação, que são executadas após a instalação das soluções do Office.

## <a name="syntax"></a>Sintaxe

```xml
<postActions>
  <postAction>
    <entryPoint>
    </entryPoint>
    <postActionData>
    </postActionData>
  </postAction>
</postActions>
```

## <a name="elements-and-attributes"></a>Elementos e atributos
 O `postActions` elemento é opcional e está no `vstav3` namespace. Há apenas um `postActions` elemento definido em um manifesto do aplicativo.

 O `postActions` elemento não tem atributos.

 `postActions`tem o seguinte elemento.

### <a name="postaction"></a>Ação
 Opcional. A função do `postAction` elemento no `vstav3` namespace é definida no [elemento&#60;ação&#62; &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/postaction-element-office-development-in-visual-studio.md).

## <a name="post-deployment-action-example"></a>Exemplo de ação pós-implantação

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra o `postActions` elemento em um manifesto de aplicativo para uma solução do Office implantada usando o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] . Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

### <a name="code"></a>Código

```xml
<vstav3:postActions>
  <vstav3:postAction>
    <vstav3:entryPoint
      class="PostDeploymentAction.PostDeploymentActionSample">
      <assemblyIdentity
        name="PostDeploymentAction"
        version="1.0.0.0"
        language="neutral"
        processorArchitecture="msil" />
    </vstav3:entryPoint>
    <vstav3:postActionData>
    </vstav3:postActionData>
  </vstav3:postAction>
</vstav3:postActions>
```

## <a name="see-also"></a>Consulte também

- [Manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)
- [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)
