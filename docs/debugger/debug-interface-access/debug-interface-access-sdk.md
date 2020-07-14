---
title: SDK de acesso à interface de depuração | Microsoft Docs
ms.date: 07/24/2018
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- debugging [DIA SDK]
- debugger [DIA SDK]
- DIA SDK
ms.assetid: 4c0abe53-11d3-4b7a-bdc7-b054f85aaf40
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: da0ced56e8bf7e61e7fa5251e834a762d4c66650
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468689"
---
# <a name="debug-interface-access-sdk"></a>SDK de Acesso à Interface de Depuração

O Microsoft Debug interface Access Software Development Kit (DIA SDK) fornece acesso a informações de depuração armazenadas em arquivos do banco de dados do programa (. pdb) gerados pelas ferramentas do Microsoft CreateCompiler. Como o formato do arquivo. pdb gerado pelas ferramentas do compilador subpassa pela revisão constante, expor o formato é impraticável. Usando a API do DIA, você pode desenvolver aplicativos que pesquisem e procurem informações de depuração armazenadas em um arquivo. pdb. Tais aplicativos poderiam, por exemplo, informações de rastreamento de pilha de relatório e análise de dados de desempenho.

## <a name="in-this-section"></a>Nesta seção

[Introdução](../../debugger/debug-interface-access/getting-started-debug-interface-access-sdk.md)

Fornece uma visão geral dos recursos de DIA SDK e especifica onde o DIA SDK é instalado, bem como os arquivos de cabeçalho e biblioteca necessários.

[Consultando o arquivo .Pdb](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)

Fornece instruções sobre como usar a API do DIA para consultar o arquivo. pdb.

[Símbolos e marcas de símbolos](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)

Discute como símbolos e marcas de símbolo são usados na API de DIA.

[Referência](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)

Contém as interfaces, os métodos, as enumerações e as estruturas da API de DIA.

[Exemplo de Dia2dump](../../debugger/debug-interface-access/dia2dump-sample.md)

Ilustra como usar a API do DIA para pesquisar e procurar informações de depuração.
