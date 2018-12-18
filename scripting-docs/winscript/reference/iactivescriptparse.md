---
title: IActiveScriptParse | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptParse interface
ms.assetid: 8c967d70-f582-4f64-9e79-49f40c4dcb7c
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5b0e3990ca43043909d99b309f58a344c1727450
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645826"
---
# <a name="iactivescriptparse"></a>IActiveScriptParse
Se o Script do Windows mecanismo permite texto não processado miniscripts de código a ser adicionado ao script ou permite que o texto de expressão a ser avaliada em tempo de execução, ele implementa o `IActiveScriptParse` interface. Interpretado para linguagens de scripts com nenhum ambiente de criação independente, como o VBScript, isso fornece um mecanismo alternativo (diferente de `IPersist*`) para obter o código de script no mecanismo de script e anexar objeto vários fragmentos de script eventos.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IActiveScriptParse::InitNew](../../winscript/reference/iactivescriptparse-initnew.md)|Inicializa o mecanismo de script.|  
|[IActiveScriptParse::AddScriptlet](../../winscript/reference/iactivescriptparse-addscriptlet.md)|Adiciona um miniscript de código para o script.|  
|[IActiveScriptParse::ParseScriptText](../../winscript/reference/iactivescriptparse-parsescripttext.md)|Analisa o miniscript de código fornecido, adicionar declarações para o espaço de nome e avaliar o código conforme apropriado.|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de script ativo](../../winscript/reference/active-script-interfaces.md)