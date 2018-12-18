---
title: Como especificar o binário para iniciar | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.property.itemlaunch
helpviewer_keywords:
- profiling tools, launching
- performance tools, launching
- performance sessions, launching
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 87fc4102b3cbd3420f1e5c3b7ea4a067e0d95a0d
ms.sourcegitcommit: ce154aee5b403d5c1c41da42302b896ad3cf8d82
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34844853"
---
# <a name="how-to-specify-the-binary-to-start"></a>Como especificar o binário a ser iniciado

Para analisar binários, como DLLs, você deve inserir informações na caixa de diálogo **\<Destino> Páginas de Propriedade**. Essa informação indica onde o projeto DLL pode localizar o aplicativo de chamada.

1. No **Gerenciador de Desempenho**, clique com o botão direito do mouse no binário de destino e, em seguida, clique em **Propriedades**.

2. Na caixa de diálogo **Páginas de Propriedades**, clique nas propriedades de **Inicialização**.

3. Selecione a caixa de seleção **Substituir as propriedades de projeto**.

4. Na caixa de texto **Executável a Ser Iniciado**, especifique o local do arquivo.

5. Na caixa de texto **Argumentos**, especifique os argumentos que são necessários para iniciar o aplicativo.

6. Na caixa de texto **Diretório de Trabalho**, especifique o local do diretório.

7. Clique em **OK**.

## <a name="see-also"></a>Consulte também

[Configurar sessões de desempenho](../profiling/configuring-performance-sessions.md)