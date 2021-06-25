---
title: Elemento Strings | Microsoft Docs
description: O elemento Strings contém um elemento filho ButtonText e outros elementos filho opcionais. Um e ampersand na cadeia de caracteres de texto especifica um atalho de teclado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Strings element (VSCT XML schema)
- VSCT XML schema elements, Strings
ms.assetid: 23a42074-a689-481d-824f-b43aa448f266
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 27a649c7d3a8bb808153c280921d2304de59c379
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899401"
---
# <a name="strings-element"></a>Elemento Strings
O elemento Strings deve conter pelo menos um **elemento filho ButtonText.** Todos os outros elementos filho são opcionais. Caracteres XML inválidos, como '&' e '<' devem ser codificados como entidades (' &amp; ' e ' ' e assim por &lt; diante).

 Um e ampersand na cadeia de caracteres de texto especifica o atalho de teclado para o comando.

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
|Linguagem|Opcional. Language=".".|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|Buttontext|Esse campo e os cinco campos de texto a seguir em uma definição de comando permitem especificar o texto que aparece em vários menus. Por padrão, o `ButtonText` campo aparece nos controladores de menu. O `ButtonText` campo também se tornará o padrão se os outros campos de texto estão em branco. O `ButtonText` campo não poderá ficar em branco mesmo que os outros campos de texto sejam especificados.|
|Tooltiptext|O `ToolTipText` campo especifica o texto que aparece na dica de ferramenta para um item de menu.<br /><br /> Se o `ToolTipText` campo estiver em branco, o campo será `ButtonText` usado.|
|Menutext|O campo especifica o texto exibido para um comando se ele estiver no menu principal, uma barra de ferramentas, em um menu de atalho ou em `MenuText` um submenu. Se o `MenuText` campo estiver em branco, o IDE (ambiente de desenvolvimento integrado) usará o `ButtonText` campo . O `MenuText` campo também pode ser usado para localização.<br /><br /> Para menus de atalho, o campo é o nome exibido na barra de ferramentas Menus de Atalho, que permite a personalização de menus de atalho no `MenuText` IDE. Portanto, seja específico em qual nome você nomeia o menu de atalho; por exemplo, use "Menu de Atalho do Pacote de Widget" em vez de "Atalho".<br /><br /> Se o `MenuText` campo não for especificado, o campo será `ButtonText` usado.|
|CommandName|O campo especifica o texto que aparece na categoria de teclado na guia Comandos na caixa de diálogo Personalizar (disponível clicando em Personalizar no `CommandName` menu Ferramentas).    |
|Canonicalname|O campo inglês especifica o nome do comando em texto em inglês que pode ser inserido na janela `CanonicalName` **Comando** para executar o item de menu. O IDE retira todos os caracteres que não são letras, dígitos, sublinhados ou períodos inseridos. Em seguida, esse texto é concatenado ao `ButtonText` campo para definir o comando. Por exemplo, **Novo Projeto** no menu **Arquivo** torna-se o comando File.NewProject.<br /><br /> Se o campo inglês não for especificado, o IDE usará o campo e retirará todas as letras, dígitos, sublinhados e `CanonicalName` `ButtonText` períodos inseridos. Por exemplo, o texto do botão "&definir comandos..." torna-se DefineCommands, em que o entese, o espaço e as reellipses são removidos.<br /><br /> Se o sinalizador for especificado e o texto do comando for alterado, o comando correspondente reconhecido pela janela Comando não será alterado; ele permanecerá na forma canônica dos campos original ou `TextChanges`  `ButtonText` `CanonicalName` inglês.|
|LocCanonicalName|O campo se comporta de forma idêntica ao campo inglês, mas permite que o texto do comando localizado `LocCanonicalName` `CanonicalName` seja especificado. Ambos os campos canônicos podem ser especificados. Como o IDE apenas analisará  o texto inserido na janela Comando e o associará a um comando, o texto em inglês e não inglês pode ser associado ao mesmo comando.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento Button](../extensibility/button-element.md)|Define um elemento com o qual o usuário pode interagir.|
|[Elemento Menu](../extensibility/menu-element.md)|Define um único item de menu.|
|[Elemento Combo](../extensibility/combo-element.md)|Define comandos que aparecem em uma caixa de combinação.|

## <a name="see-also"></a>Confira também
- [Arquivos .Vsct (Visual Studio Command Table)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
