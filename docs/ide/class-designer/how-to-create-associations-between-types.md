---
title: Como criar associações entre tipos (Designer de Classe)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.associationline
helpviewer_keywords:
- types [Visual Studio], associations
- association lines, defining (Class Designer)
- defining association lines (Class Designer)
- associations, types
- association lines
ms.assetid: adccb9c8-2f8a-4086-9fa9-f70f99fb6e00
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0b27530abeec1c01b5537fd91bfbe3e0e10448af
ms.sourcegitcommit: 4c0db930d9d5d8b857d3baf2530ae89823799612
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "33958549"
---
# <a name="how-to-create-associations-between-types-in-class-designer"></a>Como criar associações entre tipos no Designer de Classe

As linhas de associação no **Designer de Classe** mostram como as classes em um diagrama são relacionadas. Uma linha de associação representa uma classe que é o tipo de uma propriedade ou de um campo de outra classe no seu projeto. As linhas de associação geralmente são usadas para ilustrar as relações mais importantes entre classes do projeto.

Embora você possa exibir todos os campos e propriedades como associações, faz mais sentido mostrar apenas membros importantes como associações, dependendo do que você pretende enfatizar no diagrama. (É possível mostrar membros menos importantes como membros regulares ou ocultá-los no geral.)

> [!NOTE]
> O **Designer de Classe** é compatível com apenas associações unidirecionais.

## <a name="to-define-an-association-line-in-the-class-diagram"></a>Para definir uma linha de associação no Diagrama de Classes

1. Na Caixa de Ferramentas, em **Designer de Classe**, selecione **Associação**.

2. Desenhe uma linha entre as duas formas que deseja vincular a uma associação.

     Uma nova propriedade é criada na primeira classe. Essa propriedade é exibida como uma linha de associação (não como uma propriedade em um compartimento na forma) com um nome padrão. Seu tipo é a forma para a qual a linha de associação aponta.

## <a name="to-change-the-name-of-an-association"></a>Para alterar o nome de uma associação

Na superfície de diagrama, clique no rótulo da linha de associação e edite-o.

Ou siga estas etapas:

1. Selecione a forma que contém a propriedade mostrada como uma associação.

   A forma obtém foco e seus membros são exibidos nas janelas **Detalhes da Classe** e **Propriedades**.

2. Na janela **Detalhes da Classe** ou **Propriedades**, edite o campo de nome dessa propriedade e pressione **Enter**.

   O nome é atualizado na janela **Detalhes da Classe**, na linha de associação, na janela **Propriedades** e no código.

## <a name="see-also"></a>Consulte também

- [Como alternar entre notação de membro e notação de associação](how-to-change-between-member-notation-and-association-notation.md)
