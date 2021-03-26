---
title: Glossário de plug-in de controle do código-fonte | Microsoft Docs
description: Este artigo inclui os termos e definições úteis que pertencem à documentação do SDK de plug-in de controle do código-fonte.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- glossary [Visual Studio SDK]
- source control plug-ins, glossary
ms.assetid: f224bbc9-38fc-4c80-ab09-51dcc8969f8e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5fe262091b25db3dae0388427afc3af6c9027872
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090090"
---
# <a name="source-control-plug-in-glossary"></a>Glossário de plug-in de controle do código-fonte
Os termos e definições úteis a seguir pertencem à documentação do SDK de plug-in de controle do código-fonte.

## <a name="definitions"></a>Definições
 Check-in quando um usuário faz alterações em uma cópia de trabalho, um usuário deve enviar alterações da cópia de trabalho para o repositório do controle do código-fonte central. Isso cria uma nova revisão do arquivo que está disponível para outros usuários. Esse processo é chamado de check-in.

 Faça o check-in do ato de solicitar uma cópia de trabalho do repositório, informando o repositório de sua intenção de modificá-la. Uma cópia de trabalho reflete o estado do projeto a partir do momento em que é feito o check-out.

 Cliente um programa que usa o sistema de controle do código-fonte. Para a finalidade desta documentação, é o IDE do Visual Studio.

 Comente uma mensagem que descreve as alterações que um usuário pode anexar a uma revisão quando uma operação de controle do código-fonte é executada.

 Conflito uma situação quando dois usuários tentam fazer check-in de alterações na mesma região do mesmo arquivo. Normalmente, uma mesclagem deve ser executada.

 Diretório uma pasta local do lado do cliente é referida como um diretório. Essa é a cópia na qual um usuário realmente faz alterações. Pode haver muitas cópias de trabalho de um determinado projeto; em geral, cada desenvolvedor tem sua própria cópia.

 Obter uma operação get leva a cópia de trabalho do usuário atualizada com a cópia do repositório. Ao contrário de um check-out, um get é executado quando o usuário simplesmente precisa da cópia mais recente, mas pretende não fazer nenhuma alteração.

 Histórico, normalmente é um resumo de todos os check-outs, check-ins, atualizações, marcas e versões feitas no repositório do controle do código-fonte.

 O IDE geralmente se refere ao ambiente de desenvolvimento integrado do Visual Studio. No entanto, também pode se referir a outros ambientes de cliente que reconheçam a API de plug-in de controle do código-fonte.

 Mescle o processo durante o qual dois ou mais arquivos de código-fonte são combinados para formar um novo arquivo que incorpora todos os recursos dos arquivos anteriores. Esse conceito é vital no controle de versão, onde dois ou mais desenvolvedores trabalham em arquivos simultaneamente.

 Projeto uma pasta de controle do código-fonte geralmente é chamada de projeto. Isso não tem nenhuma relação com projetos ou soluções no Visual Studio.

 Plug-in uma DLL que fornece funcionalidade de controle do código-fonte implementando a API de plug-in de controle do código-fonte.

 Repositório a cópia mestre em que um sistema de controle do código-fonte armazena o histórico de revisão completo de um projeto. Cada projeto tem exatamente um repositório.

 Revisar uma alteração confirmada no histórico de um arquivo ou conjunto de arquivos. Uma revisão é um instantâneo em um projeto de alteração contínua.

## <a name="see-also"></a>Confira também
- [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)
