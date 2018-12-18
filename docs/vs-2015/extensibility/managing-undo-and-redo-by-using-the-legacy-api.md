---
title: Gerenciamento de desfazer e refazer, usando a API herdada | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - undo management
ms.assetid: 838c0ddf-fdf3-4df1-8d21-79610b8ba0b1
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: ab655c4822f7f5186cbcd18d451cfa3bb0aa656e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51764171"
---
# <a name="managing-undo-and-redo-by-using-the-legacy-api"></a>Gerenciamento de desfazer e refazer, usando a API herdada
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Editores devem oferecer suporte a operações de desfazer que permitem aos usuários reverter suas alterações recentes, ao modificar o código. A maioria dos editores implementados nos [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] pode ter suporte de desfazer automaticamente fornecido pelo ambiente de desenvolvimento integrado (IDE).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Como implementar o gerenciamento de desfazer](../extensibility/how-to-implement-undo-management.md)  
 Fornece a capacidade de desfazer para editores com único ou vários modos de exibição.  
  
 [Como limpar a pilha de desfazer](../extensibility/how-to-clear-the-undo-stack.md)  
 Descreve como limpar uma pilha de desfazer.  
  
 [Como usar o gerenciamento de desfazer vinculado](../extensibility/how-to-use-linked-undo-management.md)  
 Incorpora o gerenciamento de desfazer vinculado em seu editor.  
  
## <a name="reference"></a>Referência  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager>  
 Fornece gerenciamento de desfazer para um editor que dá suporte a vários modos de exibição.  
  
## <a name="related-sections"></a>Seções relacionadas

