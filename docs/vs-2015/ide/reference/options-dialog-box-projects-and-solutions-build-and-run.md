---
title: Caixa de diálogo Opções, Projetos e Soluções, Compilar e Executar | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Projects.Build_and_Run
- VS.ToolsOptionsPag.Projects.Build_and_Run
helpviewer_keywords:
- builds [Visual Studio], setting up
- run actions
- debugger, run options
ms.assetid: c884976e-c0df-4c6d-8e3a-856ea2bd547c
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 9669437ff47bc141c898a61c055b3a0de8d5d235
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49189287"
---
# <a name="options-dialog-box--projects-and-solutions-build-and-run"></a>Caixa de diálogo Opções, Projetos e Soluções, Compilar e Executar
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Nesta caixa de diálogo, você pode especificar o número máximo de projetos do Visual C++ ou do Visual C# que podem ser compilados ao mesmo tempo, determinados comportamentos de build padrão e algumas configurações de log de build. Para abrir a caixa de diálogo **Opções**, escolha **Ferramentas**, **Opções** na barra de menus. Para acessar esse conjunto de opções, expanda **Projetos e Soluções** e, em seguida, escolha **Compilar e Executar**.  
  
## <a name="uielement-list"></a>Lista UIElement  
 **número máximo de compilações paralelas de projetos**  
 Especifica o número máximo de projetos do Visual C++ e do Visual C# que podem ser compilados ao mesmo tempo. Para otimizar o processo de build, o número máximo de compilações paralelas de projetos é automaticamente definido como o número de CPUs do seu computador. O máximo é de 32.  
  
 **Somente compilar dependências e projetos de inicialização ao Executar**  
 Somente o projeto de inicialização e suas dependências serão compilados se essa caixa de seleção estiver marcada quando você escolher a tecla F5; escolha **Depurar**, **Iniciar** na barra de menus; ou escolha **Build**, **Build** na barra de menus. Todos os projetos, dependências e arquivos de solução serão compilados se essa caixa de seleção estiver desmarcada quando você escolher a tecla F5; escolha **Depurar**, **Iniciar** na barra de menus; ou escolha **Build**, **Build** na barra de menus. Por padrão, essa opção está desmarcada.  
  
 **Ao Executar, quando os projetos estiverem desatualizados**  
 > [!NOTE]
>  Essa lista aplica-se somente a projetos [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)].  
  
 Por padrão, uma mensagem será exibida se uma configuração de projeto estiver desatualizada quando você escolher a tecla F5 ou escolher **Depurar**, **Iniciar** na barra de menus. Você pode especificar se deseja compilar o projeto mesmo assim e se mensagem será exibida. Use esta opção para especificar se a mensagem é exibida e qual deve ser o comportamento de build se a mensagem não for exibida.  
  
 **Sempre compilar**  
 A caixa de mensagem não aparece e o projeto é compilado, apesar da configuração desatualizada. Essa opção é definida quando você seleciona a caixa **Não mostrar esta caixa de diálogo novamente** na mensagem e, em seguida, escolhe o botão **Sim**.  
  
 **Nunca compilar**  
 A caixa de mensagem não aparece e o projeto não é compilado. Essa opção é definida quando você seleciona a caixa **Não mostrar esta caixa de diálogo novamente** na mensagem e, em seguida, escolhe o botão **Não**.  
  
 **Aviso para compilar**  
 Exibe a caixa de mensagem sempre que uma configuração de projeto está desatualizada.  
  
 **Ao Executar, quando ocorrerem erros de build ou implantação**  
 Se ocorrerem erros de build quando você inicia um build no menu **Build**, uma mensagem será exibida. Você pode especificar se deseja continuar iniciando o aplicativo e se a mensagem é exibida sempre que ocorrerem erros de build. Use esta opção para especificar se a mensagem é exibida e qual deve ser o comportamento se a mensagem não for exibida.  
  
> [!NOTE]
>  Essa opção aplica-se apenas a [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] projetos.  
  
 **Aviso para iniciar**  
 Exibe uma caixa de mensagem sempre que ocorrem erros de build.  
  
 **Não iniciar**  
 A caixa de mensagem não aparece e o aplicativo não é iniciado. Essa opção é definida quando você marca a caixa de seleção **Não mostrar esta caixa de diálogo novamente** na caixa de mensagem e, em seguida, escolhe o botão **Não**.  
  
 **Iniciar versão antiga**  
 A caixa de mensagem não aparece e a versão recém-compilada do aplicativo não é iniciada. Essa opção é definida quando você marca a caixa de seleção **Não mostrar esta caixa de diálogo novamente** na caixa de mensagem e, em seguida, escolhe o botão **Sim**.  
  
 **Para novas soluções, use o projeto selecionado atualmente como o projeto de inicialização**  
 Se essa caixa de seleção for selecionada, novas soluções usarão o projeto selecionado no momento como o projeto de inicialização.  
  
 **Detalhamento da saída de build do projeto no MSBuild**  
 Determina quanta informação aparece na Janela de **Saída** para o build.  
  
 **Detalhamento do arquivo de log de build do projeto no MSBuild**  
 > [!NOTE]
>  Essa opção se aplica somente a projetos do Visual C++.  
  
 Determina quanta informação é gravada no arquivo de log de build, que está localizado em \\...\\*ProjectName*\Debug\\*ProjectName*.log.  
  
## <a name="see-also"></a>Consulte também  
 [Compilando e criando](../../ide/compiling-and-building-in-visual-studio.md)



