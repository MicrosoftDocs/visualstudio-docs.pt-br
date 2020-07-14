---
title: Depurando com Visual Studio para Mac
description: A depuração é uma parte comum e necessária da programação. Como um IDE consolidado, o Visual Studio para Mac contém um pacote completo de recursos para facilitar a depuração. Desde depuração com segurança até a visualização de dados, este artigo explicará como usar todo o potencial de depuração no Visual Studio para Mac.
author: therealjohn
ms.author: johmil
ms.date: 5/13/2020
ms.technology: vs-ide-debug
ms.assetid: BB7A084D-9AC2-48B5-8076-6C8518796BBA
ms.topic: overview
ms.openlocfilehash: 09a761a8269fa40c3fab49a34b3e43a7f0ec63cd
ms.sourcegitcommit: 2ce59c2ffeba5ba7f628c2e6c75cba4731deef8a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85939074"
---
# <a name="debugging-with-visual-studio-for-mac"></a>Depurando com Visual Studio para Mac

Visual Studio para Mac tem depuradores com suporte para aplicativos .Net Core, .NET Framework, Unity e Xamarin.

O Visual Studio para Mac usa o [*Mono Soft Debugger*](https://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger/), que foi implementado no runtime Mono, permitindo que o Visual Studio para Mac depure código gerenciado em todas as plataformas.

## <a name="the-debugger"></a>O depurador

O Visual Studio para Mac usa o Mono Soft Debugger para depurar código gerenciado (C# ou F#) em todos os aplicativos Xamarin. O soft Debugger do Mono é diferente dos depuradores regulares, pois é um depurador cooperativo criado no tempo de execução do mono; o código gerado e o tempo de execução mono cooperam com o IDE para fornecer uma experiência de depuração. O runtime Mono expõe a funcionalidade de depuração por meio de um protocolo de transmissão, sobre o qual você pode conhecer mais [na documentação do Mono](https://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger-wire-format/).

Depuradores inflexíveis, como o [LLDB]( http://lldb.llvm.org/index.html) ou o [GDB]( https://www.gnu.org/software/gdb/), controlam um programa sem o conhecimento ou a cooperação do programa depurado, mas ainda podem ser úteis ao depurar aplicativos Xamarin caso você precise depurar código Android ou iOS nativo.

Para aplicativos .NET Core e ASP.NET Core, Visual Studio para Mac usa o depurador do .NET Core. Esse depurador também é um depurador cooperativo e funciona com o tempo de execução do .NET.

## <a name="using-the-debugger"></a>Usando o depurador

Para iniciar a depuração de qualquer aplicativo, sempre verifique se a configuração está definida como **Depurar**. A configuração de depuração fornece um conjunto de ferramentas útil para dar suporte à depuração, como pontos de interrupção, uso de visualizadores de dados e exibição da pilha de chamadas:

![Configuração de depuração](media/debugging-image_0.png)

## <a name="setting-a-breakpoint"></a>Definindo um ponto de interrupção

Para definir um ponto de interrupção no IDE, clique na área de margem do editor ao lado do número de linha do código que você deseja interromper:

![Configurando o ponto de interrupção na margem](media/debugging-image0.png)

Você pode exibir todos os pontos de interrupção definidos em seu código indo para o **painel de Pontos de Interrupção**:

![Lista de pontos de interrupção](media/debugging-image0a.png)

## <a name="start-debugging"></a>Iniciar a depuração

Para iniciar a depuração, selecione o navegador de destino, o dispositivo ou o simulador/emulador:

![Configuração de depuração ](media/debugging-image_0.png)
 ![ selecionar dispositivo de destino](media/debugging-image1.png)

Em seguida, implante seu aplicativo pressionando o botão **Executar** ou **Cmd + Enter**. Quando você atingir um ponto de interrupção, o código será realçado em amarelo:

![Realce que mostra que o ponto de interrupção foi atingido](media/debugging-image2.png)

Ferramentas de depuração, como aquela usada para inspecionar os valores de objetos, podem ser usadas neste ponto para obter mais informações sobre o que está acontecendo em seu código:

![Visualizações de depuração](media/debugging-image3.png)

## <a name="conditional-breakpoints"></a>Pontos de interrupção condicionais

Você também pode definir as regras que regem as circunstâncias nas quais um ponto de interrupção deverá ocorrer, o que é conhecido como adicionar um *ponto de interrupção condicional*.  Para definir um ponto de interrupção condicional, acesse a **janela Propriedades do Ponto de Interrupção**, o que pode ser feito de duas maneiras:

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

* **Executar** – Inicia a execução do código até o próximo ponto de interrupção.
* Passar **por cima** – isso executará a próxima linha de código. Se a próxima linha for uma chamada de função, passará a executar a função e será interrompido na próxima linha de código *após* a função.
* **Intervir** – Também executa a próxima linha de código. Se a próxima linha é uma chamada de função, Intervir parará na primeira linha da função, permitindo que você continue a depuração da função linha a linha. Se a próxima linha não for uma função, ela se comportará como Passar.
* **Sair** – Retorna para a linha na qual a função atual foi chamada.

## <a name="change-which-statement-is-executed-next"></a>Alterar qual instrução é executada em seguida

Enquanto o depurador está em pausa, uma seta na margem mostra qual linha de código será executada em seguida. Você pode clicar e arrastar a seta para outra linha de código para alterar a instrução que será executada. Você pode obter a mesma coisa também clicando com o botão direito do mouse em uma linha de código e selecionando **definir próxima instrução** no menu de contexto.

![Arraste e solte a seta para definir a próxima instrução](media/debugger-drag-setnextstatement.gif)

> [!CAUTION]
> A alteração da linha atual de execução pode causar um comportamento inesperado em um aplicativo. Também há algumas condições em que a alteração da próxima instrução a ser executada não é possível. Por exemplo, arrastar a seta de um método para outro método não funcionará. Nesses casos sem suporte, Visual Studio para Mac exibirá uma caixa de diálogo para que você saiba que não foi possível alterar a linha atual da execução. 

## <a name="debugging-monos-class-libraries"></a>Depuração de bibliotecas de classes Mono

Os produtos Xamarin são fornecidos com o código-fonte para bibliotecas de classes Mono e você pode usar essa etapa única do depurador para inspecionar como tudo está funcionando nos bastidores.

Como esse recurso consome mais memória durante a depuração, ele fica desligado por padrão.

Para habilitar esse recurso, navegue até **Visual Studio para Mac preferências de > > depurador** e verifique se a opção "**etapa em código externo**" está **selecionada**, conforme ilustrado abaixo:

![Opção entrar em código externo](media/debugging-image8.png)

## <a name="see-also"></a>Confira também

- [Depurando no Visual Studio (no Windows)](/visualstudio/debugger/)
