---
title: Caixa de diálogo Opções
description: Saiba mais sobre a caixa de diálogo opções, seu layout e como o Visual estúdios aplica as opções que você seleciona para seus projetos e soluções.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.toolsoptionspages
helpviewer_keywords:
- Tools Options settings
- Options dialog box
- Options dialog box, development environment
- tools [Visual Studio], customizing
ms.assetid: 02b09877-1df1-4531-a0d1-a4ca17c7f857
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 79bd2d95a12aa7c42705d106cf71b4061a020431
ms.sourcegitcommit: 113b7df611583307d3965984233a33355d6b0318
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/16/2021
ms.locfileid: "112126535"
---
# <a name="options-dialog-box-visual-studio"></a>Caixa de diálogo Opções (Visual Studio)

A caixa de diálogo **Opções** permite que você configure o IDE (ambiente de desenvolvimento integrado) para as suas necessidades. Por exemplo, estabelecer um local de salvamento padrão para seus projetos, alterar a aparência e o comportamento padrão das janelas e criar atalhos para os comandos mais usados. Também há opções específicas para a sua plataforma e linguagem de desenvolvimento. Você pode acessar **Opções** do menu **Ferramentas**.

## <a name="layout-of-the-options-dialog-box"></a>Layout da caixa de diálogo Opções

A caixa de diálogo **Opções** é dividida em duas partes: um painel de navegação à esquerda e uma área de exibição à direita. O controle de árvore no painel de navegação inclui nós de pasta, como Ambiente, Editor de Texto, Projetos e Soluções e Controle do Código-Fonte. Expanda qualquer nó da pasta para listar as páginas de opções que ele contém. Quando você seleciona o nó para uma determinada página, suas opções aparecem na área de exibição.

Opções para um recurso IDE não aparecem no painel de navegação até que o recurso seja carregado na memória. Portanto, quando começa uma nova sessão, pode ser que não sejam exibidas as mesmas opções que eram exibidas quando você terminou a última. Quando você cria um projeto ou executa um comando que usa um aplicativo em particular, nós para opções relevantes são adicionados à caixa de diálogo Opções. Essas opções adicionadas então permanecerão disponíveis, desde que o recurso de IDE permaneça na memória.

> [!NOTE]
> Algumas coleções de configurações definem o escopo do número de páginas que aparecem no painel de navegação da caixa de diálogo Opções.

## <a name="how-options-are-applied"></a>Como as opções são aplicadas

Clicar em OK na caixa de diálogo **Opções** salva todas as configurações em todas as páginas. Clicar em Cancelar em qualquer página cancela todas as solicitações de alteração, incluindo qualquer uma recém feita em outras páginas de **Opções**. Algumas alterações nas configurações de opção, como aquelas feitas na [Caixa de Diálogo Fontes e Cores, Ambiente, Opções](../../ide/reference/fonts-and-colors-environment-options-dialog-box.md), apenas entrarão em vigor depois que você fechar e reabrir o Visual Studio.

## <a name="see-also"></a>Confira também

- [Personalizando o editor](../how-to-change-text-case-in-the-editor.md)
- [Configurações e preferências do git](../../version-control/git-settings.md)
