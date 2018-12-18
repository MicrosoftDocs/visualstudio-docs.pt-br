---
title: Interface IWebAppDiagnosticsObjectInitialization | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IWebAppDiagnosticsObjectInitialization Interface
ms.assetid: 32847838-01d9-4205-a811-3043d8c7a917
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 159b81a336accea4e4e8c035119d5525de71ae90
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24733856"
---
# <a name="iwebappdiagnosticsobjectinitialization-interface"></a>Interface IWebAppDiagnosticsObjectInitialization
Esta interface pode ser implementada em classes que implementam [IWebAppDiagnosticsSetup::CreateObjectWithSiteAtWebApp](../../winscript/reference/iwebappdiagnosticssetup-createobjectwithsiteatwebapp.md). [IWebAppDiagnosticsSetup Interface](../../winscript/reference/iwebappdiagnosticssetup-interface.md) é implementada pelo objeto que implementa [IDebugApplication Interface](../../winscript/reference/idebugapplication-interface.md). Na maioria dos casos, esse objeto é o PDM.  
  
 Depois que o objeto foi criado, [IWebAppDiagnosticsObjectInitialization::Initialize](../../winscript/reference/iwebappdiagnosticsobjectinitialization-initialize.md) é chamado com uma referência para o aplicativo de depuração PDM e `hPassToObject` parâmetro `CreateObjectWithSiteAtWebApp`.  
  
> [!IMPORTANT]
>  `IWebAppDiagnosticsObjectInitialization`foi encontrado no activdbg100.h.  
  
## <a name="methods"></a>Métodos  
 Essa interface expõe os métodos a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[IWebAppDiagnosticsObjectInitialization::Initialize](../../winscript/reference/iwebappdiagnosticsobjectinitialization-initialize.md)|Inicializa o objeto.|