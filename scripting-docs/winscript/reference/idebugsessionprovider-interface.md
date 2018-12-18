---
title: Interface IDebugSessionProvider | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugSessionProvider interface
ms.assetid: 1b898423-7af9-44f5-8dda-987005309c99
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4e61b1e5e794c68e34250f958cdda0f50b68334c
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24727136"
---
# <a name="idebugsessionprovider-interface"></a>Interface IDebugSessionProvider
A principal interface fornecida por um IDE para habilitar o host e o idioma do depurador iniciada a depuração. Ele estabelece uma sessão de depuração para um aplicativo em execução. Essa interface é implementada pelo Gerenciador de depuração de máquina.  
  
 Além dos métodos herdados de `IUnknown`, o `IDebugSessionProvider` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugSessionProvider::StartDebugSession](../../winscript/reference/idebugsessionprovider-startdebugsession.md)|Inicia uma sessão de depuração com o aplicativo especificado.|