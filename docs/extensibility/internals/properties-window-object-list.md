---
title: Lista de objetos de janela de propriedades | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Properties window, object list
ms.assetid: 6c159c9d-345d-4b23-8ddd-9839d338b62f
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: eccc7cfc432918a80723251a7b9a87ec4e13450d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62909105"
---
# <a name="properties-window-object-list"></a>Lista de objetos de janela Propriedades
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

A lista de objetos na **propriedades** janela é uma lista suspensa que permite que você altere a seleção para outros objetos disponíveis dentro de um ou mais períodos selecionados. Selecionar um objeto diferente de dentro dessa lista dispara uma chamada para <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> para informar o ambiente de que um novo objeto foi selecionado. As informações exibidas na **propriedades** janela, em seguida, é alterada para mostrar as propriedades associadas ao objeto selecionado recentemente.  
  
## <a name="the-object-list"></a>A lista de objetos  
 A lista de objeto consiste em dois campos: o nome do objeto (exibidas em negrito) e o tipo de objeto.  
  
 O nome do objeto exibido à esquerda do tipo de objeto em negrito é recuperado do objeto em si usando o `Name` propriedade fornecida pelo <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> interface. <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo.GetClassInfo%2A>, o único método no <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo>, retorna <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo> para coclass dessa interface. O **propriedades** janela usa <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> para obter o nome da coclass, que é exibido como o nome do objeto na lista suspensa.  
  
 Se o objeto não tiver um `Name` propriedade, um nome não é exibida na área de nome da lista de objetos. Você pode adicionar uma propriedade de nome para o objeto, se você quiser que o nome exibido na lista de objetos.  
  
 Se o objeto COM não implementa <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo>, o **propriedades** janela exibe o nome da interface no lugar do nome do objeto no lado esquerdo da lista.  
  
## <a name="see-also"></a>Consulte também  
 [Estender as propriedades](../../extensibility/internals/extending-properties.md)
