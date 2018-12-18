---
title: 'Como: depurar código injetado | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.injected
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- assembly language, viewing
- debugging [C++], viewing assembly code
- debugging [C++], injected code
- debugging [C++], enabling source annotation
- injected code
- Show Source Code command [debugger]
- debugging [C++], using attributes
- disassembly code, debugging
ms.assetid: a1b4104d-d49e-451f-a91e-e39ceaf35875
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8efcc5780b27967644330e55dc540333a19105a2
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389332"
---
# <a name="how-to-debug-injected-code"></a>Como depurar código injetado

> [!NOTE]
> As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha Importar e Exportar Configurações no menu Ferramentas. Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

Usar atributos pode simplificar muito a programação C++. Para obter mais informações, consulte [conceitos](/cpp/windows/attributed-programming-concepts). Alguns atributos são interpretados diretamente pelo compilador. Outros atributos injetam o código na origem do programa, que o compilador em seguida compila. Este código injetado facilita a programação reduzindo a quantidade de códigos que você precisa escrever. Entretanto, às vezes, um bug pode causar falha no aplicativo ao executar o código injetado. Quando isso acontece, você provavelmente desejará examinar o código injetado. O Visual Studio fornece duas maneiras de ver o código injetado:

- Você pode exibir o código injetado na janela **Desmontagem**.

- Usando [/Fx](/cpp/build/reference/fx-merge-injected-code), você pode criar um arquivo de origem mesclada que contém o código original e injetado.

A janela **Desmontagem** mostra as instruções da linguagem assembly que corresponde ao código-fonte e o código injetado por atributos. Além disso, a janela **Desmontagem** pode mostrar a anotação do código-fonte.

## <a name="to-turn-on-source-annotation"></a>Para ativar a anotação de origem

-   Clique com o botão direito do mouse na janela **Desmontagem** e escolha **Mostrar Código-Fonte** no menu de atalho.

     Se você souber a localização de um atributo em uma janela de origem, poderá usar o menu de atalho para localizar o código injetado na janela **Desmontagem**.

## <a name="to-view-injected-code"></a>Para exibir o código injetado

1.  O depurador deve estar no modo de interrupção.

2.  Em uma janela do código-fonte, coloque o cursor na frente do atributo cujo código injetado você deseja exibir.

3.  Clique com o botão direito do mouse e selecione **Ir para Desmontagem** no menu de atalho.

     Se a localização do atributo estiver perto do ponto de execução atual, você poderá selecionar a janela **Desmontagem** no menu **Depurar**.

## <a name="to-view-the-disassembly-code-at-the-current-execution-point"></a>Para exibir o código de desmontagem no ponto de execução atual

1.  O depurador deve estar no modo de interrupção.

2.  No menu **Depurar**, escolha **Windows** e clique em **Desmontagem**.

## <a name="see-also"></a>Consulte também

- [Segurança do depurador](../debugger/debugger-security.md)
- [Depurando código nativo](../debugger/debugging-native-code.md)