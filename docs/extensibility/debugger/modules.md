---
title: Módulos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- modules
- debugging [Debugging SDK], modules
ms.assetid: c4cf2809-dbdb-4e75-9273-b3d3d77b67d0
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 8750c1f6676966be8564fbf4a175a66fa180a401
ms.sourcegitcommit: 25a62c2db771f938e3baa658df8b1ae54a960e4f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39233159"
---
# <a name="modules"></a>Módulos
Em termos de arquitetura do depurador, uma *módulo*:  
  
-   É um contêiner físico de código, como um arquivo executável ou uma DLL.  
  
-   Pode recarregar seus símbolos e descreva a mesmo. Descrições do módulo são exibidas na janela de módulos do IDE.  
  
-   É representado por um [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md) interface, criado por um mecanismo de depuração para descrever o módulo.  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)   
 [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md)