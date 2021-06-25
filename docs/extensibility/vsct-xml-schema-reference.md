---
title: Referência de esquema XML do VSCT | Microsoft Docs
description: Os artigos de referência de esquema XML do VSCT descrevem elementos de esquema do Compilador de Tabela de Comando, com elementos filho e atributos permitidos para cada um.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Visual Studio command table configuration files (VSCT), XML schema
- VSCT XML schema elements
ms.assetid: 49e7efae-e713-4762-a824-96fdaf92cdc9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7d82cda9c91642b094deea50eda02676f9bb73f3
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905222"
---
# <a name="vsct-xml-schema-reference"></a>Referência de esquema XML do VSCT
Fornece uma tabela de elementos de esquema do Compilador de Tabela de Comando, com elementos filho e atributos permitidos para cada um.

 Um arquivo de configuração de tabela de comando baseado em XML (.vsct) define os elementos de comando que um VSPackage fornece ao IDE (ambiente de desenvolvimento integrado). Esses elementos incluem itens de menu, menus, barras de ferramentas e caixas de combinação.

> [!NOTE]
> O compilador do VSCT pode executar um pré-processador no arquivo .vsct. Como esse normalmente é o pré-processador do C++, você pode definir as macros e includes que têm a mesma sintaxe usada em arquivos C++. Exemplos disso são fornecidos no arquivo .vsct que o assistente **novo** projeto cria para um projeto VSPackage.

## <a name="optional-elements"></a>Elementos opcionais
 Alguns elementos VSCT são opcionais. Se um `Parent` argumento não for especificado, Group_Undefined:0 será implícito. Se um `Icon` argumento não for especificado, guidOfficeIcon:msotcidNoIcon será implícito. Quando uma tecla de atalho é definida, a emulação, que normalmente não éusada, é opcional.

 Os itens de bitmap podem ser inseridos no tempo de compilação especificando o local da faixa de bitmap no `href` argumento . A faixa de bitmap é copiada durante a mesclagem em vez de extraída dos recursos da DLL. Quando um `href` argumento é fornecido, o `usedList` argumento se torna opcional e todos os slots na faixa de bitmap são considerados usados.

 Todos os valores de GUID e ID devem ser definidos usando nomes simbólicos. Esses nomes podem ser definidos em arquivos de header ou em seções \<Symbols> do VSCT. Os nomes simbólicos devem ser locais, incluídos por \<Include> meio de elementos ou referenciados por \<Extern> elementos. Um nome simbólico será importado de um arquivo de título especificado em um elemento se seguir o padrão simples de #define \<Extern> SYMBOL VALUE. O valor pode ser outro símbolo, desde que esse símbolo tenha sido definido anteriormente. As definições de GUID devem seguir o formato OLE ou C++. Os valores de ID podem ser dígitos decimais ou dígitos hexadecimais precedido por 0x, conforme mostrado nas seguintes linhas:

- {6D484634-E53D-4a2c-ADCB-55145C9362C8}

- { 0x6d484634, 0xe53d, 0x4a2c, { 0xad, 0xcb, 0x55, 0x14, 0x5c, 0x93, 0x62, 0xc8 } } }

  Comentários XML podem ser usados, mas ferramentas de GUI (interface gráfica do usuário) de ida e volta podem descartá-los. É garantido que \<Annotation> o conteúdo dos elementos seja mantido independentemente do formato.

## <a name="schema-hierarchy"></a>Hierarquia de esquema
 Um arquivo .vsct tem os seguintes elementos principais.

- [Elemento CommandTable](../extensibility/commandtable-element.md)

- [Elemento Extern](../extensibility/extern-element.md)

- [Elemento Include](../extensibility/include-element.md)

- [Definir elemento](../extensibility/define-element.md)

- [Elemento Commands](../extensibility/commands-element.md)

- [Elemento CommandPlacements](../extensibility/commandplacements-element.md)

- [Elemento VisibilityConstraints](../extensibility/visibilityconstraints-element.md)

- [Elemento KeyBindings](../extensibility/keybindings-element.md)

- [Elemento UsedCommands](../extensibility/usedcommands-element.md)

- [Elemento pai](../extensibility/parent-element.md)

- [Elemento Icon](../extensibility/icon-element.md)

- [Elemento Strings](../extensibility/strings-element.md)

- [Elemento Command Flag](../extensibility/command-flag-element.md)

- [Elemento Symbols](../extensibility/symbols-element.md)

- [Atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md)

## <a name="see-also"></a>Confira também
- [Como o VSPackages adiciona elementos de interface do usuário](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Roteamento de comando no VSPackages](../extensibility/internals/command-routing-in-vspackages.md)
