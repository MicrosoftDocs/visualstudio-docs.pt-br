---
title: Posicionamento do comando, grupo e barra de ferramentas padrão | Microsoft Docs
description: Saiba mais sobre os comandos do IDE, os comandos do produto e os comandos do editor, que a interface do usuário do Visual Studio exibe por padrão.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands [Visual Studio], default groups
- toolbars [Visual Studio], default
- commands [Visual Studio], default editor
- command groups
- commands [Visual Studio], default IDE
- commands [Visual Studio], default product
ms.assetid: 35342110-d639-4577-8367-00b21dcc6f07
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 07e93db9ffe79c3c49072b3379def14a3be2852c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091000"
---
# <a name="default-command-group-and-toolbar-placement"></a>Posicionamento do comando, grupo e barra de ferramentas padrão
Para a uniformidade e a estabilidade do produto, a interface do usuário exibe determinados grupos de comandos por padrão e [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] fornece definições para comandos e grupos de comandos. O VSPackages também pode usar os comandos padrão e os grupos de comandos.

 Os grupos de comandos padrão se enquadram em três categorias: comandos do IDE, comandos do produto e comandos do editor.

## <a name="default-ide-commands"></a>Comandos padrão do IDE
 A barra de ferramentas padrão do IDE inclui comandos compartilhados por todos os produtos contidos no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Isso inclui comandos relacionados a operações de projeto genéricas, como o comando **Save** e o comando **Add Item** . VSPackages não deve adicionar ou subtrair dessa barra de ferramentas, com uma exceção: se o produto ou o VSPackage adicionar uma nova janela de ferramenta, a janela deverá ser adicionada à lista de janelas de ferramentas disponíveis no menu **Exibir** . Novos produtos ou VSPackages podem adicionar sua própria barra de ferramentas.

## <a name="default-product-commands"></a>Comandos de produto padrão
 Cada produto pode fornecer ao IDE sua própria barra de ferramentas padrão que contém comandos importantes e frequentemente usados. No entanto, é melhor usar menus e barras de ferramentas existentes sempre que possível e complementá-los com outras barras de ferramentas específicas da tarefa, conforme necessário.

 O campo prioridade de uma barra de ferramentas determina seu posicionamento de linha. Prioridade zero coloca a barra de ferramentas na terceira linha (linha 3), abaixo da barra de menus (linha 1) e da barra de ferramentas **padrão** (linha 2). Portanto, outras barras de ferramentas aparecem na linha (prioridade + 3). As barras de ferramentas subsequentes são colocadas na mesma linha, se houver espaço; caso contrário, elas serão automaticamente movidas para a próxima linha.

## <a name="default-editor-commands"></a>Comandos do editor padrão
 Um VSPackage que fornece um editor personalizado deve fornecer uma barra de ferramentas padrão que contenha os comandos mais importantes e frequentemente usados nesse editor. A barra de ferramentas do editor deve aparecer quando o editor está ativo e deve ser ocultada quando o editor não está ativo. Essa visibilidade é controlada no `VisibilityConstraints` elemento do arquivo *. vsct* .

 As barras de ferramentas do editor devem ser colocadas abaixo das barras de ferramentas do IDE e do produto.

## <a name="see-also"></a>Confira também
- [Comandos, menus e grupos definidos pelo IDE](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)
- [Como VSPackages adicionar elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
