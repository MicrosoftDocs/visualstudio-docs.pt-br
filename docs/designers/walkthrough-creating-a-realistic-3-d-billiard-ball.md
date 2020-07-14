---
title: 'Passo a passo: Criando uma bola de bilhar realista em 3D'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: af8eb0f3-bf6a-4d1c-ab47-dcd88ab04efa
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4bebaa8c197d0b0a4447739d900062bef2bda37c
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816651"
---
# <a name="walkthrough-create-a-realistic-3d-billiard-ball"></a>Passo a passo: Criar uma bola de bilhar 3D realista

Este passo a passo demonstra como criar uma bola de bilhar realista em 3D usando o Designer de Sombreador e o Editor de Imagens no Visual Studio. A aparência 3D da bola de bilhar é obtida pela combinação de várias técnicas de sombreador com recursos de textura adequados.

## <a name="prerequisites"></a>Pré-requisitos

Você precisa dos seguintes componentes e habilidades para concluir este passo a passo:

- Uma ferramenta para criar texturas em um mapa de cubo, como a ferramenta de textura do DirectX que está incluída no SDK do DirectX de junho de 2010.

- Familiaridade com o Editor de Imagens no Visual Studio.

- Familiaridade com o Designer de Sombreador no Visual Studio.

## <a name="create-the-basic-appearance-with-shape-and-texture"></a>Criar a aparência básica com forma e textura

Em gráficos de computador, os elementos mais básicos de aparência são forma e cor. Em uma simulação de computador, é comum usar um modelo 3D para representar a forma de um objeto real. O detalhe de cor é, então, aplicado para a superfície do modelo usando um mapa de textura.

Você talvez precise solicitar a criação de um modelo 3D que possa usar, mas como uma bola de bilhar é uma forma comum (uma esfera), o Designer de Sombreador já tem um modelo adequado criado.

A esfera é a forma de visualização padrão no Designer de Sombreador. Se você estiver usando uma forma diferente para visualizar seu sombreador, mude para a esfera.

### <a name="to-preview-the-shader-by-using-a-sphere"></a>Para visualizar o sombreador usando uma esfera

- Na barra de ferramentas do Designer de Sombreador, escolha **Visualização com esfera**.

Na próxima etapa, você criará um programa sombreador que aplica uma textura ao modelo, mas primeiro você precisa criar uma textura que possa usar. Este passo a passo demonstra como criar a textura usando o Editor de Imagens, que é uma parte do Visual Studio, mas você pode usar qualquer editor de imagens que possa salvar a textura em um formato adequado.

Verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.

### <a name="to-create-a-billiard-ball-texture-by-using-the-image-editor"></a>Como criar uma textura de bola de bilhar usando o Editor de Imagens

1. Crie uma textura com a qual trabalhar. Para obter informações sobre como adicionar uma textura em seu projeto, consulte a seção de Introdução em [Editor de Imagens](../designers/image-editor.md).

2. Defina o tamanho da imagem para que sua largura seja duas vezes sua altura. Isso é necessário devido à maneira em que uma textura é mapeada na superfície esférica da bola de bilhar. Para redimensionar a imagem, na janela **Propriedades**, especifique novos valores para as propriedades **Largura** e **Altura**. Por exemplo, defina a largura para 512 e a altura para 256.

3. Desenhe uma textura para a bola de bilhar, tendo em mente como uma textura é mapeada em uma esfera.

    A textura deverá ser parecida com esta:

    ![Textura para a bola de bilhar](../designers/media/gfx_shader_demo_billiard_art_ball_texture.png)

4. Opcionalmente, você talvez queira diminuir os requisitos de armazenamento dessa textura. Você pode fazer isso reduzindo a largura da textura para corresponder a sua altura. Isso compacta a textura ao longo de sua largura, mas devido à maneira que a textura é mapeada para a esfera, ela será expandida quando a bola de bilhar for renderizada. Após o redimensionamento, a textura deverá ser parecida com esta:

    ![Textura de bilhar compactada em um quadrado](../designers/media/gfx_shader_demo_billiard_art_ball_texture_square.png)

   Agora, você pode criar um sombreador que aplica essa textura ao modelo.

### <a name="to-create-a-basic-texture-shader"></a>Para criar um sombreador de textura básico

1. Crie um sombreador DGSL com o qual trabalhar. Para obter informações sobre como adicionar um sombreador DGSL ao seu projeto, consulte a seção de Introdução em [Designer de Sombreador](../designers/shader-designer.md).

    Por padrão, um grafo de sombreador tem esta aparência:

    ![O grafo de sombreador padrão](../designers/media/gfx_shader_demo_billiard_step_0.png)

2. Modifique o sombreador padrão para que ele seja aplicado ao valor de uma amostra de textura ao pixel atual. O gráfico de sombreador deve ter esta aparência:

    ![Um grafo sombreador que aplica textura a um objeto](../designers/media/gfx_shader_demo_billiard_step_1.png)

3. Aplique a textura que você criou no procedimento anterior ao configurar as propriedades de textura. Defina o valor da propriedade **Textura** do nó **Amostra de Textura** em **Texture1** e, em seguida, especifique o arquivo de textura usando a propriedade **Filename** do grupo de propriedades **Texture1** na mesma janela de propriedade.

   Para obter mais informações sobre como aplicar uma textura no sombreador, confira [Como criar um sombreador de textura básica](../designers/how-to-create-a-basic-texture-shader.md).

   Sua bola de bilhar agora deve ser semelhante a esta:

   ![Uma vista de perto da bola de bilhar texturizada](../designers/media/gfx_shader_demo_.png)

## <a name="create-depth-with-the-lambert-lighting-model"></a>Criar profundidade com o modelo de iluminação Lambert

Até agora, você criou uma bola de bilhar facilmente reconhecível. No entanto, ela é plana e desinteressante — mais como uma imagem de desenho de uma bola de bilhar do que uma réplica convincente. A aparência plana é resultado do sombreador simplista, que se comporta como se cada pixel na superfície da bola de bilhar recebesse a mesma quantidade de luz.

No mundo real, a luz é mais brilhante em superfícies com uma fonte de luz direta e é menos brilhante em superfícies que estão em um ângulo oblíquo em relação à fonte de luz. Isso ocorre porque a energia nos raios de luz é distribuída entre a área de superfície menor quando a superfície tem fonte de luz direta. À medida que a superfície fica longe da fonte de luz, a mesma quantidade de energia é distribuída em uma área de superfície maior. Uma superfície que fica longe de uma fonte de luz não recebe nenhuma luz, resultando em uma aparência totalmente escura. Essa variação no brilho na superfície de um objeto é uma dica visual importante que ajuda a indicar a forma de um objeto. Sem ela, o objeto fica plano.

Em gráficos de computador, *modelos de iluminação* — aproximações simplificadas de interações de luz complexas e reais — são usados para replicar a aparência de iluminação do mundo real. O modelo de iluminação Lambert varia a quantidade de luz refletida difusamente na superfície de um objeto, conforme descrito no parágrafo anterior. Você pode adicionar o modelo de iluminação Lambert em seu sombreador para dar à bola de bilhar uma aparência 3D mais convincente.

### <a name="to-add-lambert-lighting-to-your-shader"></a>Como adicionar iluminação Lambert ao seu sombreador

- Modifique seu sombreador para variar o valor da amostra de textura pelo valor de iluminação Lambert. Seu gráfico de sombreador deve ter esta aparência:

   ![O grafo de sombreador com iluminação Lambert adicionada](../designers/media/gfx_shader_demo_billiard_step_2.png)

- Opcionalmente, você pode ajustar o comportamento da iluminação configurando a propriedade **MaterialDiffuse** do gráfico do sombreador. Para acessar as propriedades do gráfico do sombreador, escolha uma área vazia da superfície de design e, em seguida, localize a propriedade que você deseja acessar na janela **Propriedades**.

Para obter mais informações sobre como aplicar a iluminação Lambert no sombreador, confira [Como criar um sombreador Lambert básico](../designers/how-to-create-a-basic-lambert-shader.md).

Com a iluminação Lambert aplicada, a bola de bilhar deve ser semelhante a esta:

![Uma vista de perto da bola de bilhar acesa e texturizada](../designers/media/gfx_shader_demo_billiard_ball_2.png)

## <a name="enhance-the-basic-appearance-with-specular-highlights"></a>Aprimorar a aparência básica com realces especulares

O modelo de iluminação Lambert fornece o senso de forma e dimensão que estava ausente no sombreador somente textura. No entanto, a bola de bilhar ainda tem uma aparência um pouco fosca.

Uma bola de bilhar real normalmente tem um acetinado que reflete uma parte da luz contida nela. Um pouco da luz refletida resulta em realces especulares, que simulam as propriedades de reflexão de uma superfície. Dependendo das propriedades de acabamento, os realces podem ser localizados ou amplos, intensos ou sutis. Esses reflexos especulares são modelados usando a relação entre uma fonte de luz, a orientação da superfície e a posição da câmera — ou seja, o realce é mais intenso quando a orientação da superfície reflete a fonte de luz diretamente na câmera e é menos intenso quando a reflexão é menos direta.

O modelo de iluminação Phong se baseia no modelo de iluminação Lambert para incluir realces especulares, conforme descrito no parágrafo anterior. Você pode adicionar o modelo de iluminação Phong ao seu sombreador para dar à bola de bilhar um acabamento simulado que resulta em uma aparência mais interessante.

### <a name="to-add-specular-highlights-to-your-shader"></a>Como adicionar realces especulares ao seu sombreador

1. Modifique seu sombreador para incluir a contribuição especular usando combinação aditiva. Seu gráfico de sombreador deve ter esta aparência:

    ![O grafo de sombreador com iluminação especular adicionada](../designers/media/gfx_shader_demo_billiard_step_3.png)

2. Opcionalmente, você pode ajustar a maneira que o realce especular se comporta ao configurar as propriedades especulares (**MaterialSpecular** e **MaterialSpecularPower**) do gráfico do sombreador. Para acessar as propriedades do gráfico do sombreador, escolha uma área vazia da superfície de design e, em seguida, localize a propriedade que você deseja acessar na janela **Propriedades**.

   Para obter mais informações sobre como aplicar realces especulares no sombreador, confira [Como criar um sombreador Phong básico](../designers/how-to-create-a-basic-phong-shader.md).

   Com a iluminação especular aplicada, sua bola de bilhar deve ser semelhante a esta:

   ![Uma vista de perto da bola de bilhar com especular adicionado](../designers/media/gfx_shader_demo_billiard_ball_3.png)

## <a name="create-a-sense-of-space-by-reflecting-the-environment"></a>Criar um senso de espaço ao refletir o ambiente

Com os realces especulares aplicados, a bola de bilhar parece muito convincente. Ela tem a forma, o trabalho de pintura e o acabamento corretos. No entanto, ainda há uma técnica que fará com que a bola de bilhar pareça fazer parte de seu ambiente.

Se examinar de perto uma bola de bilhar real, você poderá ver que sua superfície brilhante não exibe apenas realces especulares, mas também reflete, de modo esmaecido, uma imagem do mundo em torno dele. Você pode simular essa reflexão usando uma imagem do ambiente como uma textura e combiná-la com a textura do modelo para determinar a cor final de cada pixel. Dependendo do tipo de acabamento que desejar, você pode combinar mais ou menos da reflexão de textura junto com o restante do sombreador. Por exemplo, um sombreador que simula uma superfície altamente refletiva, como um espelho, pode usar somente a textura de reflexão, mas um sombreador que simula um reflexo mais sutil, como o de uma bola de bilhar, pode combinar apenas uma pequena parte do valor da textura de reflexão junto com o restante do cálculo do sombreador.

Obviamente, você não pode aplicar apenas a imagem refletida no modelo da mesma maneira que aplica o mapa de textura do modelo. Se fez isso, a reflexão do mundo será movida com a bola de bilhar como se estivesse colada a ela. Como um reflexo pode vir de qualquer direção, você precisa de uma maneira para fornecer um valor de mapa de reflexão para qualquer ângulo e uma maneira de manter o mapa de reflexão orientado de acordo com o mundo. Para atender a esses requisitos, você pode usar um tipo especial de mapa de textura — chamado de *mapa de cubo* — que fornece seis texturas organizadas para formar os lados de um cubo. De dentro desse cubo, você pode apontar em qualquer direção para localizar um valor de textura. Se as texturas em cada lado do cubo contiverem imagens do ambiente, você poderá simular qualquer reflexão ao fazer a amostragem do local correto na superfície do cubo. Ao manter o cubo alinhado com o mundo, você obterá um reflexo preciso do ambiente. Para determinar onde o cubo deve ser amostrado, calcule a reflexão do vetor da câmera na superfície do objeto e, em seguida, use-o como coordenadas de textura 3D. Usar mapas de cubo dessa forma é uma técnica comum que é conhecida como *mapeamento de ambiente*.

O mapeamento de ambiente fornece uma aproximação eficiente de reflexos reais conforme descrito nos parágrafos anteriores. Você pode misturar os reflexos mapeados de ambiente em seu sombreador para dar à bola de bilhar um acabamento simulado que faz com que a bola de bilhar pareça mais conectada com a cena.

A primeira etapa é criar uma textura de mapa de cubo. Em muitos tipos de aplicativos, o conteúdo do mapa de cubo não precisa ser perfeito para ser eficaz, especialmente quando a reflexão for sutil ou não ocupar um espaço de destaque na tela. Por exemplo, muitos jogos usam mapas de cubo pré-calculados de mapeamento de ambiente e usam apenas o mais próximo de cada objeto reflexivo, embora isso signifique que a reflexão não está correta. Até mesmo uma aproximação grosseira geralmente é boa o bastante para um efeito convincente.

### <a name="to-create-textures-for-an-environment-map-by-using-the-image-editor"></a>Como criar texturas para um mapa de ambiente usando o Editor de Imagens

1. Crie uma textura com a qual trabalhar. Para obter informações sobre como adicionar uma textura em seu projeto, consulte a seção de Introdução em [Editor de Imagens](../designers/image-editor.md).

2. Defina o tamanho da imagem para que a largura seja igual à altura e o lateral tenha um valor ao quadrado. Isso é necessário devido à maneira que um mapa de cubo é indexado. Para redimensionar a imagem, na janela **Propriedades**, especifique novos valores para as propriedades **Largura** e **Altura**. Por exemplo, defina o valor das propriedades **Largura** e **Altura** como 256.

3. Use uma cor sólida para preencher a textura. Este textura será a parte inferior do mapa de cubo, que corresponde à superfície da tabela de bilhar. Mantenha a cor usada em mente para a próxima textura.

4. Crie uma segunda textura com o mesmo tamanho que a primeira. Essa textura será repetida nos quatro lados do mapa de cubo, que correspondem à superfície e aos lados de uma tabela de bilhar e à área ao redor da tabela de bilhar. Certifique-se de desenhar a superfície da tabela de bilhar nessa textura usando a mesma cor que na textura inferior. A textura deverá ser parecida com esta:

    ![A textura dos lados do cubemap](../designers/media/gfx_shader_demo_billiard_art_env_texture_side.png)

    Lembre-se de que um mapa de reflexão não precisa ser realista para ser eficaz. Por exemplo, o mapa de cubo usado para criar as imagens neste artigo contém apenas quatro cavidades em vez de seis.

5. Crie uma terceira textura com o mesmo tamanho que as outras. Este textura será a parte superior do mapa de cubo, que corresponde à superfície da tabela de bilhar. Para tornar essa parte da reflexão mais interessante, você pode desenhar uma luz acima para reforçar os realces especulares que você adicionou ao sombreador no procedimento anterior. A textura deverá ser parecida com esta:

    ![A textura da parte superior do cubemap](../designers/media/gfx_shader_demo_billiard_art_env_texture_top2.png)

   Agora que você criou texturas individuais para os lados do mapa de cubo, use uma ferramenta para agrupá-las em um mapa de cubo que pode ser armazenado em uma única textura *.dds*. Você pode usar qualquer programa que deseja que crie o mapa de cubo contanto que ele possa salvar o mapa de cubo no formato de textura .dds. Este passo a passo demonstra como criar a textura usando a Ferramenta de Textura do DirectX, que faz parte do SDK do DirectX de junho de 2010.

### <a name="to-assemble-a-cube-map-by-using-the-directx-texture-tool"></a>Como montar um mapa de cubo usando a ferramenta de textura do DirectX

1. Na ferramenta textura do DirectX, no menu principal, escolha **arquivo**  >  **nova textura**. A caixa de diálogo **Nova Textura** é exibida.

2. No grupo **Tipo de Textura**, escolha **Textura do Mapa de Cubo**.

3. No grupo **Dimensões**, digite o valor correto para a **Largura** e a **Altura**e, em seguida, escolha **OK**. Um novo documento de textura é exibido. Por padrão, a textura mostrada pela primeira vez no documento de textura corresponde à face do cubo **X positivo**.

4. Carregue a textura que você criou para o lado do cubo de textura na face do cubo. No menu principal, escolha **arquivo**  >  **abrir para este cubemap face**, selecione a textura que você criou para o lado do cubo e, em seguida, escolha **abrir**.

5. Repita a etapa 4 para as faces do cubo **X negativo**, **Z positivo** e **Z negativo**. Para fazer isso, você deve exibir a face que deseja carregar. Para exibir uma face de mapa de cubos diferente, no menu principal, escolha **Exibir**  >  a**face do mapa do cubo**e, em seguida, selecione a face que você deseja exibir.

6. Para a face do cubo **Y positivo**, carregue a textura que você criou na parte de cima do cubo de textura.

7. Para a face do cubo **Y negativo**, carregue a textura que você criou na parte de baixo do cubo de textura.

8. Salve a textura.

   Você pode imaginar o layout do mapa de cubo como este:

   ![Layout do mapa de cubo do ambiente](../designers/media/gfx_shader_demo_billiard_art_env_texture_top.png)

   A imagem na parte superior é a face do cubo Y positivo (+Y); no meio, da esquerda para a direita, é -X, +Z, +X e -Z; na parte inferior, é -Y.

   Agora você pode modificar o sombreador para mesclar o exemplo de mapa de cubo para o restante do sombreador.

### <a name="to-add-environment-mapping-to-your-shader"></a>Como adicionar o mapeamento de ambiente ao sombreador

1. Modifique seu sombreador para incluir a contribuição do mapeamento de ambiente usando combinação aditiva. Seu gráfico de sombreador deve ter esta aparência:

    ![Uma vista de perto dos dois tipos de nós do sombreador reflexivo](../designers/media/gfx_shader_demo_billiard_step_4b.png)

    Observe que você pode usar um nó de **Adição Múltipla** nó para simplificar o gráfico do sombreador.

    Aqui está uma visão mais detalhada dos nós do sombreador que implementam o mapeamento de ambiente:

    ![O grafo de sombreador com o mapeamento de ambiente adicionado](../designers/media/gfx_shader_demo_billiard_step_4a.png)

2. Aplique a textura que você criou no procedimento anterior ao configurar as propriedades de textura do mapa de cubo. Defina o valor da propriedade **Textura** do nó **Amostra do Mapa de Cubo** em **Texture2** e, em seguida, especifique o arquivo de textura usando a propriedade **Filename** do grupo de propriedades **Texture2**.

3. Opcionalmente, você pode ajustar a reflexibilidade da bola de bilhar ao configurar a propriedade **Saída** do nó **Constante**. Para acessar as propriedades do nó, selecione-o na janela **Propriedades** e localize a propriedade que você deseja acessar.

   Com o mapeamento de ambiente aplicado, a bola de bilhar deve ser semelhante a esta:

   ![Uma vista de perto da bola de bilhar de ambiente mapeada](../designers/media/gfx_shader_demo_billiard_ball_4.png)

   Nesta imagem final, observe como os efeitos que você adicionou se unem para criar uma bola de bilhar muito convincente. A forma, a textura e a iluminação criam a aparência básica de um objeto 3D e os realces especulares e os reflexos tornam a bola de bilhar mais interessante e fazem com que ela pareça fazer parte do ambiente.

## <a name="see-also"></a>Veja também

- [Como: exportar um sombreador](../designers/how-to-export-a-shader.md)
- [Como: aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md)
- [Designer de sombreador](../designers/shader-designer.md)
- [Editor de imagem](../designers/image-editor.md)
- [Nós do designer do sombreador](../designers/shader-designer-nodes.md)
