---
title: IDebugProgramProvider2::GetProviderProcessData | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- IDebugProgramProvider2::GetProviderProcessData
helpviewer_keywords:
- IDebugProgramProvider2::GetProviderProcessData
ms.assetid: 90cf7b7f-53d2-487e-b793-94501a6e24dd
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 10a98502d432d454d8720ea637d906b6faa67978
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51779626"
---
# <a name="idebugprogramprovider2getproviderprocessdata"></a>IDebugProgramProvider2::GetProviderProcessData
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Recupera uma lista de programas em execução de um processo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetProviderProcessData(  
   PROVIDER_FLAGS         Flags,  
   IDebugDefaultPort2*    pPort,  
   AD_PROCESS_ID          processId,  
   CONST_GUID_ARRAY       EngineFilter,  
   PROVIDER_PROCESS_DATA* pProcess  
);  
```  
  
```csharp  
int GetProviderProcessData(  
   enum_PROVIDER_FLAGS     Flags,  
   IDebugDefaultPort2      pPort,  
   AD_PROCESS_ID           ProcessId,  
   CONST_GUID_ARRAY        EngineFilter,  
   PROVIDER_PROCESS_DATA[] pProcess  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `Flags`  
 [in] Uma combinação de sinalizadores do [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md) enumeração. Os sinalizadores a seguir são típicos para essa chamada:  
  
|Sinalizador|Descrição|  
|----------|-----------------|  
|`PFLAG_REMOTE_PORT`|Chamador está em execução no computador remoto.|  
|`PFLAG_DEBUGGEE`|Chamador está atualmente em depuração (informações adicionais sobre a realização de marshaling serão retornadas para cada nó).|  
|`PFLAG_ATTACHED_TO_DEBUGGEE`|Chamador foi anexado ao, mas não é iniciado pelo depurador.|  
|`PFLAG_GET_PROGRAM_NODES`|Chamador está pedindo para obter uma lista de nós de programa a ser retornado.|  
  
 `pPort`  
 [in] A porta que o processo de chamada está em execução.  
  
 `processId`  
 [in] Uma [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) estrutura que contém a ID do processo que contém o programa em questão.  
  
 `EngineFilter`  
 [in] Uma matriz de GUIDs para os mecanismos de depuração atribuídos para depurar esse processo (eles serão usados para filtrar os programas que são retornados, na verdade, com base no que o suportam os mecanismos fornecidos; se não há mecanismos forem especificados, em seguida, serão retornados todos os programas).  
  
 `pProcess`  
 [out] Um [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md) estrutura será preenchida com as informações solicitadas.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Normalmente, esse método é chamado por um processo para obter uma lista de programas em execução nesse processo. As informações retornadas são uma lista dos [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) objetos.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)   
 [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)   
 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)   
 [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md)   
 [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)   
 [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)   
 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)

