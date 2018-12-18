---
title: Modificar o estilo de objetos no Blend | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 31192d2c-5b84-41bc-94c0-898638c170bd
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 70bf451a828e3884a6004f6304b91351e866ee52
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49843619"
---
# <a name="modify-the-style-of-objects-in-blend"></a>Modificar o estilo de objetos no Blend
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A maneira mais fácil de personalizar um objeto é definir as propriedades no painel **Propriedades**.  
  
 Se você quiser reutilizar configurações ou grupos de configurações, crie um recurso reutilizável. Pode ser um *estilo*, *modelo*, ou algo simples como uma cor personalizada. Você também pode fazer um controle aparecer diferentemente com base em seu estado. Por exemplo, um botão muda para verde quando o usuário clica nele.  
  
 **Neste tópico**:  
  
-   [Pincéis: Modificar a aparência de um objeto](#Brushes)  
  
-   [Estilos e modelos: criar uma aparência consistente entre os controles](#Styles)  
  
-   [Estados visuais: alterar a aparência de um controle com base em seu estado](#Visual)  
  
-   [Recursos: criar cores, estilos e modelos e reutilizá-los posteriormente](#Resources)  
  
##  <a name="Brushes"></a> Pincéis: Modificar a aparência de um objeto  
 Aplique um pincel a um objeto se você quiser alterar sua aparência.  
  
 **Assista a um breve vídeo:** ![Configurar recursos instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Editor de Pincéis](http://www.popscreen.com/v/6A4mO/Microsoft-Expression-Blend-The-Brushes-Editor).  
  
### <a name="paint-a-repeating-image-or-pattern-on-an-object"></a>Pinte uma imagem ou padrão de repetição em um objeto  
 Pinte uma imagem ou padrão de repetição em um objeto usando um *pincel de bloco*.  
  
 Para criar um pincel de bloco, comece criando um *pincel de imagem*, *pincel de desenho* ou *pincel visual*.  
  
 Crie um pincel de imagem usando uma imagem. As ilustrações a seguir mostram o pincel de imagem, o pincel de imagem lado a lado e o pincel de imagem invertido.  
  
 ![](../designers/media/81f84f56-906d-456b-8288-d77da1e01e31.png "81f84f56-906d-456b-8288-d77da1e01e31") ![](../designers/media/d3782ca8-64da-47a4-a095-c6cdd0fa47a2.png "d3782ca8-64da-47a4-a095-c6cdd0fa47a2") ![](../designers/media/38ae3691-f3f1-4a1e-82ca-c7fa164bf56e.png "38ae3691-f3f1-4a1e-82ca-c7fa164bf56e")  
  
 Crie um pincel de desenho usando um desenho vetorial como um caminho ou uma forma. As ilustrações a seguir mostram o pincel de desenho, o pincel de desenho lado a lado e o pincel de desenho invertido.  
  
 ![](../designers/media/197666ac-ef57-4c5c-9779-669e991a00a5.png "197666ac-ef57-4c5c-9779-669e991a00a5") ![](../designers/media/ba09cda3-4cee-40ba-b3d4-edc032158bdc.png "ba09cda3-4cee-40ba-b3d4-edc032158bdc") ![](../designers/media/15bf6021-620c-4490-9eae-086153d3f14f.png "15bf6021-620c-4490-9eae-086153d3f14f")  
  
 Crie um pincel visual a partir de um controle, como um botão. As ilustrações a seguir mostram o pincel visual e o pincel visual lado a lado.  
  
 ![](../designers/media/fb6c90e0-153c-48fe-b563-e601beac6227.png "fb6c90e0-153c-48fe-b563-e601beac6227") ![](../designers/media/e261b99f-7d8f-4d91-bc84-19c7beccc255.png "e261b99f-7d8f-4d91-bc84-19c7beccc255")  
  
 **Assista a um breve vídeo:** ![Configure Installed Features (Configurar recursos instalados)](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Pincéis de Bloco](http://www.popscreen.com/v/6A4iM/Microsoft-Expression-Blend-Tile-Brushes).  
  
##  <a name="Styles"></a>Estilos e modelos: Criar uma aparência consistente entre os controles  
 Você pode criar uma vez a aparência e o comportamento de um controle uma vez e aplicar esse design a outros controles, para que você não precise mantê-los individualmente.  
  
 **Você deve usar um estilo?** : se você só quiser definir as propriedades padrão (como a cor de um botão), use um *estilo*. Modifique um controle, mesmo após aplicar um estilo a ele.  
  
 **Você deve usar um modelo?**: se você quiser alterar a estrutura de um controle, use um *modelo*. Imagine a conversão de um gráfico ou logotipo em um botão. Não é possível modificar um controle depois de aplicar um estilo a ele.  
  
### <a name="create-a-template-or-style"></a>Criar um modelo ou estilo  
 Há duas maneiras de criar um modelo. Você pode converter qualquer objeto de sua prancheta em um controle, ou pode basear seu modelo em um controle existente.  
  
 Para converter qualquer objeto em um modelo de controle, selecione o objeto e, em seguida, no menu **Ferramentas**, escolha **Transformar em Controle**.  
  
 Se você quiser basear seu modelo em um controle existente, selecione um objeto na prancheta. Depois, na parte superior da prancheta, escolha o botão de navegação estrutural, escolha **Editar Modelo** e, em seguida, escolha **Editar uma Cópia** ou **Criar Vazio**.  
  
 ![](../designers/media/5ebdb33f-aad2-4c10-a328-5e8b04c56a36.png "5ebdb33f-aad2-4c10-a328-5e8b04c56a36")  
  
 Para criar um estilo, selecione o objeto e, no menu **Objeto**, escolha **Editar Estilo**e escolha **Editar uma Cópia** ou **Criar Vazio**.  
  
- Escolha **Editar uma Cópia** para iniciar com o estilo ou modelo padrão do controle.  
  
- Escolha **Criar Vazio** para começar do zero.  
  
  A opção **Editar Atual** só aparecerá se você editar um estilo ou modelo já criado. Ela não aparecerá para um controle que ainda está usando um modelo de sistema padrão.  
  
  Na caixa de diálogo **Criar Recurso de Estilo**, você pode nomear o estilo ou modelo para que possa usá-lo posteriormente, ou pode aplicar o estilo ou modelo a todos os controles desse tipo.  
  
  ![](../designers/media/4818ee6a-ce60-4b79-91c8-3b1871829eea.png "4818ee6a-ce60-4b79-91c8-3b1871829eea")  
  
> [!NOTE]
>  Você não pode criar estilos ou modelos para cada tipo de controle. Se um controle não oferecer suporte a eles, o botão de navegação estrutural não aparecerá acima da prancheta.  
>   
>  Para retornar ao escopo de edição de seu documento principal, clique em **Retornar escopo para** ![](../designers/media/55844eb3-ed98-4f20-aa66-a6f5b23eeb2b.png "55844eb3-ed98-4f20-aa66-a6f5b23eeb2b").  
>   
>  ![](../designers/media/4a5612e1-7a28-4587-b870-0fe7112ec2ad.png "4a5612e1-7a28-4587-b870-0fe7112ec2ad")  
  
 **Assista a um breve vídeo:** ![Configurar recursos instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Criar um estilo](http://www.microsoft.com/showcase/details.aspx?uuid=9b8e86e2-8e90-4d61-81af-fa5b5afb3e95).  
  
 **Assista a um breve vídeo:** ![Configurar recursos instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Criar um modelo de controle no Expression Blend](http://msdn.microsoft.com/expression/cc263912.aspx).  
  
### <a name="apply-a-style-or-template-to-a-control"></a>Aplicar um estilo ou modelo a um controle  
 Clique com o botão direito do mouse em um objeto no painel [Objetos e Linha do Tempo](http://msdn.microsoft.com/en-us/135a5a5e-ec6d-4f38-8827-60e284cd5f57), escolha **Editar Modelo** e escolha**Aplicar Recurso**.  
  
 ![](../designers/media/dc12debc-7711-47d9-84ce-10322a384397.png "dc12debc-7711-47d9-84ce-10322a384397")  
  
### <a name="restore-the-default-style-or-template-of-a-control"></a>Restaurar o estilo ou modelo padrão de um controle  
 Selecione o controle e, no painel [Propriedades](http://msdn.microsoft.com/en-us/135a5a5e-ec6d-4f38-8827-60e284cd5f57), localize a propriedade **Estilo** ou **Modelo**. Em seguida, clique em **Opções avançadas** ![](../designers/media/12e06962-5d8a-480d-a837-e06b84c545bb.png "12e06962-5d8a-480d-a837-e06b84c545bb") e clique em **Redefinir** no menu de atalho.  
  
##  <a name="Visual"></a>Estados visuais: Alterar a aparência de um controle com base em seu estado  
 Os controles podem ter aparências diferentes com base nas interações do usuário. Por exemplo, você pode fazer um botão ficar verde quando um usuário clica nele, ou pode executar uma animação. Reduza ou aumente o tempo entre estados visuais usando transições.  
  
 ![](../designers/media/a95c671a-5639-40b9-83db-1e6b214330d5.png "a95c671a-5639-40b9-83db-1e6b214330d5")  
  
 **Assista a um breve vídeo:** ![Configurar recursos instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Gerenciar o estado de seus controles WPF](https://www.youtube.com/watch?v=m0PlkF5i6uw).  
  
##  <a name="Resources"></a>Recursos: Criar cores, estilos e modelos e reutilizá-los posteriormente  
 Converta qualquer coisa em seu projeto em um recurso. Um recurso é apenas um objeto que pode ser reutilizado em locais diferentes de seu aplicativo. Por exemplo, você pode criar uma cor uma vez, torná-la um recurso e, depois, usar essa cor em vários objetos. Para alterar a cor de todos os objetos, basta alterar o recurso de cor.  
  
 ![](../designers/media/89203705-cf66-46e0-b153-52a23cd744f7.png "89203705-cf66-46e0-b153-52a23cd744f7") ![](../designers/media/6bff8b19-3cd5-41a0-bbf9-ff65532d5aae.png "6bff8b19-3cd5-41a0-bbf9-ff65532d5aae")  
  
 **Assista a um breve vídeo:** ![Configurar recursos instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Um breve resumo sobre recursos](http://www.popscreen.com/v/6A4k7/Microsoft-Expression-Blend-Brief-Touch-on-Resources).  
  
## <a name="see-also"></a>Consulte também  
 [Criando uma interface do usuário usando o Blend for Visual Studio](../designers/creating-a-ui-by-using-blend-for-visual-studio.md)



