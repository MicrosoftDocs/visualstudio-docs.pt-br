---
title: Assistentes | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], providing wizard support
ms.assetid: 59d9a77f-ee80-474b-a14f-90f477ab717b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 03cee9de14da76ea65882d906acb3af88e72e999
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31138708"
---
# <a name="wizards"></a>Assistentes
Depois de criar um assistente, você geralmente deseja adicioná-lo para o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] integrado (IDE) do ambiente de desenvolvimento, de forma que outras pessoas podem usá-lo. O assistente adicionado aparece no **adicionar novo projeto** ou **Adicionar Novo Item** caixas de diálogo. Para ver o **adicionar novo projeto** ou **Adicionar Novo Item** diálogo caixas, clique uma solução aberta no **Solution Explorer**, aponte para **adicionar**, e em seguida, clique em **novo projeto** ou **Novo Item**.  
  
 Assistentes podem ser implementados em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] para permitir que usuários Selecione um modo de exibição de árvore de valores disponíveis quando abrirem o **adicionar novo projeto** caixa de diálogo ou o **Adicionar Novo Item** caixa de diálogo, ou quando eles um item no **Gerenciador de soluções**.  
  
 No assistente, você pode fornecer a opção de localizar o nome de um novo projeto ou HTTP, e você pode determinar o ícone que os usuários verão quando eles selecionam o assistente. Você também pode controlar a ordem na qual novos itens são exibidos em relação a outros itens disponíveis; itens não precisam ser organizados em ordem alfabética.  
  
 Você também pode fornecer um assistente que inicia de forma diferente, com base em parâmetros personalizados que são passados para o Assistente quando ele é aberto.  
  
 Os tópicos nesta seção abordam os arquivos que você pode implementar para fazer com que o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **adicionar novo projeto** e **Adicionar Novo Item** caixas de diálogo para listar o assistente entre os assistentes disponíveis e os modelos, e os requisitos que o assistente deve atender para operar corretamente no IDE.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Arquivos de descrição do diretório do modelo (.Vsdir)](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)  
 Fornece uma visão geral de qual modelo arquivos de descrição de diretório e explica como eles funcionam no IDE para exibir pastas, arquivos. vsz do assistente e os arquivos de modelo que estão associados um projeto nas caixas de diálogo.  
  
 [Arquivo do assistente (.Vsz)](../../extensibility/internals/wizard-dot-vsz-file.md)  
 Explica como o IDE inicia assistentes e lista as três partes do arquivo. vsz.  
  
 [Interface do assistente (IDTWizard)](../../extensibility/internals/wizard-interface-idtwizard.md)  
 Descreve o `IDTWizard` interface assistentes devem implementar para trabalhar no IDE.  
  
 [Parâmetros de contexto](../../extensibility/internals/context-parameters.md)  
 Explica como os assistentes são implementados e o que ocorre quando o IDE passa parâmetros de contexto para a implementação.  
  
 [Parâmetros personalizados](../../extensibility/internals/custom-parameters.md)  
 Explica como usar parâmetros personalizados para controlar a operação do assistente, depois que o assistente for iniciado.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Tipos de projeto](../../extensibility/internals/project-types.md)  
 Fornece links para tópicos adicionais que oferecem informações sobre como criar novos tipos de projeto.  
  
 [Estender projetos](../../extensibility/extending-projects.md)  
 Descreve como usar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] projetos e soluções para organizar os arquivos de código e arquivos de recurso e como implementar o controle de origem.