---
title: 'Idiaframedata:: Get_program | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_program method
ms.assetid: 9201409e-b4b1-4e2e-a9f8-d17678ac538b
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 125c809f32b34b077fae0bb661ef9c2f010a4b8b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49849457"
---
# <a name="idiaframedatagetprogram"></a>IDiaFrameData::get_program
Recupera a cadeia de caracteres de programa que é usada para calcular o registro definido antes da chamada para a função atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT get_program (   
   BSTR* pRetVal  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pRetVal`  
 [out] Retorna a cadeia de caracteres do programa.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.  
  
## <a name="remarks"></a>Comentários  
 A cadeia de caracteres do programa é uma sequência de macros que é interpretada para estabelecer o prólogo. Por exemplo, um quadro de pilha típica pode usar a cadeia de caracteres do programa `"$T0 $ebp = $eip $T0 4 + ^ = $ebp $T0 ^ = $esp $T0 8 + ="`. O formato é a notação inversa polonês, onde os operadores seguem os operandos. `T0` representa uma variável temporária na pilha. Este exemplo executa as seguintes etapas:  
  
1. Mover o conteúdo de registro `ebp` para `T0`.  
  
2. Adicione `4` ao valor na `T0` para produzir um endereço, obter o valor desse endereço e armazenar o valor no registro `eip`.  
  
3. Obtenha o valor no endereço armazenado em `T0` e armazenar esse valor no registro `ebp`.  
  
4. Adicione `8` ao valor na `T0` e armazenar esse valor no registro `esp`.  
  
   Observe que a cadeia de caracteres do programa é específica para a CPU e a convenção de chamada definido para a função representada por quadro de pilhas atual.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)