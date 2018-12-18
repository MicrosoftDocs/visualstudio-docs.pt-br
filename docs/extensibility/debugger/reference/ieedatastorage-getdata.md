---
title: IEEDataStorage::GetData | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IEEDataStorage::GetData
helpviewer_keywords:
- IEEDataStorage::GetData
ms.assetid: 4d384039-73d4-40b4-ace6-a2474c546397
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 88ca53843c342547a0c0641bcb76f8e1166723ab
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49860586"
---
# <a name="ieedatastoragegetdata"></a>IEEDataStorage::GetData
Recupera o número especificado de bytes do objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetData(  
   ULONG  dataSize,  
   ULONG* sizeGotten,  
   BYTE*  data  
);  
```  
  
```csharp  
int GetData(  
   uint     dataSize,  
   out uint sizeGotten,  
   byte[]   data  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `dataSize`  
 [in] O número de bytes a serem recuperados (o `data` matriz deve conter pelo menos esse número de bytes).  
  
 `sizeGotten`  
 [out] Retorna o número de bytes realmente recuperados.  
  
 `data`  
 [no, out] Matriz a ser preenchida com os dados solicitados.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 É recomendado o uso desse método recuperar todos os bytes de dados em uma matriz local, já que não há nenhuma maneira de ignorar bytes no processo de recuperação. Nesse caso, o parâmetro `dataSize` deve ser o valor retornado pelo [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md) método.  
  
## <a name="see-also"></a>Consulte também  
 [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)   
 [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)