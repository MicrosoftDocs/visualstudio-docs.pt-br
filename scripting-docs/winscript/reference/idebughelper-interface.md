---
title: Interface IDebugHelper | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugHelper interface
ms.assetid: ef5691e0-1d82-42c2-997c-888e31c478dd
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3f0f70ecb8ead264d0d4b074f8fc1d9e3a6091eb
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24727306"
---
# <a name="idebughelper-interface"></a>Interface IDebugHelper
Serve como uma fábrica para navegadores de objetos e pontos de conexão simples. O Gerenciador de depuração do processo (PDM) implementa essa interface, que é consumida pelos mecanismos de script.  
  
 Além dos métodos herdados de `IUnknown`, o `IDebugHelper` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugHelper::CreatePropertyBrowser](../../winscript/reference/idebughelper-createpropertybrowser.md)|Retorna um navegador de propriedade que encapsula uma VARIANTE.|  
|[IDebugHelper::CreatePropertyBrowserEx](../../winscript/reference/idebughelper-createpropertybrowserex.md)|Retorna um navegador de propriedade que encapsula uma VARIANTE e permite conversão personalizada de valores de variação ou tipos VARTYPE em cadeias de caracteres.|  
|[IDebugHelper::CreateSimpleConnectionPoint](../../winscript/reference/idebughelper-createsimpleconnectionpoint.md)|Retorna uma interface de eventos que encapsula um determinado `IDispatch` objeto.|