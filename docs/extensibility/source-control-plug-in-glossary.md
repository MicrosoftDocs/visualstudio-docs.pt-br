---
title: Glossário de plug-in do controle do código-fonte | Microsoft Docs
description: Este artigo inclui termos e definições úteis que pertencem à documentação do SDK do Plug-in do Controle do Código-Fonte.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- glossary [Visual Studio SDK]
- source control plug-ins, glossary
ms.assetid: f224bbc9-38fc-4c80-ab09-51dcc8969f8e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 05b215de4191362a539d3b03ac858da6bb7ee292
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899518"
---
# <a name="source-control-plug-in-glossary"></a>Glossário de plug-in de controle do código-fonte
Os termos úteis e definições a seguir pertencem à documentação do SDK do Plug-in de Controle do Código-Fonte.

## <a name="definitions"></a>Definições
 Check-in Quando um usuário faz alterações em uma cópia de trabalho, um usuário deve enviar alterações da cópia de trabalho para o repositório de controle do código-fonte central. Isso cria uma nova revisão do arquivo que está disponível para outros usuários. Esse processo é chamado de check-in.

 Check-out O ato de solicitar uma cópia de trabalho do repositório, informando o repositório de sua intenção de modificá-la. Uma cópia de trabalho reflete o estado do projeto a partir do momento em que ele é verificado.

 Cliente Um programa que usa o sistema de controle de código-fonte. Para a finalidade desta documentação, é o Visual Studio IDE.

 Comentário Uma mensagem que descreve as alterações que um usuário pode anexar a uma revisão quando uma operação de controle do código-fonte é executada.

 Conflito Uma situação em que dois usuários tentam fazer check-in das alterações na mesma região do mesmo arquivo. Normalmente, uma mesclagem deve ser executada.

 Diretório Uma pasta local do lado do cliente é conhecida como um diretório. Essa é a cópia na qual um usuário realmente faz alterações. Pode haver muitas cópias de trabalho de um determinado projeto; geralmente, cada desenvolvedor tem sua própria cópia.

 Obter Uma operação get traz a cópia de trabalho do usuário atualizada com a cópia do repositório. Ao contrário de um check-out, um get é executado quando o usuário simplesmente precisa da cópia mais recente, mas não pretende fazer alterações.

 Histórico Normalmente, é um resumo de todos os check-ins, check-ins, atualizações, marcas e versões feitas no repositório de controle do código-fonte.

 O IDE geralmente se refere ao Visual Studio de Desenvolvimento Integrado. No entanto, ele também pode se referir a outros ambientes cliente que reconhecem a API de plug-in de controle do código-fonte.

 Mesclar O processo durante o qual dois ou mais arquivos de código-fonte são combinados para formar um novo arquivo que incorpora todos os recursos de arquivos anteriores. Esse conceito é vital no controle de versão em que dois ou mais desenvolvedores trabalham em arquivos simultaneamente.

 Projeto Uma pasta de controle do código-fonte geralmente é conhecida como um projeto. Isso não tem nenhuma relação com projetos ou soluções no Visual Studio.

 Conecte uma DLL que fornece a funcionalidade de controle do código-fonte implementando a API de plug-in de controle do código-fonte.

 Repositório A cópia mestra em que um sistema de controle do código-fonte armazena o histórico de revisão completo de um projeto. Cada projeto tem exatamente um repositório.

 Revisão Uma alteração comprometida no histórico de um arquivo ou conjunto de arquivos. Uma revisão é um instantâneo em um projeto que muda continuamente.

## <a name="see-also"></a>Confira também
- [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)
