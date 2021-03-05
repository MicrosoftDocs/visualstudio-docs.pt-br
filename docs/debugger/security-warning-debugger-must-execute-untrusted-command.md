---
description: Esta caixa de diálogo de aviso aparece quando você estiver usando o servidor de origem.
title: 'Aviso de segurança: o depurador deve executar o comando não confiável | Microsoft Docs'
ms.date: 11/04/2016
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1ca71db31fc976a2bc3c652929fd9215f2f3123f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166652"
---
# <a name="security-warning-debugger-must-execute-untrusted-command"></a>Aviso de segurança: o depurador deve executar o comando não confiável
Esta caixa de diálogo de aviso aparece quando você estiver usando o servidor de origem. Indica que o comando que o depurador precisa executar para obter o código-fonte não está na lista de comandos confiáveis para o servidor de origem contido no arquivo srcsvr.ini. Se esse for um comando válido, você poderá adicioná-lo ao arquivo srcsvr.ini. Caso contrário, você não deverá executá-lo. Para obter mais informações, consulte [especificar símbolo (. pdb) e arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

## <a name="message-text"></a>Texto da mensagem
 **O depurador deve executar o seguinte comando não confiável para obter o código-fonte do servidor de origem.**

 **Se o arquivo de símbolo de depuração (\*.pdb) não for de uma origem conhecida e confiável, a execução deste comando pode ser inválida ou perigosa.**

 **Você deseja executar este comando?**

## <a name="uielement-list"></a>Lista de elementos de interface do usuário
 Comando de caixa de texto do arquivo. pdb a ser executado.

 Execute permitir que o comando seja executado.

 Não execute parar a execução do comando e o download do arquivo do servidor de origem.

## <a name="see-also"></a>Confira também
- [Especificar os arquivos de origem e símbolo (.pdb)](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [Segurança do depurador](../debugger/debugger-security.md)
- [Servidor de origem](/windows/desktop/Debug/source-server-and-source-indexing)
