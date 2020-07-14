---
title: '&lt;elemento de ação &gt; (desenvolvimento do Office no Visual Studio)'
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <postAction> element
- <postAction> element
- postAction element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 149aa0cf8543f5b5b1b5ada18a8b2f0e58f063d0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546933"
---
# <a name="ltpostactiongt-element-office-development-in-visual-studio"></a>&lt;elemento de ação &gt; (desenvolvimento do Office no Visual Studio)
  O `postAction` elemento do `vstav3` namespace contém os `entrypoint` elementos e todos os `postActionData` elementos associados às ações pós-implantação, que são executadas após a instalação das soluções do Office.

## <a name="syntax"></a>Sintaxe

```xml
<postAction>
  <entryPoint>
  </entryPoint>
  <postActionData>
  </postActionData>
</postAction>
```

## <a name="elements-and-attributes"></a>Elementos e atributos
 O `postAction` elemento é opcional e está no `vstav3` namespace. Há um `postAction` elemento definido em um manifesto de aplicativo para cada ação pós-implantação.

 O `postAction` elemento não tem atributos.

 `postAction`tem os elementos a seguir.

### <a name="entrypoint"></a>entryPoint
 Opcional. A função do `entryPoint` elemento no `vstav3` namespace é definida no [elemento&#60;entrypoints&#62; &#40;o desenvolvimento do Office no Visual Studio&#41;](../vsto/entrypoints-element-office-development-in-visual-studio.md).

### <a name="postactiondata"></a>postActionData
 Opcional. A função do `postActionData` elemento no `vstav3` namespace é definida no [elemento&#60;postActionData&#62; &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/postactiondata-element-office-development-in-visual-studio.md).

## <a name="post-deployment-action-example"></a>Exemplo de ação pós-implantação

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra o `postAction` elemento em um manifesto de aplicativo para uma solução do Office que é implantada usando o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] . Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

### <a name="code"></a>Código

```xml
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
```

## <a name="see-also"></a>Confira também

- [Manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)
- [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)
