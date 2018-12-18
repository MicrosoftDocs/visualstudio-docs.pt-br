---
title: Comando Listar Origem | Microsoft Docs
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
- Debug.ListSource
helpviewer_keywords:
- Debug.ListSource command
- list source command
- ListSource command
ms.assetid: e45f08d2-f4a3-49c3-9452-aa60508e2f74
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ff216ddd8943ea971669c6ebb1c7c0306b02160f
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49171971"
---
# <a name="list-source-command"></a>Comando Listar Origem
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Exibe as linhas de código-fonte especificadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Debug.ListSource [/Count:number] [/Current] [/File:filename]  
[/Line:number] [/ShowLineNumbers:yes|no]  
```  
  
## <a name="switches"></a>Opções  
 /Count:`number`  
 Opcional. Especifica o número de linhas que serão mostradas.  
  
 /Current  
 Opcional. Mostra a linha atual.  
  
 /File:`filename`  
 Opcional. Caminho do arquivo a ser exibido. Se nenhum nome de arquivo for especificado, o comando mostrará o código-fonte da linha da instrução atual.  
  
 /Line:`number`  
 Opcional. Mostra um número de linha específico.  
  
 /ShowLineNumbers:`yes|no`  
 Opcional. Especifica se os números de linha devem ser exibidos.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="example"></a>Exemplo  
 Este exemplo lista o código-fonte da linha 4 do arquivo Form1.vb, com números de linha visíveis.  
  
```  
Debug.ListSource /File:"C:\Visual Studio Projects\Form1.vb" /Line:4 /ShowLineNumbers:yes  
```  
  
## <a name="see-also"></a>Consulte também  
 [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)   
 [Janela Comando](../../ide/reference/command-window.md)



