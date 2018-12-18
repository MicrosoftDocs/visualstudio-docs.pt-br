---
title: Elemento de cadeias de caracteres | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Strings element (VSCT XML schema)
- VSCT XML schema elements, Strings
ms.assetid: 23a42074-a689-481d-824f-b43aa448f266
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: c5994144f07b8af84f61d7833737f45593c551b2
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31143879"
---
# <a name="strings-element"></a>Elemento de cadeias de caracteres
O elemento de cadeias de caracteres deve conter pelo menos um **ButtonText** elemento filho. Todos os outros elementos filho são opcionais. Caracteres de XML inválido como '&' e ' <' devem ser codificados como entidades ('&amp;'e'&lt;' e assim por diante).  
  
 Um e comercial na cadeia de texto Especifica o atalho de teclado para o comando.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<Strings>  
  <ButtonText>... </ButtonText>  
  <CommandName>... </CommandName>  
</Strings>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|linguagem|Opcional. Language = ".".|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|ButtonText|Esse campo e cinco seguintes campos de texto em uma definição de comando permitem que você especifique o texto que aparece em vários menus. Por padrão, o `ButtonText` campo aparece em controladores de menu. O `ButtonText` campo também se tornará o padrão se campos de texto estão em branco. O `ButtonText` campo não pode ficar em branco, mesmo se os outros campos de texto forem especificados.|  
|ToolTipText|O `ToolTipText` campo especifica o texto que aparece na dica de ferramenta para um item de menu.<br /><br /> Se o `ToolTipText` campo fica em branco, o `ButtonText` campo será usado.|  
|MenuText|O `MenuText` campo especifica o texto que é exibido para um comando se ele estiver no menu principal, uma barra de ferramentas em um menu de atalho ou em um submenu. Se o `MenuText` campo fica em branco, o ambiente de desenvolvimento integrado (IDE) usa o `ButtonText` campo. O `MenuText` campo também pode ser usado para localização.<br /><br /> Menus de atalho, o `MenuText` campo é o nome que é exibido na barra de Menus de atalho, que permite a personalização de menus de atalho no IDE. Portanto, ser específico no qual o nome seu menu de atalho; Por exemplo, use "Menu de atalho do Widget de pacote" em vez de "Atalho".<br /><br /> Se o `MenuText` campo não for especificado, o `ButtonText` campo será usado.|  
|CommandName|O `CommandName` campo especifica o texto que aparece na categoria de teclado no **comandos** guia o **personalizar** caixa de diálogo (disponível ao clicar em **personalizar**no **ferramentas** menu).|  
|canonicalName|O inglês `CanonicalName` campo especifica o nome do comando no texto em inglês que pode ser inserido no **comando** janela para executar o item de menu. O IDE remove qualquer caractere que não é letras, dígitos, sublinhados ou pontos inseridos. Esse texto é concatenado, em seguida, o `ButtonText` campo para definir o comando. Por exemplo, **novo projeto** no **arquivo** menu torna-se o comando, File.NewProject.<br /><br /> Se o inglês `CanonicalName` campo não for especificado, o IDE usará o `ButtonText` campos e faixas todos exceto letras, dígitos, sublinhados e pontos inseridos. Por exemplo, o texto do botão "& Definir comandos..." se torna DefineCommands, onde o e comercial, o espaço e o botão de reticências são removidos.<br /><br /> Se o `TextChanges` sinalizador for especificado e o texto do comando é alterado, o comando correspondente reconhecido pelo **comando** janela não altera; ele permanece a forma canônica do original `ButtonText` ou inglês `CanonicalName` campos.|  
|LocCanonicalName|O `LocCanonicalName` campo se comporta de forma idêntica para o inglês `CanonicalName` campo mas permite texto do comando localizada seja especificado. Os dois campos canônicos podem ser especificados. Porque o IDE analisa apenas o texto inserido no **comando** janela e associa-o com um comando, em inglês e outro idioma texto pode ser associado com o mesmo comando.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Elemento Button](../extensibility/button-element.md)|Define um elemento que o usuário pode interagir com.|  
|[Elemento Menu](../extensibility/menu-element.md)|Define um item único de menu.|  
|[Elemento Combo](../extensibility/combo-element.md)|Define os comandos que aparecem em uma caixa de combinação.|  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos da tabela de comandos do Visual Studio (.Vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)