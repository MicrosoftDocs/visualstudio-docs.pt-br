---
title: Lista de objetos da janela de propriedades | Microsoft Docs
description: Saiba mais sobre as interfaces usadas para interagir com a lista de objetos no janela Propriedades no IDE do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Properties window, object list
ms.assetid: 6c159c9d-345d-4b23-8ddd-9839d338b62f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 908acf3f8ecad390266c3d085778dc13077a6fa8
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903431"
---
# <a name="properties-window-object-list"></a>Lista de objetos de janela Propriedades
A lista de objetos na janela **Propriedades** é uma lista suspensa que permite alterar a seleção para outros objetos disponíveis em uma ou mais janelas selecionadas. A seleção de um objeto diferente dentro dessa lista dispara uma chamada para <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> para informar ao ambiente que um novo objeto foi selecionado. As informações exibidas na janela **Propriedades** são então alteradas para mostrar as propriedades associadas ao objeto selecionado recentemente.

## <a name="the-object-list"></a>A lista de objetos
 A lista de objetos consiste em dois campos: o nome do objeto (exibido em negrito) e o tipo de objeto.

 O nome do objeto exibido à esquerda do tipo de objeto em negrito é recuperado do próprio objeto usando a `Name` propriedade fornecida pela <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> interface. <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo.GetClassInfo%2A>, o único método em <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> , retorna <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo> para a coclasse dessa interface. A janela **Propriedades** usa <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> para obter o nome da coclasse, que é exibido como o nome do objeto na lista suspensa.

 Se o objeto não tiver uma `Name` propriedade, um nome não será exibido na área nome da lista de objetos. Você pode adicionar uma propriedade de nome ao objeto se desejar que o nome seja exibido na lista de objetos.

 Se o objeto COM não for implementado <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> , a janela **Propriedades** exibirá o nome da interface no lugar do nome do objeto no lado esquerdo da lista.

## <a name="see-also"></a>Confira também
- [Estendendo propriedades](../../extensibility/internals/extending-properties.md)
