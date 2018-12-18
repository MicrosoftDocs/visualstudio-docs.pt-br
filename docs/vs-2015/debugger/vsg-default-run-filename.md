---
title: VSG_DEFAULT_RUN_FILENAME | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ea549d2f-c857-458c-93c7-bc5a2d11d15d
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 07407dc0a50da935d8d5a9fa0eed213633adbe4f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51801050"
---
# <a name="vsgdefaultrunfilename"></a>VSG_DEFAULT_RUN_FILENAME
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Define o nome de arquivo padrão do arquivo de log de gráficos.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
#define VSG_DEFAULT_FILENAME filename  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `filename`  
 O nome do arquivo fornecido por padrão para o arquivo de log de gráficos quando informações de gráficos são capturadas por meio de programação.  
  
## <a name="value"></a>Valor  
 Arquivo de log de uma cadeia de caracteres literal que representa o nome de arquivo dos elementos gráficos. Por padrão, L"default.vsglog".  
  
```cpp  
#define VSG_DEFAULT_FILENAME L"default.vsglog"  
```  
  
## <a name="remarks"></a>Comentários  
 Se o símbolo do pré-processador `DONT_SAVE_VSGLOG_TO_TEMP` é definido, em seguida, o nome do arquivo é relativo ao diretório atual do aplicativo capturado, ou é um caminho absoluto; caso contrário, ele é relativo ao diretório de arquivos temporários do usuário e não pode ser um caminho absoluto.  
  
 Para alterar o nome do arquivo definidos, você deve redefini-la antes de incluir `vsgcapture.h` em seu programa.  
  
## <a name="example"></a>Exemplo  
 Este exemplo mostra como alterar o nome de arquivo padrão do arquivo de captura:  
  
```cpp  
// Redefine the default capture filename before including vsgcapture.h  
#define VSG_DEFAULT_FILENAME L"capture.vsglog"  
  
#include <vsgcapture.h>  
```  
  
## <a name="see-also"></a>Consulte também  
 [DONT_SAVE_VSGLOG_TO_TEMP](../debugger/dont-save-vsglog-to-temp.md)



