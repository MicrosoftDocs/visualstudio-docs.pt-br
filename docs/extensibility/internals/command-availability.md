---
title: Disponibilidade do comando | Microsoft Docs
description: Saiba como o contexto de comando, que é alterado com base no projeto atual, no editor atual e em outros fatores, determina quais comandos estão disponíveis no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- commands, context
- menu items, visibility contexts
ms.assetid: c74e3ccf-d771-48c8-a2f9-df323b166784
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 738e326c0e6300520d66d64fda4bb5040f231c75
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074737"
---
# <a name="command-availability"></a>Disponibilidade do comando

O contexto do Visual Studio determina quais comandos estão disponíveis. O contexto pode ser alterado dependendo do projeto atual, do editor atual, do VSPackages que são carregados e de outros aspectos do IDE (ambiente de desenvolvimento integrado).

## <a name="command-contexts"></a>Contextos de comando

Os seguintes contextos de comando são os mais comuns:

- IDE: os comandos fornecidos pelo IDE estão sempre disponíveis.

- VSPackage: VSPackages pode definir quando os comandos devem ser exibidos ou ocultos.

- Projeto: os comandos do projeto aparecem apenas para o projeto selecionado no momento.

- Editor: somente um editor pode estar ativo por vez. Os comandos do editor ativo estão disponíveis. Um editor trabalha em conjunto com um serviço de linguagem. O serviço de idioma deve processar seus comandos no contexto do editor associado.

- Tipo de arquivo: um editor pode carregar mais de um tipo de arquivo. Os comandos disponíveis podem ser alterados dependendo do tipo de arquivo.

- Janela ativa: a última janela do documento ativo define o contexto da interface do usuário para associações de chave. No entanto, uma janela de ferramenta que tem uma tabela de associação de chave que se assemelha ao navegador da Web interno também pode definir o contexto da interface do usuário. Para janelas de documentos com várias guias, como o editor de HTML, cada guia tem um GUID de contexto de comando diferente. Depois que uma janela de ferramentas é registrada, ela está sempre disponível no menu **Exibir** .

- Contexto de interface do usuário: contextos de interface do usuário são identificados pelos valores da <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT> classe, por exemplo, <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionBuilding_guid> quando a solução está sendo compilada ou <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Debugging_guid> quando o depurador está ativo. Vários contextos de interface do usuário podem estar ativos ao mesmo tempo.

## <a name="define-custom-context-guids"></a>Definir GUIDs de contexto personalizados

Se um GUID de contexto de comando apropriado ainda não estiver definido, você poderá definir um em seu VSPackage e, em seguida, programá-lo para estar ativo ou inativo conforme necessário para controlar a visibilidade dos seus comandos:

1. Registre GUIDs de contexto chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A> método.

2. Obtenha o estado de um GUID de contexto chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> método.

3. Ativar e desativar os GUIDs de contexto chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A> método.

> [!CAUTION]
> Verifique se o VSPackage não afeta nenhum GUID de contexto existente porque outros VSPackages podem depender deles.

## <a name="see-also"></a>Confira também

- [Objetos de contexto de seleção](../../extensibility/internals/selection-context-objects.md)
- [Como VSPackages adicionar elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
