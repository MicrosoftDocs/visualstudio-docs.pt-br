---
title: Elemento de cadeias de caracteres | Microsoft Docs
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
- Strings element (VSCT XML schema)
- VSCT XML schema elements, Strings
ms.assetid: 23a42074-a689-481d-824f-b43aa448f266
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 5cc9adc4d13718fc9b0379c73b1892ba14e61d47
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51789792"
---
# <a name="strings-element"></a>Elemento Strings
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O elemento de cadeias de caracteres deve conter pelo menos um **ButtonText** elemento filho. Todos os outros elementos filho são opcionais. Caracteres de XML inválido, como '&' e ' <' devem ser codificados como entidades ('&amp;'e'&lt;' e assim por diante).  
  
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
|ButtonText|Este campo e os cinco seguintes campos de texto em uma definição de comando permitem que você especifique o texto que aparece em vários menus. Por padrão, o `ButtonText` campo aparece em controladores de menu. O `ButtonText` campo também se tornará o padrão se campos de texto estiverem em branco. O `ButtonText` campo não pode ficar em branco, mesmo se os outros campos de texto forem especificados.|  
|ToolTipText|O `ToolTipText` campo especifica o texto que aparece na dica de ferramenta para um item de menu.<br /><br /> Se o `ToolTipText` campo fica em branco, o `ButtonText` campo é usado.|  
|MenuText|O `MenuText` campo especifica o texto que é exibido para um comando se ele estiver no menu principal, uma barra de ferramentas em um menu de atalho ou em um submenu. Se o `MenuText` campo estiver em branco, o ambiente de desenvolvimento integrado (IDE) usa o `ButtonText` campo. O `MenuText` campo também pode ser usado para a localização.<br /><br /> Para menus de atalho, o `MenuText` campo é o nome que é exibido na barra de Menus de atalho, que permite a personalização de menus de atalho no IDE. Portanto, ser específico no qual o nome seu menu de atalho; Por exemplo, use "Menu de atalho do Widget de pacote" em vez de "Atalho".<br /><br /> Se o `MenuText` campo não for especificado, o `ButtonText` campo é usado.|  
|commandName|O `CommandName` campo especifica o texto que aparece na categoria de teclado em de **comandos** guia o **personalizar** caixa de diálogo (disponível ao clicar em **personalizar**sobre o **ferramentas** menu).|  
|CanonicalName|O inglês `CanonicalName` campo especifica o nome do comando no texto em inglês que pode ser inserido em de **comando** janela para executar o item de menu. O IDE elimine qualquer caractere que não é letras, dígitos, sublinhados ou pontos inseridos. Esse texto é concatenado, em seguida, o `ButtonText` campo para definir o comando. Por exemplo, **novo projeto** sobre o **arquivo** menu torna-se o comando, File.NewProject.<br /><br /> Se o inglês `CanonicalName` campo não for especificado, o IDE usa o `ButtonText` campo e faixas todas, exceto letras, dígitos, sublinhados e pontos inseridos. Por exemplo, o texto do botão "& Definir comandos..." se torna DefineCommands, onde o e comercial, o espaço e as reticências são removidos.<br /><br /> Se o `TextChanges` sinalizador for especificado e o texto do comando é alterado, o comando correspondente reconhecido pelo **comando** janela não é alterado; ele permanece a forma canônica do original `ButtonText` ou inglês `CanonicalName` campos.|  
|LocCanonicalName|O `LocCanonicalName` campo comporta-se identicamente para o inglês `CanonicalName` campo, mas permite que o texto de comando localizada seja especificado. Ambos os campos canônicos podem ser especificados. Como o IDE apenas analisa o texto inserido na **comando** janela e associa-o com um comando, o inglês e o texto de inglês pode ser associado com o mesmo comando.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Elemento Button](../extensibility/button-element.md)|Define um elemento que o usuário pode interagir com o.|  
|[Elemento Menu](../extensibility/menu-element.md)|Define um item de menu único.|  
|[Elemento Combo](../extensibility/combo-element.md)|Define os comandos que aparecem em uma caixa de combinação.|  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos da tabela de comandos do Visual Studio (.Vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)

