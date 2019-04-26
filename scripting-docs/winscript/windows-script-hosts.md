---
title: Windows Script Hosts | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Windows Script Host, implementing hosts
ms.assetid: 9d5f6471-b318-40f3-be01-d9cd0b1cdd47
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: eec1824bd3ba1a8acb7e3c540656151cd4b11d1f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62840038"
---
# <a name="windows-script-hosts"></a>Windows Script Hosts
Ao implementar um host do Microsoft Windows Script, você pode supor com segurança que um mecanismo de script só chama a interface [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) no contexto do thread base se o host faz o seguinte:  
  
- Escolhe um thread de base (geralmente o thread que contém o loop de mensagens).  
  
- Cria uma instância do mecanismo de script no thread base.  
  
- Chama métodos de mecanismo de script somente do thread base, exceto quando especificamente permitido, assim como nos casos de [IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md) e [IActiveScript::Clone](../winscript/reference/iactivescript-clone.md).  
  
- Chama o objeto de expedição do mecanismo de script somente do thread base.  
  
- Garante que o loop de mensagens será executado no thread base se um identificador de janela for fornecido.  
  
- Garante que os objetos no modelo de objeto do host apenas originem eventos no thread base.  
  
  Essas regras são seguidas automaticamente por todos os hosts de thread único. O modelo restrito descrito acima é intencionalmente flexível o suficiente para permitir que um host anule um script travado chamando [IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md) de outro thread (iniciado por um manipulador CTRL+BREAK ou semelhante) ou para duplicar um script em um novo thread usando [IActiveScript::Clone](../winscript/reference/iactivescript-clone.md).  
  
## <a name="remarks"></a>Comentários  
 Nenhuma dessas restrições se aplicam a um host que opta por implementar uma interface [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) de thread livre e um modelo de objeto de thread livre. Um host desse tipo pode usar a interface [IActiveScript](../winscript/reference/iactivescript.md) de qualquer thread, sem restrição.  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces do Windows Script](../winscript/windows-script-interfaces.md)