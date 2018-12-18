---
title: Interface IActiveScriptAuthor | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptAuthor interface
ms.assetid: df1f454d-01ee-4beb-928b-48513d07365a
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 37abb356ab24d64a05a1f1209809d63e2f55e228
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645766"
---
# <a name="iactivescriptauthor-interface"></a>Interface IActiveScriptAuthor
Representa a criação de serviços, incluindo IntelliSense e agrupamento de informações.  
  
 Além dos métodos herdados de `IUnknown`, o `IActiveScriptAuthor` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IActiveScriptAuthor::AddNamedItem](../../winscript/reference/iactivescriptauthor-addnameditem.md)|Adiciona o nome de um item de nível raiz para o namespace do mecanismo de criação de script. Um *item de nível raiz* é um objeto que pode conter propriedades e métodos, e também podem conter uma fonte de evento.|  
|[IActiveScriptAuthor::AddScriptlet](../../winscript/reference/iactivescriptauthor-addscriptlet.md)|Adiciona um miniscript de código como um filho do nível raiz `IScriptNode` objeto. No host, o nome totalmente qualificado do miniscript pode ter apenas dois níveis.|  
|[IActiveScriptAuthor::AddTypeLib](../../winscript/reference/iactivescriptauthor-addtypelib.md)|Adiciona uma biblioteca de tipos para o namespace para o script.|  
|[IActiveScriptAuthor::GetChars](../../winscript/reference/iactivescriptauthor-getchars.md)|Retorna o conjunto de caracteres de preenchimento para um contexto de conclusão solicitada.|  
|[IActiveScriptAuthor::GetEventHandler](../../winscript/reference/iactivescriptauthor-geteventhandler.md)|Retorna o miniscript que tem os atributos especificados.|  
|[IActiveScriptAuthor::GetInfoFromContext](../../winscript/reference/iactivescriptauthor-getinfofromcontext.md)|Retorna informações e as posições de âncora para um determinado caractere de tipo em um bloco de código. Isso fornece informações de membro, IntelliSense, listas globais e dicas de parâmetro.|  
|[IActiveScriptAuthor::GetLanguageFlags](../../winscript/reference/iactivescriptauthor-getlanguageflags.md)|Retorna informações de idioma.|  
|[IActiveScriptAuthor::GetRoot](../../winscript/reference/iactivescriptauthor-getroot.md)|Retorna o `IScriptNode` raiz da árvore de script do autor.|  
|[IActiveScriptAuthor::GetScriptletTextAttributes](../../winscript/reference/iactivescriptauthor-getscriptlettextattributes.md)|Retorna os atributos de texto de um miniscript.|  
|[IActiveScriptAuthor::GetScriptTextAttributes](../../winscript/reference/iactivescriptauthor-getscripttextattributes.md)|Retorna os atributos de texto de um bloco de script.|  
|[IActiveScriptAuthor::IsCommitChar](../../winscript/reference/iactivescriptauthor-iscommitchar.md)|Retorna um valor que indica se um determinado caractere deve confirmar a conclusão de instrução pelo aplicativo.|  
|[IActiveScriptAuthor::ParseScriptText](../../winscript/reference/iactivescriptauthor-parsescripttext.md)|Analisa o texto do script, adiciona o texto ao script de criação de mecanismo de criação e cria um `IScriptEntry` objeto que corresponde ao bloco de script.|  
|[IActiveScriptAuthor::RemoveNamedItem](../../winscript/reference/iactivescriptauthor-removenameditem.md)|Remove um `NamedItem` objeto do namespace do script de criação de mecanismo.|  
|[IActiveScriptAuthor::RemoveTypeLib](../../winscript/reference/iactivescriptauthor-removetypelib.md)|Remove uma biblioteca de tipos o namespace do mecanismo de criação de script.|  
  
## <a name="see-also"></a>Consulte também  
 [Active Script Authoring Interfaces](../../winscript/reference/active-script-authoring-interfaces.md)