---
title: Interface IWebAppDiagnosticsSetup | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IWebAppDiagnosticsSetup Interface
ms.assetid: ec7359f2-633e-4d59-b64b-9cab0134dfd0
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6e273f29bee6e4d2aae26c01c477373a735624c8
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24733996"
---
# <a name="iwebappdiagnosticssetup-interface"></a>Interface IWebAppDiagnosticsSetup
Essa interface é implementada por um aplicativo de depuração PDM para criar objetos COM no processo que está sendo depurado e habilitar o diagnóstico da web. Se o PDM Depurar aplicativo objeto implementa [IObjectWithSite](http://go.microsoft.com/fwlink/?LinkId=232438), Internet Explorer chama [SetSite](http://go.microsoft.com/fwlink/?LinkId=232439) após ele ter sido criado e passa uma referência ao [IWebBrowser2](http://go.microsoft.com/fwlink/?LinkId=232449). Um aplicativo WWA chama [SetSite](http://go.microsoft.com/fwlink/?LinkId=232439) e passa no WWA interface IWebApplicationHost em vez disso. Se [SetSite](http://go.microsoft.com/fwlink/?LinkId=232439) foi chamado com um valor não nulo, [IWebAppDiagnosticsSetup::DiagnosticsSupported](../../winscript/reference/iwebappdiagnosticssetup-diagnosticssupported.md) retorna true. Se não, ela retorna false e chamadas para [IWebAppDiagnosticsSetup::CreateObjectWithSiteAtWebApp](../../winscript/reference/iwebappdiagnosticssetup-createobjectwithsiteatwebapp.md) falhar.  
  
> [!IMPORTANT]
>  `IWebAppDiagnosticsSetup`é implementado por v PDM 11.0 e maior. Localizado em. activdbg100.h.  
  
## <a name="methods"></a>Métodos  
 Essa interface expõe os métodos a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[IWebAppDiagnosticsSetup::CreateObjectWithSiteAtWebApp](../../winscript/reference/iwebappdiagnosticssetup-createobjectwithsiteatwebapp.md)|Obtém os documentos de texto que são ocultados pelo filtro especificado.|  
|[IWebAppDiagnosticsSetup::DiagnosticsSupported](../../winscript/reference/iwebappdiagnosticssetup-diagnosticssupported.md)|Determina se o documento especificado pertence a um de nós filho deste nó.|