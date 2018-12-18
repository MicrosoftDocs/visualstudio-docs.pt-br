---
title: AddMessage | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 102a0404-a00c-4566-93f3-01bc8df63280
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: de3460a345dba21e3a8f481adb510b9e3bdd4990
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31473342"
---
# <a name="addmessage"></a>AddMessage
Adiciona uma mensagem personalizada para o diagnóstico de gráficos *HUD* (visor).  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
void AddMessage(  
  wchar_t const * szMessage  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `szMessage`  
 A mensagem a ser adicionada para o HUD.  
  
## <a name="remarks"></a>Comentários  
 O HUD de diagnóstico de gráficos é exibido no canto superior esquerdo do aplicativo que está sendo executado com o diagnóstico de gráficos. Exibe informações de tempo de execução sobre o aplicativo e sobre a captura de informações de elementos gráficos e mensagens que são adicionadas ao chamar essa função.  
  
 Para adicionar uma mensagem para o HUD, você não precisa estar ativamente capturando informações de gráficos — ou seja, uma mensagem pode ser adicionada por meio de uma instância do `VsgDbg` classe, mas o [Init](init.md) função de membro não ser chamado primeiro. Mensagens são exibidas somente no HUD, eles não são registrados no arquivo de log de elementos gráficos.