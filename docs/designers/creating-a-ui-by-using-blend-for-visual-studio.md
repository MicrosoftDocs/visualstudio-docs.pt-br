---
title: Criando uma interface de usuário usando o Blend para Visual Studio
ms.date: 07/17/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
f1_keywords:
- Blend.Start.Dev12
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0cd1d8ab718575977e9f65ed55bfc6c3185d1642
ms.sourcegitcommit: 522ba712c0d625e51352506146b0556414681964
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2018
ms.locfileid: "37890136"
---
# <a name="creating-a-ui-by-using-blend-for-visual-studio"></a>Criando uma interface de usuário usando o Blend para Visual Studio

O Blend for Visual Studio ajuda você a projetar aplicativos Web e Windows baseados em XAML. Ele fornece a mesma experiência básica de design XAML que o Visual Studio e adiciona designers visuais para tarefas avançadas, como animações e comportamentos. Para obter uma comparação entre o Blend e o Visual Studio, confira [Criar XAML no Visual Studio e no Blend para Visual Studio](../designers/designing-xaml-in-visual-studio.md).

Blend para Visual Studio é um componente do Visual Studio. Para instalar o Blend, no **Instalador do Visual Studio** escolha a carga de trabalho **desenvolvimento de Plataforma Universal do Windows** ou **desenvolvimento de área de trabalho do .NET**. As duas cargas de trabalho incluem o componente Blend para Visual Studio.

![Componentes da carga de trabalho UWP](media/installer-uwp.png)&nbsp;&nbsp;&nbsp;&nbsp;![Componentes da carga de trabalho de desenvolvimento de área de trabalho do .NET](media/installer-dotnet-desktop.png)

Se você estiver começando a usar o Blend for Visual Studio, reserve um tempo para familiarizar-se com os recursos exclusivos do espaço de trabalho. Este tópico apresenta um tour rápido.

> [!NOTE]
> Para fazer um tour pelos recursos de design compartilhados, como a prancheta, a janela **Estrutura de Tópicos do Documento** e a janela **Dispositivo**, confira [Criando uma interface do usuário usando o Designer XAML](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md).

## <a name="tour-of-the-tools-panel"></a>Tour pelo painel Ferramentas

É possível usar o painel **Ferramentas** no Blend for Visual Studio para criar e modificar objetos no aplicativo. Você cria os objetos selecionando uma ferramenta e desenhando na prancheta com o mouse.

![Painel Ferramentas](../designers/media/blend5toolspanel.png)

|||||
|-|-|-|-|
|![Ferramentas de seleção](../designers/media/b1_1.png)|**Ferramentas Seleção** Selecione objetos e demarcadores.<br /><br /> Use a ferramenta **Seleção Direta** para selecionar objetos aninhados e segmentos de caminho.|![Texto explicativo A](../designers/media/b5_label_a.png)|**Ferramentas gradiente e pincel**|
|![Ferramentas de exibição](../designers/media/b1_2.png)|**Ferramentas de exibição** Ajuste a prancheta, como para zoom e movimento panorâmico.|![Texto explicativo B](../designers/media/b5_label_b.png)|**Ferramentas de caminho**|
|![Ferramentas de pincel](../designers/media/b1_3.png)|**Ferramentas pincel** Trabalhe com os atributos visuais de um objeto, como transformar um pincel, pintar um objeto ou selecionar os atributos de um objeto para aplicação em outro objeto.|![Texto explicativo C](../designers/media/b5_label_c.png)|**Ferramentas Forma**|
|![Ferramentas de objeto](../designers/media/b1_4.png)|**Ferramentas de objeto** Desenhe os objetos mais comuns na prancheta, como demarcadores, formas, painéis de layout, texto e controles.|![Texto explicativo D](../designers/media/b5_label_d.png)|**Painéis de layout**|
|![Ferramentas de ativo](../designers/media/b1_5.png)|**Ferramentas de ativos** Acesse o painel **Ativos** e mostre o ativo usado mais recentemente na biblioteca.|![Texto explicativo E](../designers/media/b5_label_e.png)|**Controles de texto**|
|||![Texto explicativo F](../designers/media/b5_label_f.png)|**Controles comuns**|

**Assista a um vídeo curto:** ![Configure installed features](../designers/media/bldadminconsoleinitialconfigicon.png) [The Toolbar](https://www.youtube.com/watch?v=VkdUJcvoo54&list=PLBDF977B2F1DAB358&index=4) (Configurar recursos instalados, A barra de ferramentas).

## <a name="tour-of-the-assets-panel"></a>Tour pelo painel Ativos

É possível encontrar todos os controles no painel **Ativos**, semelhante à **Caixa de ferramentas** no Visual Studio. Além dos controles, você encontrará tudo o que pode adicionar à sua prancheta no painel **Ativos**, incluindo estilos, mídias, comportamentos e efeitos.

![Painel Ativos](../designers/media/blend5_assets_panel.png)

|||
|-|-|
|![](../designers/media/b1_1.png)|**Caixa de pesquisa** Digite na caixa **Pesquisar** para filtrar a lista de ativos.|
|![Modo de grade e modo de lista](../designers/media/b1_2.png)|**Modo de grade e Modo de lista** Mude entre as exibições **Modo de grade** e **Modo de lista** dos ativos.|
|![Categorias de ativos](../designers/media/b1_3.png)|**Categorias de ativos** Clique em uma categoria ou subcategoria para exibir a lista de ativos nessa categoria.|
|![Estilos](../designers/media/b1_4.png)|**Estilos** Mostre todos os estilos contidos no dicionário de recursos.|
|![Descrição](../designers/media/b1_5.png)|**Descrição** Exiba uma descrição da categoria ou subcategoria de ativos selecionada.|

## <a name="tour-of-the-objects-and-timeline-panel"></a>Tour pelo painel Objetos e Linha do Tempo

Use esse painel para organizar os objetos na prancheta e, se quiser, para animá-los.

![Painel Objeto e Linha do Tempo no modo de animação](../designers/media/b5_object_timeline_animation.png)

|||
|-|-|
|![Modo de exibição de objetos](../designers/media/b1_1.png)|**Exibição Objetos** Exiba uma árvore visual de um documento. É possível fazer uma busca detalhada em vários níveis de detalhamento. Você também pode adicionar camadas para organizar ainda mais os objetos na prancheta. Dessa forma, é possível bloqueá-los e ocultá-los como um grupo.|
|![Indicador de modo de registro](../designers/media/b1_2.png)|**Indicador do modo de registro** Veja se você está gravando as alterações de propriedade em uma linha do tempo.|
|![Seletor de storyboard](../designers/media/b1_3.png)|**Seletor de storyboard** Exiba uma lista dos storyboards criados.|
|![Fechar storyboard](../designers/media/b1_4.png)|**Fechar storyboard** Feche o storyboard atual.|
|![Opções do storyboard](../designers/media/b1_5.png)|**Opções de storyboard** Crie, duplique, inverta, exclua, renomeie ou feche um storyboard.|
|![Controles de reprodução](../designers/media/b1_6.png)|**Controles de reprodução** Navegue pela linha do tempo. Também é possível arrastar o playhead para navegar pela linha do tempo (ou *remover*).|
|![{1&gt;Retornar escopo a&lt;1}](../designers/media/b1_7.png)|**Retornar escopo para** Defina o escopo da exibição Objetos de volta ao objeto raiz anterior ou ao escopo anterior. Você poderá fazer isso somente quando estiver modificando um estilo ou um modelo.|
|![Registrar um quadro chave](../designers/media/b1_8.png)|**Registrar um quadro chave** Registre um instantâneo das propriedades do objeto selecionado no ponto no tempo atual.|
|![Opções de ajuste](../designers/media/b1_9.png)|**Opções de ajuste** Defina o ajuste da linha do tempo, a resolução de ajuste e desligue o ajuste da linha do tempo.|
|![Mostrar ocultar bloquear desbloquear](../designers/media/97fa60b9-0caf-4387-9225-b57510d32209.png)|**Mostrar/ocultar**, **Bloquear/desbloquear** Mostre ou oculte opções de visibilidade e bloqueio para a exibição Objetos.|
|![Posição do playhead na linha do tempo](../designers/media/b1_11.png)|**Posição do playhead na linha do tempo** Mostre o tempo atual em milissegundos. Você também pode inserir um valor de tempo diretamente nesse campo para saltar até um ponto no tempo específico. A precisão depende da resolução de ajuste definida nas **Opções de Ajuste**.|
|![Playhead](../designers/media/b1_12.png)|**Playhead** Determine em qual ponto no tempo a animação está. É possível arrastar o playhead na linha do tempo para visualizar a animação.|
|![Quadros chave definidos em linhas do tempo](../designers/media/b1_13.png)|**Quadros chave definidos em linhas do tempo** Altere um valor da propriedade em um ponto no tempo específico.|
|![Alterar a ordem dos objetos](../designers/media/d839d12c-07a1-4127-a830-4a8e7069f4fe.png)|**Alterar a ordem dos objetos** Defina a ordem de exibição dos objetos. Clique neste botão para organizar os objetos na exibição de estrutura pela ordem Z (de frente para trás) ou pela ordem de marcação (a ordem na qual eles aparecem na exibição **XAML**).|
|![Zoom da linha do tempo](../designers/media/b1_15.png)|**Zoom da linha do tempo** Defina a resolução de zoom da linha do tempo. Aumentar o zoom permite editar uma animação com mais detalhes e diminuir o zoom mostra mais uma visão geral do que está acontecendo no decorrer de períodos de tempo mais longos. Se você aumentar o zoom, mas não conseguir definir um quadro chave na posição de tempo desejada, verifique se a resolução de ajuste está definida com um valor suficientemente alto.|
|![Texto explicativo 16](../designers/media/b5_label_16.png)|**Área de composição da linha do tempo** Exiba a linha do tempo e mova quadros chave arrastando-os ou usando os menus de atalho.|

## <a name="tour-of-the-properties-panel"></a>Tour pelo painel Propriedades

Use esse painel para exibir e modificar as propriedades de um objeto. Você também pode defini-las diretamente na prancheta. Nesse caso, as alterações na propriedade serão refletidas no painel **Propriedades**.

![Painel Propriedades](../designers/media/blend5_properties_panel.png)

**Categorias** Expanda e recolha categorias de propriedades. Clique em **Expandir** ![Expandir](../designers/media/6375953d-074c-421a-bbb3-6f5055b67b64.png) e em **Recolher** ![Recolher](../designers/media/b5_collapse_button.png) para mostrar ou ocultar detalhes da categoria.

|||
|-|-|
|![Nome e tipo](../designers/media/b1_1.png)|**Nome e Tipo** Exiba o ícone, o nome e o tipo do objeto selecionado.|
|![Organizar por](../designers/media/b1_2.png)|**Organizar por** Organize as propriedades em ordem alfabética por nome, origem ou categoria.|
|![Propriedades do pincel](../designers/media/b1_3.png)|**Propriedades do pincel** Defina as propriedades visuais de pincéis, como pincel de Preenchimento, pincel de Traço e pincel de Primeiro Plano.|
|![Editor de cores](../designers/media/b1_4.png)|**Editor de cor** Use para cor sólida e pincéis de gradiente.|
|![Seletor de cor](../designers/media/b1_5.png)|**Seletor de cor** Selecione uma cor.|
|![Chips de cor](../designers/media/b1_6.png)|**Chips de cor** Exiba a cor inicial, a cor atual e a última cor|
|![Conta-gotas](../designers/media/b1_7.png)|**Conta-gotas** Use a cor de qualquer elemento na tela. O **Conta-gotas de cor** fica disponível quando o **Pincel de cor sólida** é selecionado. O **Conta-gotas de gradiente** fica disponível quando o **Pincel de gradiente** é selecionado.|
|![Propriedades e eventos](../designers/media/b1_8.png)|**Propriedades e Eventos** Defina as propriedades ou escolha os eventos de um elemento selecionado.|
|![Caixa de pesquisa](../designers/media/b1_9.png)|**Caixa de pesquisa** Pesquise propriedades. Filtre as propriedades exibidas digitando na caixa **Pesquisar**.|
|![Guias do editor de pincel](../designers/media/97fa60b9-0caf-4387-9225-b57510d32209.png)|**Guias do editor de pincel** Use-as para selecionar um editor de pincel. Você pode escolher **Sem pincel**, **Pincel de cor sólida**, **Pincel de gradiente**, **Pincel de bloco** ou **Recurso pincel**.|
|![Recurso de cor](../designers/media/b1_11.png)|**Recursos de cor** Aplique exatamente a mesma cor a propriedades diferentes. A guia **Recursos de Cor** inclui **Recursos Locais** e **Recursos do Sistema**.|
|![Espaço de cores RGB](../designers/media/b1_12.png)|**Espaço de cores RGB** Modifique a cor ajustando os valores para os editores de número **R**, **G** ou **B** (vermelho, verde, azul).|
|![Canal alfa](../designers/media/b1_13.png)|**Canal alfa** Modifique o valor Alfa usando o editor de número ao lado de **A**.|
|![Converter cor em recurso](../designers/media/d839d12c-07a1-4127-a830-4a8e7069f4fe.png)|**Converter cor em recurso** Converta a cor selecionada em um recurso de cor. Os recursos de cor ficam disponíveis ao clicar na guia Recursos de cor.|
|![](../designers/media/b1_15.png)|**Valor hexadecimal** Exibe o valor hexadecimal da cor exibida.|
|![Texto explicativo 16](../designers/media/b5_label_16.png)|**Controle deslizante de gradiente** É exibido somente se um pincel de gradiente é selecionado.|
|![Propriedades avançadas de apresentação](../designers/media/d50027a1-6824-4ad8-8b4e-558b0756dcf8.png)|**Mostrar propriedades avançadas** Exiba categorias das propriedades menos usadas.|

**Assista a um vídeo curto:** ![Configure installed features](../designers/media/bldadminconsoleinitialconfigicon.png) [Properties panel](https://www.youtube.com/watch?v=HCqQfiobdag&list=PLBDF977B2F1DAB358&index=7) (Configurar recursos instalados, Painel Propriedades).

## <a name="see-also"></a>Consulte também

- [Inserir controles e modificar seu comportamento](../designers/insert-controls-and-modify-their-behavior-in-xaml-designer.md)
- [Animar objetos](../designers/animate-objects-in-xaml-designer.md)
- [Desenhar formas e demarcadores](../designers/draw-shapes-and-paths.md)
- [Criando o XAML no Visual Studio e no Blend for Visual Studio](../designers/designing-xaml-in-visual-studio.md)
