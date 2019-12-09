---
title: DONT_SAVE_VSGLOG_TO_TEMP | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: f27ab0e6-9575-4ca0-9901-37d3e5c3a2f5
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 449c6c1ecdb0644b9b52b6ec12ce867dc34d66c4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68156097"
---
# <a name="dontsavevsglogtotemp"></a>DONT_SAVE_VSGLOG_TO_TEMP
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Define sua presença se o arquivo de log de gráficos é salvo para o diretório de arquivos temporários do usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
#define DONT_SAVE_VSGLOG_TO_TEMP  
```  
  
## <a name="value"></a>Valor  
 Um símbolo do pré-processador que, por sua presença ou ausência, determina se o arquivo de log de gráficos é salvo para o diretório de arquivos temporários do usuário. Se esse símbolo é definido e, em seguida, o nome de arquivo definido pelo `VSG_DEFAULT_RUN_FILENAME` é relativo ao diretório atual do aplicativo capturado, ou é um caminho absoluto; caso contrário, o nome de arquivo definido pelo `VSG_DEFAULT_RUN_FILENAME` é relativo ao diretório de arquivos temporários do usuário e não pode ser um caminho absoluto.  
  
## <a name="remarks"></a>Comentários  
 Dependendo dos privilégios do usuário, o arquivo de log de gráficos não poderá ser salva em um local arbitrário. É recomendável que você prefere salvar os logs de gráficos para o diretório de arquivos temporários do usuário ou outro local válida, se você não souber o local, você escolheria se pode ser gravado em pelo usuário.  
  
 Para impedir que o arquivo de log de gráficos que estão sendo salvos no diretório de arquivos temporários, você deve ser definido `DONT_SAVE_VSGLOG_TO_TEMP` antes de incluir `vsgcapture.h`.  
  
## <a name="example"></a>Exemplo  
 Este exemplo mostra como salvar o arquivo de log de gráficos em um caminho absoluto no computador host.  
  
```  
// Define DONT_SAVE_VSGLOG_TO_TEMP and VSG_DEFAULT_RUN_FILENAME before including vsgcapture.h  
#define DONT_SAVE_VSGLOG_TO_TEMP  
#define VSG_DEFAULT_RUN_FILENAME L"C:\\Graphics Diagnostics Captures\\default.vsglog"  
  
#include <vsgcapture.h>  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [VSG_DEFAULT_RUN_FILENAME](../debugger/vsg-default-run-filename.md)
