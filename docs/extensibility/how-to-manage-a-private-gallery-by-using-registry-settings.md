---
title: Gerenciar uma galeria privada usando as configurações do Registro
description: Saiba como controlar o acesso aos controles, modelos e ferramentas na Galeria Visual Studio, na Galeria de Exemplos ou em galerias privadas.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- VSIX private galleries, managing
- managing VSIX private galleries
ms.assetid: 86b86442-4293-4cad-9fe2-876eef65f426
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9fef1e6447ac07e9c3d4ccfb76a9ee1e06f91e42
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898829"
---
# <a name="how-to-manage-a-private-gallery-by-using-registry-settings"></a>Como gerenciar uma galeria privada usando as configurações do Registro
Se você for um administrador ou desenvolvedor de uma extensão do Shell Isolado, poderá controlar o acesso aos controles, modelos e ferramentas na Galeria Visual Studio, na Galeria de Exemplos ou em galerias privadas. Para tornar uma galeria disponível ou indisponível, crie um *arquivo .pkgdef* que descreve as chaves do Registro modificadas e seus valores.

## <a name="manage-private-galleries"></a>Gerenciar galerias privadas
 Você pode criar um *arquivo .pkgdef* para controlar o acesso a galerias em vários computadores. Esse arquivo deve ter o seguinte formato.

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

 A `Repositories` chave refere-se à galeria a ser habilitada ou desabilitada. A Visual Studio e a Galeria de Exemplos usam os seguintes GUIDs de repositório:

- Visual Studio: 0F45E408-7995-4375-9485-86B8DB553DC9

- Galeria de exemplos: AEB9CB40-D8E6-4615-B52C-27E307F8506C

  O `Disabled` valor é opcional. Por padrão, uma galeria está habilitada.

  O `Priority` valor determina a ordem na qual as galerias são listadas na caixa de **diálogo** Opções. Visual Studio Gallery tem prioridade 10 e a Galeria de Exemplos tem prioridade 20. As galerias privadas começam com a prioridade 100. Se várias galerias têm o mesmo valor de prioridade, a ordem na qual elas aparecem é determinada pelos valores de seus atributos `DisplayName` localizados.

  O valor é necessário para galerias baseadas em Atom ou `Protocol` sharePoint.

  Ou `DisplayName` e `DisplayNameResourceID` , devem ser `DisplayNamePackageGuid` especificados. Se todos são especificados, o `DisplayNameResourceID` par `DisplayNamePackageGuid` e é usado.

## <a name="disable-the-visual-studio-gallery-using-a-pkgdef-file"></a>Desabilitar a Visual Studio usando um arquivo .pkgdef
 Você pode desabilitar uma galeria em um *arquivo .pkgdef.* A seguinte entrada desabilita o Visual Studio Gallery:

```
[$RootKey$\ExtensionManager\Repositories\{0F45E408-7995-4375-9485-86B8DB553DC9}]
"Disabled"=dword:00000001

```

 A seguinte entrada desabilita a Galeria de Exemplos:

```
[$RootKey$\ExtensionManager\Repositories\{AEB9CB40-D8E6-4615-B52C-27E307F8506C}]
"Disabled"=dword:00000001

```

## <a name="see-also"></a>Confira também
- [Galerias privadas](../extensibility/private-galleries.md)
