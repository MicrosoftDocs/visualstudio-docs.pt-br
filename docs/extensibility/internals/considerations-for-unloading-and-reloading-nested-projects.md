---
title: Descarregando e recarregando projetos aninhados
description: Conheça as etapas adicionais que devem ser executadas ao descarregar e recarregar projetos aninhados no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- nested projects, unloading and reloading
- projects [Visual Studio SDK], unloading and reloading nested
ms.assetid: 06c3427e-c874-45b1-b9af-f68610ed016c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9852454d487ab2a7ee08218c9712aa0afc1467ad
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057065"
---
# <a name="considerations-for-unloading-and-reloading-nested-projects"></a>Considerações para descarregar e recarregar projetos aninhados

Ao implementar tipos de projeto aninhados, você deve executar etapas adicionais ao descarregar e recarregar os projetos. Para notificar corretamente os ouvintes aos eventos da solução, você deve gerar corretamente os `OnBeforeUnloadProject` `OnAfterLoadProject` eventos e.

Um motivo para gerar esses eventos é o SCC (controle de código-fonte). Você não quer que o SCC exclua os itens do servidor e os adicione novamente como *novo* se houver uma `Get` operação do SCC. Nesse caso, um novo arquivo será carregado do SCC. Você precisará descarregar e recarregar todos os arquivos caso eles sejam diferentes.

Chamadas de controle do código-fonte `ReloadItem` . Implemente a <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents> interface para chamar `OnBeforeUnloadProject` e `OnAfterLoadProject` excluir o projeto e recrie-o. Quando você implementa a interface dessa forma, o SCC é informado de que o projeto foi excluído temporariamente e adicionado novamente. Portanto, o SCC não funciona no projeto como se o projeto fosse *realmente* excluído e adicionado novamente.

## <a name="reload-projects"></a>Recarregar projetos

Para dar suporte ao recarregamento de projetos aninhados, você implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> método. Na implementação do `ReloadItem` , você fecha os projetos aninhados e os recria.

Normalmente, quando um projeto é recarregado, o IDE gera os <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeUnloadProject%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject%2A> eventos e. No entanto, para projetos aninhados que são excluídos e recarregados, o projeto pai inicia o processo, não o IDE. Como o projeto pai não gera eventos de solução e o IDE não tem informações sobre a inicialização do processo, os eventos não são gerados.

Para lidar com esse processo, o projeto pai chama `QueryInterface` a <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents> interface. `IVsFireSolutionEvents` tem funções que instruem o IDE a gerar o `OnBeforeUnloadProject` evento para descarregar o projeto aninhado e, em seguida, gerar o `OnAfterLoadProject` evento para recarregar o mesmo projeto.

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>
- [Aninhar projetos](../../extensibility/internals/nesting-projects.md)
