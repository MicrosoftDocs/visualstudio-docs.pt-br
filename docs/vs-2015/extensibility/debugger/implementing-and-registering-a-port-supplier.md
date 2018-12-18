---
title: Implementar e registrar um fornecedor de porta | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- debugging [Debugging SDK], registering port suppliers
- port suppliers, registering
ms.assetid: fb057052-ee16-4272-8e16-a4da5dda0ad4
caps.latest.revision: 18
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 3844d6beca76781f741bfbe0c6bff71923075d36
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51728937"
---
# <a name="implementing-and-registering-a-port-supplier"></a>Implementando e registrando um fornecedor de porta
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

A função de um fornecedor de porta é acompanhar e fornecer portas, que por sua vez, gerenciar processos. No momento em que uma porta precisa ser criado, o fornecedor de porta é instanciado usando CoCreate com o GUID do fornecedor de porta (o Gerenciador de sessão de depuração [SDM] usará o fornecedor de porta, o usuário selecionado ou o fornecedor de porta especificada pelo sistema do projeto). Em seguida, chamará o SDM [CanAddPort](../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md) para ver se todas as portas podem ser adicionadas. Se uma porta pode ser adicionada, uma nova porta é solicitada, chamando [adicionar porta](../../extensibility/debugger/reference/idebugportsupplier2-addport.md) e passando-o um [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md) que descreve a porta. `AddPort` Retorna uma nova porta representada por uma [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) interface.  
  
## <a name="discussion"></a>Discussão  
 Uma porta é criada por um fornecedor de porta, por sua vez, associado a um servidor de depuração ou de máquina. Um servidor pode enumerar seus fornecedores de porta por meio de[EnumPortSuppliers](../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md) método e um fornecedor de porta podem enumerar suas portas por meio das [EnumPorts](../../extensibility/debugger/reference/idebugportsupplier2-enumports.md) método.  
  
 O registro COM típico, além de um fornecedor de porta deve ser registrado com o Visual Studio, colocando seu CLSID e o nome em locais específicos do registro. Chamado de uma função auxiliar de depuração SDK `SetMetric` manipula esse fardo: ele é chamado uma vez para cada item a ser registrado, assim:  
  
```cpp#  
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
  
 Um fornecedor de porta cancela o registro em si chamando `RemoveMetric` (outra função de auxiliar de depuração SDK) uma vez para cada item que foi registrado, assim:  
  
```cpp#  
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
>  O [auxiliares do SDK para depuração](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) `SetMetric` e `RemoveMetric` são definidos no dbgmetric.h e compilados em ad2de.lib de funções estáticas. O `metrictypePortSupplier`, `metricCLSID`, e `metricName` auxiliares também são definidos no dbgmetric.h.  
  
 Um fornecedor de porta pode fornecer seu nome e GUID, por meio dos métodos [GetPortSupplierName](../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md) e [GetPortSupplierId](../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md), respectivamente.  
  
## <a name="see-also"></a>Consulte também  
 [Implementando um fornecedor de porta](../../extensibility/debugger/implementing-a-port-supplier.md)   
 [Auxiliares do SDK para depuração](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)   
 [Fornecedores de porta](../../extensibility/debugger/port-suppliers.md)

