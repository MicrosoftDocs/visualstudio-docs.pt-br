---
title: Exibindo arquivos usando o comando abrir arquivo | Microsoft Docs
description: Saiba como o IDE (ambiente de desenvolvimento integrado) do Visual Studio manipula o comando abrir arquivo no menu arquivo para exibir arquivos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, supporting Open File command
- Open File command
- persistence, supporting Open File command
ms.assetid: 4fff0576-b2f3-4f17-9769-930f926f273c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b2617050ff26536df5a94d0cb51fe74d37a55725
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061336"
---
# <a name="display-files-by-using-the-open-file-command"></a>Exibir arquivos usando o comando abrir arquivo
As etapas a seguir descrevem como o IDE manipula o comando **Abrir arquivo** , que está disponível no menu **arquivo** no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . As etapas também descrevem como os projetos devem responder a chamadas que se originam desse comando.

 Quando um usuário clica no comando **Abrir arquivo** no menu **arquivo** e seleciona um arquivo na caixa de diálogo **Abrir arquivo** , ocorre o seguinte processo:

1. Usando a tabela de documentos em execução, o IDE determina se o arquivo já está aberto em um projeto.

    - Se o arquivo estiver aberto, o IDE retona a janela.

    - Se o arquivo não estiver aberto, o IDE chamará <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> para consultar cada projeto para determinar qual projeto pode abrir o arquivo.

        > [!NOTE]
        > Na implementação do projeto do <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> , forneça um valor de prioridade que indica o nível no qual o projeto abre o arquivo. Os valores de prioridade são fornecidos na <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> enumeração.

2. Cada projeto responde com um nível de prioridade que indica a importância que ele coloca para que o projeto Abra o arquivo.

3. O IDE usa os critérios a seguir para determinar qual projeto abre o arquivo:

    - O projeto que responde com a prioridade mais alta ( `DP_Intrinsic` ) abre o arquivo. Se mais de um projeto responder com essa prioridade, o primeiro projeto a responder abrirá o arquivo.

    - Se nenhum projeto responder com a prioridade mais alta ( `DP_Intrinsic` ), mas todos os projetos responderem com a mesma prioridade mais baixa, o projeto ativo abrirá o arquivo. Se nenhum projeto estiver ativo, o primeiro projeto a ser respondido abrirá o arquivo.

    - Se nenhum projeto alega a propriedade do arquivo ( `DP_Unsupported` ), o projeto de arquivos diversos abre o arquivo.

         Se uma instância do projeto de arquivos diversos for criada, o projeto sempre responderá com o valor `DP_CanAddAsExternal` . Esse valor indica que o projeto pode abrir o arquivo. Este projeto é usado para alojar arquivos abertos que não estão em nenhum outro projeto. A lista de itens neste projeto não é persistente; Esse projeto é visível em **Gerenciador de soluções** somente quando é usado para abrir um arquivo.

         Se o projeto de arquivos diversos não indicar que ele pode abrir o arquivo, uma instância do projeto não será criada. Nesse caso, o IDE cria uma instância do projeto de arquivos diversos e informa ao projeto para abrir o arquivo.

4. Assim que o IDE determina qual projeto abre o arquivo, ele chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> método nesse projeto.

5. Em seguida, o projeto tem a opção de abrir o arquivo usando um editor específico do projeto ou um editor padrão. Para obter mais informações, consulte [como: abrir editores específicos do projeto](../../extensibility/how-to-open-project-specific-editors.md) e [como: abrir editores padrão](../../extensibility/how-to-open-standard-editors.md), respectivamente.

## <a name="see-also"></a>Confira também
- [Exibir arquivos usando o comando abrir com](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)
- [Abrir e salvar itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md)
- [Como: abrir editores específicos do projeto](../../extensibility/how-to-open-project-specific-editors.md)
- [Como: abrir editores padrão](../../extensibility/how-to-open-standard-editors.md)
