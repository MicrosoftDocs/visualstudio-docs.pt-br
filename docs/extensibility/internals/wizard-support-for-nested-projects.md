---
title: Suporte do assistente para projetos aninhados | Microsoft Docs
description: Saiba mais sobre os dois assistentes que um projeto pai pode implementar para projetos aninhados em seu VSPackage no SDK do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add Item wizard
- nested projects, wizard support
- New Project wizard
ms.assetid: 1b496acc-b326-4cdb-bb48-e3b5c6f12e05
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7f52b42462fdc4b7878f97c01bdc65322f32eb5b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074139"
---
# <a name="wizard-support-for-nested-projects"></a>Suporte do assistente para projetos aninhados
O IDE executa dois assistentes que o projeto pai para projetos aninhados podem implementar: o assistente de **novo projeto** e o assistente para **Adicionar item** .

 Se um usuário iniciar o assistente de **novo projeto** selecionando **Adicionar projeto** e clicando em **novo projeto** no menu arquivo ou selecionando **Adicionar** e clicando com o botão direito em **novo projeto** no Gerenciador de soluções, o IDE executa o comando **AddProject** e a implementação do projeto pai do comando **AddProject** retorna um arquivo de projeto de modelo ou um arquivo de assistente (. vsz) que tem um conjunto de parâmetros de contexto.

 Da mesma forma, a implementação de assistentes de **AddItem** de um projeto pai retorna um arquivo. vsz que tem um conjunto diferente de parâmetros de contexto.

 Para obter mais informações sobre assistentes, consulte [Wizard (. Vsz) arquivo](../../extensibility/internals/wizard-dot-vsz-file.md), [parâmetros de contexto](../../extensibility/internals/context-parameters.md) e [registro de modelos de projeto e item](../../extensibility/internals/registering-project-and-item-templates.md).

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>
- [Aninhando projetos](../../extensibility/internals/nesting-projects.md)
