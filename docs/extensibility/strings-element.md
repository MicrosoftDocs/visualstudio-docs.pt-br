---
title: Elemento Strings | Microsoft Docs
description: O elemento Strings contém um elemento filho ButtonText e outros elementos filho opcionais. Um e comercial na cadeia de texto especifica um atalho de teclado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Strings element (VSCT XML schema)
- VSCT XML schema elements, Strings
ms.assetid: 23a42074-a689-481d-824f-b43aa448f266
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a0bd9ad9b8059eb7fd566c1e0c26a938af6d18b2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089895"
---
# <a name="strings-element"></a>Elemento Strings
O elemento Strings deve conter pelo menos um elemento filho **ButtonText** . Todos os outros elementos filho são opcionais. Caracteres XML inválidos, como ' & ' e ' < ', devem ser codificados como entidades (' &amp; ' e ' &lt; ' e assim por diante).

 Um e comercial na cadeia de texto especifica o atalho de teclado para o comando.

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
|Linguagem|Opcional. Language = ".".|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|ButtonText|Esse campo e os cinco campos de texto a seguir em uma definição de comando permitem especificar o texto que aparece em vários menus. Por padrão, o `ButtonText` campo aparece em controladores de menu. O `ButtonText` campo também se tornará o padrão se os outros campos de texto estiverem em branco. O `ButtonText` campo não pode ficar em branco mesmo que os outros campos de texto sejam especificados.|
|ToolTipText|O `ToolTipText` campo especifica o texto que aparece na dica de ferramenta para um item de menu.<br /><br /> Se o `ToolTipText` campo estiver em branco, o `ButtonText` campo será usado.|
|MenuText|O `MenuText` campo especifica o texto que será exibido para um comando se ele estiver no menu principal, em uma barra de ferramentas, em um menu de atalho ou em um submenu. Se o `MenuText` campo estiver em branco, o ambiente de desenvolvimento integrado (IDE) usará o `ButtonText` campo. O `MenuText` campo também pode ser usado para localização.<br /><br /> Para menus de atalho, o `MenuText` campo é o nome exibido na barra de ferramentas menus de atalho, que permite a personalização de menus de atalho no IDE. Portanto, seja específico em nome do seu menu de atalho; por exemplo, use "menu de atalho do pacote de widget" em vez de "Shortcut".<br /><br /> Se o `MenuText` campo não for especificado, o `ButtonText` campo será usado.|
|CommandName|O `CommandName` campo especifica o texto que aparece na categoria teclado na guia **comandos** da caixa de diálogo **Personalizar** (disponível clicando em **Personalizar** no menu **ferramentas** ).|
|Canônicaname|O `CanonicalName` campo inglês especifica o nome do comando em texto em inglês que pode ser inserido na janela de **comando** para executar o item de menu. O IDE remove os caracteres que não são letras, dígitos, sublinhados ou períodos inseridos. Esse texto é concatenado ao `ButtonText` campo para definir o comando. Por exemplo, **novo projeto** no menu **arquivo** torna-se o comando File. NewProject.<br /><br /> Se o campo em inglês `CanonicalName` não for especificado, o IDE usará o `ButtonText` campo e exprime tudo, exceto letras, dígitos, sublinhados e períodos inseridos. Por exemplo, o texto do botão "&definir comandos..." torna-se DefineCommands, em que o e comercial, o espaço e as reticências são removidos.<br /><br /> Se o `TextChanges` sinalizador for especificado e o texto do comando for alterado, o comando correspondente reconhecido pela janela de **comando** não será alterado; ele permanecerá na forma canônica dos campos original `ButtonText` ou Inglês `CanonicalName` .|
|LocCanonicalName|O `LocCanonicalName` campo se comporta de forma idêntica ao campo em inglês `CanonicalName` , mas permite que o texto de comando localizado seja especificado. Ambos os campos canônicos podem ser especificados. Como o IDE apenas analisa o texto inserido na janela de **comando** e o associa a um comando, tanto o texto em inglês quanto o idioma não inglês podem ser associados ao mesmo comando.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento Button](../extensibility/button-element.md)|Define um elemento com o qual o usuário pode interagir.|
|[Elemento Menu](../extensibility/menu-element.md)|Define um único item de menu.|
|[Elemento Combo](../extensibility/combo-element.md)|Define os comandos que aparecem em uma caixa de combinação.|

## <a name="see-also"></a>Confira também
- [Arquivos .Vsct (Visual Studio Command Table)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
