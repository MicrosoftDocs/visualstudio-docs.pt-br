---
title: 'Como: depurar o código otimizado | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- breakpoints, in optimized code
- debugging [C++], optimized code
- optimization, debug builds
- debug builds, optimizing
- optimized code, debugging
ms.assetid: fc8eeeb8-6629-4c9b-99f7-2016aee81dff
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c6e212129c17ec7b4fe6cb9a6808c91cb302deb3
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52387850"
---
# <a name="how-to-debug-optimized-code"></a>Como depurar o código otimizado

> [!NOTE]
> As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha Importar e Exportar Configurações no menu Ferramentas. Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

> [!NOTE]
> O [/Zo (aprimorar otimizado de depuração)](/cpp/build/reference/zo-enhance-optimized-debugging)opção de compilador (apresentada na atualização 3 do Visual Studio) gera informações de depuração mais avançadas para código otimizado (projetos que não são criados com o **/Od** opção de compilador. Ver [/O opções (otimizar código)](/cpp/build/reference/o-options-optimize-code)). Isso inclui suporte aprimorado para as funções embutidas e variáveis locais de depuração.
>
> [Editar e continuar](../debugger/edit-and-continue-visual-csharp.md) é desabilitada quando o **/Zo** ocompiler opção é usada.

 Quando o compilador otimiza o código, ele reposiciona e reclassifica instruções. Isso resulta em um código compilado mais eficiente. Devido a esse rearranjo, o depurador nem sempre pode identificar o código-fonte que corresponde a um conjunto de instruções.

 A otimização pode afetar:

- As variáveis locais, que podem ser removidas pelo otimizador ou movidas para locais que o depurador não entende.

- Posições dentro de uma função, que são alteradas quando o otimizador mescla blocos de código.

- Nomes de função para quadros na pilha de chamadas, que pode estar errado se o otimizador mesclar duas funções.

  Os quadros que você vê na pilha de chamadas estão quase sempre corretos, porém, supondo que você tenha símbolos para todos os quadros. Os quadros na pilha de chamadas estarão incorretos se você tiver um dano na pilha, se você tiver as funções escritas na linguagem assembly, ou se houver quadros do sistema operacional sem símbolos correspondentes na pilha de chamadas.

  As variáveis globais e estáticas são sempre mostradas corretamente. Da mesma forma que o layout da estrutura. Se você tiver um ponteiro para uma estrutura e o valor do ponteiro estiver correto, cada variável de membro da estrutura mostrará o valor correto.

  Devido a essas restrições, você deverá depurar usando uma versão não otimizada do programa se isso for possível. Por padrão, a otimização está desativada na configuração de Depuração de um programa do Visual C++ e ativada na configuração de Versão.

  No entanto, um bug pode aparecer somente em uma versão otimizada de um programa. Nesse caso, você deverá depurar o código otimizado.

## <a name="to-turn-on-optimization-in-a-debug-build-configuration"></a>Para ativar a otimização em uma configuração da compilação de Depuração

1. Quando você cria um novo projeto, selecione o destino de `Win32 Debug`. Use o destino `Win32``Debug` até que seu programa seja depurado completamente e você esteja pronto para compilar um destino de `Win32 Release`. O compilador não otimiza o destino de `Win32 Debug`.

2. Selecione o projeto no Gerenciador de Soluções.

3. No menu **Exibir**, clique em **Páginas de Propriedades**.

4. Na caixa de diálogo **Páginas de Propriedades**, verifique se `Debug` está selecionado na lista suspensa **Configuração**.

5. Na exibição da pasta à esquerda, selecione a pasta **C/C++**.

6. Na pasta **C++**, selecione `Optimization`.

7. Na lista de propriedades à direita, localize `Optimization`. A configuração ao lado provavelmente informa `Disabled (`[/Od](/cpp/build/reference/od-disable-debug)`)`. Escolha uma dessas opções (`Minimum Size``(`[O1](/cpp/build/reference/o1-o2-minimize-size-maximize-speed)`)`, `Maximum Speed``(`[/O2](/cpp/build/reference/o1-o2-minimize-size-maximize-speed)`)`, `Full Optimization``(`[/Ox](/cpp/build/reference/ox-full-optimization)`)` ou `Custom`).

8. Se você escolher a opção `Custom` para `Optimization`, agora poderá definir opções para qualquer uma das outras propriedades mostradas na lista de propriedades.

9. Selecione as propriedades de configuração, C/C++, nó de linha de comando da página de propriedades do projeto e adicione `(` [/Zo](/cpp/build/reference/zo-enhance-optimized-debugging) `)` para o **opções adicionais** caixa de texto.

    > [!WARNING]
    >  `/Zo` requer o Visual Studio 2013 atualização 3 ou posterior.
    >
    >  Adicionando `/Zo` desabilitará [editar e continuar](../debugger/edit-and-continue-visual-csharp.md).

   Quando você depura o código otimizado, use a janela **Desmontagem** para ver quais instruções de fato estão criadas e executadas. Quando você define pontos de interrupção, precisa saber que o ponto de interrupção pode mover junto com uma instrução. Por exemplo, considere o seguinte código:

```cpp
for (x=0; x<10; x++)
```

 Suponha que você defina um ponto de interrupção nesta linha. Você pode esperar que o ponto de interrupção seja atingido 10 vezes, mas se o código for otimizado, o ponto de interrupção será atingido somente uma vez. Isso ocorre porque a primeira instrução define o valor de `x` como 0. O compilador reconhece que isso somente precisa ser feito uma vez e o move para fora do loop. O ponto de interrupção também será movido. As instruções que comparam e incrementam `x` permanecem dentro do loop. Quando você exibe a janela **Desmontagem**, a [unidade da etapa](/previous-versions/visualstudio/visual-studio-2010/ek13f001(v=vs.100)) será definida automaticamente como Instrução para obter maior controle, o que é útil quando você passa por código otimizado.

## <a name="see-also"></a>Consulte também

- [Segurança do depurador](../debugger/debugger-security.md)
- [Depurando código nativo](../debugger/debugging-native-code.md)