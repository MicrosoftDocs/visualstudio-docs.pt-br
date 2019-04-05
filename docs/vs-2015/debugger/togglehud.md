---
title: ToggleHUD | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 7261e01d-3c72-46ce-9fb3-5f33b2ddb901
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 87c2571926b92e59ae03e5e988bbf535474dc6d0
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58924251"
---
# <a name="togglehud"></a>ToggleHUD
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Alterna o diagnóstico de gráficos *HUD* de sobreposição (Head-Up Display) ativada ou desativada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
void ToggleHUD();  
```  
  
## <a name="remarks"></a>Comentários  
 O HUD do diagnóstico de gráficos é exibida no canto superior esquerdo do aplicativo que está em execução no diagnóstico de gráficos. Ele exibe informações de tempo de execução sobre o aplicativo e captura de informações de gráficos e as mensagens que são adicionadas por meio da chamada a [AddMessage](../debugger/addmessage.md) função de membro.  
  
 Para ativar ou desativar o HUD, você não precisa ser ativamente capturando informações de gráficos — ou seja, ele pode ser alternado por meio de uma instância das `VsgDbg` classe, mas o [Init](../debugger/init.md) função de membro não precisa ser chamado primeiro.
