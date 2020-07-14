---
title: Como adicionar diagramas de classe a projetos (Designer de Classe)
ms.date: 05/08/2018
ms.topic: how-to
helpviewer_keywords:
- class diagrams, creating
- Class Designer [Visual Studio], opening
ms.assetid: 0eac1b54-2711-4e4b-9654-a0c429c08c8f
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a54b01f718c2faab8d36cc8e44805707fd0cc35f
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771035"
---
# <a name="how-to-add-class-diagrams-to-projects"></a>Como adicionar diagramas de classe a projetos

Para criar, editar e refatorar classes e outros tipos, adicione um diagrama de classe ao projeto em C#, Visual Basic ou C++. Para visualizar diferentes partes do código em um projeto, adicione vários diagramas de classes ao projeto.

Não é possível criar diagramas de classes a partir de projetos que compartilham o código por meio de diversos aplicativos. Para criar diagramas de classe UML, consulte [Criar diagramas e projetos de modelagem UML](../../modeling/what-s-new-for-design-in-visual-studio.md).

## <a name="install-the-class-designer-component"></a>Instalar o componente do Designer de Classe

Se você não tiver instalado o componente do **Designer de Classe**, siga estas etapas para instalá-lo.

1. Abra o **Instalador do Visual Studio** no menu Iniciar do Windows ou selecionando **Ferramentas** > **Obter Ferramentas e Recursos** na barra de menus no Visual Studio.

   O **Instalador do Visual Studio** é aberto.

1. Selecione a guia **Componentes individuais** e, em seguida, role para baixo até a categoria **Ferramentas de código**.

1. Selecione **Designer de Classe** e, em seguida, selecione **Modificar**.

   ![Componente do Designer de Classe no Instalador do Visual Studio](media/class-designer-component.png)

   O componente do **Designer de Classe** inicia a instalação.

## <a name="add-a-blank-class-diagram-to-a-project"></a>Adicionar um diagrama de classe em branco a um projeto

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto e escolha **Adicionar** > **Novo Item**. Ou pressione **Ctrl** + **Shift** + **A**.

   A caixa de diálogo **Adicionar novo item** é aberta.

2. Expanda **itens comuns**  >  **geral**e, em seguida, selecione **diagrama de classe** na lista modelo. Para projetos do Visual C++, examine a categoria **Utilitário** para localizar o modelo **Diagrama de Classe**.

   > [!NOTE]
   > Se você não vir o modelo **Diagrama de Classe**, [siga as etapas](#install-the-class-designer-component) para instalar o componente do **Designer de Classe** para o Visual Studio.

   O diagrama de classe é aberto no Designer de Classe e é exibido como um arquivo que tem uma extensão *.cd* no **Gerenciador de Soluções**. É possível arrastar formas e linhas para o diagrama da **Caixa de ferramentas**.

Para adicionar vários diagramas de classes, repita as etapas deste procedimento.

## <a name="add-a-class-diagram-based-on-existing-types"></a>Adicionar um diagrama de classe com base em tipos existentes

No **Gerenciador de Soluções**, abra o menu de contexto de um arquivo de classe (clique com o botão direito do mouse) e escolha **Exibir em Diagrama de Classe**.

-ou-

No **Modo de Exibição de Classe**, abra o namespace ou o menu de contexto de tipo e escolha **Exibir Diagrama de Classe**.

> [!TIP]
> Se **modo de exibição de classe** não estiver aberto, abra **modo de exibição de classe** no menu **Exibir** .

## <a name="to-display-the-contents-of-a-complete-project-in-a-class-diagram"></a>Para exibir o conteúdo de um projeto completo em um diagrama de classe

Em **Gerenciador de soluções** ou modo de exibição de classe, clique com o botão direito do mouse no projeto e escolha **Exibir**e, em seguida, escolha **Exibir diagrama de classe**.

Um diagrama de classe populado automaticamente é criado.

> [!NOTE]
> O Designer de Classe não está disponível nos projetos .NET Core.

## <a name="see-also"></a>Confira também

- [Como criar tipos usando o Designer de Classe](how-to-create-types.md)
- [Como exibir tipos existentes](how-to-view-existing-types.md)
- [Criar e exibir classes e tipos](designing-and-viewing-classes-and-types.md)
