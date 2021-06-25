---
title: Contexto do projeto | Microsoft Docs
description: Saiba como o IDE do Visual Studio usa o contexto do projeto para determinar como executar operações quando o usuário adiciona ou trabalha com projetos e itens de projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- projects [Visual Studio SDK], opening items
ms.assetid: d1803f4a-24eb-44b0-b5d2-cb40c15534be
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 73e3c8a94607e7e0b31bacddac8e7f19b6139328
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899817"
---
# <a name="project-context"></a>Contexto do projeto
Quando o usuário adiciona ou trabalha com projetos e itens de projeto, o IDE usa a noção do contexto do projeto para determinar como várias operações devem ser executadas.

 Normalmente, os arquivos são os objetos de projeto padrão que o usuário cria explicitamente selecionando o comando **novo projeto** ou disponibilizando-o selecionando o comando **Abrir projeto** no menu **arquivo** . Nesses casos, os arquivos são criados e abertos no contexto de um projeto e o tipo de projeto define o contexto para editar o documento.

 Alguns projetos fornecem um contexto muito rico. Por exemplo, o projeto gerencia um namespace de escopo de projeto, programático ou conexão de banco de dados com escopo de projeto para associação de dado. O usuário pode abrir com frequência arquivos ou conexões de banco de dados diretamente usando um objeto de projeto específico, como um item de projeto exibido no Gerenciador de Soluções.

 Em outras ocasiões, o contexto do projeto de um item não é especificado explicitamente. Por exemplo, o contexto de um item não está disponível quando o usuário abre um arquivo selecionando o comando **Abrir arquivo existente** no menu **arquivo** , quando o depurador opera em um arquivo ou quando o usuário clica no comando **localizar nos arquivos** na caixa de diálogo **Localizar e substituir** . Para lidar com essas situações, o IDE chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument> para gerenciar o processo de localização do melhor projeto para abrir um documento.

## <a name="see-also"></a>Confira também
- [Prioridade do projeto](../../extensibility/internals/project-priority.md)
- [Adicionando o projeto e os modelos de item do projeto](../../extensibility/internals/adding-project-and-project-item-templates.md)
