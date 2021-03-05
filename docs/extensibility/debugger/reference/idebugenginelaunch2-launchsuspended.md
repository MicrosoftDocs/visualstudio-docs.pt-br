---
description: Esse método inicia um processo por meio do mecanismo de depuração (DE).
title: 'IDebugEngineLaunch2:: LaunchSuspended | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineLaunch2::LaunchSuspended
helpviewer_keywords:
- IDebugEngineLaunch2::LaunchSuspended
ms.assetid: 5dd2643e-c20a-470e-9024-2a423eb39856
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9fd8b610f99161a9716b9bffc235196165306711
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153580"
---
# <a name="idebugenginelaunch2launchsuspended"></a>IDebugEngineLaunch2::LaunchSuspended
Esse método inicia um processo por meio do mecanismo de depuração (DE).

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

## <a name="parameters"></a>Parâmetros
`pszMachine`\
no O nome do computador no qual iniciar o processo. Use um valor nulo para especificar o computador local.

`pPort`\
no A interface [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) que representa a porta na qual o programa será executado.

`pszExe`\
no O nome do executável a ser iniciado.

`pszArgs`\
no Os argumentos a serem passados para o executável. Pode ser um valor nulo se não houver argumentos.

`pszDir`\
no O nome do diretório de trabalho usado pelo executável. Pode ser um valor nulo se nenhum diretório de trabalho for necessário.

`bstrEnv`\
no Bloco de ambiente de cadeias de caracteres terminadas em nulo, seguido por um terminador nulo adicional.

`pszOptions`\
no As opções para o executável.

`dwLaunchFlags`\
no Especifica o [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md) para uma sessão.

`hStdInput`\
no Identificador para um fluxo de entrada alternativo. Pode ser 0 se o redirecionamento não for necessário.

`hStdOutput`\
no Identificador para um fluxo de saída alternativo. Pode ser 0 se o redirecionamento não for necessário.

`hStdError`\
no Identificador para um fluxo de saída de erro alternativo. Pode ser 0 se o redirecionamento não for necessário.

`pCallback`\
no O objeto [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) que recebe eventos do depurador.

`ppDebugProcess`\
fora Retorna o objeto [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) resultante que representa o processo iniciado.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Normalmente, [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] o inicia um programa usando o método [LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md) e anexa o depurador ao programa suspenso. No entanto, há circunstâncias em que o mecanismo de depuração pode precisar iniciar um programa (por exemplo, se o mecanismo de depuração faz parte de um intérprete e o programa que está sendo depurado é uma linguagem interpretada), nesse caso, o [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] usa o `IDebugEngineLaunch2::LaunchSuspended` método.

 O método [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md) é chamado para iniciar o processo depois que o processo é iniciado com êxito em um estado suspenso.

## <a name="see-also"></a>Confira também
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)
- [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)
