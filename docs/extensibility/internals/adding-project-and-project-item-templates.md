---
title: Adicionando o projeto e modelos de Item de projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], adding
- project items [Visual Studio], adding
ms.assetid: 8c59217f-56e5-4540-a73b-cd10de189373
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: db53ddce3161097347760026aea16a51f8098519
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39499628"
---
# <a name="add-project-and-project-item-templates"></a>Adicione o projeto e modelos de item de projeto
Quando você cria seus próprios tipos de projeto, você deve fornecer suporte para adição de novos projetos e itens de projeto usando o padrão [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] integrado caixas de diálogo (IDE) do ambiente de desenvolvimento. Os tópicos a seguir discutem as técnicas diferentes para adicionar projetos e itens de projeto.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Contexto do projeto](../../extensibility/internals/project-context.md)  
 Explica o que o projeto fornece a maioria das informações de contexto para o que ocorre no ambiente.  
  
 [Prioridade do projeto](../../extensibility/internals/project-priority.md)  
 Explica o que um item de projeto geralmente é um membro de um projeto para ajudar a evitar a ambiguidade sobre o qual o projeto é usado para abrir o item.  
  
 [Projeto arquivos diversos](../../extensibility/internals/miscellaneous-files-project.md)  
 Fornece informações sobre os dois tipos de editores que podem ser usados para abrir arquivos em um projeto e a função que o projeto é reproduzido na determinação de qual editor a ser usado quando um item de projeto é aberto.  
  
 [Registrar os modelos de projeto e de item](../../extensibility/internals/registering-project-and-item-templates.md)  
 Explica o que ocorre quando um [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] projeto é criado.  
  
 [Adicionar itens à caixa de diálogo Adicionar Novo Item](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)  
 Explica o processo de adição de itens para o **Adicionar Novo Item** caixa de diálogo.  
  
 [Adicionar diretórios à caixa de diálogo Novo projeto](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)  
 Fornece um exemplo de como registrar um novo diretório que contém os modelos personalizados, disponibilizados por um VSPackage.  
  
 [Adicionar diretórios à caixa de diálogo Adicionar Novo Item](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)  
 Fornece um exemplo de como registrar um novo conjunto de diretórios para o **Adicionar Novo Item** caixa de diálogo.  
  
 [Comandos definidos pelo IDE para estender sistemas de projeto](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)  
 Lista os diferentes tipos de itens de comando usados para estender sistemas de projeto.  
  
 [CATIDs para objetos que normalmente são usados para estender projetos](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)  
 Lista CATIDs para objetos que são usados para estender [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)], [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)], e [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] sistemas de projeto.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Como: abrir editores específicos do projeto](../../extensibility/how-to-open-project-specific-editors.md)  
 Fornece instruções passo a passo para abrir um item intrinsecamente associado a um editor específico para um projeto.  
  
 [Como: abrir editores padrão](../../extensibility/how-to-open-standard-editors.md)  
 Fornece instruções passo a passo para abrir um editor padrão.  
  
 [Subtipos de projeto](../../extensibility/internals/project-subtypes.md)  
 Fornece links para tópicos conceituais do subtipo de projeto. Estendem o subtipos do projeto existente [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] e [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] projetos.  
  
 [Tipos de projeto](../../extensibility/internals/project-types.md)  
 Fornece links para tópicos adicionais que oferecem informações sobre como criar novos tipos de projeto.