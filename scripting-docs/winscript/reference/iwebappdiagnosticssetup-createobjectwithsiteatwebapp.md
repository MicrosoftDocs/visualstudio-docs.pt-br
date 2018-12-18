---
title: IWebAppDiagnosticsSetup::CreateObjectWithSiteAtWebApp | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IWebAppDiagnosticsSetup::CreateObjectWithSiteAtWebApp
ms.assetid: 30975973-acb1-48f4-8266-5e097a57db22
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1442297fcacb3a9464f9ea67489c91c8ab64ad78
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24733936"
---
# <a name="iwebappdiagnosticssetupcreateobjectwithsiteatwebapp"></a>IWebAppDiagnosticsSetup::CreateObjectWithSiteAtWebApp
Esse método cria junto a classe cuja ID é passar com `rclsid` usando o `dwClsContext`. Isso é semelhante à forma como [IRemoteDebugApplication::CreateInstanceAtApplication](../../winscript/reference/iremotedebugapplication-createinstanceatapplication.md) funciona, exceto que no caso de `CreateObjectWithSiteAtWebApp` o objeto é criado de forma assíncrona no thread de interface do usuário do aplicativo da web. O objeto especificado pela ID de classe deve implementar [IWebAppDiagnosticsObjectInitialization Interface](../../winscript/reference/iwebappdiagnosticsobjectinitialization-interface.md). Depois que o objeto foi criado, [IWebAppDiagnosticsObjectInitialization::Initialize](../../winscript/reference/iwebappdiagnosticsobjectinitialization-initialize.md) é chamado com uma referência para o aplicativo de depuração PDM e `hPassToObject` parâmetro `CreateObjectWithSiteAtWebApp`. Você pode usar esse método para passar um identificador para o aplicativo para um pipe anônimo que você copiou usando [DuplicateHandle](http://go.microsoft.com/fwlink/?LinkId=232450).  
  
> [!IMPORTANT]
>  [IWebAppDiagnosticsSetup Interface](../../winscript/reference/iwebappdiagnosticssetup-interface.md) é implementada por v PDM 11.0 e maior. Localizado em. activdbg100.h.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateObjectWithSiteAtWebApp(        [in] REFCLSID rclsid,         [in] DWORD dwClsContext,         [in] REFIID riid,         [in] DWORD_PTR hPassToObject        );  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `rclsid`  
 A ID de classe da classe para criar.  
  
 `dwClsContext`  
 O contexto no qual o código será executado. Na maioria dos casos é CLSCTX_INPROC_SERVER.  
  
 `riid`  
 Não usado.  
  
 `hPassToObject`  
 Um valor que será passado para o objeto quando ele é criado no thread da interface do usuário, se o objeto implementa [IWebAppDiagnosticsObjectInitialization Interface](../../winscript/reference/iwebappdiagnosticsobjectinitialization-interface.md).