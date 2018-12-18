---
title: Assistentes | Microsoft Docs
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
- projects [Visual Studio SDK], providing wizard support
ms.assetid: 59d9a77f-ee80-474b-a14f-90f477ab717b
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: cbf2eceeb3ae8a3870954d53f8d85c46f3322d24
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51747604"
---
# <a name="wizards"></a>Assistentes
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Depois de criar um assistente, você geralmente deseja adicioná-lo para o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ambiente desenvolvimento integrado (IDE) para que outras pessoas possam usá-lo. O Assistente de adição, em seguida, aparece na **adicionar novo projeto** ou **Adicionar Novo Item** caixas de diálogo. Para ver os **adicionar novo projeto** ou **Adicionar Novo Item** caixa de diálogo caixas, clique duas vezes em uma solução aberta no **Gerenciador de soluções**, aponte para **adicionar**, e em seguida, clique em **novo projeto** ou **Novo Item**.  
  
 Assistentes podem ser implementados em [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] para permitir que os usuários select de uma exibição de árvore de valores disponíveis quando abrirem o **adicionar novo projeto** caixa de diálogo ou o **Adicionar Novo Item** caixa de diálogo, ou quando eles com o botão direito um item na **Gerenciador de soluções**.  
  
 No assistente, você pode fornecer a opção de localizar o nome de um novo projeto ou ites e você pode determinar o ícone que os usuários verão quando eles selecionarem o assistente. Você também pode controlar a ordem na qual novos itens aparecem em relação a outros itens disponíveis; itens não precisa ser organizados em ordem alfabética.  
  
 Você também pode fornecer um assistente que é iniciado de forma diferente, com base em parâmetros personalizados que são passados para o Assistente quando ele é aberto.  
  
 Os tópicos desta seção discutem os arquivos que você pode implementar para fazer com que o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **adicionar novo projeto** e **Adicionar Novo Item** caixas de diálogo para listar seu assistente entre os assistentes disponíveis e os modelos, e os requisitos que o assistente deve atender para operar corretamente no IDE.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Arquivos de descrição do diretório do modelo (.Vsdir)](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)  
 Fornece uma visão geral de qual modelo arquivos de descrição de diretório e explica como eles funcionam no IDE para exibir pastas, arquivos. vsz do assistente e arquivos de modelo que estão associados um projeto nas caixas de diálogo.  
  
 [Arquivo do assistente (.Vsz)](../../extensibility/internals/wizard-dot-vsz-file.md)  
 Explica como o IDE é iniciado em assistentes e lista as três partes do arquivo. vsz.  
  
 [Interface do assistente (IDTWizard)](../../extensibility/internals/wizard-interface-idtwizard.md)  
 Descreve o `IDTWizard` interface assistentes devem implementar para trabalhar no IDE.  
  
 [Parâmetros de contexto](../../extensibility/internals/context-parameters.md)  
 Explica como os assistentes são implementados e o que ocorre quando o IDE passa parâmetros de contexto para a implementação.  
  
 [Parâmetros personalizados](../../extensibility/internals/custom-parameters.md)  
 Explica como usar parâmetros personalizados para controlar a operação do assistente depois que o assistente for iniciado.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Tipos de projeto](../../extensibility/internals/project-types.md)  
 Fornece links para tópicos adicionais que oferecem informações sobre como criar novos tipos de projeto.  
  
 [Passo a passo: Criando um assistente](http://msdn.microsoft.com/library/adb41fe9-fcca-4e87-bf4f-bf2fa68e8b06)  
 Ilustra como criar um assistente.  
  
 [Estender projetos](../../extensibility/extending-projects.md)  
 Descreve como usar [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] projetos e soluções para organizar os arquivos de código e arquivos de recurso e como implementar o controle do código-fonte.

