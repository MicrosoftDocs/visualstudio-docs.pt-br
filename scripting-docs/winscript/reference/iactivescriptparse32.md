---
title: IActiveScriptParse32 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c39c14aa-beb7-4eca-8b8c-2181da1c2e3e
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 688a89515179912c1ed3ac815f0febf50ab4db0f
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724396"
---
# <a name="iactivescriptparse32"></a>IActiveScriptParse32
Se o Script do Windows mecanismo permite texto não processado miniscripts de código a ser adicionado ao script ou permite que o texto de expressão a ser avaliada em tempo de execução, ele implementa o `IActiveScriptParse32` interface. Interpretado para linguagens de scripts com nenhum ambiente de criação independente, como o VBScript, isso fornece um mecanismo alternativo (diferente de `IPersist*`) para obter o código de script no mecanismo de script e anexar objeto vários fragmentos de script eventos.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IActiveScriptParse32::AddScriptlet](../../winscript/reference/iactivescriptparse32-addscriptlet.md)|Adiciona um miniscript de código para o script.|  
|[IActiveScriptParse32::InitNew](../../winscript/reference/iactivescriptparse32-initnew.md)|Inicializa o mecanismo de script.|  
|[IActiveScriptParse32::ParseScriptText](../../winscript/reference/iactivescriptparse32-parsescripttext.md)|Analisa o miniscript de código fornecido, adicionar declarações para o espaço de nome e avaliar o código conforme apropriado.|