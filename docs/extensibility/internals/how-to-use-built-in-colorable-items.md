---
title: 'Como: usar itens de cores internas | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- colorable items
- language services, built-in colorable items
ms.assetid: 5e5f3436-6bad-4fd2-8823-6a30353ba648
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 762d1e53f7aafa11ed345859e68fc98766eec77d
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905217"
---
# <a name="how-to-use-built-in-colorable-items"></a>Como: usar itens de cores internos
Antes de usar os itens coloridos internos, você deve primeiro sinalizar para o IDE (ambiente de desenvolvimento integrado) que você não está fornecendo seus próprios itens personalizáveis personalizados, que nesse caso seriam <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> objetos. Você faz isso definindo uma entrada de registro para o serviço de idioma.

## <a name="to-use-built-in-colorable-items"></a>Para usar itens coloráveis internos

1. Em **HKEY_LOCAL_MACHINE \visualstudio \\<X. Y> serviços \Languages\language \\<\> nome do idioma**, em que \<X.Y> é uma versão do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] e \<Language Name> é o nome do seu idioma, crie um valor de entrada do Registro DWORD chamado **RequestStockColors**.

2. Defina o valor de entrada do registro **RequestStockColors** como *1*.

    Depois de criar a entrada do registro, o método de Colorizer <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> pode usar os membros da <xref:Microsoft.VisualStudio.TextManager.Interop.DEFAULTITEMS> enumeração para preencher a matriz de atributos de cor para uso pelo editor.

   > [!NOTE]
   > Não defina essa entrada de registro se você estiver fornecendo itens coloridos personalizados. Para obter mais informações, consulte [itens colorable personalizados](../../extensibility/internals/custom-colorable-items.md).

## <a name="see-also"></a>Confira também
- [Cores de sintaxe em editores personalizados](../../extensibility/syntax-coloring-in-custom-editors.md)
- [Cores de sintaxe em um serviço de idioma herdado](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [Implementando a cor da sintaxe](../../extensibility/internals/implementing-syntax-coloring.md)
- [Itens coloridos personalizados](../../extensibility/internals/custom-colorable-items.md)
- [Registrar um serviço de idioma herdado](../../extensibility/internals/registering-a-legacy-language-service2.md)
