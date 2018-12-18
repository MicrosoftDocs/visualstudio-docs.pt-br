---
title: Interface IApplicationDebuggerUI | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IApplicationDebuggerUI interface
ms.assetid: b8828817-ca24-4012-802c-7dcaeea65dc8
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dbaa04f6790ffc4d80447a6745ca82cc8dba6802
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725136"
---
# <a name="iapplicationdebuggerui-interface"></a>Interface IApplicationDebuggerUI
Implementado pelo ambiente de desenvolvimento integrado (IDE) do depurador (além `IApplicationDebugger`) para fornecer mais controle sobre a interface do usuário (IU) do depurador de um componente externo.  
  
 Além dos métodos herdados de `IUnknown`, o `IApplicationDebuggerUI` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IApplicationDebuggerUI::BringDocumentToTop](../../winscript/reference/iapplicationdebuggerui-bringdocumenttotop.md)|Coloca a janela que contém o documento de depuração especificado para a parte superior do depurador de interface do usuário.|  
|[IApplicationDebuggerUI::BringDocumentContextToTop](../../winscript/reference/iapplicationdebuggerui-bringdocumentcontexttotop.md)|Coloca a janela que contém o contexto do documento fornecido na parte superior na interface de usuário do depurador e rolar a janela para o contexto.|