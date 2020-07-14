---
title: Como iniciar o Spy + + | Microsoft Docs
ms.date: 12/16/2018
ms.topic: how-to
helpviewer_keywords:
- Spy++, starting
ms.assetid: 1d36813a-dc2a-4fda-9b3d-a38928a62ced
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b659350adc39fd1088964976b8bcdef629bad44b
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348998"
---
# <a name="how-to-start-spy"></a>Como iniciar Spy++

Você pode iniciar o Spy + + no Visual Studio ou em um prompt de comando.

 Quando você iniciar o Spy + +, se uma mensagem for exibida para pedir permissão para fazer alterações no computador, selecione **Sim**.

> [!NOTE]
> Você pode executar apenas uma instância do Spy + +. Se você tentar iniciar uma segunda instância, isso apenas fará com que a instância em execução no momento tenha o foco.

## <a name="prerequisites"></a>Pré-requisitos

O Spy + + requer os seguintes componentes. Você pode selecionar esses componentes na Instalador do Visual Studio selecionando a guia **componentes individuais** e, em seguida, selecionando os componentes a seguir.

* Em depuração e teste, selecione **ferramentas de criação de perfil do C++**
* Em atividades de desenvolvimento, selecione **recursos principais do C++**

Se você fez alterações, siga os prompts para instalar esses componentes.

## <a name="start-spy-from-visual-studio"></a>Iniciar o Spy + + no Visual Studio

No menu **ferramentas** , selecione **Spy + +**.

Como o Spy + + é executado de forma independente, depois de iniciá-lo, você pode fechar o Visual Studio.

> [!NOTE]
> Quando você registra mensagens com o Spy + +, isso pode fazer com que o sistema operacional seja executado mais lentamente.

## <a name="start-spy-at-a-command-prompt"></a>Iniciar o Spy + + em um prompt de comando

1. Em uma janela de prompt de comando, altere os diretórios para a pasta que contém spyxx.exe. Normalmente, o caminho para essa pasta é.. \\ *Pasta de instalação do Visual Studio*\Common7\Tools \\ .

2. Insira **spyxx.exe**.

## <a name="see-also"></a>Veja também
- [Usando Spy++](../debugger/using-spy-increment.md)
- [Exibições do Spy++](../debugger/spy-increment-views.md)
- [Referência de Spy++](../debugger/spy-increment-reference.md)
