---
title: IDiaSymbol::get_virtualBaseTableType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_virtualBaseTableType method
ms.assetid: e0581c4f-0343-49b5-9754-a48477460e9f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4cb880f82097b8780b7203886977077dd3c16682
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55036895"
---
# <a name="idiasymbolgetvirtualbasetabletype"></a>IDiaSymbol::get_virtualBaseTableType
Recupera o tipo de um ponteiro da tabela base virtual.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT get_virtualBaseTableType(  
   IDiaSymbol *pRetVal  
};  
```  
  
#### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`pRetVal`|[out] Retorna um [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) objeto que especifica o tipo de tabela base.|  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna `S_FALSE` ou um código de erro.  
  
> [!NOTE]
>  Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.  
  
## <a name="remarks"></a>Comentários  
 Um ponteiro da tabela base virtual (`vbtptr`) é um ponteiro oculto em um [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] vtable que manipula a herança de classes base virtuais. Um `vbtptr` podem ter tamanhos diferentes, dependendo das classes herdadas.  
  
 Esse método retorna um [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) objeto que pode ser usado para determinar o tamanho do vbtptr.  
  
## <a name="requirements"></a>Requisitos  
  
|Requisito|Descrição|  
|-----------------|-----------------|  
|Cabeçalho:|dia2.h|  
|Versão:|V DIA SDK 8.0|  
  
## <a name="see-also"></a>Consulte também  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)