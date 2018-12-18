---
title: 'Vsgdbg:: Vsgdbg (construtor) | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 670651e6-5e79-4845-b0c2-671beb7055a8
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 04f33b117a7ee47fb0c11932c3722f6f2a4a3541
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31473297"
---
# <a name="vsgdbgvsgdbg-constructor"></a>VsgDbg::VsgDbg (Construtor)
Constrói uma instância do `VsgDbg` classe com ou sem Preparando o componente no aplicativo de diagnóstico de gráficos para capturar e registrar informações de gráficos por padrão, com base no parâmetro booliano especificado ativamente.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
VsgDbg(  
  bDefaultInit  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `bDefaultInit`  
 `true` para especificar que o componente no aplicativo de diagnóstico de gráficos deve estar preparado para capturar ativamente e gravar informações de elementos gráficos. `false` para especificar que o aplicativo não deve estar preparado para capturar e registrar informações de elementos gráficos no momento ativamente.  
  
## <a name="remarks"></a>Comentários  
 Quando o construtor for chamado com `bDefaultInit` definida como `true`, o nome do arquivo do arquivo de log do gráfico é determinado por como o `DONT_SAVE_VSGLOG_TO_TEMP` e `VSG_DEFAULT_RUN_FILENAME` símbolos de pré-processamento são definidos antes de `vsgcapture.h` está incluído em seu aplicativo.  
  
 Quando o construtor for chamado com `bDefaultInit` definida como `false`, o componente no aplicativo de diagnóstico de gráficos pode estar preparado para capturar ativamente e registram as informações de elementos gráficos em um momento posterior, chamando o `Init` função.  
  
## <a name="see-also"></a>Consulte também  
 [VsgDbg:: ~ VsgDbg (destruidor)](vsgdbg-tilde-vsgdbg-destructor.md)   
 [Init](init.md)   
 [DONT_SAVE_VSGLOG_TO_TEMP](dont-save-vsglog-to-temp.md)   
 [VSG_DEFAULT_RUN_FILENAME](vsg-default-run-filename.md)