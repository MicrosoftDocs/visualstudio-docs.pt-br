---
title: Elemento CommandTable | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- CommandTable
helpviewer_keywords:
- CommandTable element (VSCT XML schema)
- VSCT XML schema elements, CommandTable
ms.assetid: 15c38159-660a-4ef4-9643-aa6fcfca82a9
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 8c2adca249ba245825f9b664b46e1b4674d0ea50
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49879903"
---
# <a name="commandtable-element"></a>Elemento CommandTable
CommandTable é o elemento raiz do *VSCT* arquivo. Esse é o arquivo que define o layout real e o tipo dos comandos a um VSPackage fornece ao IDE. Comandos podem incluir itens de menu, menus, barras de ferramentas e caixas de combinação. Para obter mais informações, consulte [arquivos de tabela (. VSCT) de comando do Visual Studio](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).  
  
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
| xmlns | Necessário. Namespaces XML:<br /><br /> xmlns = "<http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable>"<br /><br /> xmlns: xs = "<http://www.w3.org/2001/XMLSchema>" |
| linguagem | Opcional. O atributo de idioma pode ser usado para especificar o idioma padrão de todos os \<cadeias de caracteres > elementos na tabela de comandos.  Se o idioma não for especificado, será usado o idioma do processo atual:<br /><br /> Language = "en-us" |
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Elemento extern](../extensibility/extern-element.md)|Opcional. Contém as diretivas de pré-processador para o compilador.|  
|[Incluir elemento](../extensibility/include-element.md)|Opcional. Contém os caminhos para todos os arquivos para incluir na compilação.|  
|[Definir o elemento](../extensibility/define-element.md)|Opcional. Define um símbolo informado seu nome e valor.|  
|[Elemento Commands](../extensibility/commands-element.md)|Opcional. O elemento pai definindo todos os comandos para o VSPackage que contém todos os outros elementos.|  
|[Elemento CommandPlacements](../extensibility/commandplacements-element.md)|Opcional. Define onde os comandos na barra de comandos devem ser colocados.|  
|[Element visibilityconstraints](../extensibility/visibilityconstraints-element.md)|Opcional. Determina a visibilidade estática de comandos e barras de ferramentas.|  
|[Elemento KeyBindings](../extensibility/keybindings-element.md)|Opcional. Especifica as combinações de teclas de atalho, se houver, para os comandos.|  
|[Elemento UsedCommands](../extensibility/usedcommands-element.md)|Opcional. Permite que um VSPackage, opcionalmente, implementar sua própria versão da funcionalidade de outros VSPackages originalmente com suporte.|  
|[Elemento Symbols](https://www.microsoft.com/download/details.aspx?id=55984)|Opcional. Contém os dados de símbolo – GUIDs, IDs e assim por diante – para o compilador.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|Nenhum||  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos de tabela (. VSCT) de comando do Visual Studio](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)