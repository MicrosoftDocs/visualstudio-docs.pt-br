---
title: Melhorar o desempenho se o Visual Studio estiver lento
titleSuffix: ''
ms.date: 04/11/2018
ms.topic: conceptual
helpviewer_keywords:
- performance [Visual Studio]
author: gewarren
ms.author: gewarren
manager: douge
f1_keywords:
- vs.performancecenter
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: f5fe9324360a01700024e14e6c70755d61aa3e60
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53065769"
---
# <a name="optimize-visual-studio-performance"></a>Otimizar o desempenho do Visual Studio

Este artigo fornece algumas sugestões para tentar se você achar que o Visual Studio está sendo executado lentamente. Você também pode dar uma olhada em [Dicas e truques de desempenho do Visual Studio](../ide/visual-studio-performance-tips-and-tricks.md) para obter mais sugestões sobre como melhorar o desempenho.

## <a name="upgrade-to-visual-studio-2017-version-156-or-later"></a>Atualizar o Visual Studio 2017 versão 15.6 ou posterior

Se estiver usando Visual Studio 2015, baixe o [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) gratuitamente para conhecer seu desempenho aprimorado. As soluções são carregadas duas a três vezes mais rapidamente no Visual Studio 2017, com melhorias de desempenho em outras áreas também. O Visual Studio 2017 é compatível lado a lado com o Visual Studio 2015, para que você não perca nada por experimentá-lo.

Se estiver usando o Visual Studio 2017, verifique se você está executando a versão 15.6 ou posterior. Dados mostram que as soluções são carregadas duas ou três vezes mais rapidamente na versão 15.6. Faça download dela [aqui](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).

## <a name="extensions-and-tool-windows"></a>Extensões e janelas de ferramentas

Você pode ter extensões instaladas que estão diminuindo o Visual Studio. Para obter ajuda sobre como gerenciar extensões para melhorar o desempenho, consulte [Alterar configurações de extensão para melhorar o desempenho](../ide/optimize-visual-studio-startup-time.md#extensions).

Da mesma forma, você pode ter janelas de ferramentas que estão deixando o Visual Studio mais lento. Para obter ajuda sobre como gerenciar janelas de ferramentas, consulte [Alterar as configurações da janela de ferramentas](../ide/optimize-visual-studio-startup-time.md#tool-windows).

## <a name="hardware"></a>Hardware

Se você estiver pensando em atualizar seu hardware, uma SSD (unidade de estado sólido) tem mais efeito sobre o desempenho do que memória RAM adicional ou uma CPU mais rápida.

Se você adicionar uma SSD, para ter o desempenho ideal, instale o Windows nessa unidade em vez de uma HDD (unidade de disco rígido). O local da unidade de suas soluções do Visual Studio parece não importar tanto.

Além disso, não execute sua solução de uma unidade USB. Copie-a para a HDD ou SSD.

## <a name="help-us-improve"></a>Ajude-nos a melhorar

Seus comentários nos ajudam a melhorar. Use o recurso **Relatar um Problema** para "registrar" um rastreamento e nos enviar. Selecione o ícone de comentários ao lado de **QuickLaunch** ou selecione **Ajuda** > **Enviar Comentários** > **Relatar um Problema** na barra de menus. Para saber mais, veja [Como relatar um problema com o Visual Studio 2017](../ide/how-to-report-a-problem-with-visual-studio-2017.md).

## <a name="see-also"></a>Consulte também

- [Dicas e truques de desempenho](../ide/visual-studio-performance-tips-and-tricks.md)
- [Blog do Visual Studio – Carregar soluções mais rapidamente com o Visual Studio 2017 versão 15.6](https://blogs.msdn.microsoft.com/visualstudio/2018/04/04/load-solutions-faster-with-visual-studio-2017-version-15-6/)