---
title: Melhorar o tempo de inicialização
description: Saiba como controlar as configurações de extensões e janelas de ferramentas na caixa de diálogo Gerenciar desempenho do Visual Studio para melhorar o tempo de inicialização do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/15/2017
ms.topic: how-to
helpviewer_keywords:
- startup time [Visual Studio]
- optimizing performance [Visual Studio]
- speed up start time [Visual Studio]
ms.assetid: d1508121-8499-4084-8eb5-fa89fa7b17d3
author: TerryGLee
ms.author: tglee
manager: jillfra
f1_keywords:
- vs.performancecenter
ms.workload:
- multiple
ms.openlocfilehash: c409ad35b3d9c09a5dbe574d00a24d1f2bcb8370
ms.sourcegitcommit: df6ba39a62eae387e29f89388be9e3ee5ceff69c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96479947"
---
# <a name="optimize-visual-studio-startup-time"></a>Otimizar o tempo de inicialização do Visual Studio

O Visual Studio foi projetado para iniciar da forma mais rápida e eficiente possível. No entanto, determinadas extensões e janelas de ferramentas do Visual Studio poderão afetar negativamente o tempo de inicialização quando forem carregadas. É possível controlar o comportamento das extensões e das janelas de ferramentas lentas na caixa de diálogo **Gerenciar o Desempenho do Visual Studio**. Para ver mais dicas gerais sobre como melhorar o desempenho, veja [Dicas e truques de desempenho do Visual Studio](../ide/visual-studio-performance-tips-and-tricks.md).

## <a name="startup-behavior"></a>Comportamento da inicialização

Para evitar estender o tempo de inicialização, o Visual Studio carrega extensões usando uma abordagem _sob demanda_. Esse comportamento significa que as extensões não abrem imediatamente após o Visual Studio ser iniciado, mas conforme necessário. Além disso, como as janelas de ferramentas deixadas abertas em uma sessão anterior do Visual Studio podem deixar o tempo de inicialização lento, o Visual Studio abre as janelas de ferramentas de uma maneira mais inteligente para evitar afetar o tempo de inicialização.

Se o Visual Studio detectar lentidão na inicialização, uma mensagem pop-up será exibida, alertando-o para a janela de ferramentas ou extensão que está causando a lentidão. A mensagem fornece um link para a caixa de diálogo **Gerenciar o Desempenho do Visual Studio**. Você também pode acessar essa caixa de diálogo escolhendo **ajudar a**  >  **gerenciar o desempenho do Visual Studio** na barra de menus.

![Gerenciar o Desempenho do Visual Studio – pop-up indicando "Observamos que a extensão ... está deixando o Visual Studio mais lento"](../ide/media/vside_perfdialog_popup.png)

A caixa de diálogo lista as janelas de ferramentas e extensões que estão afetando o desempenho de inicialização. Você pode alterar as configurações das janelas de ferramentas e das extensões para melhorar o desempenho de inicialização.

## <a name="to-change-extension-settings-to-improve-startup-solution-load-and-typing-performance"></a><a name="extensions" />Para alterar as configurações das extensões para melhorar o desempenho da inicialização, do carregamento de soluções e da digitação

1. Abra a caixa de diálogo **Gerenciar o Desempenho do Visual Studio** escolhendo **Ajuda** > **Gerenciar o Desempenho do Visual Studio** na barra de menus.

    Se uma extensão estiver retardando a inicialização, o carregamento de soluções ou a digitação no Visual Studio, a extensão aparecerá na caixa de diálogo **Gerenciar o Desempenho do Visual Studio** em **Extensões** > **Inicialização** (ou **Carregamento da Solução** ou **Digitação**).

    ![Gerenciar o desempenho do Visual Studio – exibição de extensões](../ide/media/vside_perfdialog_extensions.png)

2. Escolha a extensão que você deseja desabilitar e clique no botão **Desabilitar**.

Você sempre pode reabilitar a extensão para sessões futuras usando o Gerenciador de **extensões** ou a caixa de diálogo **gerenciar desempenho do Visual Studio** .

## <a name="to-change-tool-window-settings-to-improve-startup-time"></a><a name="tool-windows" />Para alterar as configurações das janelas de ferramentas para melhorar o tempo de inicialização

1. Abra a caixa de diálogo **Gerenciar o Desempenho do Visual Studio** escolhendo **Ajuda** > **Gerenciar o Desempenho do Visual Studio** na barra de menus.

    Se uma janela de ferramentas estiver retardando a inicialização do Visual Studio, ela será exibida na caixa de diálogo **Gerenciar o Desempenho do Visual Studio** em **Janelas de Ferramentas** > **Inicialização**.

2. Escolha a janela de ferramentas da qual você deseja alterar o comportamento.

3. Escolha uma das seguintes três opções:

   - **Usar comportamento padrão:** o comportamento padrão da janela de ferramentas. Manter essa opção selecionada não melhorará o desempenho de inicialização.

   - **Não mostrar janela na inicialização:** a janela de ferramentas especificada sempre estará fechada ao abrir o Visual Studio, mesmo se ela for deixada aberta em uma sessão anterior. Você pode abrir a janela de ferramentas no menu apropriado quando necessário.

   - **Ocultar automaticamente janela na inicialização:** se uma janela de ferramentas tiver sido deixada aberta em uma sessão anterior, essa opção recolherá o grupo da janela de ferramentas na inicialização para evitar inicializar a janela de ferramentas. Essa opção é uma boa alternativa se você usa uma janela de ferramentas com frequência. A janela de ferramentas ainda está disponível, mas não afeta mais negativamente o tempo de inicialização do Visual Studio.

     ![Gerenciar o desempenho do Visual Studio – exibição da janela de ferramentas](../ide/media/vside_perfdialog_toolwindows.png)

> [!NOTE]
> Algumas versões anteriores do Visual Studio 2017 tinham um recurso chamado **carga de solução leve**. Nas versões atuais, soluções grandes que contêm um código gerenciado são carregadas mais rapidamente do que antes, mesmo sem a carga de solução leve.

## <a name="see-also"></a>Confira também

- [Otimizar o desempenho do Visual Studio](../ide/optimize-visual-studio-performance.md)
- [Dicas e truques de desempenho do Visual Studio](../ide/visual-studio-performance-tips-and-tricks.md)
- [Blog do Visual Studio – Carregar soluções mais rapidamente com o Visual Studio 2017 versão 15.6](https://devblogs.microsoft.com/visualstudio/load-solutions-faster-with-visual-studio-2017-version-15-6/)
