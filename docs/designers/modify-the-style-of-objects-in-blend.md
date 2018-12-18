---
title: Modificar o estilo de objetos no Blend
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4ae494a82e92086cfa0e8e2a69b7f7eee022807a
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31917196"
---
# <a name="modify-the-style-of-objects-in-blend"></a>Modificar o estilo de objetos no Blend

A maneira mais fácil de personalizar um objeto é definir as propriedades no painel **Propriedades**.

Se você quiser reutilizar configurações ou grupos de configurações, crie um recurso reutilizável. Pode ser um *estilo*, *modelo*, ou algo simples como uma cor personalizada. Você também pode fazer um controle aparecer diferentemente com base em seu estado. Por exemplo, um botão muda para verde quando o usuário clica nele.

## <a name="brushes-modify-the-appearance-of-an-object"></a>Pincéis: Modificar a aparência de um objeto

Aplique um pincel a um objeto se você quiser alterar sua aparência.

### <a name="paint-a-repeating-image-or-pattern-on-an-object"></a>Pinte uma imagem ou padrão de repetição em um objeto

Pinte uma imagem ou padrão de repetição em um objeto usando um *pincel de bloco*.

Para criar um pincel de bloco, comece criando um *pincel de imagem*, *pincel de desenho* ou *pincel visual*.

Crie um pincel de imagem usando uma imagem. As ilustrações a seguir mostram o pincel de imagem, o pincel de imagem lado a lado e o pincel de imagem invertido.

![Pincel de imagem](../designers/media/81f84f56-906d-456b-8288-d77da1e01e31.png) ![Imagem pincel lado a lado](../designers/media/d3782ca8-64da-47a4-a095-c6cdd0fa47a2.png) ![Imagem pincel invertido](../designers/media/38ae3691-f3f1-4a1e-82ca-c7fa164bf56e.png)

Crie um pincel de desenho usando um desenho vetorial como um caminho ou uma forma. As ilustrações a seguir mostram o pincel de desenho, o pincel de desenho lado a lado e o pincel de desenho invertido.

![Pincel de desenho](../designers/media/197666ac-ef57-4c5c-9779-669e991a00a5.png) ![Pincel de desenho lado a lado](../designers/media/ba09cda3-4cee-40ba-b3d4-edc032158bdc.png) ![Pincel de desenho invertido](../designers/media/15bf6021-620c-4490-9eae-086153d3f14f.png)

Crie um pincel visual a partir de um controle, como um botão. As ilustrações a seguir mostram o pincel visual e o pincel visual lado a lado.

![Pincel visual](../designers/media/fb6c90e0-153c-48fe-b563-e601beac6227.png) ![Pincel visual lado a lado](../designers/media/e261b99f-7d8f-4d91-bc84-19c7beccc255.png)

## <a name="styles-and-templates-create-a-consistent-look-and-feel-across-controls"></a>Estilos e modelos: criar uma aparência consistente entre os controles

Você pode criar uma vez a aparência e o comportamento de um controle uma vez e aplicar esse design a outros controles, para que você não precise mantê-los individualmente.

**Você deve usar um estilo?** : se você só quiser definir as propriedades padrão (como a cor de um botão), use um *estilo*. É possível modificar um controle, mesmo após aplicar um estilo a ele.

**Você deve usar um modelo?**: se você quiser alterar a estrutura de um controle, use um *modelo*. Imagine a conversão de um gráfico ou logotipo em um botão. Não é possível modificar um controle depois de aplicar um modelo a ele.

### <a name="create-a-template-or-style"></a>Criar um modelo ou estilo

Há duas maneiras de criar um modelo. Você pode converter qualquer objeto de sua prancheta em um controle, ou pode basear seu modelo em um controle existente.

Para converter qualquer objeto em um modelo de controle, selecione o objeto e, em seguida, no menu **Ferramentas**, escolha **Transformar em Controle**.

Se você quiser basear seu modelo em um controle existente, selecione um objeto na prancheta. Depois, na parte superior da prancheta, escolha o botão de navegação estrutural, escolha **Editar Modelo** e, em seguida, escolha **Editar uma Cópia** ou **Criar Vazio**.

![Menu Editar Modelo](../designers/media/5ebdb33f-aad2-4c10-a328-5e8b04c56a36.png)

Para criar um estilo, selecione o objeto e, no menu **Objeto**, escolha **Editar Estilo**e escolha **Editar uma Cópia** ou **Criar Vazio**.

- Escolha **Editar uma Cópia** para iniciar com o estilo ou modelo padrão do controle.

- Escolha **Criar Vazio** para começar do zero.

A opção **Editar Atual** só aparecerá se você editar um estilo ou modelo já criado. Ela não aparecerá para um controle que ainda esteja usando um modelo padrão do sistema.

Na caixa de diálogo **Criar Recurso de Estilo**, você pode nomear o estilo ou modelo para que possa usá-lo posteriormente, ou pode aplicar o estilo ou modelo a todos os controles desse tipo.

![Caixa de diálogo Criar Recurso de Estilo](../designers/media/4818ee6a-ce60-4b79-91c8-3b1871829eea.png)

> [!NOTE]
> Você não pode criar estilos ou modelos para todos os tipos de controles. Se o controle não der suporte a eles, o botão de navegação estrutural não aparecerá acima da prancheta.
> Para retornar ao escopo de edição de seu documento principal, clique em **Retornar escopo para** ![Ícone de Retornar escopo para](../designers/media/55844eb3-ed98-4f20-aa66-a6f5b23eeb2b.png).

### <a name="apply-a-style-or-template-to-a-control"></a>Aplicar um estilo ou modelo a um controle

Clique com o botão direito do mouse em um objeto no painel [Objetos e Linha do Tempo](../designers/creating-a-ui-by-using-blend-for-visual-studio.md#tour-of-the-objects-and-timeline-panel), escolha **Editar Modelo** e escolha**Aplicar Recurso**.

![Menu Aplicar Recurso](../designers/media/dc12debc-7711-47d9-84ce-10322a384397.png)

### <a name="restore-the-default-style-or-template-of-a-control"></a>Restaurar o estilo ou modelo padrão de um controle

Selecione o controle e, no painel [Propriedades](../designers/creating-a-ui-by-using-blend-for-visual-studio.md#tour-of-the-properties-panel), localize a propriedade **Estilo** ou **Modelo**. Escolha **Opções avançadas** e clique em **Redefinir** no menu de atalho.

## <a name="visual-states-change-the-appearance-of-a-control-based-on-its-state"></a>Estados visuais: Alterar a aparência de um controle com base em seu estado

Os controles podem ter aparências diferentes com base nas interações do usuário. Por exemplo, você pode fazer um botão ficar verde quando um usuário clica nele, ou pode executar uma animação. Reduza ou aumente o tempo entre estados visuais usando transições.

![Mouse sobre o estado](../designers/media/a95c671a-5639-40b9-83db-1e6b214330d5.png)

**Assista a um vídeo curto:** ![botão Reproduzir](../designers/media/bldadminconsoleinitialconfigicon.PNG) [Gerenciar o estado dos controles WPF](https://www.youtube.com/watch?v=m0PlkF5i6uw).

## <a name="resources-create-colors-styles-and-templates-and-reuse-them-later"></a>Recursos: Criar cores, estilos e modelos e reutilizá-los posteriormente

Converta qualquer coisa em seu projeto em um recurso. Um recurso é apenas um objeto que pode ser reutilizado em locais diferentes de seu aplicativo. Por exemplo, você pode criar uma cor uma vez, torná-la um recurso e, depois, usar essa cor em vários objetos. Para alterar a cor de todos os objetos, basta alterar o recurso de cor.

![Botão Converter cores em recurso](../designers/media/89203705-cf66-46e0-b153-52a23cd744f7.png) ![Caixa de diálogo Criar Recurso de Cor](../designers/media/6bff8b19-3cd5-41a0-bbf9-ff65532d5aae.png)

## <a name="see-also"></a>Consulte também

- [Criando uma interface do usuário usando o Blend for Visual Studio](../designers/creating-a-ui-by-using-blend-for-visual-studio.md)