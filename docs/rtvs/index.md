---
title: Ferramentas R para Visual Studio
description: As RTVS (Ferramentas do R para Visual Studio) são uma extensão de software livre gratuita que fornece muitos recursos de idioma, incluindo IntelliSense, depuração e workspaces remotos.
ms.date: 11/13/2017
ms.prod: visual-studio-dev15
ms.technology: vs-rtvs
ms.topic: overview
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- data-science
ms.openlocfilehash: 05ffd249be3d7734979f3a131a3a10423b76cb9d
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35667009"
---
# <a name="work-with-r-in-visual-studio"></a>Trabalhar com o R no Visual Studio

O R é uma linguagem altamente extensível e um ambiente para gráficos e computação estatística. Ele é distribuído gratuitamente sob a Licença Pública Geral GNU, dispõe de suporte à comunidade forte e é conhecido por sua capacidade de gerar plotagens de qualidade de publicação incluindo fórmulas e símbolos matemáticos. Você pode saber mais sobre o R em [r-project.org](https://www.r-project.org/about.html) e [Uma introdução ao R](https://cran.r-project.org/doc/manuals/r-release/R-intro.html).

As RTVS (Ferramentas do R para Visual Studio) são uma extensão de [software livre](https://github.com/microsoft/RTVS) gratuita para Visual Studio 2017 e Visual Studio 2015 Atualização 3 (ou superior), lançado sob a licença MIT. (Um segundo componente de software livre chamado [RHost](https://github.com/microsoft/R-Host), que é vinculado aos binários do interpretador do R, é lançado sob a Licença Pública GNU V2.)

> [!Note]
> Atualmente, as RTVS são compatíveis apenas com o Visual Studio para Windows, mas não com o Visual Studio para Mac.

Para experimentar o R no Visual Studio:

- [Instale as Ferramentas do R](installing-r-tools-for-visual-studio.md).
- Siga o guia de [Introdução](getting-started-with-r.md) e os artigos [Exemplos](getting-started-samples.md) e [Obtendo ajuda](getting-started-help.md).

Depois, siga os links abaixo para saber mais sobre recursos relacionados ao R, bem como os próprios recursos gerais do Visual Studio.

| Recurso | Descrição | Documentação geral do Visual Studio |
| --- | --- | --- |
| [Sistema de projeto do Visual Studio](r-projects-in-visual-studio.md) | Organize e gerencie arquivos relacionados em uma estrutura conveniente e aproveite modelos úteis para itens como código R, documentação de R, R Markdown, consultas SQL e procedimentos armazenados. Aproveite também o [gerenciador de pacotes](r-package-manager-in-visual-studio.md) e a [integração do SQL Server](integrating-sql-server-with-r.md).  | [Soluções e projetos no Visual Studio](../ide/solutions-and-projects-in-visual-studio.md) |
| [Workspace](r-workspaces-in-visual-studio.md) | As RTVS podem ser associadas a workspaces locais e remotos, permitindo que você desenvolva o código R localmente com conjuntos de dados menores, em seguida, execute com facilidade o código em computadores baseados em nuvem mais poderosos com conjuntos de dados muito maiores. | N/D |
| [Opções de Ferramentas R](options-for-r-tools-in-visual-studio.md) | Controle vários aspectos das RTVS. | [Caixa de diálogo de opções](../ide/reference/options-dialog-box-visual-studio.md) |
| [Edição avançada, IntelliSense e snippets de código](editing-r-code-in-visual-studio.md) | Inclui coloração de sintaxe, [IntelliSense](r-intellisense.md) em todo o código e todas as bibliotecas, formatação de código, ajuda da assinatura, comandos Ir Para Definição e Localizar Todas as Referências, [snippets de código](code-snippets-for-r.md) e muito mais. | [Recursos do Editor de Códigos](../ide/writing-code-in-the-code-and-text-editor.md) |
| [R Markdown](rmarkdown-with-r-in-visual-studio.md) | Os documentos do R Markdown R ajudam você a compartilhar os resultados de dados, com código R integrado dentro dos blocos de código de markdown. | N/D |
| [Janela Interativa](interactive-repl-for-r-in-visual-studio.md) | Fornece uma experiência completa de REPL para o R com a capacidade de executar facilmente o código em um arquivo de origem na janela interativa. | N/D |
| [Visualização de dados](visualizing-data-with-r-in-visual-studio.md) | A plotagem é parte integral da experiência do R, e as RTVS são compatíveis com várias janelas de gráficos independentes, cada qual com seu próprio histórico e a capacidade de mover as plotagens entre as janelas. As plotagens podem ser salvas em bitmap e arquivos PDF ou copiadas para a área de transferência como um bitmap ou metarquivo.  | N/D |
| [Gerenciador de Variáveis](variable-explorer.md) | Examine as variáveis em escopos globais ou específicos do pacote, com a possibilidade de exibir tabelas classificáveis e exportar para CSV. | N/D |
| [Depuração completa](debugging-r-in-visual-studio.md) | Inclui a integração com a janela interativa. | [Depurando no Visual Studio](../debugger/debugging-in-visual-studio.md) |

Confira também as [Perguntas frequentes](faq.md).

|   |   |
|---|---|
| ![ícone de câmera para vídeo](../install/media/video-icon.png "Assistir a um vídeo") | [Assista a um vídeo (youtube.com)](https://www.youtube.com/watch?v=dll3IS1bfWQ) para obter uma visão geral das ferramentas do R para Visual Studio (12min 36s). Assista também a [mais vídeos de ferramentas do R](https://www.youtube.com/results?search_query=R+Tools+for+visual+studio). |

## <a name="send-us-your-feedback"></a>Envie-nos seus comentários!

1. **Problemas do GitHub**: a melhor maneira de entrar em contato com a equipe de RTVS é [registrar um problema no GitHub](https://github.com/Microsoft/RTVS/issues) ou usar o menu **Ferramentas R** > **Comentários**.

1. **Envie um Smiley/Rosto Triste**: o menu **Ferramentas R** > **Comentários** é uma maneira rápida de enviar comentários e anexar arquivos de log das RTVS para auxiliar no diagnóstico do seu problema. (Os logs são registrados em *%temp%/RTVSlogs.zip* caso você queira enviá-los separadamente.) O log será desabilitado se você tiver cancelado a telemetria do Visual Studio por meio do comando de menu **Ajuda** > **Comentários** > **Configurações** ou durante a instalação.

1. **Email**: você pode enviar comentários diretos para a equipe em *rtvsuserfeedback (arroba) microsoft.com*.
