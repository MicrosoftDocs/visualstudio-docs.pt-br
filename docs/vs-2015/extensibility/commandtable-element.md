---
title: Elemento CommandTable | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- CommandTable
helpviewer_keywords:
- CommandTable element (VSCT XML schema)
- VSCT XML schema elements, CommandTable
ms.assetid: 15c38159-660a-4ef4-9643-aa6fcfca82a9
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 1adc3e8f8c7894cfb3a55617ce594f52a60f2498
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51817367"
---
# <a name="commandtable-element"></a>Elemento CommandTable
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

CommandTable é o elemento raiz do arquivo. VSCT. Esse é o arquivo que define o layout real e o tipo dos comandos a um VSPackage fornece ao IDE. Comandos podem incluir itens de menu, menus, barras de ferramentas e caixas de combinação. Para obter mais informações, consulte [tabela de comando do Visual Studio (. VSCT) arquivos](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
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
  
| Atributo |                                                                                                                   Descrição                                                                                                                   |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   xmlns   |                                   Necessário. Namespaces XML:<br /><br /> xmlns = "<http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable>"<br /><br /> xmlns: xs = "<http://www.w3.org/2001/XMLSchema>"                                   |
| linguagem  | Opcional. O atributo de idioma pode ser usado para especificar o idioma padrão de todos os \<cadeias de caracteres > elementos na tabela de comandos.  Se o idioma não for especificado, será usado o idioma do processo atual:<br /><br /> Language = "en-us" |
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Elemento Extern](../extensibility/extern-element.md)|Opcional. Contém as diretivas de pré-processador para o compilador.|  
|[Elemento Include](../extensibility/include-element.md)|Opcional. Contém os caminhos para todos os arquivos para incluir na compilação.|  
|[Elemento Define](../extensibility/define-element.md)|Opcional. Define um símbolo informado seu nome e valor.|  
|[Elemento Commands](../extensibility/commands-element.md)|Opcional. O elemento pai definindo todos os comandos para o VSPackage que contém todos os outros elementos.|  
|[Elemento CommandPlacements](../extensibility/commandplacements-element.md)|Opcional. Define onde os comandos na barra de comandos devem ser colocados.|  
|[Element VisibilityConstraints](../extensibility/visibilityconstraints-element.md)|Opcional. Determina a visibilidade estática de comandos e barras de ferramentas.|  
|[Elemento KeyBindings](../extensibility/keybindings-element.md)|Opcional. Especifica as combinações de teclas de atalho, se houver, para os comandos.|  
|[Elemento UsedCommands](../extensibility/usedcommands-element.md)|Opcional. Permite que um VSPackage, opcionalmente, implementar sua própria versão da funcionalidade de outros VSPackages originalmente com suporte.|  
|[Elemento Symbols](http://msdn.microsoft.com/en-us/f2ddd0aa-c3dd-439e-834d-28f136a27ffa)|Opcional. Contém os dados de símbolo – GUIDs, IDs e assim por diante – para o compilador.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|Nenhum||  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos da tabela de comandos do Visual Studio (.Vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)

