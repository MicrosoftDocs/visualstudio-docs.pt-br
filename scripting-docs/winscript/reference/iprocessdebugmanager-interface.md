---
title: Interface IProcessDebugManager | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IProcessDebugManager interface
ms.assetid: b6ecb2bd-a4d1-4857-9232-036c154d0cb1
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 26c97fda6fc8657164e22d51eb041017a6239d98
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24729216"
---
# <a name="iprocessdebugmanager-interface"></a>Interface IProcessDebugManager
A interface primária para o gerenciador de depuração do processo. Essa interface pode criar, adicionar ou remover um aplicativo virtual de um processo. Ele pode enumerar os quadros de pilhas e threads do aplicativo.  
  
 Além dos métodos herdados de `IUnknown`, o `IProcessDebugManager` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IProcessDebugManager::CreateApplication](../../winscript/reference/iprocessdebugmanager-createapplication.md)|Cria um novo objeto de aplicativo de depuração para este aplicativo.|  
|[IProcessDebugManager::GetDefaultApplication](../../winscript/reference/iprocessdebugmanager-getdefaultapplication.md)|Retorna um objeto de aplicativo padrão para o processo atual.|  
|[IProcessDebugManager::AddApplication](../../winscript/reference/iprocessdebugmanager-addapplication.md)|Adiciona um aplicativo à lista do Gerenciador de depuração de máquina de aplicativos em execução.|  
|[IProcessDebugManager::RemoveApplication](../../winscript/reference/iprocessdebugmanager-removeapplication.md)|Remove um aplicativo de execução de lista de aplicativos.|  
|[IProcessDebugManager::CreateDebugDocumentHelper](../../winscript/reference/iprocessdebugmanager-createdebugdocumenthelper.md)|Cria um novo auxiliar de documento de depuração para este aplicativo.|