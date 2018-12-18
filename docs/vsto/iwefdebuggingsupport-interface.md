---
title: Interface IWefDebuggingSupport
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 351fb69b99393a10518168f4f9b01efe1f9efaa7
ms.sourcegitcommit: 0aafcfa08ef74f162af2e5079be77061d7885cac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34572667"
---
# <a name="iwefdebuggingsupport-interface"></a>Interface IWefDebuggingSupport
  Implementado por um ambiente de depuração, como o Visual Studio, para facilitar a depuração de aplicativos do Office. O aplicativo do Office, como o Word ou Excel, obtém essa interface do Visual Studio e, em seguida, chama métodos na interface em determinados pontos durante a sessão de depuração.  
  
## <a name="syntax"></a>Sintaxe  
  
```csharp 
[  
    uuid(ccaf1a90-ce1c-4199-9cd6-b40c5c57a671),  
    oleautomation  
]  
interface IWefDebuggingSupport : IUnknown  
{  
    HRESULT SetWefProcessId(  
        [in] DWORD dwProcessId);  
    HRESULT GetAutoInsertExtensions(  
        [out, retval] SAFEARRAY(BSTR)* psaExtensionNames);  
}  
```  
  
## <a name="methods"></a>Métodos  
 A tabela a seguir lista os métodos que define a interface IWefDebuggingSupport.  
  
|Nome|Descrição|  
|----------|-----------------|  
|[Método GetAutoInsertExtensions](../vsto/getautoinsertextensions-method.md)|Obtém informações sobre os aplicativos do Office que serão inseridos automaticamente durante a depuração.|  
|[Método SetWefProcessId](../vsto/setwefprocessid-method.md)|Fornece o identificador do processo que executará o conteúdo da estrutura de extensões da Web (WEF).|  
  
  