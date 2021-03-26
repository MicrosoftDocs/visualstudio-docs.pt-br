---
title: Adicionando projetos e modelos de item de projeto | Microsoft Docs
description: Saiba como adicionar modelos de item de projeto e projeto às caixas de diálogo no IDE (ambiente de desenvolvimento integrado) do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], adding
- project items [Visual Studio], adding
ms.assetid: 8c59217f-56e5-4540-a73b-cd10de189373
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3f2c10b310569a412025fd114f7818734106bc18
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079053"
---
# <a name="add-project-and-project-item-templates"></a>Adicionar projeto e modelos de item de projeto
Ao criar seus próprios tipos de projeto, você deve fornecer suporte para adicionar novos projetos e itens de projeto usando as caixas de diálogo padrão do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente de desenvolvimento integrado (IDE). Os tópicos a seguir discutem técnicas diferentes para adicionar projetos e itens de projeto.

## <a name="in-this-section"></a>Nesta seção
- [Contexto do projeto](../../extensibility/internals/project-context.md)

 Explica que o projeto fornece a maioria das informações de contexto para o que ocorre no ambiente.

- [Prioridade do projeto](../../extensibility/internals/project-priority.md)

 Explica que um item de projeto é geralmente um membro de um projeto para ajudar a evitar ambigüidade sobre qual projeto é usado para abrir o item.

- [Projeto de arquivos diversos](../../extensibility/internals/miscellaneous-files-project.md)

 Fornece informações sobre os dois tipos de editores que podem ser usados para abrir arquivos em um projeto e a função que o projeto desempenha para determinar qual editor deve ser usado quando um item de projeto é aberto.

- [Registrar modelos de projeto e item](../../extensibility/internals/registering-project-and-item-templates.md)

 Explica o que ocorre quando um [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] projeto é criado.

- [Adicionar itens à caixa de diálogo Adicionar novo item](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)

 Explica o processo para adicionar itens à caixa de diálogo **Adicionar novo item** .

- [Adicionar diretórios à caixa de diálogo novo projeto](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)

 Fornece um exemplo de registro de um novo diretório que contém modelos personalizados disponibilizados por um VSPackage.

- [Adicionar diretórios à caixa de diálogo Adicionar novo item](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)

 Fornece um exemplo de registro de um novo conjunto de diretórios para a caixa de diálogo **Adicionar novo item** .

- [Comandos definidos pelo IDE para estender sistemas de projeto](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)

 Lista diferentes tipos de itens de comando usados para estender sistemas de projeto.

- [CATIDs para objetos que normalmente são usados para estender projetos](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)

 Lista os CATIDs para objetos que são usados para estender [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] , [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] e [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] sistemas de projeto.

## <a name="related-sections"></a>Seções relacionadas
- [Como: abrir editores específicos do projeto](../../extensibility/how-to-open-project-specific-editors.md)

 Fornece instruções passo a passo para abrir um item associado intrinsecamente a um editor específico para um projeto.

- [Como: abrir editores padrão](../../extensibility/how-to-open-standard-editors.md)

 Fornece instruções passo a passo para abrir um editor padrão.

- [Subtipos de projeto](../../extensibility/internals/project-subtypes.md)

 Fornece links para tópicos conceituais de subtipo de projeto. Os subtipos de projeto estendem [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] projetos e existentes [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] .

- [Tipos de projeto](../../extensibility/internals/project-types.md)

 Fornece links para tópicos adicionais que oferecem informações sobre como criar novos tipos de projeto.
