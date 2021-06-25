---
title: Elemento CommandTable | Microsoft Docs
description: CommandTable é o elemento raiz do arquivo .vsct, que define o layout e o tipo dos comandos que um VSPackage fornece ao IDE.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CommandTable
helpviewer_keywords:
- CommandTable element (VSCT XML schema)
- VSCT XML schema elements, CommandTable
ms.assetid: 15c38159-660a-4ef4-9643-aa6fcfca82a9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 55faf4ee8bdc7ec261508fd07f5a573e7a29560f
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901845"
---
# <a name="commandtable-element"></a>Elemento CommandTable
CommandTable é o elemento raiz do *arquivo .vsct.* Esse é o arquivo que define o layout real e o tipo dos comandos que um VSPackage fornece ao IDE. Os comandos podem incluir itens de menu, menus, barras de ferramentas e caixas de combinação. Para obter mais informações, [consulte Visual Studio arquivos de tabela de comando (.vsct).](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)

## <a name="syntax"></a>Sintaxe

```xml
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema" >
  <Extern>... </Extern>
  <Include>... </Include>
  <Define>... </Define>
  <Commands>... </Commands>
  <CommandPlacements>... </CommandPlacements>
  <VisibilityConstraints>... </VisibilityConstraints>
  <KeyBindings>... </KeyBindings>
  <UsedCommands... </UsedCommands>
  <Symbols>... </Symbols>
</CommandTable>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

| Atributo | Descrição |
|-----------| - |
| xmlns | Obrigatórios. Namespaces XML:<br /><br /> `xmlns=http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable`<br /><br /> xmlns:xs=" <http://www.w3.org/2001/XMLSchema> " |
| Linguagem | Opcional. O atributo language pode ser usado para especificar o idioma padrão de todos \<Strings> os elementos na tabela de comandos.  Se o idioma não for especificado, o idioma do processo atual será usado:<br /><br /> language="en-us" |

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento Extern](../extensibility/extern-element.md)|Opcional. Contém diretivas de pré-processador para o compilador.|
|[Elemento Include](../extensibility/include-element.md)|Opcional. Contém caminhos para qualquer arquivo a ser incluído na compilação.|
|[Definir elemento](../extensibility/define-element.md)|Opcional. Define um símbolo dado seu nome e valor.|
|[Elemento Commands](../extensibility/commands-element.md)|Opcional. O elemento pai que define todos os comandos para o VSPackage que contém todos os outros elementos.|
|[Elemento CommandPlacements](../extensibility/commandplacements-element.md)|Opcional. Define onde na barra de comandos os comandos devem ser colocados.|
|[Elemento VisibilityConstraints](../extensibility/visibilityconstraints-element.md)|Opcional. Determina a visibilidade estática de comandos e barras de ferramentas.|
|[Elemento KeyBindings](../extensibility/keybindings-element.md)|Opcional. Especifica as combinações de teclas de atalho, se alguma, para os comandos.|
|[Elemento UsedCommands](../extensibility/usedcommands-element.md)|Opcional. Permite que um VSPackage implemente opcionalmente sua própria versão da funcionalidade originalmente com suporte de outros VSPackages.|
|[Elemento Symbols](https://www.microsoft.com/download/details.aspx?id=55984)|Opcional. Contém todos os dados de símbolo – GUIDs, IDs e assim por diante – para o compilador.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|Nenhum||

## <a name="see-also"></a>Confira também
- [Visual Studio de tabela de comandos (.vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
