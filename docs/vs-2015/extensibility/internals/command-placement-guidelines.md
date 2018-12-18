---
title: Diretrizes de posicionamento de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- commands, small command sets
- small command sets
- command sets
ms.assetid: 63b3478e-e08a-420b-a0ec-76767e0cb289
caps.latest.revision: 29
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 1729d4b5e65e60246926c1a3fd25342b10545068
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51731002"
---
# <a name="command-placement-guidelines"></a>Diretrizes de posicionamento de comando
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Práticas recomendadas para comandos de posicionamento no ambiente de desenvolvimento integrado (IDE) do Visual Studio variam dependendo do tamanho do conjunto de comandos. Comandos são definidos e posicionados de acordo com as informações em arquivos. VSCT.  
  
## <a name="best-practices-for-all-command-sets"></a>Práticas recomendadas para todos os conjuntos de comandos  
 Para cada conjunto de comandos, siga estas diretrizes:  
  
-   Prepare um gráfico da estrutura de comando com antecedência. Identifique os comandos, caixas de combinação, grupos de comando e menus de atalho que serão usados em mais de um único local.  
  
-   Comandos que aparecem no mesmo grupo devem estar relacionados.  
  
-   Grupos que contêm apenas um comando são aceitáveis.  
  
-   Pacotes não devem adicionar muitos dos comandos a menus existentes do Visual Studio. Em vez disso, eles devem criar menus ou submenus para hospedar os novos comandos.  
  
-   Quando você colocar um comando em um menu existente, nome de comando para que sua finalidade é clara e ela não será ser confundida com os comandos existentes.  
  
## <a name="best-practices-for-small-command-sets"></a>Práticas recomendadas para conjuntos de comandos pequeno  
 Se você estiver desenvolvendo um VSPackage que tenha apenas alguns comandos, também siga estas diretrizes:  
  
-   Quando possível, use o [elemento pai](../../extensibility/parent-element.md) de um comando, caixa de combinação, grupo ou menu filho para colocá-lo no grupo apropriado.  
  
-   Atribua grupos aos menus exibidos pelo VSPackage.  
  
-   O pai de um menu filho ou um comando deve ser um [elemento Group](../../extensibility/group-element.md). Atribuir comandos e menus filho aos grupos e, em seguida, atribua os grupos aos menus pai.  
  
-   Você pode colocar um comando em grupos adicionais com a adição de um [elemento CommandPlacements](../../extensibility/commandplacements-element.md) seção após a definição do comando e, em seguida, adicionando ao `CommandPlacements Element` um [elemento CommandPlacement](../../extensibility/commandplacement-element.md) para cada grupo adicional.  
  
## <a name="best-practices-for-large-command-sets"></a>Práticas recomendadas para conjuntos grandes de comando  
 Se o VSPackage terá muitos comandos que serão exibido em vários contextos, também siga estas diretrizes:  
  
-   Verifique os menus, grupos e comandos de gerenciamento automaticamente do domínio pai. Ou seja, não atribua um `Parent Element` na definição do item.  
  
-   Use `CommandPlacement Element` entradas na `CommandPlacements Element` seção colocar menus, grupos e comandos em seus menus pai e grupos.  
  
-   No `CommandPlacements` seção, as entradas que preenchem um determinado menu ou grupo deve ser adjacente um ao outro. Isso auxilia na legibilidade e torna o `Priority` classificações mais fácil de determinar.  
  
## <a name="see-also"></a>Consulte também  
 [Como os VSPackages adicionam elementos da Interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [Arquivos da tabela de comandos do Visual Studio (.Vsct)](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)

