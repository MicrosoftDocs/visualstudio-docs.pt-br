---
title: 'Como: Criar e remover dependências de projeto'
ms.date: 06/21/2017
ms.topic: conceptual
f1_keywords:
- VS.ProjectDependenciesDlg
helpviewer_keywords:
- vs.build.projectdependencies
- project dependencies
- builds [Visual Studio], setting up
- project build configurations, dependencies
- dependencies, project
- projects [Visual Studio], dependencies
ms.assetid: e2a0a8ff-dae7-40a8-b774-b88aa5235183
ms.technology: vs-ide-compile
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ce26c74aced2dd979f9f9847d5c56ead30f897ce
ms.sourcegitcommit: 59e5758036223ee866f3de5e3c0ab2b6dbae97b6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68415594"
---
# <a name="how-to-create-and-remove-project-dependencies"></a>Como: Criar e remover dependências de projeto

Ao compilar uma solução que contém vários projetos, pode ser necessário compilar determinados projetos primeiro, para gerar o código usado por outros projetos. Quando um projeto consome o código executável gerado por outro projeto, o projeto que gera o código é chamado de uma dependência de projeto do projeto que consome o código. Esses relacionamentos de dependência podem ser definidos na caixa de diálogo **Dependências do Projeto**.

## <a name="to-assign-dependencies-to-projects"></a>Para atribuir dependências a projetos

1. No **Gerenciador de Soluções**, selecione um projeto.

2. No menu **Projeto**, escolha **Dependências do Projeto**.

    A caixa de diálogo **Dependências do Projeto** é aberta.

   > [!NOTE]
   > A opção **Dependências do Projeto** está disponível apenas em uma solução com mais de um projeto.

3. Na guia **Dependências**, selecione um projeto no menu suspenso **Projeto**.

4. No campo **Depende de**, marque a caixa de seleção de qualquer outro projeto que deve ser compilado antes desse projeto.

   A solução deve consistir em mais de um projeto antes que seja possível criar dependências de projeto.

## <a name="to-remove-dependencies-from-projects"></a>Para remover dependências de projetos

1. No **Gerenciador de Soluções**, selecione um projeto.

2. No menu **Projeto**, escolha **Dependências do Projeto**.

     A caixa de diálogo **Dependências do Projeto** é aberta.

    > [!NOTE]
    > A opção **Dependências do Projeto** está disponível apenas em uma solução com mais de um projeto.

3. Na guia **Dependências**, selecione um projeto no menu suspenso **Projeto**.

4. No campo **Depende de**, desmarque as caixas de seleção ao lado de outros projetos que não são mais dependências desse projeto.

## <a name="see-also"></a>Consulte também

- [Criar e limpar projetos e soluções no Visual Studio](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)
- [Compilação e build](../ide/compiling-and-building-in-visual-studio.md)
- [Compreender configurações de build](../ide/understanding-build-configurations.md)
- [Gerenciar propriedades do projeto e da solução](managing-project-and-solution-properties.md)
