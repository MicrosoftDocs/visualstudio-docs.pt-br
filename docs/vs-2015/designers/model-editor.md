---
title: Editor de Modelo | Microsoft Docs
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
- vs.graphics.designer.3dscene
- vs.graphics.modelviewer
ms.assetid: 5edf1a30-9307-43c3-9b8b-831217be0104
caps.latest.revision: 38
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 1e947793dff1f0068c1341ba6b70c21df07463f6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49844076"
---
# <a name="model-editor"></a>Editor de modelo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este documento descreve como trabalhar com o Editor de Modelos do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para exibir, criar e modificar modelos 3D.  
  
 Você pode usar o Editor de Modelos para criar modelos 3D do zero ou exibir e modificar modelos 3D mais complexos que foram criados usando as ferramentas de modelagem 3D com recursos completos. O Editor de Modelos oferece suporte a vários formatos de modelo 3D que são usados no desenvolvimento de aplicativos DirectX.  
  
## <a name="supported-formats"></a>Formatos com suporte  
 O Editor de Modelos oferece suporte os seguintes formatos de modelo:  
  
|Nome do formato|Extensão do arquivo|Operações com suporte (Exibir, Editar, Criar)|  
|-----------------|--------------------|-------------------------------------------------|  
|Arquivo de Intercâmbio AutoDesk FBX|.fbx|Exibir, Editar, Criar|  
|Arquivo Collada DAE|.dae|Exibir, Editar (Modificações em arquivos Collada DAE são salvas usando o formato FBX.)|  
|OBJ|.obj|Exibir, Editar (Modificações em arquivos OBJ são salvos usando o formato FBX.)|  
  
## <a name="getting-started"></a>Introdução  
 Esta seção descreve como adicionar um modelo 3D ao seu projeto do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e fornece informações básicas necessárias para você começar.  
  
#### <a name="to-add-a-3-d-model-to-your-project"></a>Para adicionar um modelo 3D ao projeto  
  
1.  No **Gerenciador de Soluções**, abra o menu de atalho do projeto ao qual você deseja adicionar a imagem e selecione **Adicionar**, **Novo Item**.  
  
2.  Na caixa de diálogo **Adicionar Novo Item**, em **Instalado**, selecione **Gráficos** e **Cena 3D (.fbx)**.  
  
3.  Especifique o **Nome** do arquivo de modelo e a **Localização** em que deseja que ele seja criado.  
  
4.  Escolha o botão **Adicionar**.  
  
### <a name="axis-orientation"></a>Orientação do eixo  
 O [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] oferece suporte a cada orientação do eixo 3D e carrega as informações da orientação do eixo dos formatos do arquivo de modelo que oferecem suporte a ele. Se nenhuma orientação de eixo for especificada, o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] usará o sistema de coordenadas da direita por padrão. O **indicador de eixo** mostra a orientação atual do eixo no canto inferior direito da superfície de design. No **indicador de eixo**, vermelho representa o eixo x, verde representa o eixo y e azul representa o eixo z.  
  
### <a name="beginning-your-3-d-model"></a>Iniciando o modelo 3D  
 No Editor de modelos, cada novo objeto sempre começa como uma das formas 3D básicas (ou *primitivos*) que são criadas no Editor de modelos. Para criar objetos novos e exclusivos, você adiciona um primitivo à cena e altera sua forma modificando seus vértices. Para formas complexas, você inclui vértices adicionais usando extrusão ou subdivisão e as modifica. Para obter informações sobre como adicionar um objeto primitivo à sua cena, consulte [Criando e Importando Objetos 3D](#Adding3DObjects). Para obter informações sobre como adicionar mais vértices a um objeto, consulte [Modificando Objetos](#ModifyingObjects).  
  
## <a name="working-with-the-model-editor"></a>Trabalho com o Editor de Modelos  
 As seções a seguir descrevem como usar o Editor de Modelos para trabalhar com modelos 3D.  
  
### <a name="model-editor-toolbars"></a>Barras de ferramentas do Editor de Modelos  
 As barras de ferramentas do Editor de Modelos contêm comandos que ajudam a trabalhar com modelos 3D.  
  
 Os comandos que afetam o estado do Editor de modelos estão localizados na barra de ferramentas **Modo do Editor de Modelos** na janela principal do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. As ferramentas de modelagem e os comandos em script estão localizados na barra de ferramentas **Editor de Modelos** na superfície de design do Editor de Modelos.  
  
 Esta é a barra de ferramentas **Modo do Editor de Modelos**:  
  
 ![A barra de ferramentas modal do Visualizador do Modelo.](../designers/media/digit-mre-modal-toolbar.png "Digit-MRE-Modal-Toolbar")  
  
 Esta tabela descreve os itens na barra de ferramentas **Modo do Editor de Modelos**, que são listados na ordem em que aparecem, da esquerda para a direita.  
  
|Item da barra de ferramentas|Descrição|  
|------------------|-----------------|  
|**Selecionar**|Permite a seleção de pontos, bordas, faces ou objetos na cena, dependendo do modo de seleção ativo.|  
|**Panorâmica**|Permite a movimentação de uma cena 3D em relação ao quadro da janela. Para obter uma panorâmica, selecione um ponto na cena e movimente-o ao redor.<br /><br /> No modo **Selecionar**, você pode manter pressionada a tecla Ctrl para ativar o modo **Panorâmico** temporariamente.|  
|**Zoom**|Permite a exibição de mais ou menos detalhes da cena em relação ao quadro da janela. No modo **Zoom**, selecione um ponto na cena e mova-o para a direita ou para baixo para ampliar ou para a esquerda ou para cima para reduzir.<br /><br /> No modo **Selecionar**, você pode ampliar ou reduzir usando a roda do mouse enquanto mantém a tecla Ctrl pressionada.|  
|**Órbita**|Posiciona a exibição em um caminho circular em volta do objeto selecionado. Se nenhum objeto for selecionado, o caminho será centralizado na origem da cena. **Nota:** esse modo não terá efeito quando a projeção **Ortográfica** estiver habilitada.|  
|**Local do mundo**|Quando esse item é habilitado, as transformações no objeto selecionado ocorrem no espaço do mundo. Caso contrário, as transformações no objeto selecionado ocorrem no espaço local.|  
|**Modo Dinâmico**|Quando esse item for habilitado, as transformações afetarão o local e a orientação do *ponto dinâmico* do objeto selecionado (O ponto dinâmico define o centro das operações de translação, dimensionamento e rotação.) Caso contrário, as transformações afetam o local e a orientação da geometria do objeto, em relação ao ponto dinâmico.|  
|**Bloquear eixo X**|Restringe a manipulação de objetos ao eixo x. Aplica-se apenas quando você usa a parte central do widget do manipulador.|  
|**Bloquear eixo Y**|Restringe a manipulação de objetos ao eixo y. Aplica-se apenas quando você usa a parte central do widget do manipulador.|  
|**Bloquear eixo Z**|Restringe a manipulação de objetos ao eixo z. Aplica-se apenas quando você usa a parte central do widget do manipulador.|  
|**Objeto de Quadro**|Enquadra o objeto selecionado para que ele se localize no centro da exibição.|  
|**Exibir**|Define a orientação da exibição. Veja as orientações disponíveis:<br /><br /> **Frente**<br /> Posiciona a exibição na frente da cena.<br /><br /> **Atrás**<br /> Posiciona a exibição atrás da cena.<br /><br /> **Esquerda**<br /> Posiciona a exibição à esquerda da cena.<br /><br /> **Direita**<br /> Posiciona a exibição à direita da cena.<br /><br /> **Superior**<br /> Posiciona a exibição acima da cena.<br /><br /> **Inferior**<br /> Posiciona a exibição abaixo da cena. **Nota:** essa é a única maneira de alterar a direção da exibição quando a projeção **Ortográfica** estiver habilitada.|  
|**Projeção**|Define o tipo de projeção que é usado para desenhar a cena. Veja as projeções disponíveis:<br /><br /> **Perspectiva**<br /> Na projeção de perspectiva, os objetos que estão mais longe do ponto de vista parecem menores em tamanho e, por fim, convergem para um ponto distante.<br /><br /> **Ortográfica**<br /> Na projeção Ortográfica, os objetos parecem ser do mesmo tamanho, independentemente da sua distância do ponto de vista. Nenhuma convergência é exibida. Quando a projeção **Ortográfica** estiver habilitada, não é possível usar o modo **Órbita** para posicionar a exibição.|  
|**Estilo de Desenho**|Define como os objetos da cena são renderizados. Veja os estilos disponíveis:<br /><br /> **Esboço**<br /> Quando habilitado, os objetos são renderizados como delineados.<br /><br /> **Exceder**<br /> Quando habilitado, os objetos são renderizados usando combinação aditiva. Você pode usar esse item para visualizar o excedente que existe no cenário.<br /><br /> **Sombra Simples**<br /> Quando habilitado, os objetos são renderizados usando um modelo de iluminação básico de sombra simples. Você pode usar esse item para ver as faces de um objeto com mais facilidade.<br /><br /> Se nenhuma dessas opções for habilitada, cada objeto será renderizado usando o material que é aplicado a ele.|  
|**Modo de Renderização em Tempo Real**|Quando a renderização em tempo real for habilitada, o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] redesenhará a superfície de design, mesmo quando nenhuma ação de usuário for executada. Esse modo é útil quando você trabalha com sombreadores que se alteram ao longo do tempo.|  
|**Ativar/Desativar Grade**|Quando esse item é habilitado, uma grade é exibida. Caso contrário, a grade não é exibida.|  
|**Caixa de Ferramentas**|De modo alternado, mostra ou oculta a **Caixa de Ferramentas**.|  
|**Estrutura de Tópicos do Documento**|De modo alternado, mostra ou oculta a janela **Estrutura de Tópicos de Documentos**.|  
|**Propriedades**|De modo alternado, mostra ou oculta a janela **Propriedades**.|  
|**Avançado**|Contém comandos e opções avançados.<br /><br /> **Mecanismos Gráficos**<br /><br /> **Renderizar com o D3D11**<br /> Usa o Direct3D 11 para renderizar a superfície de design do Editor de Modelos.<br /><br /> **Renderizar com o D3D11WARP**<br /> Usa o Direct3D 11 Windows Advanced Rasterization Platform (WARP) para renderizar a superfície de design do Editor de Modelos.<br /><br /> **Gerenciamento de Cena**<br /><br /> **Importarar**<br /> Importa objetos de outro arquivo de modelo 3D para a cena atual.<br /><br /> **Anexar ao Pai**<br /> Estabelece o primeiro de vários objetos selecionados como o pai dos objetos selecionados restantes.<br /><br /> **Desanexar do Pai**<br /> Desanexa o objeto selecionado de seu pai. O objeto selecionado torna-se um *objeto raiz* na cena. Um objeto raiz não tem um objeto pai.<br /><br /> **Criar Grupo**<br /> Agrupa os objetos selecionados como objetos irmãos.<br /><br /> **Mesclar Objetos**<br /> Combina os objetos selecionados em um objeto.<br /><br /> **Criar Novo Objeto da Seleção de Polígono**<br /> Remove as faces selecionadas do objeto atual e adiciona à cena um novo objeto que contenha essas faces.<br /><br /> **Ferramentas**<br /><br /> **Inverter Enrolamento do Polígono**<br /> Inverte os polígonos selecionados para que a ordem de rolagem e a superfície normal sejam invertidas.<br /><br /> **Remover Toda Animação**<br /> Remove os dados de animação dos objetos.<br /><br /> **Triangular**<br /> Converte o objeto selecionado em triângulos.<br /><br /> **Exibir**<br /><br /> Seleção de Face Traseira<br /> Habilita ou desabilita a seleção de face traseira.<br /><br /> **Taxa de Quadros**<br /> Exibe a taxa de quadros no canto superior direito da superfície de design. A taxa de quadros é o número de quadros desenhados por segundo.<br /><br /> Essa opção é útil quando você habilita a opção **Modo de Renderização em Tempo Real**.<br /><br /> **Mostrar Tudo**<br /> Mostra todos os objetos na cena. Isso redefine a propriedade **Oculto** de cada objeto para **Falso**.<br /><br /> **Mostrar Normais da Face**<br /> Mostra o normal de cada face.<br /><br /> **Mostrar Materiais Ausentes**<br /> Exibe uma textura especial em objetos que não têm um material atribuído a eles.<br /><br /> **Mostrar Ponto Dinâmico**<br /> Habilita ou desabilita a exibição de um marcador de eixo 3D no ponto de dinâmico da seleção ativa.<br /><br /> **Mostrar Nós de Espaço Reservado**<br /> Mostra nós de espaço reservado. Um nó de espaço reservado é criado quando você agrupa objetos.<br /><br /> **Mostrar Normais de Vértice**<br /> Mostra o normal de cada vértice. **Dica:**  você pode escolher o botão **Scripts** para executar novamente o último script.|  
  
 Veja a barra de ferramentas **Editor de Modelos**:  
  
 ![Barra de ferramentas do Visualizador de Modelos](../designers/media/digit-mre-toolbar.png "Digit-MRE-Toolbar")  
  
 A tabela a seguir descreve os itens da barra de ferramentas **Editor de Modelos**, que são listados na ordem em que aparecem, de cima para baixo.  
  
|Item da barra de ferramentas|Descrição|  
|------------------|-----------------|  
|**Mover**|Move a seleção.|  
|**Ajustar Escala**|Altera o tamanho da seleção.|  
|**Girar**|Gira a seleção.|  
|**Selecionar Ponto**|Define o **Modo de seleção** para selecionar pontos individuais em um objeto.|  
|**Selecionar Borda**|Define o **Modo de seleção** para selecionar uma borda (uma linha entre dois vértices) em um objeto.|  
|**Selecionar Face**|Define o **Modo de seleção** para selecionar uma face em um objeto.|  
|**Selecionar Objeto**|Define o **Modo de seleção** para selecionar um objeto inteiro.|  
|**Extrusão**|Cria uma face adicional e a conecta à face selecionada.|  
|**Subdividir**|Divide cada face selecionada em várias faces. Para criar novas faces, novos vértices são adicionados – um no centro da face original e um entre cada borda – e unidos aos vértices originais. O número de faces adicionadas é igual ao número de bordas na face original.|  
  
### <a name="controlling-the-view"></a>Controlando a exibição  
 A cena 3D é renderizada de acordo com a exibição, que pode ser considerada como uma câmera virtual com uma posição e orientação. Para alterar a posição e orientação, use os controles de exibição na barra de ferramentas **Modo do Editor de Modelos**.  
  
 A tabela a seguir descreve os principais controles de exibição.  
  
|Controle de exibição|Descrição|  
|------------------|-----------------|  
|**Panorâmica**|Permite a movimentação de uma cena 3D em relação ao quadro da janela. Para obter uma panorâmica, selecione um ponto na cena e movimente-o ao redor.<br /><br /> No modo **Selecionar**, você pode manter pressionada a tecla Ctrl para ativar o modo **Panorâmico** temporariamente.|  
|**Zoom**|Permite a exibição de mais ou menos detalhes da cena em relação ao quadro da janela. No modo **Zoom**, selecione um ponto na cena e mova-o para a direita ou para baixo para ampliar ou para a esquerda ou para cima para reduzir.<br /><br /> No modo **Selecionar**, você pode ampliar ou reduzir usando a roda do mouse enquanto mantém a tecla Ctrl pressionada.|  
|**Órbita**|Posiciona a exibição em um caminho circular em volta do objeto selecionado. Se nenhum objeto for selecionado, o caminho será centralizado na origem da cena. **Nota:** esse modo não terá efeito quando a projeção **Ortográfica** estiver habilitada.|  
|**Objeto de Quadro**|Enquadra o objeto selecionado para que ele se localize no centro da exibição.|  
  
 A exibição é estabelecida pela câmera virtual, mas também é definida por uma projeção. A projeção define como as formas e os objetos, no modo de exibição, são convertidos em pixels na superfície de design. Na barra de ferramentas **Editor de Modelos**, escolha a projeção **Perspectiva** ou **Ortográfica**.  
  
|Projeção|Descrição|  
|----------------|-----------------|  
|**Perspectiva**|Na projeção de perspectiva, os objetos que estão mais longe do ponto de vista parecem menores em tamanho e, por fim, convergem para um ponto distante.|  
|**Ortográfica**|Na projeção Ortográfica, os objetos parecem ser do mesmo tamanho, independentemente da sua distância do ponto de vista. Nenhuma convergência é exibida. Quando a projeção **Ortográfica** é habilitada, não é possível usar o modo **Órbita** para posicionar arbitrariamente a exibição.|  
  
 Talvez seja útil exibir uma cena 3D de uma posição e um ângulo conhecidos, por exemplo, quando você desejar comparar duas cenas semelhantes. Para esse cenário, o Editor de Modelos fornece várias exibições predefinidas. Para usar um modo de exibição predefinido, na barra de ferramentas **Modo do Editor de Modelos**, escolha **Exibir** e escolha a exibição predefinida que deseja: frontal, posterior, esquerda, direita, superior ou inferior. Nesses modos de exibição, a câmera virtual foca diretamente a origem da cena. Por exemplo, se você optar pela **Parte Superior do Modo de Exibição**, a câmera virtual foca a origem da cena diretamente da parte de cima.  
  
### <a name="viewing-additional-geometry-details"></a>Exibindo detalhes adicionais de geometria  
 Para entender melhor um objeto ou cena 3D, você pode exibir detalhes adicionais de geometria, como normais por vértice, normais por face, os pontos dinâmico da seleção ativa e outros detalhes. Para habilitá-los ou desabilitá-los, na barra de ferramentas **Editor de Modelos**, escolha **Scripts**, **Exibir** e o modo desejado.  
  
###  <a name="Adding3DObjects"></a> Criando e importando objetos 3D  
 Para adicionar uma forma 3D predefinida à cena, na **Caixa de Ferramentas**, selecione a forma desejada e mova-a para a superfície de design. As novas formas são posicionadas na origem da cena. O Editor de Modelos fornece sete formas: **Cone**, **Cubo**, **Cilindro**, **Disco**, **Plano**, **Esfera** e **Bule**.  
  
 Para importar um objeto 3D de um arquivo, na barra de ferramentas **Editor de Modelos**, escolha **Avançado**, **Gerenciamento de Cena**, **Importar** e especifique o arquivo que deseja importar.  
  
### <a name="transforming-objects"></a>Transformando objetos  
 Você pode *transformar* um objeto alterando suas propriedades de **Rotação**, **Escala** e **Translação**. *Rotação* orienta um objeto aplicando rotações sucessivas ao redor dos eixos x, y e z definidos pelo seu ponto dinâmico. Cada especificação de rotação tem três componentes (x, y e z, nessa ordem) e os componentes são especificados em graus. **Dimensionamento** redimensiona um objeto expandindo-a por um fator especificado ao longo de um ou mais eixos centrados no seu ponto dinâmico. *Translação* localiza um objeto no espaço tridimensional em relação a seu pai e não ao ponto dinâmico.  
  
 Você pode transformar um objeto usando ferramentas de modelagem ou definindo propriedades.  
  
##### <a name="to-transform-an-object-by-using-modeling-tools"></a>Para transformar um objeto usando ferramentas de modelagem  
  
1.  No modo **Selecionar**, selecione o objeto que deseja transformar. Uma sobreposição delineada indica que o objeto está selecionado.  
  
2.  Na barra de ferramentas **Editor de Modelos**, escolha a ferramenta **Mover**, **Dimensionar** ou **Girar**. Uma manipulador de translação, dimensionamento ou rotação é exibido para o objeto selecionado.  
  
3.  Use o manipulador para executar a transformação. Para transformações de translação e dimensionamento, o manipulador é um indicador de eixo. Você pode alterar um eixo por vez ou alterar todos os eixos ao mesmo tempo usando o cubo branco no centro do indicador. Para rotação, o manipulador é uma esfera feita de círculos codificados por cores que correspondem ao eixo x (vermelho), eixo y (verde) e o eixo z (azul). Você precisa alterar cada eixo individualmente para criar a rotação desejada.  
  
##### <a name="to-transform-an-object-by-setting-its-properties"></a>Para transformar um objeto definindo suas propriedades  
  
1. No modo **Selecionar**, selecione o objeto que deseja transformar. Uma sobreposição delineada indica que o objeto está selecionado.  
  
2. Na janela **Propriedades**, especifique os valores para as propriedades **Rotação**, **Escala** e **Translação**.  
  
   > [!IMPORTANT]
   >  Para a propriedade **Rotação**, especifique o grau de rotação ao redor de cada um dos três eixos. As rotações são aplicadas em ordem, portanto, planeje uma rotação, primeiro em termos de rotação do eixo x, depois do eixo y e, em seguida, do eixo z.  
  
   Usando as ferramentas de modelagem, você pode criar transformações rapidamente, mas não com precisão. Ao definir as propriedades do objeto, você pode especificar transformações de forma precisa, mas não rápida. É recomendável usar as ferramentas de modelagem para ficar "próximo o suficiente" das transformações que deseja e, em seguida, ajustar os valores de propriedade.  
  
   Se não desejar usar manipuladores, você poderá habilitar o modo de forma livre. Na barra de ferramentas **Editor de Modelos**, escolha **Scripts**, **Ferramentas** e **Manipulação de forma livre** para habilitar (ou desabilitar) o modo de forma livre. No modo de forma livre, é possível iniciar uma manipulação em qualquer ponto na superfície de design, em vez de em um ponto no manipulador. No modo de forma livre, você pode restringir as alterações a determinados eixos, bloqueando aqueles que não deseja alterar. Na barra de ferramentas **Modo do Editor de Modelos**, escolha qualquer combinação dos botões **Bloquear X**, **Bloquear Y** e **Bloquear Z**.  
  
   Você pode achar útil trabalhar com objetos usando o recurso ajustar à grade. Na barra de ferramentas **Modo do Editor de Modelos**, escolha **Encaixar** para habilitar (ou desabilitar) o recurso de ajustar à grade. Quando esse recurso é habilitado, as transformações de translação, rotação e dimensionamento são restringidas a incrementos predefinidos.  
  
### <a name="working-with-the-pivot-point"></a>Trabalhando com o ponto dinâmico  
 O ponto dinâmico de um objeto define seu centro de rotação e dimensionamento. É possível alterar o ponto dinâmico de um objeto par alterar como ele é afetado pelas transformações de rotação e dimensionamento. Na barra de ferramentas **Modo do Editor de Modelos**, escolha **Modo Dinâmico** para habilitar (ou desabilitar) o modo dinâmico. Quando o modo dinâmico é habilitado, um pequeno indicador de eixo aparece no ponto dinâmico do objeto selecionado. Você pode usar as ferramentas **Translação** e **Rotação** para manipular o ponto dinâmico.  
  
 Para uma demonstração que mostra como usar o ponto dinâmico, consulte [Como Modificar o Ponto Dinâmico de um Modelo 3D](../designers/how-to-modify-the-pivot-point-of-a-3-d-model.md).  
  
### <a name="world-and-local-modes"></a>Modos local e mundial  
 A translação e a rotação podem ocorrer no sistema de coordenada local (ou *quadro de referência local*) do objeto ou no sistema de coordenada mundial (ou *quatro de referência mundial*). O quadro de referência mundial é independente da rotação do objeto. O modo local é o padrão. Para habilitar (ou desabilitar) o modo mundial, na barra de ferramentas **Modo do Editor de Modelos**, escolha o botão **WorldLocal**.  
  
###  <a name="ModifyingObjects"></a> Modificando objetos  
 Você pode alterar a forma de um objeto 3D movendo ou excluindo seus vértices, bordas e faces. Por padrão, o Editor de modelos está no *modo de objeto*, para que você possa selecionar e transformar objetos inteiros. Para selecionar os pontos, as bordas ou as faces, escolha o modo de seleção adequado. Na barra de ferramentas **Modo do Editor de Modelos**, escolha **Modos de seleção** e, em seguida, escolha o modo desejado.  
  
 É possível criar vértices adicionais por extrusão ou por subdivisão. A extrusão duplica os vértices de uma face (um conjunto coplanar de vértices), que permanece conectada pelos vértices duplicados. A subdivisão adiciona vértices para criar várias faces onde anteriormente havia uma. Para criar novas faces, novos vértices são adicionados – um no centro da face original e um entre cada borda – e unidos aos vértices originais. O número de faces adicionadas é igual ao número de bordas na face original. Em ambos os casos, você pode transladar, girar e dimensionar os novos vértices para alterar a geometria do objeto.  
  
##### <a name="to-extrude-a-face-from-an-object"></a>Para extrudar uma face de um objeto  
  
1.  No modo de seleção de face, selecione aquela que deseja extrudar.  
  
2.  Na barra de ferramentas **Editor de Modelos**, escolha **Scripts**, **Ferramentas** e **Extrusão**.  
  
##### <a name="to-subdivide-faces"></a>Para subdividir faces  
  
1. No modo de seleção de face, selecione aquelas que deseja subdividir. Como a subdivisão cria novos dados de borda, subdividir todas as faces de uma vez proporciona resultados mais consistentes quando as faces são adjacentes.  
  
2. Na barra de ferramentas **Editor de Modelos**, escolha **Scripts**, **Ferramentas** e **Subdividir**.  
  
   Você também pode triangular faces, mesclar objetos e converter as seleções de polígonos em novos objetos. A triangulação cria bordas adicionais para que uma face não triangular seja convertida em um número ideal de triângulos; no entanto, ela não fornece detalhes adicionais geométricos. A mescla combina objetos selecionados em um único objeto. Novos objetos podem ser criados de uma seleção de polígono.  
  
##### <a name="to-triangulate-a-face"></a>Para triangular uma face  
  
1.  No modo de seleção de face, selecione a face que deseja triangular.  
  
2.  Na barra de ferramentas **Editor de Modelos**, escolha **Scripts**, **Ferramentas** e **Triangular**.  
  
##### <a name="to-merge-objects"></a>Para mesclar objetos  
  
1.  No modo de seleção de objeto, selecione os objetos que deseja mesclar.  
  
2.  Na barra de ferramentas **Editor de Modelos**, escolha **Scripts**, **Ferramentas** e **Mesclar Objetos**.  
  
##### <a name="to-create-an-object-from-a-polygon-selection"></a>Para criar um objeto de uma seleção de polígono  
  
1.  No modo de seleção de face, selecione as faces das quais deseja criar um novo objeto.  
  
2.  Na barra de ferramentas **Editor de Modelos**, escolha **Scripts**, **Ferramentas** e **Criar Novo Objeto da Seleção de Polígono**.  
  
### <a name="working-with-materials-and-shaders"></a>Trabalho com materiais e sombreadores  
 A aparência de um objeto é determinada pela interação da iluminação na cena e do material do objeto. Os materiais são definidos pelas propriedades que descrevem como a superfície reage a diferentes tipos de luz e por um programa sombreador que calcula a cor final de cada pixel na superfície do objeto com base na informação de iluminação, mapas de textura, mapas normais e outros dados.  
  
 O Editor de Modelos fornece os seguintes materiais padrão:  
  
|Material|Descrição|  
|--------------|-----------------|  
|Apagado|Renderiza uma superfície sem nenhuma iluminação simulada.|  
|Lambert|Renderiza uma superfície com luz ambiente simulada e iluminação difusa.|  
|Phong|Renderiza uma superfície com luz ambiente simulada, iluminação difusa e realces especulares.|  
  
 Cada um desses materiais aplica uma textura na superfície de um objeto. Você pode definir uma textura diferente para cada objeto que usa o material.  
  
 Para modificar como um objeto específico reage a diferentes fontes de luz na cena, você pode alterar as propriedades de iluminação do material independentemente dos outros objetos que usam o material. Esta tabela descreve as propriedades comuns de iluminação:  
  
|Propriedade de iluminação|Descrição|  
|-----------------------|-----------------|  
|Ambiente|Descreve como a superfície é afetada pela iluminação ambiente.|  
|Difusa|Descreve como a superfície é afetada por luzes direcionais e pontuais.|  
|Emissiva|Descreve como a superfície emite luz, independentemente de outra iluminação.|  
|Especular|Descreve como a superfície reflete as luzes direcionais e pontuais.|  
|Energia Especular|Descreve a largura e a intensidade de realces especulares.|  
  
 Dependendo do que um material suporte, você pode alterar as respectivas propriedades de iluminação, as texturas e outros dados. No modo **Selecionar**, selecione o objeto cujo material você deseja alterar e, na janela **Propriedades**, altere **MaterialAmbient**, **MaterialDiffuse**, **MaterialEmissive**, **MaterialSpecular**, **MaterialSpecularPower** ou outra propriedade disponível. Um material pode expor até oito texturas, cujas propriedades são chamadas sequencialmente de **Texture1** a **Texture8**.  
  
 Para remover todos os materiais de um objeto, na barra de ferramentas **Editor de modelos**, escolha **Scripts**, **Materiais**, **Remover Materiais**.  
  
 Você pode usar o **Designer de Sombreador** para criar materiais sombreadores personalizados que possam ser aplicados a objetos na cena 3D. Para obter informações sobre como criar materiais sombreadores personalizados, consulte [Designer de Sombreador](../designers/shader-designer.md). Para obter informações sobre como aplicar um material sombreador personalizado a um objeto, consulte [Como Aplicar um Sombreador a um Modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md).  
  
### <a name="scene-management"></a>Gerenciamento de cena  
 Você pode gerenciar cenas como uma hierarquia de objetos. Quando vários objetos são organizados em uma hierarquia, qualquer translação, dimensionamento ou rotação de um nó pai também afeta seus filhos. Isso é útil quando você deseja construir cenas ou objetos complexos de objetos mais básicos.  
  
 Você pode usar a janela **Estrutura de Tópicos de Documentos** para exibir a hierarquia da cena e selecionar os nós da cena. Ao selecionar um nó na estrutura de tópicos, você pode usar a janela **Propriedades** para alterar suas propriedades.  
  
 Você pode construir uma hierarquia de objetos tornando um deles o pai dos outros ou agrupando-os como irmãos em um nó de espaço reservado que atua como o pai.  
  
##### <a name="to-create-a-hierarchy-that-has-a-parent-object"></a>Para criar uma hierarquia que tem um objeto pai  
  
1.  No modo **Selecionar**, selecione dois ou mais objetos. O primeiro que você selecionar será o objeto pai.  
  
2.  Na barra de ferramentas **Editor de Modelos**, escolha **Scripts**, **Gerenciamento de Cena** e **Anexar ao Pai**.  
  
##### <a name="to-create-a-hierarchy-of-sibling-objects"></a>Para criar uma hierarquia de objetos irmãos  
  
1. No modo **Selecionar**, selecione dois ou mais objetos. Um objeto de espaço reservado é criado e se torna seu objeto pai.  
  
2. Na barra de ferramentas **Editor de Modelos**, escolha **Scripts**, **Gerenciamento de Cena** e **Criar Grupo**.  
  
   O Editor de Modelos usa um delineado branco para identificar o primeiro objeto selecionado, que se torna o pai. Outros objetos na seleção têm um delineado azul. Por padrão, os nós de espaço reservado não são exibidos. Para exibir os nós de espaço reservado, na barra de ferramentas **Editor de Modelos**, escolha **Scripts**, **Gerenciamento de Cena**, **Mostrar Nós de Espaço Reservado**. Você pode trabalhar com nós de espaço reservado da mesma forma que trabalha com objetos que não são de espaço reservado.  
  
   Para remover a associação pai/filho entre dois objetos, selecione o objeto filho e, na barra de ferramentas **Editor de Modelos**, escolha **Scripts**, **Gerenciamento da Cena**, **Desanexar do Pai**. Quando você desanexa o pai de um objeto filho, o objeto filho se torna um objeto raiz na cena.  
  
## <a name="keyboard-shortcuts"></a>Atalhos de teclado  
  
|Comando|Atalhos de teclado|  
|-------------|------------------------|  
|Mudar para o modo **Selecionar**|Ctrl+G, Gtrl+Q<br /><br /> S|  
|Mudar para o modo **Zoom**|Ctrl+G, Ctrl+Z<br /><br /> Z|  
|Mudar para o modo **Panorâmico**|Ctrl+G, Ctrl+P<br /><br /> M|  
|Selecionar tudo|Ctrl+A|  
|Excluir a seleção atual|Excluir|  
|Cancelar a seleção atual|Escape|  
|Ampliar|Roda do mouse para frente<br /><br /> Ctrl+Roda do mouse para frente<br /><br /> Shift+Roda do mouse para frente<br /><br /> Ctrl+PageUp<br /><br /> Sinal de mais (+)|  
|Reduzir|Roda do mouse para trás<br /><br /> Ctrl+Roda do mouse para trás<br /><br /> Shift+Roda do mouse para trás<br /><br /> Ctrl+PageDown<br /><br /> Sinal de menos (-)|  
|Panorâmica da câmera para cima|PageDown|  
|Panorâmica da câmera para baixo|PageUp|  
|Panorâmica da câmera para a esquerda|Roda do mouse para a esquerda<br /><br /> Ctrl+PageDown|  
|Panorâmica da câmera para a direita|Roda do mouse para a direita<br /><br /> Ctrl+PageDown|  
|Exibir parte superior de modelo|Ctrl+L, Ctrl+T<br /><br /> T|  
|Exibir parte inferior do modelo|Ctrl+L, Ctrl+U|  
|Exibir lado esquerdo do modelo|Ctrl+L, Ctrl+L|  
|Exibir lado direito do modelo|Ctrl+L, Ctrl+R|  
|Exibir a parte da frente do modelo|Ctrl+L, Ctrl+F|  
|Exibir a parte de trás do modelo|Ctrl+L, Ctrl+B|  
|Enquadrar objeto na janela|F|  
|Ativar/desativar modo delineado|Ctrl+L, Ctrl+W|  
|Ativar/desativar Ajustar à grade|Ctrl+G, Ctrl+N|  
|Ativar/desativar modo dinâmico|Ctrl+G, Ctrl+V|  
|Ativar/desativar restrição do eixo x|Ctrl+L, Ctrl+X|  
|Ativar/desativar restrição do eixo y|Ctrl+L, Ctrl+Y|  
|Ativar/desativar restrição do eixo z|Ctrl+L, Ctrl+Z|  
|Alternar para modo de translação|Ctrl+G, Ctrl+W<br /><br /> W|  
|Alternar para modo de dimensionamento|Ctrl+G, Ctrl+E<br /><br /> E|  
|Alternar para modo de rotação|Ctrl+G, Ctrl+R<br /><br /> R|  
|Alterar para modo de seleção de ponto|Ctrl+L, Ctrl+1|  
|Alternar para modo de seleção de borda|Ctrl+L, Ctrl+2|  
|Alternar para modo de seleção de face|Ctrl+L, Ctrl+3|  
|Alternar para modo de seleção de objeto|Ctrl+L, Ctrl+4|  
|Alternar para modo de órbita (câmera)|Ctrl+G, Ctrl+O|  
|Selecionar próximo objeto na cena|Tabulação|  
|Selecionar objeto anterior na cena|Shift+Tab|  
|Manipular o objeto selecionado com base na ferramenta atual.|As teclas de seta|  
|Desativar o manipulador atual|Q|  
|Girar câmera|Alt+Arrastar com o botão esquerdo do mouse|  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Trabalhando com ativos 3D para jogos e aplicativos](../designers/working-with-3-d-assets-for-games-and-apps.md)|Fornece uma visão geral das ferramentas do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] que você pode usar para trabalhar com recursos gráficos, como texturas e imagens, modelos 3D e efeitos de sombreamento.|  
|[Editor de Imagens](../designers/image-editor.md)|Descreve como usar o Editor de Imagens do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para trabalhar com texturas e imagens.|  
|[Designer de Sombreador](../designers/shader-designer.md)|Descreve como usar o Designer de Sombreador do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para trabalhar com sombreadores.|



