---
title: Estendendo outras partes do Visual Studio | Microsoft Docs
description: Saiba mais sobre partes da interface do usuário do Visual Studio que você pode estender. Você pode criar um VSPackage, gravar no log de atividades e estender a caixa de ferramentas e a barra de status.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces
ms.assetid: 27d2f1e1-2503-4aca-9cfc-707abd07ccf0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e21c5b8a3570b4da0cb0286d3c0d6d7c84c2f704
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99895837"
---
# <a name="extend-other-parts-of-visual-studio"></a>Estender outras partes do Visual Studio

Há muitas outras partes da interface do usuário do Visual Studio que você pode estender. Aqui, mostramos apenas alguns.

## <a name="create-a-vspackage"></a>Criar um VSPackage

Os blocos de construção básicos da extensibilidade do Visual Studio são VSPackages.  Saiba como adicionar um VSPackage: [criar uma extensão com um VSPackage](../extensibility/creating-an-extension-with-a-vspackage.md)

## <a name="extend-the-toolbox"></a>Estender a caixa de ferramentas

Saiba como adicionar novos controles e outros itens à caixa de ferramentas e como usar a funcionalidade da caixa de ferramentas:

- [Criar um controle de caixa de ferramentas do WPF](../extensibility/creating-a-wpf-toolbox-control.md)

- [Criar um controle de caixa de ferramentas de Windows Forms](../extensibility/creating-a-windows-forms-toolbox-control.md)

## <a name="extend-the-status-bar"></a>Estender a barra de status

Saiba como ler e gravar na barra de status e na barra de progresso e como fornecer animações e outras interfaces do usuário: [estenda a barra de status](../extensibility/extending-the-status-bar.md).

::: moniker range="vs-2017"

## <a name="create-custom-start-pages"></a>Criar páginas iniciais personalizadas

Saiba como fazer sua própria página inicial, do zero ou de uma amostra de página inicial baixável: [criar uma página inicial personalizada](../extensibility/creating-a-custom-start-page.md).

::: moniker-end

## <a name="write-to-the-activity-log"></a>Gravar no log de atividades

Saiba como gravar no log de atividades: [como usar o log de atividades](../extensibility/how-to-use-the-activity-log.md).
