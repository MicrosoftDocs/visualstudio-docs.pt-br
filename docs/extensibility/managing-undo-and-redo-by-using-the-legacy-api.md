---
title: Gerenciamento de desfazer e refazer, usando a API herdada | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - undo management
ms.assetid: 838c0ddf-fdf3-4df1-8d21-79610b8ba0b1
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ccb49abc1251b489807efcb4d7e9ce89b25dcd16
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53842691"
---
# <a name="manage-undo-and-redo-by-using-the-legacy-api"></a>Gerenciar desfazer e refazer, usando a API herdada
Editores devem oferecer suporte a operações de desfazer que permitem aos usuários reverter suas alterações recentes, ao modificar o código. A maioria dos editores implementados nos [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e o [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] pode ter suporte de desfazer automaticamente fornecido pelo ambiente de desenvolvimento integrado (IDE).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Como: Implementar o gerenciamento de desfazer](../extensibility/how-to-implement-undo-management.md)  
 Fornece a capacidade de desfazer para editores com único ou vários modos de exibição.  
  
 [Como: Limpar a pilha de desfazer](../extensibility/how-to-clear-the-undo-stack.md)  
 Descreve como limpar uma pilha de desfazer.  
  
 [Como: Use o gerenciamento de desfazer vinculado](../extensibility/how-to-use-linked-undo-management.md)  
 Incorpora o gerenciamento de desfazer vinculado em seu editor.  
  
## <a name="reference"></a>Referência  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager>  
 Fornece gerenciamento de desfazer para um editor que dá suporte a vários modos de exibição.  
