---
description: Define por sua presença se uma instância padrão da classe de classe VsgDbg, que fornece a interface de captura programática, é fornecida.
title: VSG_NODEFAULT_INSTANCE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 19c95b0d-9a4d-441f-9ed7-3acb39e67521
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: eccdd71c66a9f25e1b0a26f4ea851bcccb738a0b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102155240"
---
# <a name="vsg_nodefault_instance"></a>VSG_NODEFAULT_INSTANCE
Define por sua presença se uma instância padrão da classe de [classe VsgDbg](vsgdbg-class.md) , que fornece a interface de captura programática, é fornecida.

## <a name="syntax"></a>Sintaxe

```C++
#define VSG_NODEFAULT_INSTANCE
```

## <a name="value"></a>Valor
 Um símbolo de pré-processador que, por sua presença ou ausência, determina se uma instância padrão da `VsgDbg` classe é fornecida. Se esse símbolo for definido, nenhuma instância padrão da `VsgDbg` classe será fornecida; caso contrário, uma instância padrão será fornecida e inicializada antes de o programa ser executado.

 A interface de captura programática é fornecida por meio de um ponteiro com escopo global, `g_pVsgDbg` .

```cpp
VsgDbg *g_pVsgDbg;
```

## <a name="remarks"></a>Comentários
 A instância padrão geralmente é suficiente, mas para usar a interface de captura programática dentro de uma DLL quando o dispositivo D3D tiver sido criado fora dessa DLL, você deverá criar e gerenciar sua própria instância da `VsgDbg` classe. Se você estiver gerenciando sua própria interface para a API de captura programática dessa forma, desabilite a instância padrão definindo `VSG_NODEFAULT_INSTANCE` para evitar sobrecarga.

 Se a instância padrão não estiver desabilitada, ela será inicializada automaticamente antes de o programa ser executado e será destruída automaticamente quando o programa terminar. Você não precisa inicializar ou cancelar a inicialização dessa instância explicitamente.

 Para desabilitar a instância padrão, você deve definir o `VSG_NODEFAULT_INSTANCE` antes `vsgcapture.h` de incluir em seu programa.

## <a name="example"></a>Exemplo
 Este exemplo mostra como desabilitar a instância padrão:

```cpp
// Define VSG_NODEFAULT_INSTANCE before including vsgcapture.h
#define VSG_NODEFAULT_INSTANCE

#include <vsgcapture.h>
```
