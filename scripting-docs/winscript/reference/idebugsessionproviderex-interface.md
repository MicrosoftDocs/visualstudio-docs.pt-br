---
title: Interface IDebugSessionProviderEx | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 26c5da2d-8c93-4d2b-94d2-97aaa377dcfe
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 545b60f13e86e59143ce0e57f454b13f61041f11
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24726926"
---
# <a name="idebugsessionproviderex-interface"></a>Interface IDebugSessionProviderEx
A principal interface fornecida por um depurador IDE para habilitar a depuração de host e idioma iniciada. Ele estabelece uma sessão de depuração para um aplicativo em execução. Essa interface é implementada pelo Gerenciador de máquina de depuração.  
  
 Além dos métodos herdados de `IUnknown`, o `IDebugSessionProviderEx` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugSessionProviderEx:CanJITDebug](../../winscript/reference/idebugsessionproviderex-canjitdebug.md)|Determina se é possível com o aplicativo especificado somente em vez de depuração.|  
|[IDebugSessionProviderEx:StartDebugSession](../../winscript/reference/idebugsessionproviderex-startdebugsession.md)|Inicia uma sessão de depuração com o aplicativo especificado.|