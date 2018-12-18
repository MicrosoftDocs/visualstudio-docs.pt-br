---
title: Diretrizes de posicionamento de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, small command sets
- small command sets
- command sets
ms.assetid: 63b3478e-e08a-420b-a0ec-76767e0cb289
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: bac09a361c885d866bf6a78e6fe7b49c246265ba
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39511180"
---
# <a name="command-placement-guidelines"></a>Diretrizes de posicionamento do comando
Práticas recomendadas para comandos de posicionamento no ambiente de desenvolvimento integrado (IDE) do Visual Studio variam dependendo do tamanho do conjunto de comandos. Comandos são definidos e posicionados de acordo com as informações em *VSCT* arquivos.  
  
## <a name="best-practices-for-all-command-sets"></a>Práticas recomendadas para todos os conjuntos de comandos  
 Para cada conjunto de comandos, siga estas diretrizes:  
  
-   Prepare um gráfico da estrutura de comando com antecedência. Identifique os comandos, caixas de combinação, grupos de comando e menus de atalho que serão usados em mais de um único local.  
  
-   Comandos que aparecem no mesmo grupo devem estar relacionados.  
  
-   Grupos que contêm apenas um comando são aceitáveis.  
  
-   Pacotes não devem adicionar muitos dos comandos a menus existentes do Visual Studio. Em vez disso, eles devem criar menus ou submenus para hospedar os novos comandos.  
  
-   Quando você colocar um comando em um menu existente, nome de comando para que sua finalidade é clara e ela não será ser confundida com os comandos existentes.  
  
## <a name="best-practices-for-small-command-sets"></a>Práticas recomendadas para conjuntos de comandos pequeno  
 Se você estiver desenvolvendo um VSPackage que tenha apenas alguns comandos, também siga estas diretrizes:  
  
-   Quando possível, use o [pai](../../extensibility/parent-element.md) elemento de um comando, caixa de combinação, grupo ou menu filho para colocá-lo no grupo apropriado.  
  
-   Atribua grupos aos menus exibidos pelo VSPackage.  
  
-   O pai de um menu filho ou um comando deve ser um [grupo](../../extensibility/group-element.md) elemento. Atribuir comandos e menus filho aos grupos e, em seguida, atribua os grupos aos menus pai.  
  
-   Você pode colocar um comando em grupos adicionais com a adição de um [CommandPlacements](../../extensibility/commandplacements-element.md) seção do elemento após a definição do comando e, em seguida, adicionando ao `CommandPlacements` elemento uma [CommandPlacement](../../extensibility/commandplacement-element.md) elemento para cada grupo adicional.  
  
## <a name="best-practices-for-large-command-sets"></a>Práticas recomendadas para conjuntos grandes de comando  
 Se o VSPackage terá muitos comandos que serão exibido em vários contextos, também siga estas diretrizes:  
  
-   Verifique os menus, grupos e comandos de gerenciamento automaticamente do domínio pai. Ou seja, não atribua um `Parent` elemento na definição do item.  
  
-   Use `CommandPlacement` entradas do elemento no `CommandPlacements` seção do elemento para colocar os menus, grupos e comandos em seus menus pai e grupos.  
  
-   No `CommandPlacements` seção do elemento, as entradas que preenchem um determinado menu ou grupo devem ser adjacentes um ao outro. Isso auxilia na legibilidade e torna o `Priority` classificações mais fácil de determinar.  
  
## <a name="see-also"></a>Consulte também  
 [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [Arquivos de tabela (. VSCT) de comando do Visual Studio](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)