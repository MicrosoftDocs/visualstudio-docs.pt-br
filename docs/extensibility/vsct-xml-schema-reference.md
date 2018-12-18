---
title: Referência de esquema XML do VSCT | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio command table configuration files (VSCT), XML schema
- VSCT XML schema elements
ms.assetid: 49e7efae-e713-4762-a824-96fdaf92cdc9
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 51be3e86f1f19cc3701dd456b3085d3e8993b7a8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49915549"
---
# <a name="vsct-xml-schema-reference"></a>Referência de esquema XML do VSCT
Fornece uma tabela de elementos de esquema do compilador de tabela de comando, com filho permitido elementos e atributos para cada um.  
  
 Um arquivo de configuração (. VSCT) da tabela de comando baseado em XML define os elementos de comando que fornece um VSPackage para o ambiente de desenvolvimento integrado (IDE). Esses elementos incluem itens de menu, menus, barras de ferramentas e caixas de combinação.  
  
> [!NOTE]
>  O compilador VSCT pode executar um pré-processador no arquivo. VSCT. Como isso é normalmente o pré-processador, que você pode definir C++ inclui e macros que têm a mesma sintaxe que é usada em arquivos de C++. Exemplos disso são fornecidos na. VSCT de arquivos que o **novo projeto** assistente cria para um projeto de VSPackage.  
  
## <a name="optional-elements"></a>Elementos opcionais  
 Alguns elementos VSCT são opcionais. Se um `Parent` argumento não for especificado, Group_Undefined:0 será implícita. Se um `Icon` argumento não for especificado, guidOfficeIcon:msotcidNoIcon será implícita. Quando uma tecla de atalho é definida, a emulação, que é normalmente usada, é opcional.  
  
 Itens de bitmap podem ser inseridos em tempo de compilação, especificando o local da faixa de bitmap no `href` argumento. A faixa de bitmap é copiada durante a mesclagem em vez de extraídos dos recursos da DLL. Quando um `href` argumento for fornecido, o `usedList` argumento torna-se opcional e todos os slots na faixa de bitmap são considerados usado.  
  
 Todos os valores GUID e ID devem ser definidos usando nomes simbólicos. Esses nomes podem ser definidos em arquivos de cabeçalho ou no VSCT \<símbolos > seções. Os nomes simbólicos devem ser locais, incluídos por meio \<Include > elementos, ou referenciada pela \<Extern > elementos. Um nome simbólico é importado de um arquivo de cabeçalho especificado em um \<Extern > elemento se ele segue o padrão simple de #define o valor de SÍMBOLO. O valor pode ser outro símbolo, desde que o símbolo foi definido anteriormente. Definições de GUID devem seguir o formato OLE ou C++. Valores de ID podem ser dígitos decimais ou dígitos hexadecimais que são precedidos por 0x, conforme mostrado nas linhas a seguir:  
  
- {6D484634-E53D-4a2c-ADCB-55145C9362C8}  
  
- {0x6d484634, 0xe53d, 0x4a2c, {0xad, 0xcb, 0x55, 0x14, 0x5c, 0x93, 0x62, 0xc8}}  
  
  Comentários XML podem ser usados, mas as ferramentas de GUI (interface) de ida e volta gráfica do usuário podem descartá-las. O conteúdo de \<anotação > elementos têm garantia de ser mantida, independentemente do formato.  
  
## <a name="schema-hierarchy"></a>Hierarquia de esquema  
 Um arquivo. VSCT tem os seguintes elementos principais.  
  
 [Elemento CommandTable](../extensibility/commandtable-element.md)  
  
 [Elemento extern](../extensibility/extern-element.md)  
  
 [Incluir elemento](../extensibility/include-element.md)  
  
 [Definir o elemento](../extensibility/define-element.md)  
  
 [Elemento Commands](../extensibility/commands-element.md)  
  
 [Elemento CommandPlacements](../extensibility/commandplacements-element.md)  
  
 [Element visibilityconstraints](../extensibility/visibilityconstraints-element.md)  
  
 [Elemento KeyBindings](../extensibility/keybindings-element.md)  
  
 [Elemento UsedCommands](../extensibility/usedcommands-element.md)  
  
 [Elemento pai](../extensibility/parent-element.md)  
  
 [Elemento Icon](../extensibility/icon-element.md)  
  
 [Elemento de cadeias de caracteres](../extensibility/strings-element.md)  
  
 [Elemento Command Flag](../extensibility/command-flag-element.md)  
  
 [Elemento Symbols](../extensibility/symbols-element.md)  
  
 [Atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md)  
  
## <a name="see-also"></a>Consulte também  
 [Como os VSPackages adicionam elementos da interface do usuário](../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [Roteamento de comando em VSPackages](../extensibility/internals/command-routing-in-vspackages.md)