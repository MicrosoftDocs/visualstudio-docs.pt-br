---
title: IActiveScriptSite | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptSite interface
ms.assetid: 4d604a11-5365-46cf-ab71-39b3dbbe9f22
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c23dba403a7889fe46817a21ed8e4be65b1c05b4
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725006"
---
# <a name="iactivescriptsite"></a>IActiveScriptSite
Implementado pelo host para criar um site para o mecanismo de Script do Windows. Normalmente, esse site será associado ao contêiner de todos os objetos que estão visíveis para o script (por exemplo, os controles ActiveX). Normalmente, esse contêiner corresponderá ao documento ou página que está sendo exibido. Por exemplo, o Microsoft Internet Explorer, criaria tal um contêiner para cada página HTML que está sendo exibido. Cada ActiveX controle (ou outro objeto de automação) na página e o mecanismo de script em si, seria enumerável dentro deste contêiner.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|||  
|-|-|  
|Método|Descrição|  
|[IActiveScriptSite::GetLCID](../../winscript/reference/iactivescriptsite-getlcid.md)|Recupera o identificador de localidade que o host usa para exibir os elementos de interface do usuário.|  
|[IActiveScriptSite::GetItemInfo](../../winscript/reference/iactivescriptsite-getiteminfo.md)|Obtém informações sobre um item que foi adicionado a um mecanismo por meio de uma chamada para o [IActiveScript::AddNamedItem](../../winscript/reference/iactivescript-addnameditem.md) método.|  
|[IActiveScriptSite::GetDocVersionString](../../winscript/reference/iactivescriptsite-getdocversionstring.md)|Recupera uma cadeia de caracteres definida pelo host que identifica com exclusividade a versão do documento atual do ponto de vista do host.|  
|[IActiveScriptSite::OnScriptTerminate](../../winscript/reference/iactivescriptsite-onscriptterminate.md)|Chamado quando o script tiver concluído a execução.|  
|[IActiveScriptSite::OnStateChange](../../winscript/reference/iactivescriptsite-onstatechange.md)|Informa ao host que o mecanismo de script foi alterado de estados.|  
|[IActiveScriptSite::OnScriptError](../../winscript/reference/iactivescriptsite-onscripterror.md)|Informa ao host que ocorreu um erro de execução durante o mecanismo de execução do script.|  
|[IActiveScriptSite::OnEnterScript](../../winscript/reference/iactivescriptsite-onenterscript.md)|Informa ao host que o mecanismo de script começou a executar o código de script.|  
|[IActiveScriptSite::OnLeaveScript](../../winscript/reference/iactivescriptsite-onleavescript.md)|Informa ao host que o mecanismo de script foi retornado de execução de código de script.|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de script ativo](../../winscript/reference/active-script-interfaces.md)