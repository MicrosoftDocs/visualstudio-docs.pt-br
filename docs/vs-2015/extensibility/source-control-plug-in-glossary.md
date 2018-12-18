---
title: Glossário do plug-in de controle de origem | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- glossary [Visual Studio SDK]
- source control plug-ins, glossary
ms.assetid: f224bbc9-38fc-4c80-ab09-51dcc8969f8e
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 9535987cc729c78c7d72ee9f51529aeb91b59450
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51732280"
---
# <a name="source-control-plug-in-glossary"></a>Glossário de plug-in de controle do código-fonte
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os seguintes termos úteis e definições referem-se a documentação do SDK de plug-in de controle do código-fonte.  
  
## <a name="definitions"></a>Definições  
 Fazer check-in  
 Quando um usuário faz alterações em uma cópia de trabalho, um usuário deve enviar as alterações da cópia funcional para o repositório de controle de origem central. Isso cria uma nova revisão do arquivo que está disponível para outros usuários. Esse processo é chamado um check-in.  
  
 Check-out  
 O ato de solicitar uma cópia de trabalho do repositório, informando o repositório de sua intenção de modificá-lo. Uma cópia funcional reflete o estado do projeto a partir do momento em que ele foi extraído.  
  
 Cliente  
 Um programa que usa o sistema de controle do código-fonte. Para fins desta documentação é o IDE do Visual Studio.  
  
 Comentário  
 Uma mensagem que descreve as alterações que um usuário pode se conectar a uma revisão quando uma operação de controle do código-fonte é executada.  
  
 Conflito  
 Uma situação em que dois usuários tentam fazer check-in é alterado para a mesma região do mesmo arquivo. Normalmente, uma mesclagem deve ser executada.  
  
 Diretório  
 Uma pasta local do lado do cliente é chamada de um diretório. Esta é a cópia no qual um usuário, na verdade, faz alterações. Pode haver muitas cópias de trabalho de um determinado projeto; em geral, cada desenvolvedor tem sua própria cópia.  
  
 Obter  
 Uma operação get traz cópia de trabalho do usuário atualizada com a cópia do repositório. Ao contrário de um check-out, um get é executado quando o usuário simplesmente precisa a cópia mais recente, mas pretende sem fazer alterações.  
  
 Histórico  
 Geralmente, é um resumo de todos os check-outs, check-ins, atualizações, marcas e versões feitas no repositório de controle de origem.  
  
 IDE  
 Geralmente se refere ao Visual Studio Integrated Development Environment. No entanto, ela pode também se referir a outros ambientes de cliente que reconhecem a API de plug-in de controle do código-fonte.  
  
 Mesclar  
 O processo durante a qual fonte de dois ou mais arquivos de código são combinados para formar um novo arquivo que incorpora a todos os recursos de arquivos anteriores. Esse conceito é vital em controle de versão em que dois ou mais desenvolvedores trabalham em arquivos simultaneamente.  
  
 Projeto  
 Uma pasta de controle de origem é conhecida como um projeto. Isso não tem nenhuma relação com projetos ou soluções no Visual Studio.  
  
 Plug-in  
 Uma DLL que fornece funcionalidade de controle do código-fonte, Implementando a API de plug-in de controle do código-fonte.  
  
 Repositório  
 A cópia mestra em que uma fonte de sistema de controle armazena o histórico de revisão completa de um projeto. Cada projeto tem exatamente um repositório.  
  
 Revisão  
 Uma alteração confirmada no histórico de um arquivo ou conjunto de arquivos. Uma revisão é um instantâneo em um projeto continuamente em alteração.  
  
## <a name="see-also"></a>Consulte também  
 [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)

