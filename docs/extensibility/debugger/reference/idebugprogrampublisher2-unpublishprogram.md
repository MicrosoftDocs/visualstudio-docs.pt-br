---
title: IDebugProgramPublisher2::UnpublishProgram | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugProgramPublisher2::UnpublishProgram
helpviewer_keywords:
- IDebugProgramPublisher2::UnpublishProgram
ms.assetid: 627e7d38-b2ac-4873-9a40-37ff7f47cd1d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 2daec6615f98d6e253e65bdc66cb7f1f545f9857
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49822209"
---
# <a name="idebugprogrampublisher2unpublishprogram"></a>IDebugProgramPublisher2::UnpublishProgram
Faz com que um programa não esteja disponível para ser depurado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT UnpublishProgram(  
   IUnknown* pDebuggeeInterface  
);  
```  
  
```csharp  
int UnpublishProgram(  
   object pDebuggeeInterface  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pDebuggeeInterface`  
 [in] Um `IUnknown` interface para o programa. Este é o mesmo valor fornecido para o [PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md) método e identifica exclusivamente o programa que está sendo removido (ou seja, ele é usado como um cookie).  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Para disponibilizar um programa para os mecanismos de depuração e o Gerenciador de sessão de depuração, use o [PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md) método.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)   
 [PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)