---
title: IDebugEngineLaunch2::LaunchSuspended | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugEngineLaunch2::LaunchSuspended
helpviewer_keywords:
- IDebugEngineLaunch2::LaunchSuspended
ms.assetid: 5dd2643e-c20a-470e-9024-2a423eb39856
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ffe5bdd0619ae5954a34fde50518adb3767d1825
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49926495"
---
# <a name="idebugenginelaunch2launchsuspended"></a>IDebugEngineLaunch2::LaunchSuspended
Esse método inicia um processo por meio do mecanismo de depuração (DES).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT LaunchSuspended (   
   LPCOLESTR             pszMachine,  
   IDebugPort2*          pPort,  
   LPCOLESTR             pszExe,  
   LPCOLESTR             pszArgs,  
   LPCOLESTR             pszDir,  
   BSTR                  bstrEnv,  
   LPCOLESTR             pszOptions,  
   LAUNCH_FLAGS          dwLaunchFlags,  
   DWORD                 hStdInput,  
   DWORD                 hStdOutput,  
   DWORD                 hStdError,  
   IDebugEventCallback2* pCallback,  
   IDebugProcess2**      ppDebugProcess  
);  
```  
  
```csharp  
int LaunchSuspended(  
   string               pszServer,   
   IDebugPort2          pPort,   
   string               pszExe,   
   string               pszArgs,   
   string               pszDir,   
   string               bstrEnv,   
   string               pszOptions,   
   enum_LAUNCH_FLAGS    dwLaunchFlags,   
   uint                 hStdInput,   
   uint                 hStdOutput,   
   uint                 hStdError,  
   IDebugEventCallback2 pCallback,   
   out IDebugProcess2   ppProcess  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pszMachine`  
 [in] O nome do computador no qual iniciar o processo. Use um valor nulo para especificar o computador local.  
  
 `pPort`  
 [in] O [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) interface que representa a porta que o programa será executado em.  
  
 `pszExe`  
 [in] O nome do executável a ser iniciado.  
  
 `pszArgs`  
 [in] Os argumentos a serem passados para o executável. Pode ser um valor nulo se não houver nenhum argumento.  
  
 `pszDir`  
 [in] O nome do diretório de trabalho usado pelo executável. Pode ser um valor nulo se nenhum diretório de trabalho é necessário.  
  
 `bstrEnv`  
 [in] Bloco de ambiente de cadeias de caracteres terminada em nulo, seguido por um terminador nulo adicional.  
  
 `pszOptions`  
 [in] As opções para o executável.  
  
 `dwLaunchFlags`  
 [in] Especifica o [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md) para uma sessão.  
  
 `hStdInput`  
 [in] Identificador para um fluxo de entrada alternativo. Pode ser 0 se o redirecionamento não for necessário.  
  
 `hStdOutput`  
 [in] Identificador para um fluxo de saída alternativos. Pode ser 0 se o redirecionamento não for necessário.  
  
 `hStdError`  
 [in] Identificador para um fluxo de saída de erro alternativa. Pode ser 0 se o redirecionamento não for necessário.  
  
 `pCallback`  
 [in] O [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) objeto que recebe eventos do depurador.  
  
 `ppDebugProcess`  
 [out] Retorna o resultante [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) objeto que representa o processo iniciado.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Normalmente, [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] inicia um programa usando o [LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md) método e, em seguida, anexa o depurador ao programa suspenso. No entanto, há circunstâncias em que o mecanismo de depuração talvez precise iniciar um programa (por exemplo, se o mecanismo de depuração é parte de um interpretador e o programa que está sendo depurado é uma linguagem interpretada), caso em que [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] usa o `IDebugEngineLaunch2::LaunchSuspended` método .  
  
 O [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md) método é chamado para iniciar o processo depois que o processo foi iniciado com êxito em um estado suspenso.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)   
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)   
 [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)   
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)   
 [LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)   
 [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)