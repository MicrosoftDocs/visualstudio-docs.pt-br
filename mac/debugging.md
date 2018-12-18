---
title: Depuração com Xamarin
description: A depuração é uma parte comum e necessária da programação. Como um IDE consolidado, o Visual Studio para Mac contém um pacote completo de recursos para facilitar a depuração. Desde depuração com segurança até a visualização de dados, este artigo explicará como usar todo o potencial de depuração no Visual Studio para Mac.
author: conceptdev
ms.author: crdun
ms.date: 05/06/2018
ms.technology: vs-ide-debug
ms.assetid: BB7A084D-9AC2-48B5-8076-6C8518796BBA
ms.openlocfilehash: e17a423e9db6826c8cc693e1c75c75bb067a19e8
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295287"
---
# <a name="debugging-with-xamarin"></a>Depuração com Xamarin

O Visual Studio para Mac tem um depurador nativo para dar suporte à depuração de aplicativos Xamarin.iOS, Xamarin.Mac e Xamarin.Android.

O Visual Studio para Mac usa o [*Mono Soft Debugger*](http://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger/), que foi implementado no tempo de execução Mono, permitindo que o Visual Studio para Mac depure código gerenciado em todas as plataformas.

## <a name="the-debugger"></a>O depurador

O Visual Studio para Mac usa o Mono Soft Debugger para depurar código gerenciado (C# ou F#) em todos os aplicativos Xamarin. O depurador Mono Soft é diferente de depuradores comuns, pois ele é um depurador cooperativo interno do tempo de execução Mono; o código gerado e o tempo de execução Mono operam junto com o IDE para fornecer uma experiência de depuração. O tempo de execução Mono expõe a funcionalidade de depuração por meio de um protocolo de transmissão, sobre o qual você pode conhecer mais [na documentação do Mono](http://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger-wire-format/).

Depuradores inflexíveis, como o [LLDB]( http://lldb.llvm.org/index.html) ou o [GDB]( https://www.gnu.org/software/gdb/), controlam um programa sem o conhecimento ou a cooperação do programa depurado, mas ainda podem ser úteis ao depurar aplicativos Xamarin caso você precise depurar código Android ou iOS nativo.

## <a name="using-the-debugger"></a>Usando o depurador

Para iniciar a depuração de qualquer aplicativo, sempre verifique se a configuração está definida como **Depurar**. A configuração de depuração fornece um conjunto de ferramentas útil para dar suporte à depuração, como pontos de interrupção, uso de visualizadores de dados e exibição da pilha de chamadas:

![Configuração de depuração](media/debugging-image_0.png)

## <a name="setting-a-breakpoint"></a>Configurando um ponto de interrupção

Para definir um ponto de interrupção no IDE, clique na área de margem do editor ao lado do número de linha do código que você deseja interromper:

![Configurando o ponto de interrupção na margem](media/debugging-image0.png)

Você pode exibir todos os pontos de interrupção definidos em seu código indo para o **painel de Pontos de Interrupção**:

![Lista de pontos de interrupção](media/debugging-image0a.png)

## <a name="start-debugging"></a>Iniciar a depuração

Para iniciar a depuração, selecione o dispositivo de destino ou um dispositivo semelhante/emulador no IDE:

![Selecione o dispositivo de destino](media/debugging-image1.png)

Em seguida, implante seu aplicativo pressionando o botão **Executar** ou **Cmd + Enter**. Quando você atingir um ponto de interrupção, o código será realçado em amarelo:

![Realce que mostra que o ponto de interrupção foi atingido](media/debugging-image2.png)

Ferramentas de depuração, como aquela usada para inspecionar os valores de objetos, podem ser usadas neste ponto para obter mais informações sobre o que está acontecendo em seu código:

![Visualizações de depuração](media/debugging-image3.png)

## <a name="conditional-breakpoints"></a>Pontos de interrupção condicionais

Você também pode definir as regras que regem as circunstâncias nas quais um ponto de interrupção deverá ocorrer, o que é conhecido como adicionar um *ponto de interrupção condicional*. Para definir um ponto de interrupção condicional, acesse a **janela Propriedades do Ponto de Interrupção**, o que pode ser feito de duas maneiras:

* Para adicionar um novo ponto de interrupção condicional, clique com o botão direito do mouse na margem do editor, à esquerda do número de linha para o código para o qual deseja definir um ponto de interrupção e selecione o novo ponto de interrupção:

 ![Menu de contexto do ponto de interrupção](media/debugging-image4.png)

* Para adicionar uma condição a um ponto de interrupção existente, clique com o botão direito do mouse no ponto de interrupção e selecione **Propriedades de ponto de interrupção** ou, no **Painel de pontos de interrupção**, selecione o botão Editar ponto de interrupção ilustrado abaixo:

 ![Editar o ponto de interrupção existente no painel de pontos de interrupção](media/debugging-image5.png)

Você poderá então inserir a condição na qual você deseja que o ponto de interrupção ocorra:

 ![Editar condições de ponto de interrupção](media/debugging-image6.png)

## <a name="stepping-through-code"></a>Executando o código em etapas

Quando um ponto de interrupção for atingido, as Ferramentas de depuração permitirão assumir o controle da execução do programa. O Visual Studio para Mac exibirá quatro botões, permitindo que você execute e percorra o código. No Visual Studio para Mac, eles terão a seguinte aparência:

 ![Botões para percorrer o código](media/debugging-image7.png)

Esses são os quatro botões:

*   **Executar** – Inicia a execução do código até o próximo ponto de interrupção.
*   **Sobrepor** – Executa a próxima linha de código. Se a próxima linha for uma chamada de função, Sobrepor executará a função e parará na próxima linha de código *depois* da função.
*   **Intervir** – Também executa a próxima linha de código. Se a próxima linha é uma chamada de função, Intervir parará na primeira linha da função, permitindo que você continue a depuração da função linha a linha. Se a próxima linha não for uma função, ela se comportará como Passar.
*   **Sair** – Retorna para a linha na qual a função atual foi chamada.

## <a name="debugging-monos-class-libraries"></a>Depuração de bibliotecas de classes Mono

Os produtos Xamarin são fornecidos com o código-fonte para bibliotecas de classes Mono e você pode usar essa etapa única do depurador para inspecionar como tudo está funcionando nos bastidores.

Como esse recurso consome mais memória durante a depuração, ele fica desligado por padrão.

Para habilitar esse recurso, navegue para **Visual Studio para Mac > Preferências > Depurador** e verifique se a opção “**Depurar somente o código do projeto, não intervir no código da estrutura.**” está **desmarcada**, como ilustrado abaixo:

![Opção Não intervir no código da estrutura](media/debugging-image8.png)

## <a name="see-also"></a>Consulte também

- [Depurando no Visual Studio (no Windows)](/visualstudio/debugger/)