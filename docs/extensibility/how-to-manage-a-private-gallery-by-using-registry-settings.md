---
title: Gerenciar uma galeria privada usando configurações do registro
description: Saiba como controlar o acesso aos controles, modelos e ferramentas na galeria do Visual Studio, na Galeria de exemplos ou nas galerias particulares.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSIX private galleries, managing
- managing VSIX private galleries
ms.assetid: 86b86442-4293-4cad-9fe2-876eef65f426
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5981dc4399e09df207b154b900fa163895c344c9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070057"
---
# <a name="how-to-manage-a-private-gallery-by-using-registry-settings"></a>Como: gerenciar uma galeria privada usando configurações do registro
Se você for um administrador ou o desenvolvedor de uma extensão de shell isolada, poderá controlar o acesso aos controles, modelos e ferramentas na galeria do Visual Studio, na Galeria de exemplos ou nas galerias particulares. Para tornar uma galeria disponível ou indisponível, crie um arquivo *. pkgdef* que descreva as chaves de registro modificadas e seus valores.

## <a name="manage-private-galleries"></a>Gerenciar galerias particulares
 Você pode criar um arquivo *. pkgdef* para controlar o acesso a galerias em vários computadores. Esse arquivo deve ter o formato a seguir.

```
[$RootKey$\ExtensionManager\Repositories\{UniqueGUID}]
@={URI}  (REG_SZ)
Disabled=0 | 1 (DWORD)
Priority=0 (highest priority) ... MaxInt (lowest priority) (DWORD) (uint)
Protocol=Atom Feed|Sharepoint (REG_SZ)
DisplayName={DisplayName} (REG_SZ)
DisplayNameResourceID={ID} (REG_SZ)
DisplayNamePackageGuid={GUID} (REG_SZ)

```

 A `Repositories` chave refere-se à galeria a ser habilitada ou desabilitada. A galeria do Visual Studio e a Galeria de exemplos usam os seguintes GUIDs de repositório:

- Galeria do Visual Studio: 0F45E408-7995-4375-9485-86B8DB553DC9

- Galeria de exemplos: AEB9CB40-D8E6-4615-B52C-27E307F8506C

  O `Disabled` valor é opcional. Por padrão, uma galeria está habilitada.

  O `Priority` valor determina a ordem na qual as galerias são listadas na caixa de diálogo **Opções** . A galeria do Visual Studio tem a prioridade 10 e a Galeria de exemplos tem a prioridade 20. As galerias privadas começam com a prioridade 100. Se várias galerias tiverem o mesmo valor de prioridade, a ordem na qual eles aparecem será determinada pelos valores de seus `DisplayName` atributos localizados.

  O `Protocol` valor é necessário para galerias baseadas em Atom ou no SharePoint.

  `DisplayName`Ou ambos, `DisplayNameResourceID` e `DisplayNamePackageGuid` devem ser especificados. Se todos forem especificados, o `DisplayNameResourceID` par e `DisplayNamePackageGuid` será usado.

## <a name="disable-the-visual-studio-gallery-using-a-pkgdef-file"></a>Desabilitar a galeria do Visual Studio usando um arquivo. pkgdef
 Você pode desabilitar uma galeria em um arquivo *. pkgdef* . A seguinte entrada desabilita a galeria do Visual Studio:

```
[$RootKey$\ExtensionManager\Repositories\{0F45E408-7995-4375-9485-86B8DB553DC9}]
"Disabled"=dword:00000001

```

 A seguinte entrada desabilita a Galeria de exemplos:

```
[$RootKey$\ExtensionManager\Repositories\{AEB9CB40-D8E6-4615-B52C-27E307F8506C}]
"Disabled"=dword:00000001

```

## <a name="see-also"></a>Confira também
- [Galerias privadas](../extensibility/private-galleries.md)
