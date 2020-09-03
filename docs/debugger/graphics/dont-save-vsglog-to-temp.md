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
ms.openlocfilehash: 40f3c3c22de6b4b0ebdbdf2dfc953f4cb1c9b5e6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "72736085"
---
# <a name="dont_save_vsglog_to_temp"></a>DONT_SAVE_VSGLOG_TO_TEMP
Define por sua presença se o arquivo de log de gráficos é salvo no diretório de arquivos temporários do usuário.

## <a name="syntax"></a>Syntax

```C++
#define DONT_SAVE_VSGLOG_TO_TEMP
```

## <a name="value"></a>Valor
 Um símbolo de pré-processador que, por sua presença ou ausência, determina se o arquivo de log de gráficos é salvo no diretório de arquivos temporários do usuário. Se esse símbolo for definido, o nome do arquivo definido pelo `VSG_DEFAULT_RUN_FILENAME` será relativo ao diretório atual do aplicativo capturado, ou será um caminho absoluto; caso contrário, o nome do arquivo definido pelo `VSG_DEFAULT_RUN_FILENAME` será relativo ao diretório de arquivos temporários do usuário e não poderá ser um caminho absoluto.

## <a name="remarks"></a>Comentários
 Dependendo dos privilégios do usuário, o arquivo de log de gráficos pode não ser capaz de ser salvo em um local arbitrário. Recomendamos que você prefira salvar os logs de gráficos no diretório de arquivos temporários do usuário ou em outro local válido, se não tiver certeza se o local escolhido pode ser gravado pelo usuário.

 Para impedir que o arquivo de log de elementos gráficos seja salvo no diretório de arquivos temporários, você deve definir `DONT_SAVE_VSGLOG_TO_TEMP` antes de incluir `vsgcapture.h` .

## <a name="example"></a>Exemplo
 Este exemplo mostra como salvar o arquivo de log de gráficos em um caminho absoluto no computador host.

```cpp
// Define DONT_SAVE_VSGLOG_TO_TEMP and VSG_DEFAULT_RUN_FILENAME before including vsgcapture.h
#define DONT_SAVE_VSGLOG_TO_TEMP
#define VSG_DEFAULT_RUN_FILENAME L"C:\\Graphics Diagnostics Captures\\default.vsglog"

#include <vsgcapture.h>
```

## <a name="see-also"></a>Confira também
- [VSG_DEFAULT_RUN_FILENAME](vsg-default-run-filename.md)
