---
title: Como exibir documentos de script | Microsoft Docs
ms.date: 11/05/2019
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Script Explorer
ms.assetid: 8b621e53-4508-4b4a-9995-70995b0b9ac8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dcd9823e414005a1711ddccf9d972da929090920
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348438"
---
# <a name="how-to-view-script-documents-javascript"></a>Como exibir documentos de script (JavaScript)

Os arquivos de script do lado do servidor são visíveis no Gerenciador de Soluções. Os arquivos de script do lado do cliente são visíveis apenas quando você está no modo de depuração ou modo de interrupção. Os arquivos de script do lado do cliente são exibidos no nó **documentos de script** .

Para alguns tipos de aplicativos que geram dinamicamente páginas, é mais fácil entrar no modo de interrupção e depurar quando você define um ponto de interrupção de um documento de script que é carregado no navegador. Da mesma forma, você pode adicionar a `debugger` instrução de um documento de script carregado para entrar no modo de interrupção. Este artigo mostra como exibir esses documentos.

> [!NOTE]
> Anteriormente [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] , os arquivos de script do lado do cliente gerados a partir do script do lado do servidor apareciam na janela do Gerenciador de script.

### <a name="to-view-a-server-side-script-document"></a>Para exibir um documento de script do lado do servidor

1. Em **Gerenciador de soluções**, abra o **\<Website Pathname>** nó.

2. Clique duas vezes no arquivo de script que deseja exibir.

     O arquivo de script do lado do servidor é aberto em uma janela de origem.

### <a name="to-view-a-client-side-script-document"></a>Para exibir um documento de script do lado do cliente

1. No **Gerenciador de Soluções**, abra o nó **Documentos de Script**.

2. Clique duas vezes no arquivo de script que deseja exibir.

     O arquivo de script do lado do cliente é aberto em uma janela de origem.

## <a name="see-also"></a>Veja também
- [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)