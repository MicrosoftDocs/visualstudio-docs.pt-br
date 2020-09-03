---
title: Designer de Sombreador
ms.date: 09/21/2018
ms.topic: conceptual
f1_keywords:
- vs.graphics.designer.effectdesigner
- vs.graphics.shaderdesigner
ms.assetid: 5db09a16-b82c-4ba3-8ec9-630cdc109397
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 85ce7b0f270f0da8728b17610a683dcc17d06189
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "75589923"
---
# <a name="shader-designer"></a>Designer de Sombreador

Este documento descreve como trabalhar com o **Designer de Sombreador** do Visual Studio para criar, modificar e exportar efeitos visuais personalizados conhecidos como *sombreadores*.

Você poderá usar o **Designer de Sombreador** para criar efeitos visuais personalizados para seu jogo ou aplicativo, mesmo se não souber programação HLSL ou linguagem de sombreador de alto nível. Para criar um sombreador em **Designer de sombreador**, você organiza o layout como um gráfico. Ou seja, você adiciona *nós* que representam dados e operações à superfície de design e, em seguida, faz conexões entre eles para definir como as operações processam os dados. Em cada nó de operação, uma visualização do efeito até esse ponto é fornecida para que você possa visualizar seu resultado. Os dados fluem através de nós para um nó final que representa a saída do sombreador.

## <a name="supported-formats"></a>Formatos com suporte

O **Designer de sombreador** dá suporte a estes formatos de sombreador:

|Nome do formato|Extensão do arquivo|Operações com suporte (Exibir, Editar, Exportar)|
|-----------------| - | - |
|Idioma do Sombreador de Gráfico Direcionado|*.dgsl*|Exibir, Editar|
|Sombreador HLSL (código-fonte)|*.hlsl*|Exportação|
|Sombreador HLSL (código de bytes)|*.cso*|Exportação|
|Cabeçalho C++ (matriz de código de bytes HLSL)|*. h*|Exportação|

## <a name="get-started"></a>Introdução

Esta seção descreve como adicionar um sombreador DGSL ao seu projeto do Visual Studio C++ e fornece informações básicas para ajudá-lo a começar.

> [!NOTE]
> A integração de compilação automática de itens gráficos, como gráficos do sombreador (arquivos .dgsl) tem suporte apenas para projetos em C++.

### <a name="to-add-a-dgsl-shader-to-your-project"></a>Para adicionar um sombreador DGSL ao seu projeto

1. Verifique se você tem o componente necessário do Visual Studio instalado para trabalhar com gráficos. O componente é chamado de **Editores de imagens e modelos 3D**.

   Para instalá-lo, abra instalador do Visual Studio selecionando **ferramentas**  >  **obter ferramentas e recursos** na barra de menus e, em seguida, selecione a guia **componentes individuais** . Selecione o componente **imagem e editores de modelo 3D** na categoria **jogos e gráficos** e, em seguida, selecione **Modificar**.

   ![Componente Editores de imagens e modelos 3D](media/image-3d-model-editors-component.png)

2. No **Gerenciador de Soluções**, abra o menu de atalho do projeto do C++ ao qual deseja adicionar o sombreador e escolha **Adicionar** > **Novo Item**.

3. Na caixa de diálogo **Adicionar Novo Item**, em **Instalado**, selecione **Gráficos** e **Visual Shader Graph (.dgsl)**.

   > [!NOTE]
   > Se a categoria **Elementos Gráficos** não aparece na caixa de diálogo **Adicionar Novo Item** e você tem o componente **Editores de imagens e modelos 3D** instalado, não há suporte para os itens de gráficos desse tipo de projeto.

4. Especifique o **Nome** do arquivo de modelo e a **Localização** em que deseja que ele seja criado.

5. Clique no botão **Adicionar**.

### <a name="the-default-shader"></a>O sombreador padrão

Cada vez que você criar um sombreador DGSL, ele começará como um sombreador mínimo com apenas um nó de **Cor de Ponto** conectado ao nó **Cor Final**. Embora esse sombreador seja completo e funcional, ele não faz muita coisa. Portanto, a primeira etapa na criação de um sombreador de trabalho geralmente é excluir o nó **Cor de Ponto** ou desconectá-lo do nó **Cor Final** para liberar espaço para outros nós.

## <a name="work-with-the-shader-designer"></a>Trabalhar com o Designer de Sombreador

As seções a seguir descrevem como usar o Designer de Sombreador para trabalhar com sombreadores personalizados.

### <a name="shader-designer-toolbars"></a>Barras de ferramentas do Designer de sombreador

As barras de ferramentas do Designer de Sombreador contêm comandos que ajudam a trabalhar com grafos de sombreador DGSL.

Os comandos que afetam o estado do Designer de Sombreador estão localizados na barra de ferramentas **Modo do Designer de Sombreador** na janela principal do Visual Studio. Ferramentas de design e comandos estão localizados na barra de ferramentas **Designer de Sombreador** na superfície de design do Designer de Sombreador.

Aqui está a barra de ferramentas **Modo de Designer de Sombreador**:

![A barra de ferramentas modal do Designer de Sombreador.](../designers/media/digit-dsd-modal-toolbar.png)

Esta tabela descreve os itens na barra de ferramentas **Modo do Designer de Sombreador**, que são listados na ordem em que aparecem, da esquerda para a direita:

|Item da barra de ferramentas|Descrição|
|------------------|-----------------|
|**Selecionar**|Habilita a interação com nós e bordas no grafo. Nesse modo você pode selecionar nós e movê-los ou excluí-los, além de poder estabelecer bordas ou dividi-las.|
|**Panorâmica**|Habilita a movimentação de um grafo de sombreador em relação ao quadro de janela. Para deslocar, selecione um ponto na superfície de design e movimente-o ao redor.<br /><br /> No modo de **seleção** , você pode pressionar e manter a **tecla CTRL** para ativar o modo **panorâmico** temporariamente.|
|**Zoom**|Habilita a exibição de mais ou menos detalhes do grafo de sombreador em relação ao quadro de janela. No modo **Zoom**, selecione um ponto na superfície de design e mova-o para a direita ou para baixo para ampliar ou então para a esquerda ou para cima para reduzir.<br /><br /> No modo de **seleção** , você pode pressionar e manter a **tecla CTRL** para ampliar ou reduzir usando a roda do mouse.|
|**Ajustar zoom**|Exibe o grafo de sombreador completo no quadro de janela.|
|**Modo de Renderização em Tempo Real**|Quando a renderização em tempo real for habilitada, o Visual Studio redesenhará a superfície de design, mesmo quando nenhuma ação de usuário for executada. Esse modo é útil quando você trabalha com sombreadores que se alteram ao longo do tempo.|
|**Visualizar com esfera**|Quando habilitado, um modelo de uma esfera é usado para visualizar o sombreador. Só é possível habilitar uma forma de visualização por vez.|
|**Visualizar com cubo**|Quando habilitado, um modelo de um cubo é usado para visualizar o sombreador. Só é possível habilitar uma forma de visualização por vez.|
|**Visualizar com cilindro**|Quando habilitado, um modelo de um cilindro é usado para visualizar o sombreador. Só é possível habilitar uma forma de visualização por vez.|
|**Visualizar com cone**|Quando habilitado, um modelo de um cone é usado para visualizar o sombreador. Só é possível habilitar uma forma de visualização por vez.|
|**Visualizar com bule**|Quando habilitado, um modelo de um bule é usado para visualizar o sombreador. Só é possível habilitar uma forma de visualização por vez.|
|**Visualizar com plano**|Quando habilitado, um modelo de um plano é usado para visualizar o sombreador. Só é possível habilitar uma forma de visualização por vez.|
|**Caixa de Ferramentas**|De modo alternado, mostra ou oculta a **Caixa de Ferramentas**.|
|**Propriedades**|De modo alternado, mostra ou oculta a janela **Propriedades**.|
|**Avançado**|Contém comandos e opções avançados.<br /><br /> **Exportar**: permite a exportação de um sombreador em vários formatos.<br /><br /> **Exportar Como**: exporta o sombreador como o código-fonte HLSL ou código de bytes do sombreador compilado. Para obter mais informações sobre como exportar sombreadores, consulte [como exportar um sombreador](../designers/how-to-export-a-shader.md).<br /><br /> **Mecanismos Gráficos**: permite a seleção do renderizador que é usado para exibir a superfície de design.<br /><br /> **Renderizar com D3D11**: usa o Direct3D 11 para renderizar a superfície de design do Designer de Sombreador.<br /><br /> **Renderizar com D3D11WARP**: usa a WARP (Direct3D 11 Windows Advanced Rasterization Platform) para renderizar a superfície de design do Designer de Sombreador.<br /><br /> **Exibir**: permite a seleção de informações adicionais sobre o Designer de Sombreador.<br /><br /> **Taxa de Quadros**: quando habilitada, exibe a taxa de quadros no canto superior direito da superfície de design. A taxa de quadros é o número de quadros desenhados por segundo. Essa opção é útil quando você habilita a opção **Modo de Renderização em Tempo Real**.|

> [!TIP]
> Você pode escolher o botão **Avançado** para executar novamente o último comando.

### <a name="work-with-nodes-and-connections"></a>Trabalhar com nós e conexões

Use o modo **Selecionar** para adicionar, remover, reposicionar, conectar e configurar nós. Eis como executar essas operações básicas:

#### <a name="to-perform-basic-operations-in-select-mode"></a>Para executar operações básicas no modo Selecionar

- Este é o procedimento:

  - Para adicionar um nó ao grafo, selecione-o na **Caixa de Ferramentas** e mova-o para a superfície de design.

  - Para remover um nó do grafo, selecione-o e pressione **excluir**.

  - Para reposicionar um nó, selecione-o e, em seguida, mova-o para um novo local.

  - Para conectar dois nós, mova um terminal de saída de um nó para um terminal de entrada do outro nó. Somente terminais de tipos compatíveis podem ser conectados. Uma linha entre os terminais mostra a conexão.

  - Para remover uma conexão, no menu de atalho para qualquer um dos terminais conectados, escolha **Quebrar Links**.

  - Para configurar as propriedades de um nó, selecione o nó e, em seguida, na janela **Propriedades**, especifique novos valores para as propriedades.

### <a name="preview-shaders"></a>Visualizar sombreadores

Para ajudá-lo a entender como um sombreador aparecerá em seu aplicativo, você pode configurar como seu efeito é visualizado. Para aproximar o seu aplicativo, você pode escolher uma das várias formas para renderizar, configurar texturas e outros parâmetros de material, habilitar animação dos efeitos com base em tempo e examinar a visualização de ângulos diferentes.

#### <a name="shapes"></a>Formas

O Designer de Sombreador inclui seis formas – uma esfera, um cubo, um cilindro, um cone, um bule e um plano – que você pode usar para visualizar o sombreador. Dependendo do sombreador, determinadas formas podem fornecer uma melhor visualização.

Para escolher uma forma de visualização, na barra de ferramentas **Modos do Designer de Sombreador**, escolha a forma que você deseja.

#### <a name="textures-and-material-parameters"></a>Parâmetros de materiais e texturas

Muitos sombreadores contam com texturas e propriedades de material para produzir uma aparência exclusiva para cada tipo de objeto em seu aplicativo. Para ver a aparência que seu sombreador terá em seu aplicativo, você pode definir as texturas e propriedades de material que são usadas para renderizar a visualização para corresponder às texturas e parâmetros que você deseja usar em seu aplicativo.

Para associar uma textura diferente a um registro de textura ou modificar outros parâmetros de material:

1. No modo **Selecionar**, selecione uma área vazia da superfície de design. Isso faz com que a janela **Propriedades** exiba as propriedades globais do sombreador.

2. Na janela **Propriedades**, especifique novos valores para as propriedades de textura e de parâmetro que você deseja alterar.

A tabela a seguir mostra os parâmetros de sombreador que você pode modificar:

|Parâmetro|Propriedades|
|---------------|----------------|
|**Textura 1**  -  **Textura 8**|**Acesso**:                             **público** para permitir que a propriedade seja definida no editor de modelo; caso contrário, **privado**.<br /><br /> **Filename**: o caminho completo do arquivo de textura que está associado com o registro de textura.|
|**Material Ambiente**|**Acesso**:                             **público** para permitir que a propriedade seja definida no editor de modelo; caso contrário, **privado**.<br /><br /> **Valor**: a cor difusa do pixel atual devido à iluminação indireta ou de ambiente.|
|**Material Difuso**|**Access**: **Public** para permitir que esta propriedade possa ser configurada pelo Editor de Modelo; caso contrário, **Private**.<br /><br /> **Valor**: uma cor que descreve como o pixel atual difunde a iluminação direta.|
|**Material Emissivo**|**Acesso**:                              **público** para permitir que a propriedade seja definida no editor de modelo; caso contrário, **privado**.<br /><br /> **Valor**: a contribuição de cor do pixel atual é devido à iluminação própria.|
|**Material Especular**|**Acesso**:                              **público** para permitir que a propriedade seja definida no editor de modelo; caso contrário, **privado**.<br /><br /> **Valor**: uma cor que descreve como o pixel atual reflete a iluminação direta.|
|**Material Energia Especular**|**Acesso**:                             **público** para permitir que a propriedade seja definida no editor de modelo; caso contrário, **privado**.<br /><br /> **Valor**: o expoente que define a intensidade dos realces especulares no pixel atual.|

#### <a name="time-based-effects"></a>Efeitos de tempo

Alguns sombreadores têm um componente baseado em tempo que anima o efeito. Para mostrar qual a aparência do efeito em ação, a visualização tem que ser atualizada várias vezes por segundo. Por padrão, a visualização só é atualizada quando o sombreador é alterado; para alterar esse comportamento para que você possa exibir efeitos baseados em tempo, você precisa habilitar a renderização em tempo real.

Para habilitar a renderização em tempo real, na barra de ferramentas do Designer de Sombreador, escolha **Renderização em Tempo Real**.

#### <a name="examine-the-effect"></a>Examinar o efeito

Muitos sombreadores são afetados por variáveis como ângulo de exibição ou luz direcional. Para examinar como o efeito responde às alterações nessas variáveis, você pode girar a forma de visualização livremente e observar como o sombreador se comporta.

Para girar a forma, pressione e mantenha pressionada a tecla **Alt** e, em seguida, selecione qualquer ponto na superfície de design e mova-o.

### <a name="export-shaders"></a>Exportar sombreadores

Antes de usar um sombreador em seu aplicativo, você precisa exportá-lo em um formato compatível com o DirectX.

Você pode exportar sombreadores como código-fonte HLSL ou código de bytes do sombreador compilado. O código-fonte HLSL é exportado para um arquivo de texto que tem uma extensão de nome de arquivo *. HLSL* . O código de bytes do sombreador pode ser exportado para um arquivo binário bruto que tem uma extensão de nome de arquivo *. CSO* ou para um arquivo de cabeçalho (*. h*) do C++ que codifica o código de bytes do sombreador em uma matriz.

Para obter mais informações sobre como exportar sombreadores, consulte [como exportar um sombreador](../designers/how-to-export-a-shader.md).

## <a name="keyboard-shortcuts"></a>Atalhos do teclado

|Comando|Atalhos do teclado|
|-------------| - |
|Mudar para o modo **Selecionar**|**Ctrl** + **G**, **Ctrl** + **Q**<br /><br /> **S**|
|Mudar para o modo **Zoom**|**Ctrl** + **G**, **Ctrl** + **Z**<br /><br /> **Z**|
|Mudar para o modo **Panorâmico**|**Ctrl** + **G**, **Ctrl** + **P**<br /><br /> **K**|
|Selecionar tudo|**Ctrl** + **Um**|
|Excluir a seleção atual|**Delete (excluir)**|
|Cancelar a seleção atual|**Escape** (**Esc**)|
|Ampliar|**Ctrl** + **Avanço da roda do mouse**<br /><br /> Sinal de adição ( **+** )|
|Reduzir|**Ctrl** + **Rolagem do mouse para trás**<br /><br /> Sinal de subtração ( **-** )|
|Deslocar para cima na superfície de design|**Botão de rolagem do mouse para trás**<br /><br /> **PageDown**|
|Deslocar para baixo na superfície de design|**Botão de rolagem do mouse para frente**<br /><br /> **PageUp**|
|Deslocar para a esquerda na superfície de design|**Shift** + **Rolagem do mouse para trás**<br /><br /> **Botão de rolagem do mouse para a esquerda**<br /><br /> **Shift** + **PageDown**|
|Deslocar para a direita na superfície de design|**Shift** + **Avanço da roda do mouse**<br /><br /> **Botão de rolagem do mouse para a direita**<br /><br /> **Shift** + **PageUp**|
|Mover o foco do teclado para outro nó|As teclas de **direção**|
|Selecione o nó que tem o foco do teclado (adiciona o nó para o grupo de seleção)|**Shift** + **Barra de espaços**|
|Ativar/desativar a seleção do nó que tem o foco do teclado|**Ctrl** + **Barra de espaços**|
|Ativar/desativar a seleção atual (se nenhum nó estiver selecionado, selecione o nó que tem o foco do teclado)|**Barra de espaços**|
|Mover a seleção atual para cima|**Shift** + **Seta para cima**|
|Mover a seleção atual para baixo|**Shift** + **Seta para baixo**|
|Mover a seleção atual para a esquerda|**Shift** + **Seta para a esquerda**|
|Mover a seleção atual para a direita|**Shift** + **Seta para a direita**.|

## <a name="related-topics"></a>Tópicos relacionados

|Título|Descrição|
|-----------|-----------------|
|[Trabalhando com ativos 3D para jogos e aplicativos](../designers/working-with-3-d-assets-for-games-and-apps.md)|Fornece uma visão geral das ferramentas do Visual Studio que você pode usar para trabalhar com texturas e imagens, modelos 3D e efeitos de sombreamento.|
|[Editor de imagem](../designers/image-editor.md)|Descreve como usar o Editor de Imagens do Visual Studio para trabalhar com texturas e imagens.|
|[Editor de modelos](../designers/model-editor.md)|Descreve como usar o Editor de Modelos do Visual Studio para trabalhar com modelos 3D.|
