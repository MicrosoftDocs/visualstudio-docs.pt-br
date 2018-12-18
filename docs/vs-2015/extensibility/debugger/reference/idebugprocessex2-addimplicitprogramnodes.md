---
title: IDebugProcessEx2::AddImplicitProgramNodes | Microsoft Docs
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
- IDebugProcessEx2::AddImplicitProgramNodes
helpviewer_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes method
ms.assetid: 8b491b00-f9e7-45b3-9115-fe58c3464289
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8b416fdfd3c3a08d028bb01945f2ceb02ae5f8e3
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51733581"
---
# <a name="idebugprocessex2addimplicitprogramnodes"></a>IDebugProcessEx2::AddImplicitProgramNodes
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Esse método adiciona um nó de programa para cada mecanismo de depuração (DES) especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT AddImplicitProgramNodes(  
   REFGUID guidLaunchingEngine,  
   GUID*   rgguidSpecificEngines,  
   DWORD   celtSpecificEngines  
);  
```  
  
```csharp  
int AddImplicitProgramNodes(  
   ref Guid guidLaunchingEngine,  
   Guid[]   rgguidSpecificEngines,  
   uint     celtSpecificEngines  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `guidLaunchingEngine`  
 [in] O `GUID` de a DE que deve ser usada para iniciar programas (e é considerada como para adicionar seus próprios nós de programa).  
  
 `rgguidSpecificEngines`  
 [in] Matriz de `GUID`s de DEs para qual programa nós serão adicionados.  
  
 `celtSpecificEngines`  
 [in] O número de `GUID`s no `rgguidSpecificEngines` matriz.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 [Nós de programa](../../../extensibility/debugger/program-nodes.md) será adicionado para cada Alemanha listados no `rgguidSpecificEngines`— exceto o mecanismo de inicialização (conforme indicado na `guidLaunchingEngine`), que são assumidos para adicionar seu próprio nó de programa quando ele inicia um programa.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)   
 [Nós de programa](../../../extensibility/debugger/program-nodes.md)

