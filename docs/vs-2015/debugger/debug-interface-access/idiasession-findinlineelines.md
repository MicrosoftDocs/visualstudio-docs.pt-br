---
title: IDiaSession::findInlineeLines | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
ms.assetid: b6822d8b-70d5-470b-8278-3aec4680326c
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6603186fd35b1bc2a1ba4ccf2bf5ce052e3d6d65
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68165658"
---
# <a name="idiasessionfindinlineelines"></a>IDiaSession::findInlineeLines
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Recupera uma enumeração que permite que um cliente iterar por meio das informações de número de linha de todas as funções que são embutidas, diretamente ou indiretamente, pelo símbolo pai especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT findInlineeLines (   
   IDiaSymbol*       parent,  
   IDiaEnumLineNumbers** ppResult  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `parent`  
 [in] Um `IDiaSymbol` que representa o pai do objeto.  
  
 `ppResult`  
 [out] Mantém um `IDiaEnumLineNumbers` objeto que contém a lista de números de linha são recuperadas.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)   
 [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
