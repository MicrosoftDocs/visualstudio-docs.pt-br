---
title: ToggleHUD | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 7261e01d-3c72-46ce-9fb3-5f33b2ddb901
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 86ce582ab49d4d079f01f7231f49aa761baa1069
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31472507"
---
# <a name="togglehud"></a>ToggleHUD
Alterna o diagnóstico de gráficos *HUD* (visor) sobreposição ativado ou desativado.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
void ToggleHUD();  
```  
  
## <a name="remarks"></a>Comentários  
 O HUD de diagnóstico de gráficos é exibido no canto superior esquerdo do aplicativo que está sendo executado com o diagnóstico de gráficos. Exibe informações de tempo de execução sobre o aplicativo e sobre a captura de informações de elementos gráficos e mensagens que são adicionadas ao chamar o [AddMessage](addmessage.md) função de membro.  
  
 Para alternar o HUD, você não precisa estar ativamente capturando informações de gráficos — ou seja, ele pode ser alternado por meio de uma instância do `VsgDbg` classe, mas o [Init](init.md) função de membro não precisa ser chamado primeiro.