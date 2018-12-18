---
title: Organizar objetos em contêineres de layout no Designer XAML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 29c80c38-0fa3-48d6-b3a8-3b864f482e44
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: c92af4e78715c608fdee860690fd58561b8bb2d5
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49219544"
---
# <a name="organize-objects-into-layout-containers-in-xaml-designer"></a>Organizar objetos em contêineres de layout no XAML Designer
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Imagine o local em que você deseja que os objetos apareçam, tais como imagens, botões e vídeos. Talvez você queira que eles apareçam em linhas e colunas; em uma única linha, vertical ou horizontal; ou em posições fixas.  
  
 Após ter a chance de pensar sobre como a página pode ser exibida, escolha um painel de layout. Todas as páginas começam no painel de layout, porque você precisa de algo para adicionar seus objetos. Por padrão, é ele tem o formato de uma **Grade**, mas isso pode ser alterado.  
  
 Painéis de layout ajudam a organizar objetos em uma página, mas fazem mais do que isso. Eles ajudam a projetar diferentes tamanhos de tela e resoluções. Quando usuários executam um aplicativo, tudo o que está contido no painel de layout é redimensionado para caber na tela do dispositivo em uso. Claro, se você não quiser que isso aconteça com o layout, é possível substituir esse comportamento em uma parte ou na totalidade do layout. É possível usar propriedades de altura e largura para controlar isso.  
  
 Esta página descreve painéis de layout e controles e conduz a vídeos curtos que ajudarão a introduzi-los.  
  
> [!NOTE]
>  Alguns dos vídeos podem se referir ao Blend ou ao Expression Blend, que usam o mesmo Designer XAML do Visual Studio e do Blend for Visual Studio.  
  
## <a name="layout-panels"></a>Painéis de layout  
 Comece a página escolhendo um destes painéis de layout. A página pode ter mais de um. Por exemplo, é possível iniciar com um painel de layout em **Grade** e, em seguida, adicionar um **StackPanel** a uma área na **Grade** para organizar os controles verticalmente nesse elemento.  
  
 Os painéis de layout a seguir são os mais populares, mas existem outros. É possível encontrar todos no painel **Ativos**.  
  
-   [Grade](#Grid)  
  
-   [UniformGrid](#Uniform)  
  
-   [Tela](#Canvas)  
  
-   [StackPanel](#Stack)  
  
-   [WrapPanel](#Wrap)  
  
-   [DockPanel](#Dock)  
  
###  <a name="Grid"></a> Grade  
 Organize objetos em linhas e colunas.  
  
 ![](../designers/media/98b234b2-ac3b-441f-9136-98375fee87b7.png "98b234b2-ac3b-441f-9136-98375fee87b7")  
  
 **Assista a um breve vídeo:** ![Configurar Recursos Instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Usando Grades](http://www.popscreen.com/v/6A4hj/Microsoft-Expression-Blend-Using-Grids)  
  
###  <a name="Uniform"></a> UniformGrid  
 Organize objetos em regiões de grade iguais ou uniformes. Este painel é ótimo para organizar uma lista de imagens.  
  
 ![](../designers/media/928b9284-a7e8-4678-875a-656b80b78076.png "928b9284-a7e8-4678-875a-656b80b78076")  
  
 (Disponível somente para projetos WPF)  
  
 **Assista a um breve vídeo:** ![Configurar Recursos Instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Trabalhando com um UniformGrid](http://www.popscreen.com/v/6A4iq/Microsoft-Expression-Blend-Working-with-a-UniformGrid)  
  
###  <a name="Canvas"></a> Tela  
 Organize objetos como desejar. Quando os usuários executam o aplicativo, esses elementos terão posições fixas na tela.  
  
 ![](../designers/media/e1ae27f0-3a57-454e-b580-877dcea8836d.png "e1ae27f0-3a57-454e-b580-877dcea8836d")  
  
 **Assista a um breve vídeo:** ![Configurar Recursos Instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Trabalhando com a tela](http://www.popscreen.com/v/6A4hT/Microsoft-Expression-Blend-Working-with-the-Canvas)  
  
###  <a name="Stack"></a> StackPanel  
 Organize objetos em uma única linha horizontal ou vertical.  
  
 ![](../designers/media/a85a7b57-b0a8-495e-b985-f0291e41d093.png "a85a7b57-b0a8-495e-b985-f0291e41d093")  
  
 **Assista a um breve vídeo:** ![Configurar Recursos Instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Trabalhando com o StackPanel e WrapPanel](http://www.popscreen.com/v/6A4i5/Microsoft-Expression-Blend-Using-the-StackPanel-and-WrapPanel)  
  
###  <a name="Wrap"></a> WrapPanel  
 Organize objetos em sequência da esquerda para a direita. Quando o painel fica sem espaço na margem à direita, ele *encapsula* o conteúdo na próxima linha e assim por diante, da esquerda para a direita, de cima para baixo. A orientação de um painel de encapsulamento também pode ser vertical, para que os objetos sejam direcionados de cima para baixo e da esquerda para a direita.  
  
 (Disponível somente para projetos WPF)  
  
 ![](../designers/media/b1c415fb-9a32-4a18-aa0b-308fca994ac9.png "b1c415fb-9a32-4a18-aa0b-308fca994ac9")  
  
 **Assista a um breve vídeo:** ![Configurar Recursos Instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Trabalhando com o StackPanel e WrapPanel](http://www.popscreen.com/v/6A4i5/Microsoft-Expression-Blend-Using-the-StackPanel-and-WrapPanel)  
  
###  <a name="Dock"></a> DockPanel  
 Organize objetos para que eles fiquem ou se *encaixem*, em uma borda do painel.  
  
 (Disponível somente para projetos WPF)  
  
 ![](../designers/media/72d46b58-9a49-4dd5-8af7-6843c0440226.png "72d46b58-9a49-4dd5-8af7-6843c0440226")  
  
 **Assista a um breve vídeo:** ![Configurar Recursos Instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [WPF – DockPanel](https://www.youtube.com/watch?v=EBH_OIM-zPo)  
  
## <a name="layout-controls"></a>Controles de layout  
 Também é possível adicionar objetos aos controles de layout. Eles não têm tantos recursos como o painel de layout, mas podem ser úteis em determinados cenários.  
  
 Os controles de layout a seguir são os mais populares, mas existem outros. É possível encontrar todos no painel **Ativos**.  
  
-   [Borda](#Border)  
  
-   [Pop-up](#Popup)  
  
-   [ScrollViewer](#Scroll)  
  
-   [UniformGrid](#Uniform)  
  
-   [Caixa de Visualização](#View)  
  
###  <a name="Border"></a> Borda  
 Crie uma borda, uma tela de fundo ou ambos em torno de um objeto. É possível adicionar apenas um objeto a uma **Borda**. Caso deseje aplicar uma borda ou tela de fundo a mais de um objeto, adicione o painel de layout à **Borda**. Em seguida, adicione objetos a esse painel ou controle.  
  
 ![](../designers/media/e761238b-99fd-43c5-bbc4-57538b8289ff.png "e761238b-99fd-43c5-bbc4-57538b8289ff")  
  
 **Assista a um breve vídeo:** ![Configurar Recursos Instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Trabalhando com bordas](http://www.popscreen.com/v/6A4hB/Microsoft-Expression-Blend-Working-with-Borders)  
  
###  <a name="Popup"></a> Pop-up  
 Mostra informações ou opções para usuários em uma janela. É possível adicionar apenas um objeto a um **Pop-up**. Por padrão, um **Pop-up** contém uma **Grade**, mas isso pode ser alterado.  
  
###  <a name="Scroll"></a> ScrollViewer  
 Habilita o usuário a rolar para baixo uma página ou uma área dela. É possível adicionar apenas um objeto a um **ScrollViewer**, por isso, faz sentido adicionar um painel de layout como uma **Grade** ou **StackPanel**.  
  
 ![](../designers/media/06b326d4-f23d-41a6-b26b-e1aff37572a7.png "06b326d4-f23d-41a6-b26b-e1aff37572a7")  
  
###  <a name="View"></a> Caixa de Visualização  
 Dimensionar objetos, assim como um controle de zoom. É possível adicionar apenas um objeto a uma **Caixa de Visualização**. Caso deseje aplicar esse efeito a mais de um objeto, adicione um painel de layout à **Caixa de Visualização** e, em seguida, adicione os controles a esse painel de layout.  
  
 (Disponível somente para projetos WPF)  
  
 ![](../designers/media/f5b13c66-d918-4141-8a16-bd8f8628687a.png "f5b13c66-d918-4141-8a16-bd8f8628687a")  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com elementos no Designer XAML](../designers/working-with-elements-in-xaml-designer.md)   
 [Criando uma interface do usuário usando o Designer XAML](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)



