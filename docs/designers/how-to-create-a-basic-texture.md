---
title: Como criar uma textura básica
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 0222e8bf-d29f-421b-9b1f-123d500fa179
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b4bd1d34ef2dc31935038bb1be30d548c58208fd
ms.sourcegitcommit: 25fc9605ba673afb51a24ce587cf4304b06aa577
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2018
ms.locfileid: "47028975"
---
# <a name="how-to-create-a-basic-texture"></a>Como criar uma textura básica

Este artigo demonstra como usar o Editor de imagens para criar uma textura básica, incluindo as seguintes atividades:

- Configurar o tamanho da textura

- Configurar a cor de primeiro plano e a cor da tela de fundo

- Usar o canal alfa (transparência)

- Usar as ferramentas **Preenchimento** e **Elipse**

- Configurar propriedades de ferramenta

## <a name="create-a-basic-texture"></a>Criar uma textura básica

Você pode usar o Editor de Imagens para criar e modificar imagens e texturas para o seu jogo ou aplicativo.

As etapas a seguir mostram como criar uma textura que representa um destino de "espiral". Quando você terminar, a textura deverá ser semelhante à da seguinte figura. Para demonstrar melhor a transparência na textura, o Editor de Imagens foi configurado para usar um padrão quadriculado verde para exibi-la.

![Destino de "alvo" com transparência mostrada em verde](../designers/media/digit-bullseye-texture-in-editor.png)

Antes de começar, verifique se a janela **Propriedades** está sendo exibida. A janela **Propriedades** é usada para definir o tamanho da imagem, alterar as propriedades da ferramenta e especificar cores enquanto você trabalha.

### <a name="create-a-bullseye-target-texture"></a>Criar uma textura de destino de "alvo"

1. Crie uma textura com o qual você trabalhará. Saiba mais sobre como adicionar uma textura ao seu projeto em [Editor de Imagens](../designers/image-editor.md#get-started).

2. Defina o tamanho da imagem como 512x512 pixels. Na janela **Propriedades**, defina os valores das propriedades **Largura** e **Altura** como `512`.

3. Na barra de ferramentas do Editor de Imagens, escolha a ferramenta **Preenchimento**. A janela **Propriedades** agora exibe as propriedades da ferramenta **Preenchimento** junto com as propriedades da imagem.

4. Defina a cor de primeiro plano como preto totalmente transparente. Na janela **Propriedades**, no grupo de propriedades **Cores**, selecione **Primeiro Plano**. Defina os valores das propriedades **R**, **G**, **B** e **A** ao lado do seletor de cor como `0`.

5. Na barra de ferramentas do Editor de Imagens, escolha a ferramenta **Preenchimento**, em seguida, pressione e segure a tecla **Shift** e escolha qualquer ponto na imagem. Se você usar a tecla **Shift**, o valor alfa da cor de preenchimento substituirá a cor na imagem. Caso contrário, o valor alfa será usado para misturar a cor de preenchimento com a cor da imagem.

    > [!IMPORTANT]
    > Essa etapa, junto com a seleção de cor na etapa anterior, garante que a imagem base seja preparada para a textura de destino de "alvo" que você desenhará. Quando a imagem é preenchida com preto transparente e como a borda do destino é preta, não haverá nenhum artefato de serrilhado em torno de destino.

6. Na barra de ferramentas do Editor de Imagens, escolha a ferramenta **Elipse**.

7. Defina a cor de primeiro plano como preto totalmente opaco. Defina os valores das propriedades **R**, **G** e **B** como `0` e o valor da propriedade **A** como `255`.

8. Defina a cor da tela de fundo como branco totalmente opaco. Na janela **Propriedades**, no grupo de propriedades **Cores**, selecione **Tela de Fundo**. Defina os valores das propriedades **R**, **G**, **B** e **A** como `255`.

9. Defina a largura do contorno da elipse. Na janela **Propriedades**, no grupo de propriedades **Aparência**, defina o valor da propriedade **Largura** como `8`.

10. Verifique se a suavização está habilitada. Na janela **Propriedades**, no grupo de propriedades **Aparência**, verifique se a propriedade **Suavização** está definida.

11. Usando a ferramenta **Elipse**, desenhe um círculo da coordenada de pixel `(3, 3)` até a coordenada de pixel `(508, 508)`. Para desenhar o círculo com mais facilidade, você pode pressionar e segurar a tecla **Shift** enquanto desenha.

    > [!NOTE]
    > As coordenadas de pixel do local atual do ponteiro são exibidas na barra de status do Visual Studio.

12. Altere a cor da tela de fundo. Defina **R** como `44`, **G** como `165`, **B** como `211` e **A** como `255`.

13. Desenhe outro círculo da coordenada de pixel `(64, 64)` até a coordenada de pixel `(448, 448)`.

14. Altere a cor da tela de fundo de volta para branco totalmente opaco. Defina **R**, **G**, **B** e **A** como `255`.

15. Desenhe outro círculo da coordenada de pixel `(128, 128)` até a coordenada de pixel `(384, 384)`.

16. Altere a cor da tela de fundo. Defina **R** como `255`, **G** e **B** como `64` e **A** como `255`.

17. Desenhe outro círculo da coordenada de pixel `(192, 192)` até a coordenada de pixel `(320, 320)`.

A textura de destino de "alvo" foi concluída. Aqui está a imagem final, mostrada com transparência.

![A textura de destino de "alvo" completa](../designers/media/gfx_image_demo_bullseye.png)

Como uma próxima etapa, você pode gerar níveis de MIP para essa textura. Para obter informações, confira [Como criar e modificar níveis de MIP](../designers/how-to-create-and-modify-mip-levels.md).

## <a name="see-also"></a>Consulte também

- [Editor de Imagens](../designers/image-editor.md)