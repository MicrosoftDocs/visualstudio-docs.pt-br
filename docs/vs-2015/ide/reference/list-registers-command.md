---
title: Comando Listar Registros | Microsoft Docs
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
- debug.listregisters
helpviewer_keywords:
- list registers command
- Debug.ListRegisters command
- ListRegisters command
ms.assetid: 19a9d789-f6c9-46b3-b1f6-4934fc33e055
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 9e52b7de812be9168c30093b16041db42ea4676b
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49195410"
---
# <a name="list-registers-command"></a>Comando Listar Registros
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Exibe o valor dos registros selecionados e permite modificar a lista de registros a mostrar.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Debug.ListRegisters [/Display [{register|registerGroup}...]] [/List]  
[/Watch [{register|registerGroup}...]]  
[/Unwatch [{register|registerGroup}...]]  
```  
  
## <a name="switches"></a>Opções  
 /Display [{`register`&#124;`registerGroup`}...]  
 Exibe os valores do `register` ou `registerGroup` especificado. Se nenhum `register` ou `registerGroup` for especificado, a lista padrão de registros será exibida. Se nenhuma opção for especificada, o comportamento será o mesmo. Por exemplo:  
  
 `Debug.ListRegisters /Display eax`  
  
 equivale a  
  
 `Debug.ListRegisters eax`  
  
 /List  
 Exibe todos os grupos de registros na lista.  
  
 /Watch [{`register`&#124;`registerGroup`}...]  
 Adiciona um ou mais valores `register` ou `registerGroup` à lista.  
  
 /Unwatch [{`register`&#124;`registerGroup`}...]  
 Remove um ou mais valores `register` ou `registerGroup` da lista.  
  
## <a name="remarks"></a>Comentários  
 O alias `r` pode ser usado no lugar de `Debug.ListRegisters`.  
  
## <a name="example"></a>Exemplo  
 Este exemplo usa o alias `Debug.ListRegisters` `r` para exibir os valores do registro de grupo `Flags`.  
  
```  
r /Display Flags  
```  
  
## <a name="see-also"></a>Consulte também  
 [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)   
 [Noções básicas sobre depuração: janela Registros](../../debugger/debugging-basics-registers-window.md)   
 [Como usar a janela Registros](../../debugger/how-to-use-the-registers-window.md)



