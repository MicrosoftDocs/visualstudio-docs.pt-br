---
title: Comando List Disassembly | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- debug.listdisassembly
helpviewer_keywords:
- Debug.ListDisassembly command
- list disassembly command
ms.assetid: eb363e35-e86a-4121-966f-991210c27e2a
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4cbdc3ee566135fe86301deefe1e8be8db431f9f
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49256653"
---
# <a name="list-disassembly-command"></a>Comando Listar Desmontagem
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Inicia o processo de depuração e permite que você especifique como os erros são tratados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Debug.ListDisassembly [/count:number] [/endaddress:expression]  
[/codebytes:yes|no] [/source:yes|no] [/symbolnames:yes|no]  
[/linenumbers:yes|no]  
```  
  
## <a name="switches"></a>Opções  
 Cada opção pode ser invocada usando sua forma completa ou abreviada.  
  
 /count: `number` [ou] /c: `number` [ou] /length: `number` [ou] /l: `number`  
 Opcional. Número de instruções a serem exibidas. O valor padrão é 8.  
  
 /endaddress: `expression` [ou] /e: `expression`  
 Opcional. Endereço no qual interromper a desmontagem.  
  
 /codebytes:`yes`&#124;`no` [ou] /bytes:`yes`&#124;`no` [ou] /b:`yes`&#124;`no`  
 Opcional. Indica se deve você deseja exibir bytes de código. O valor padrão é `no`.  
  
 /source:`yes`&#124;`no` [ou] /s:`yes`&#124;`no`  
 Opcional. Indica se deve você deseja exibir o código-fonte. O valor padrão é `no`.  
  
 /symbolnames:`yes`&#124;`no` [ou] /names:`yes`&#124;`no` [ou] /n:`yes`&#124;`no`  
 Opcional. Indica se deve você deseja exibir os nomes de símbolos. O valor padrão é `yes`.  
  
 [/linenumbers:`yes`&#124;`no`]  
 Opcional. Habilita a exibição de números de linha associados ao código-fonte. A opção /source deve ter um valor de `yes` para usar a opção /linenumbers.  
  
## <a name="example"></a>Exemplo  
  
```  
>Debug.ListDisassembly  
```  
  
## <a name="see-also"></a>Consulte também  
 [Comando List Call Stack](../../ide/reference/list-call-stack-command.md)   
 [Comando List Threads](../../ide/reference/list-threads-command.md)   
 [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)   
 [Janela Comando](../../ide/reference/command-window.md)   
 [Caixa Localizar/Comando](../../ide/find-command-box.md)   
 [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)



