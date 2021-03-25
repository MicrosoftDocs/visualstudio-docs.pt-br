---
title: Referência de esquema XML VSCT | Microsoft Docs
description: Os artigos de referência de esquema XML VSCT descrevem elementos de esquema de compilador de tabela de comando, com elementos filho e atributos permitidos para cada um.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio command table configuration files (VSCT), XML schema
- VSCT XML schema elements
ms.assetid: 49e7efae-e713-4762-a824-96fdaf92cdc9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9f24d11c9458b56b5b66de495a18ec75491d3ac0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062298"
---
# <a name="vsct-xml-schema-reference"></a>Referência de esquema XML VSCT
Fornece uma tabela de elementos de esquema de compilador de tabela de comando, com elementos filho permitidos e atributos para cada um.

 Um arquivo de configuração de tabela de comando (. vsct) baseado em XML define os elementos de comando que um VSPackage fornece ao IDE (ambiente de desenvolvimento integrado). Esses elementos incluem itens de menu, menus, barras de ferramentas e caixas de combinação.

> [!NOTE]
> O compilador VSCT pode executar um pré-processador no arquivo. vsct. Como esse é normalmente o pré-processador do C++, você pode definir inclusões e macros com a mesma sintaxe usada em arquivos C++. Exemplos disso são fornecidos no arquivo. vsct que o assistente de **novo projeto** cria para um projeto VSPackage.

## <a name="optional-elements"></a>Elementos opcionais
 Alguns elementos VSCT são opcionais. Se um `Parent` argumento não for especificado, Group_Undefined: 0 será implícito. Se um `Icon` argumento não for especificado, guidOfficeIcon: msotcidNoIcon será implícito. Quando uma tecla de atalho é definida, a emulação, que normalmente não é usada, é opcional.

 Itens de bitmap podem ser inseridos em tempo de compilação especificando o local da faixa de bitmap no `href` argumento. A faixa de bitmap é copiada durante a mesclagem em vez de extraída dos recursos da DLL. Quando um `href` argumento é fornecido, o `usedList` argumento torna-se opcional e todos os slots na faixa de bitmap são considerados usados.

 Todos os valores GUID e ID devem ser definidos usando nomes simbólicos. Esses nomes podem ser definidos em arquivos de cabeçalho ou em \<Symbols> seções vsct. Os nomes simbólicos devem ser locais, incluídos por meio de \<Include> elementos ou referenciados por \<Extern> elementos. Um nome simbólico é importado de um arquivo de cabeçalho especificado em um \<Extern> elemento se ele seguir o padrão simples de #define valor de símbolo. O valor pode ser outro símbolo, contanto que esse símbolo tenha sido definido anteriormente. As definições de GUID devem seguir o formato OLE ou C++. Os valores de ID podem ser dígitos decimais ou dígitos hexadecimais precedidos por 0x, conforme mostrado nas seguintes linhas:

- {6D484634-E53D-4a2c-ADCB-55145C9362C8}

- {0x6d484634, 0xe53d, 0x4a2c, {0xAD, 0xcb, 0x55, 0x14, 0x5c, 0x93, 0x62, 0xC8}}

  Os comentários XML podem ser usados, mas as ferramentas de GUI (interface gráfica do usuário) de ida e volta podem descartá-los. \<Annotation>É garantido que o conteúdo dos elementos seja mantido independentemente do formato.

## <a name="schema-hierarchy"></a>Hierarquia de esquema
 Um arquivo. vsct tem os seguintes elementos principais.

- [Elemento commandtable](../extensibility/commandtable-element.md)

- [Elemento externo](../extensibility/extern-element.md)

- [Elemento include](../extensibility/include-element.md)

- [Definir elemento](../extensibility/define-element.md)

- [Elemento Commands](../extensibility/commands-element.md)

- [Elemento CommandPlacements](../extensibility/commandplacements-element.md)

- [Elemento VisibilityConstraints](../extensibility/visibilityconstraints-element.md)

- [Elemento keybindings](../extensibility/keybindings-element.md)

- [Elemento UsedCommands](../extensibility/usedcommands-element.md)

- [Elemento pai](../extensibility/parent-element.md)

- [Elemento Icon](../extensibility/icon-element.md)

- [Elemento Strings](../extensibility/strings-element.md)

- [Elemento de sinalizador de comando](../extensibility/command-flag-element.md)

- [Elemento Symbols](../extensibility/symbols-element.md)

- [Atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md)

## <a name="see-also"></a>Confira também
- [Como VSPackages adicionar elementos da interface do usuário](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Roteamento de comandos em VSPackages](../extensibility/internals/command-routing-in-vspackages.md)
