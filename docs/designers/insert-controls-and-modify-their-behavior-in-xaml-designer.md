---
title: Inserir controles e modificar seu comportamento no XAML Designer
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: a80fff74-bf01-41c9-ab85-ada7a873c3a9
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: 739c43b0ed6665684f0a38b35dfd6eccdf8f5b2c
ms.sourcegitcommit: e5a382de633156b85b292f35e3d740f817715d47
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38977798"
---
# <a name="insert-controls-and-modify-their-behavior-in-xaml-designer"></a>Inserir controles e modificar seu comportamento no XAML Designer

Controles permitem que usuários interajam com seu aplicativo. Você pode usá-los para coletar informações e executar ações como animar um objeto ou consultar uma fonte de dados.

## <a name="add-controls-to-the-artboard"></a>Adicionar controles à prancheta

Você pode arrastar controles do painel **Ativos** para a **prancheta** e, em seguida, modificá-los na janela **Propriedades**.

![Controles guia de ativos do Blend](../designers/media/blend_assetsflipview_xaml.png)

### <a name="make-a-control-out-of-an-image-shape-or-path"></a>Fazer um controle de uma imagem, forma ou caminho

Você pode transformar qualquer objeto em um controle.

![Caixa de diálogo Transformar em Controle do Blend](../designers/media/blend_makeintocontrol_xaml.png)

Por exemplo, imagine uma imagem de uma televisão no centro da página. Você pode criar controles de imagens pequenas que se parecem com botões de televisão. Em seguida, os usuários podem clicar nesses botões para trocar de canal.

Isso é possível porque os botões agora são controles. Com controles, você pode responder às interações do usuário; Nesse caso, quando o usuário clica em um botão.

Para criar um controle, selecione um objeto. No menu **Ferramentas**, clique em **Transformar em Controle**.

## <a name="make-controls-do-things"></a>Fazer com que controles façam algo

Controles podem executar ações quando os usuários interagem com eles. Por exemplo, eles podem iniciar uma animação, atualizar uma fonte de dados ou reproduzir um vídeo.

Use *gatilhos*, *comportamentos* e *eventos* para fazer com que os controles façam coisas.

### <a name="triggers"></a>Gatilhos

O *gatilho* altera uma propriedade ou executa uma tarefa em resposta a um evento ou uma alteração em outra propriedade. Por exemplo, você pode alterar a cor de um botão quando os usuários passarem o mouse sobre ele.

![O painel Gatilhos](../designers/media/custom_button_blend_propertytriggerinfo.png)

### <a name="behaviors"></a>Comportamentos

Um *comportamento* é um pacote reutilizável de código. Ele pode fazer um pouco mais além de alterar as propriedades. Ele pode realizar ações como consultar um serviço de dados. O Blend é fornecido com uma pequena coleção de comportamentos, mas você pode adicionar mais. Arraste um comportamento para qualquer objeto na sua prancheta e personalize o comportamento configurando propriedades.

![FluidMoveBehavior no painel Propriedades](../designers/media/b4_fluidmovebehaviorproperties_sample.png)

**Assista a um vídeo:** ![Ícone de reprodução](../designers/media/bldadminconsoleinitialconfigicon.PNG) [Dicas de Blend: introdução ao uso de comportamentos Parte 1](http://www.bing.com/videos/search?q=Expression%20blend%20behaviors&qs=n&form=QBVR&pq=expression%20blend%20behavior&sc=4-25&sp=-1&sk=#view=detail&mid=CF0DD797ED84DE740904CF0DD797ED84DE740904).

### <a name="events"></a>Eventos

Para máxima flexibilidade, manipule um *evento*. Você precisará escrever um pouco de código.