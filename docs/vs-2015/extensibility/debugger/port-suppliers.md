---
title: Fornecedores de porta | Microsoft Docs
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
- port suppliers
- debugging [Debugging SDK], port suppliers
ms.assetid: a8f3db96-1a13-4e93-9ef6-0861880369e0
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 173ff6b7550731262e8f4e3293b6f7c35eac4062
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49858804"
---
# <a name="port-suppliers"></a>Fornecedores de porta
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Em termos de arquitetura do depurador, uma **fornecedor de porta**:  
  
- Está contido por um servidor e fornece as portas na solicitação para esse servidor.  
  
- Adicione e remova as portas do servidor que contém.  
  
- Pode enumerar todas as portas que ele tenha fornecido para o servidor.  
  
- É representado por um [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md) interface, que está registrado com o Visual Studio por meio do registro. Essa interface pode ser obtida chamando [GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md).  
  
  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Fornece um fornecedor de porta padrão e uma porta padrão. Se uma porta personalizada precisa ser implementado, um fornecedor de porta personalizado também precisa ser implementada para fornecer essas portas personalizadas.  
  
## <a name="see-also"></a>Consulte também  
 [Servidores](../../extensibility/debugger/servers-visual-studio-sdk.md)   
 [Portas](../../extensibility/debugger/ports.md)   
 [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)   
 [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)   
 [GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)

