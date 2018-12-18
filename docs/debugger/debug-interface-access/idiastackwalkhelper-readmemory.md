---
title: IDiaStackWalkHelper::readMemory | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::readMemory method
ms.assetid: e1eb90aa-49b7-476c-9e70-7e8f08994cbe
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 76b054d004e6c62f9d36ca5fcebe1a7f0476fbfc
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49825849"
---
# <a name="idiastackwalkhelperreadmemory"></a>IDiaStackWalkHelper::readMemory
Lê um bloco de dados de imagem do arquivo executável na memória.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT readMemory(   
   enum MemoryTypeEnum type,  
   ULONGLONG           va,  
   DWORD               cbData,  
   DWORD*              pcbData,  
   BYTE*               pbData  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `type`  
 [in] Um valor da [enumeração MemoryTypeEnum](../../debugger/debug-interface-access/memorytypeenum.md) enumeração que especifica o tipo de memória a ser lido.  
  
 VA  
 [in] Endereço virtual na imagem a partir do qual será iniciada a leitura.  
  
 `cbData`  
 [in] O tamanho do buffer de dados em bytes.  
  
 `pcbData`  
 [out] Retorna o número de bytes realmente lidos. Se `pbData` é `NULL`, em seguida, isso é o número total de bytes de dados disponíveis.  
  
 `pbData`  
 [no, out] Um buffer que será preenchido com a memória de leitura.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)   
 [Enumeração MemoryTypeEnum](../../debugger/debug-interface-access/memorytypeenum.md)