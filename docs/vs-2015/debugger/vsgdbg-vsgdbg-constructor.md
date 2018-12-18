---
title: 'Vsgdbg:: Vsgdbg (construtor) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 670651e6-5e79-4845-b0c2-671beb7055a8
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 056c5f5e19a4d1e025969aa40ad75f3852b4201b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51781914"
---
# <a name="vsgdbgvsgdbg-constructor"></a>VsgDbg::VsgDbg (Construtor)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Constrói uma instância do `VsgDbg` classe com ou sem Preparando o componente no aplicativo de diagnóstico de gráficos para capturar ativamente e gravar informações de gráficos por padrão, com base no parâmetro booliano especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
VsgDbg(  
  bDefaultInit  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `bDefaultInit`  
 `true` para especificar que o componente no aplicativo de diagnóstico de gráficos é estar preparado para capturar ativamente e registrar informações de gráficos; `false` para especificar que o aplicativo não deve estar preparado para capturar e registrar informações de gráficos no momento ativamente.  
  
## <a name="remarks"></a>Comentários  
 Quando o construtor é chamado com `bDefaultInit` definido como `true`, o nome do arquivo do arquivo de log de gráficos é determinado por como o `DONT_SAVE_VSGLOG_TO_TEMP` e `VSG_DEFAULT_RUN_FILENAME` símbolos de pré-processamento são definidos antes de `vsgcapture.h` está incluído no seu aplicativo.  
  
 Quando o construtor é chamado com `bDefaultInit` definido como `false`, o componente no aplicativo de diagnóstico de gráficos pode estar preparado para capturar ativamente e registrar informações de gráficos em um momento posterior chamando o `Init` função.  
  
## <a name="see-also"></a>Consulte também  
 [VsgDbg:: ~ VsgDbg (destruidor)](../debugger/vsgdbg-tilde-vsgdbg-destructor.md)   
 [Init](../debugger/init.md)   
 [DONT_SAVE_VSGLOG_TO_TEMP](../debugger/dont-save-vsglog-to-temp.md)   
 [VSG_DEFAULT_RUN_FILENAME](../debugger/vsg-default-run-filename.md)



