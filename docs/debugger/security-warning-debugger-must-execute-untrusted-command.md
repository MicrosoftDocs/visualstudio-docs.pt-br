---
title: 'Aviso de segurança: O depurador deve executar o comando não confiável | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.sourceserver.securityalert
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: e5c004b3-b364-4098-ac98-770076ca9981
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3e99c56efc5338feeded20621c7467bbf8274bc9
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39510918"
---
# <a name="security-warning-debugger-must-execute-untrusted-command"></a>Aviso de segurança: o depurador deve executar o comando não confiável
Esta caixa de diálogo de aviso aparece quando você estiver usando o servidor de origem. Indica que o comando que o depurador precisa executar para obter o código-fonte não está na lista de comandos confiáveis para o servidor de origem contido no arquivo srcsvr.ini. Se esse for um comando válido, você poderá adicioná-lo ao arquivo srcsvr.ini. Caso contrário, você não deverá executá-lo. Para obter mais informações, consulte [Especificar arquivos de símbolo (.pdb) e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).  
  
## <a name="message-text"></a>Mensagem de texto  
 **O depurador deve executar o seguinte comando não confiável para obter o código-fonte do servidor de origem.**  
  
 **Se o arquivo de símbolo de depuração (\*. PDB) é não de uma origem conhecida e confiável, esse comando pode ser inválida ou perigosa ser executado.**  
  
 **Você deseja executar este comando?**  
  
## <a name="uielement-list"></a>Lista UIElement  
 Caixa de texto  
 Comando do arquivo de .pdb a ser executado.  
  
 Execute  
 Permite a execução do comando.  
  
 Não execute  
 Interromper a execução de comando e fazer download do arquivo do servidor de origem.  
  
## <a name="see-also"></a>Consulte também  
 [Especifique o símbolo (. PDB) e arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)   
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Servidor de origem](/windows/desktop/Debug/source-server-and-source-indexing)