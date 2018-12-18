---
title: SDK de acesso à Interface de depuração | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- debugging [DIA SDK]
- debugger [DIA SDK]
- DIA SDK
ms.assetid: 4c0abe53-11d3-4b7a-bdc7-b054f85aaf40
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 279f5b883ca359c38ad8d357d153d02ea022b9da
ms.sourcegitcommit: 71b307ce86c4079cc7ad686d8d5f96a6a123aadd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2018
ms.locfileid: "39251660"
---
# <a name="debug-interface-access-sdk"></a>SDK de Acesso à Interface de Depuração

A Microsoft depurar Interface acesso Software Development Kit (DIA SDK) fornece acesso a informações de depuração armazenadas em arquivos de banco de dados (. PDB) do programa gerados por ferramentas de pós-compilador da Microsoft. Porque o formato do arquivo. PDB gerado pelas ferramentas de pós-compilador da passar por uma revisão de constante, expondo o formato é impraticável. Usando a API do DIA, você pode desenvolver aplicativos que pesquisarem e procurar informações de depuração armazenadas em um arquivo. PDB. Esses aplicativos poderia, por exemplo, relatar informações de pilha de retorno de rastreamento e analisar dados de desempenho.

## <a name="in-this-section"></a>Nesta seção

[Introdução](../../debugger/debug-interface-access/getting-started-debug-interface-access-sdk.md)  
Fornece uma visão geral do DIA SDK recursos e especifica onde o DIA SDK está instalado, bem como os arquivos de biblioteca e cabeçalho necessário.

[Consultando o arquivo .Pdb](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)  
Fornece instruções sobre como usar a API do DIA para consultar o arquivo. PDB.

[Símbolos e marcações de símbolos](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)  
Discute como os símbolos e marcações de símbolos são usadas na API do DIA.

[Referência](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)  
Contém as interfaces, métodos, enumerações e estruturas da API do DIA.

[Exemplo de Dia2dump](../../debugger/debug-interface-access/dia2dump-sample.md)  
Ilustra como usar a API do DIA para pesquisar e procurar informações de depuração.
