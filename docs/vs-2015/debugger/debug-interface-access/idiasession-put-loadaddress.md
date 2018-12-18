---
title: 'Idiasession:: Put_loadaddress | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::put_loadAddress method
ms.assetid: b157b245-1ea0-4b80-8962-d8b278dbc742
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: daf1e7748a95ae0ad2d7fce3592e0a6948077f45
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51762008"
---
# <a name="idiasessionputloadaddress"></a>IDiaSession::put_loadAddress
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Define o endereço de carregamento para o arquivo executável que corresponde aos símbolos nesse repositório de símbolos.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT put_loadAddress (   
   ULONGLONG NewVal  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `NewVal`  
 [in] Carregar o endereço para o arquivo executável.  
  
## <a name="remarks"></a>Comentários  
 Propriedades de endereço virtual (VA) de símbolo são calculadas usando o valor desse método. Endereços virtuais não são calculados, a menos que essa propriedade é definida como diferente de zero.  
  
> [!NOTE]
>  Você deve chamar esse método quando você receber o [IDiaSession](../../debugger/debug-interface-access/idiasession.md) do objeto e antes de começar a usar o objeto se você precisar usar quaisquer propriedades virtuais nos símbolos.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)



