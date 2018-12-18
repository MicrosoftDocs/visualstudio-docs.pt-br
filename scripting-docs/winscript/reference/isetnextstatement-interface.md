---
title: Interface ISetNextStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: b570c2e0-a173-4f14-97d8-f39465753115
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bdd71a427a8ef2c57684eef75a044d0cedf42415
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24733616"
---
# <a name="isetnextstatement-interface"></a>Interface ISetNextStatement
Essa interface é implementada por um interpretador para permitir que o Gerenciador de depuração do processo atualizar a instrução atual. Ele é implementado de um objeto de quadro de pilha, e o PDM obtém essa interface por meio de QueryInterface.  
  
 interface fornece métodos que são úteis para definir o ponto de execução, que determina a próxima instrução a ser executada.  
  
 Além dos métodos herdados de `IUnknown`, o `ISetNextStatement` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[ISetNextStatement::CanSetNextStatement](../../winscript/reference/isetnextstatement-cansetnextstatement.md)|Determina se o ponto de execução pode ser definido para o local especificado.|  
|[ISetNextStatement::SetNextStatement](../../winscript/reference/isetnextstatement-setnextstatement.md)|Define o ponto de execução para o local especificado.|