---
title: DONT_SAVE_VSGLOG_TO_TEMP | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f27ab0e6-9575-4ca0-9901-37d3e5c3a2f5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 967ff50991efbbd7b598605abd992b298367d01c
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55006171"
---
# <a name="dontsavevsglogtotemp"></a>DONT_SAVE_VSGLOG_TO_TEMP
Define sua presença se o arquivo de log de gráficos é salvo para o diretório de arquivos temporários do usuário.  

## <a name="syntax"></a>Sintaxe  

```C++  
#define DONT_SAVE_VSGLOG_TO_TEMP  
```  

## <a name="value"></a>Valor  
 Um símbolo do pré-processador que, por sua presença ou ausência, determina se o arquivo de log de gráficos é salvo para o diretório de arquivos temporários do usuário. Se esse símbolo é definido e, em seguida, o nome de arquivo definido pelo `VSG_DEFAULT_RUN_FILENAME` é relativo ao diretório atual do aplicativo capturado, ou é um caminho absoluto; caso contrário, o nome de arquivo definido pelo `VSG_DEFAULT_RUN_FILENAME` é relativo ao diretório de arquivos temporários do usuário e não pode ser um caminho absoluto.  

## <a name="remarks"></a>Comentários  
 Dependendo dos privilégios do usuário, o arquivo de log de gráficos não poderá ser salva em um local arbitrário. É recomendável que você prefere salvar os logs de gráficos para o diretório de arquivos temporários do usuário ou outro local válida, se você não souber o local, você escolheria se pode ser gravado em pelo usuário.  

 Para impedir que o arquivo de log de gráficos que estão sendo salvos no diretório de arquivos temporários, você deve ser definido `DONT_SAVE_VSGLOG_TO_TEMP` antes de incluir `vsgcapture.h`.  

## <a name="example"></a>Exemplo  
 Este exemplo mostra como salvar o arquivo de log de gráficos em um caminho absoluto no computador host.  

```cpp
// Define DONT_SAVE_VSGLOG_TO_TEMP and VSG_DEFAULT_RUN_FILENAME before including vsgcapture.h  
#define DONT_SAVE_VSGLOG_TO_TEMP  
#define VSG_DEFAULT_RUN_FILENAME L"C:\\Graphics Diagnostics Captures\\default.vsglog"  

#include <vsgcapture.h>  
```  

## <a name="see-also"></a>Consulte também  
 [VSG_DEFAULT_RUN_FILENAME](vsg-default-run-filename.md)
