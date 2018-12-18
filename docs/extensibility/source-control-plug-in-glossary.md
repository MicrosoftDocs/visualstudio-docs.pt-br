---
title: Glossário de plug-in de controle de origem | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- glossary [Visual Studio SDK]
- source control plug-ins, glossary
ms.assetid: f224bbc9-38fc-4c80-ab09-51dcc8969f8e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ccfd4cbbbca86d3b6e93d9998410c5dea117328d
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31139020"
---
# <a name="source-control-plug-in-glossary"></a>Glossário de plug-in de controle do código-fonte
Os seguintes termos úteis e definições pertencem a documentação do SDK de plug-in de controle de origem.  
  
## <a name="definitions"></a>Definições  
 Check-in  
 Quando um usuário faz alterações em uma cópia de trabalho, um usuário deve enviar as alterações da cópia de trabalho para o repositório de controle de origem central. Isso cria uma nova revisão do arquivo que está disponível para outros usuários. Esse processo é chamado um check-in.  
  
 Check-out  
 O ato de solicitando uma cópia de trabalho do repositório, informando o repositório de sua intenção de modificá-lo. Uma cópia de trabalho reflete o estado do projeto a partir do momento em que ele está checked-out.  
  
 Cliente  
 Um programa que usa o sistema de controle do código fonte. Para fins desta documentação é o Visual Studio IDE.  
  
 Comentário  
 Uma mensagem que descreve as alterações que um usuário pode se conectar a uma revisão quando uma operação de controle de origem é executada.  
  
 Conflito  
 Uma situação em que dois usuários tentam fazer check-in de alterações para a mesma região do mesmo arquivo. Normalmente, uma mesclagem deve ser executada.  
  
 Diretório  
 Uma pasta local do cliente é chamada de diretório. Essa é a cópia em que o usuário realmente faz alterações. Pode haver várias cópias de trabalho de um determinado projeto; em geral, cada desenvolvedor tem sua própria cópia.  
  
 Obter  
 Uma operação get traz cópia de trabalho do usuário atualizada com a cópia do repositório. Ao contrário de um check-out, um get é executado quando o usuário simplesmente precisa de uma cópia mais recente, mas pretende não fazer nenhuma alteração.  
  
 Histórico  
 Geralmente é um resumo de todos os check-outs, check-ins, atualizações, marcas e versões feitas no repositório de controle de origem.  
  
 IDE  
 Geralmente se refere ao Visual Studio ambiente de desenvolvimento integrado. No entanto, ela pode também se referir a outros ambientes de cliente que reconhecem a API de plug-in de controle de origem.  
  
 Mesclar  
 O processo durante a qual fonte de dois ou mais arquivos de código são combinados para formar um novo arquivo que incorpora todos os recursos de arquivos anteriores. Esse conceito é essencial no controle de versão em que dois ou mais desenvolvedores trabalham em arquivos simultaneamente.  
  
 Projeto  
 Uma pasta de controle de origem é conhecida como um projeto. Isso não tem nenhuma relação com soluções ou projetos no Visual Studio.  
  
 Plug-in  
 Uma DLL que fornece funcionalidade de controle de origem com a implementação da API de plug-in de controle de origem.  
  
 Repositório  
 A cópia mestra em que uma fonte de sistema de controle armazena o histórico de revisão completo do projeto. Cada projeto tem exatamente um repositório.  
  
 Revisão  
 Uma alteração confirmada no histórico de um arquivo ou conjunto de arquivos. Uma revisão é um instantâneo em um projeto muda continuamente.  
  
## <a name="see-also"></a>Consulte também  
 [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)