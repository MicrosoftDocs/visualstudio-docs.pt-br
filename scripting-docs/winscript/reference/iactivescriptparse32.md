---
title: IActiveScriptParse32 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c39c14aa-beb7-4eca-8b8c-2181da1c2e3e
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 568feacfe75de22a330c892a44fa4f4f6fd0e3b8
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835310"
---
# <a name="iactivescriptparse32"></a>IActiveScriptParse32
Se o mecanismo de script do Windows permitir que o código de texto bruto de scriptlets seja adicionado ao script ou permitir que o texto da expressão seja avaliado em tempo de execução, ele implementará a `IActiveScriptParse32` interface. Para linguagens de script interpretadas que não têm um ambiente de criação independente, como o VBScript, isso fornece um mecanismo alternativo (diferente de `IPersist*` ) para obter o código de script no mecanismo de script e anexar fragmentos de script a vários eventos de objeto.  
  
## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IActiveScriptParse32::AddScriptlet](../../winscript/reference/iactivescriptparse32-addscriptlet.md)|Adiciona um Scriptlet de código ao script.|  
|[IActiveScriptParse32::InitNew](../../winscript/reference/iactivescriptparse32-initnew.md)|Inicializa o mecanismo de script.|  
|[IActiveScriptParse32::ParseScriptText](../../winscript/reference/iactivescriptparse32-parsescripttext.md)|Analisa o scriptlet de código fornecido, adicionando declarações ao espaço de nome e avaliando o código conforme apropriado.|