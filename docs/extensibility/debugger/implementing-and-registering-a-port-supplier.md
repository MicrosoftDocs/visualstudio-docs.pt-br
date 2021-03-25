---
title: Implementando e registrando um fornecedor de porta | Microsoft Docs
description: Saiba como implementar e registrar um fornecedor de porta, que controla e fornece portas, que gerenciam processos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], registering port suppliers
- port suppliers, registering
ms.assetid: fb057052-ee16-4272-8e16-a4da5dda0ad4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 16c1738d4059468384df7ee2e882c20c8b5a0537
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059815"
---
# <a name="implement-and-register-a-port-supplier"></a>Implementar e registrar um fornecedor de porta
A função de um fornecedor de porta é rastrear e fornecer portas que, por sua vez, gerenciam processos. Quando uma porta precisa ser criada, o fornecedor da porta é instanciado usando CoCreate com o GUID do fornecedor da porta (o Gerenciador de depuração de sessão [SDM] usará o fornecedor da porta que o usuário selecionou ou o fornecedor da porta especificado pelo sistema de projeto). O SDM então chama [CanAddPort](../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md) para ver se qualquer porta pode ser adicionada. Se uma porta puder ser adicionada, uma nova porta será solicitada chamando [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md) e passando-a um [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md) que descreve a porta. `AddPort` Retorna uma nova porta representada por uma interface [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) .

## <a name="discussion"></a>Discussão
 Uma porta é criada por um fornecedor de porta, que está associado a um computador ou servidor de depuração. Um servidor enumera seus fornecedores de porta por meio do método[EnumPortSuppliers](../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md) e um fornecedor de porta enumera suas portas por meio do método [EnumPorts](../../extensibility/debugger/reference/idebugportsupplier2-enumports.md) .

 Além do registro COM típico, um fornecedor de porta deve se registrar no Visual Studio colocando seu CLSID e nome em locais de registro específicos. Uma função auxiliar do SDK de depuração chamada `SetMetric` manipula essa tarefa: ela é chamada uma vez para cada item a ser registrado, portanto:

```cpp
SetMetric(metrictypePortSupplier,
          <GUID of your port supplier>,
          metricCLSID,
          <CLSID of your port supplier>,
          false,
          NULL)
SetMetric(metrictypePortSupplier,
          <GUID of your port supplier>,
          metricName,
          <name of your port supplier>,
          false,
          NULL);
```

 Um fornecedor de porta cancela o registro chamando `RemoveMetric` (outra função auxiliar do SDK de depuração) uma vez para cada item registrado, portanto:

```cpp
RemoveMetric(metrictypePortSupplier,
             <GUID of your port supplier>,
             metricCLSID,
             NULL);
RemoveMetric(metrictypePortSupplier,
             <GUID of your port supplier>,
             metricName,
             NULL);
```

> [!NOTE]
> Os [auxiliares do SDK para depuração](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) `SetMetric` e `RemoveMetric` são funções estáticas definidas em *dbgmetric. h* e compiladas em *ad2de. lib*. Os `metrictypePortSupplier` `metricCLSID` `metricName` auxiliares, e também são definidos em *dbgmetric. h*.

 Um fornecedor de porta pode fornecer seu nome e GUID por meio dos métodos [GetPortSupplierName](../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md) e [GetPortSupplierId](../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md), respectivamente.

## <a name="see-also"></a>Confira também
- [Implementar um fornecedor de porta](../../extensibility/debugger/implementing-a-port-supplier.md)
- [Auxiliares do SDK para depuração](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [Fornecedores de porta](../../extensibility/debugger/port-suppliers.md)
