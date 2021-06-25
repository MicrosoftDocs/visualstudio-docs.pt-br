---
title: Elemento Command Flag | Microsoft Docs
description: O Elemento do sinalizador de comando modifica seu elemento pai. Revise seus elementos pai e filho.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- CommandFlag element (VSCT XML schema)
- VSCT XML schema elements, CommandFlag
ms.assetid: 5ef63399-d2db-4dc1-97ce-be1bd4ef4e39
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6356fd02c8045aee9dc48ebc9d30a346159080bb
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902027"
---
# <a name="command-flag-eelement"></a>Eelement do sinalizador de comando
Modifica seu elemento pai.

## <a name="syntax"></a>Sintaxe

```
<CommandFlag>DynamicVisibility</CommandFlag>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 A seção a seguir descreve valores de elemento válidos.

### <a name="attributes"></a>Atributos
 Nenhum.

### <a name="child-elements"></a>Elementos filho

|Valor|Descrição|
|-----------|-----------------|
|AllowParams|Indica que os usuários podem inserir parâmetros de comando na **janela Comando** quando digitarem o nome canônico do comando.<br /><br /> Válido para: `Button`|
|Alwayscreate|O menu é criado mesmo se não tiver grupos ou botões.<br /><br /> Válido para: `Menu`|
|CaseSensitive|As entradas do usuário são sensíveis a minúsculas.<br /><br /> Válido para: `Combo`|
|CommandWellOnly|Aplique esse sinalizador se o comando não aparecer no menu de nível superior e você quiser torná-lo disponível para personalização adicional de shell, por exemplo, para a associação a um atalho de teclado. Depois que o VSPackage for instalado, você  poderá personalizar esses comandos abrindo a caixa de diálogo Opções e editando o posicionamento do comando na categoria **Ambiente do** Teclado. Esse sinalizador não afeta o posicionamento em menus de atalho, barras de ferramentas, controladores de menu ou submenus.<br /><br /> Válido para: `Button` , `Combo`|
|DefaultDisabled|Por padrão, o comando será desabilitado se o VSPackage que o implementa não for carregado ou se o `QueryStatus` método não tiver sido chamado.<br /><br /> Válido para: `Button` , `Combo`|
|DefaultDocked|Encaixado por padrão. Essa configuração não se aplica mais a barras de ferramentas porque elas estão sempre encaixadas.|
|DefaultInvisible|Por padrão, o comando será invisível se o VSPackage que o implementa não for carregado ou se o `QueryStatus` método não tiver sido chamado.<br /><br /> Recomendamos que você combine isso com o `DynamicVisibility` sinalizador .<br /><br /> Válido para: `Button` , `Combo` , `Menu`|
|DontCache|O ambiente de desenvolvimento não armazena em cache `QueryStatus` os resultados do método para esse comando.<br /><br /> Para um menu, isso informa a um controlador de menu para não armazenar em cache o texto de seus itens de menu. Use esse sinalizador quando o menu contiver itens dinâmicos ou itens que têm texto dinâmico.<br /><br /> Válido para: `Button` , `Menu`|
|DynamicItemStart|Indica o início de uma lista dinâmica. Isso permite que o ambiente crie uma lista chamando sucessivamente o método em itens de lista até que o sinalizador `QueryStatus` OLECMDERR_E_UNSUPPORTED seja retornado. Isso funciona bem para itens como listas de MRU (listas de MRU) usadas mais recentemente e listas de janelas.<br /><br /> Válido para: `Button`|
|DynamicVisibility|A visibilidade do comando pode ser alterada por meio do método ou por meio de um GUID de `QueryStatus` contexto incluído na `VisibilityConstraints` seção.<br /><br /> Aplica-se a comandos que aparecem em menus e barras de ferramentas da janela de ferramentas, mas não em barras de ferramentas de nível superior que aparecem na janela principal. Os itens da barra de ferramentas de nível superior podem ser desabilitados, mas não ocultos, quando o sinalizador OLECMDF_INVISIBLE é retornado do `QueryStatus` método . Os comandos da barra de ferramentas que aparecem nas barras de ferramentas da janela de ferramentas podem ser ocultos.<br /><br /> Em um menu, esse sinalizador também indica que ele deve ser ocultado automaticamente quando todos os seus membros estão ocultos. Normalmente, esse sinalizador é atribuído a submenus porque os menus de nível superior já têm esse comportamento.<br /><br /> Esse sinalizador deve ser combinado com o `DefaultInvisible` sinalizador .<br /><br /> Válido para: `Button` , `Combo` , `Menu`|
|FilterKeys|Consulte o tópico Chaves de Filtragem em [Elemento Combo](../extensibility/combo-element.md).<br /><br /> Válido para: `Combo`|
|FixMenuController|Se esse comando estiver posicionado em um controlador de menu, o comando será sempre o padrão; ou seja, o comando é selecionado sempre que o botão do controlador de menu em si é selecionado. Se o controlador de menu tiver o sinalizador definido, o controlador de menu também terá seu texto do `TextIsAnchorCommand` comando que tem o sinalizador `FixMenuController` .<br /><br /> Apenas um comando em um controlador de menu deve ter o `FixMenuController` sinalizador . Se mais de um comando estiver marcado, o último comando no menu se tornará o comando padrão.<br /><br /> Válido para: `Button`|
|IconAndText|Mostrar um ícone e um texto no menu e na barra de ferramentas.<br /><br /> Válido para: `Button` , `Combo` , `Menu`|
|NoAutoComplete|O recurso de conclusão automática está desabilitado.<br /><br /> Válido para: `Combo`|
|NoButtonCustomize|Não deixe que o usuário personalize esse botão.<br /><br /> Válido para: `Button` , `Combo`|
|NoKeyCustomize|Não habilita a personalização do teclado.<br /><br /> Válido para: `Button` , `Combo`|
|NoShowOnMenuController|Se esse comando estiver posicionado em um controlador de menu, o comando não aparecerá na lista suspenso.<br /><br /> Válido para: `Button`|
|NotInTBList|Não aparece na lista de barras de ferramentas disponíveis. Isso só é válido para tipos de menu da Barra de Ferramentas.<br /><br /> Válido para: `Menu`|
|NoToolbarClose|O usuário não pode fechar a barra de ferramentas. Isso só é válido para tipos de menu da Barra de Ferramentas.<br /><br /> Válido para: `Menu`|
|Pict|Mostrar apenas um ícone em uma barra de ferramentas, mas apenas texto em um menu. Se nenhum ícone for especificado, mostrará um espaço em branco clicável em uma barra de ferramentas.<br /><br /> Válido para: `Button`|
|PostExec|Torna o comando sem bloqueio. O ambiente de desenvolvimento adia a execução até que todas as consultas de pré-processamento sejam concluídas.<br /><br /> Válido para: `Button`|
|RouteToDocs|O comando é roteado para o documento ativo.<br /><br /> Válido para: `Button`|
|StretchHorizontally|Quando esse sinalizador é definido, a largura se torna a largura mínima para a caixa de combinação e, se houver espaço na barra de ferramentas, a caixa de combinação se alonga para preencher o espaço disponível. Isso ocorrerá somente se a barra de ferramentas estiver encaixada horizontalmente e apenas uma caixa de combinação na barra de ferramentas puder usar o sinalizador (o sinalizador será ignorado em todos, exceto na primeira caixa de combinação).<br /><br /> Válido para: `Combo`|
|TextChanges|O texto do comando ou do menu pode ser alterado em tempo de executar, normalmente por meio do `QueryStatus` método .<br /><br /> Válido para: `Button` , `Menu`|
|TextChangesButton|Válido para: `Button`|
|TextIsAnchorCommand|Para um controlador de menu, o texto do menu é retirado do comando padrão (âncora). Um comando de âncora é o último comando selecionado ou travado. Se esse sinalizador não estiver definido, o controlador de menu usará seu `MenuText` próprio campo. No entanto, clicar no controlador de menu ainda habilita o último comando selecionado desse controlador.<br /><br /> Recomendamos que você combine esse sinalizador com o `TextChanges` sinalizador .<br /><br /> Esse sinalizador se aplica somente a menus do tipo MenuController ou MenuControllerLatched.<br /><br /> Válido para: `Menu`|
|TextMenuCtrlUseMenu|Use o `MenuText` campo em controladores de menu. O campo padrão é `ButtonText` .<br /><br /> Válido para: `Button`|
|TextMenuUseButton|Use o `ButtonText` campo para menus. O campo padrão `MenuText` será se for especificado.<br /><br /> Válido para: `Button`|
|Textonly|Mostre apenas o texto em uma barra de ferramentas ou um menu, mas nenhum ícone, mesmo se o ícone for especificado.<br /><br /> Válido para: `Button`|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento Buttons](../extensibility/buttons-element.md)|Fornece um grupo para elementos [do elemento](../extensibility/button-element.md) Button.|
|[Elemento Menus](../extensibility/menus-element.md)|Define todos os menus que um VSPackage implementa.|

## <a name="see-also"></a>Confira também
- [Visual Studio de comando (. Vsct) Arquivos](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
