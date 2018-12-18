---
title: Padrão de comando, o grupo e o posicionamento da barra de ferramentas | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands [Visual Studio], default groups
- toolbars [Visual Studio], default
- commands [Visual Studio], default editor
- command groups
- commands [Visual Studio], default IDE
- commands [Visual Studio], default product
ms.assetid: 35342110-d639-4577-8367-00b21dcc6f07
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: da5716460c428098b2b6cc3bb78a51c3831201b2
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39498224"
---
# <a name="default-command-group-and-toolbar-placement"></a>Posicionamento de comando, grupo e barra de ferramentas padrão
Para a uniformidade de produto e estabilidade, a interface do usuário exibe determinados grupos de comando por padrão, e [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] fornece definições de comandos e grupos de comando. Os VSPackages também pode usar os comandos padrão e os grupos de comando.  
  
 Os grupos de comando padrão se enquadram em três categorias: IDE comandos, comandos de produto e comandos do editor.  
  
## <a name="default-ide-commands"></a>Comandos do IDE padrão  
 A barra de ferramentas IDE padrão inclui comandos compartilhados por todos os produtos contidos em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. Eles incluem comandos relacionados a operações de projeto genérico, como o **salve** comando e o **Add Item** comando. Os VSPackages não deve adicionar a ou subtrair essa barra de ferramentas, com uma exceção: se o produto ou VSPackage adiciona uma nova janela de ferramenta, a janela deve ser adicionada à lista de janelas de ferramentas disponíveis na **exibição** menu. Novos produtos ou VSPackages pode adicionar suas próprias ferramentas.  
  
## <a name="default-product-commands"></a>Comandos de produto padrão  
 Cada produto pode fornecer o IDE com sua própria barra de ferramentas padrão que contém importantes e comandos usados com frequência. No entanto, é melhor, usar menus e barras de ferramentas sempre que possível existentes e complementá-los com outras barras de ferramentas de tarefas específicas, conforme necessário.  
  
 O campo de prioridade para uma barra de ferramentas determina seu posicionamento de linha. Zero a prioridade coloca a barra de ferramentas na terceira linha (linha 3), abaixo da barra de menu (linha 1) e o **Standard** barra de ferramentas (linha 2). Portanto, outras barras de ferramentas são exibidos na linha (prioridade + 3). Barras de ferramentas subsequentes são colocadas na mesma linha, se houver espaço; Caso contrário, eles são automaticamente movidos para a próxima linha.  
  
## <a name="default-editor-commands"></a>Comandos do editor padrão  
 Um VSPackage que fornece um editor personalizado deve fornecer uma barra de ferramentas padrão que contém o mais importante e comandos usados com frequência no editor. A barra de ferramentas do editor deve aparecer quando o editor está ativo e deve ser ocultado quando o editor não está ativo. Essa visibilidade é controlada na `VisibilityConstraints` elemento do *VSCT* arquivo.  
  
 Barras de ferramentas do Editor devem ser colocadas abaixo barras de ferramentas do IDE e produto.  
  
## <a name="see-also"></a>Consulte também  
 [Grupos, menus e comandos definidos pelo IDE](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)   
 [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)