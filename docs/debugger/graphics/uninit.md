---
title: UnInit | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 4cd4fc0b-974a-4e61-9ea8-0aaa1a0c52ea
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 56aa940d65934f7cc72f692f5bdf5e44854d276c
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31471447"
---
# <a name="uninit"></a>UnInit
Finaliza o arquivo de log do gráfico, fecha e libera os recursos que foram usados enquanto o aplicativo foi ativamente gravando informações de gráficos.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
void UnInit();  
```  
  
## <a name="remarks"></a>Comentários  
 `UnInit` é chamado automaticamente quando uma instância do `VsgDbg` classe é destruída. Se o `VsgDbg` instância não foi ativamente gravando informações de gráficos, isso não tem nenhum efeito.  
  
 Após `UnInit` foi chamado em uma instância do `VsgDbg` classe gráficos uma novo arquivo de log pode ser criado chamando `Init` e finalizado chamando `UnInit`. Você pode repetir esta quantas vezes você deseja usar o mesmo `VsgDbg` instância para criar o gráfico independente de vários arquivos de log.  
  
## <a name="see-also"></a>Consulte também  
 [Init](init.md)