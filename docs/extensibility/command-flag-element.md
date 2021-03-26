---
title: Elemento de sinalizador de comando | Microsoft Docs
description: O elemento flag de comando modifica seu elemento pai. Examine os elementos pai e os elementos filho.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CommandFlag element (VSCT XML schema)
- VSCT XML schema elements, CommandFlag
ms.assetid: 5ef63399-d2db-4dc1-97ce-be1bd4ef4e39
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1f9f9db3d7a8146bd7b44cf779fd62fd75803d86
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089635"
---
# <a name="command-flag-eelement"></a>Sinalizador de comando Eelement
Modifica seu elemento pai.

## <a name="syntax"></a>Sintaxe

```
<CommandFlag>DynamicVisibility</CommandFlag>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 A seção a seguir descreve os valores de elemento válidos.

### <a name="attributes"></a>Atributos
 Nenhum.

### <a name="child-elements"></a>Elementos filho

|Valor|Descrição|
|-----------|-----------------|
|AllowParams|Indica que os usuários podem inserir parâmetros de comando na janela de **comando** quando digitam o nome canônico do comando.<br /><br /> Válido para: `Button`|
|AlwaysCreate|O menu é criado mesmo que não tenha grupos ou botões.<br /><br /> Válido para: `Menu`|
|CaseSensitive|As entradas de usuário diferenciam maiúsculas de minúsculas.<br /><br /> Válido para: `Combo`|
|CommandWellOnly|Aplique esse sinalizador se o comando não aparecer no menu de nível superior e você desejar disponibilizá-lo para personalização adicional do Shell, por exemplo, para associá-lo a um atalho de teclado. Depois que o VSPackage for instalado, você poderá personalizar esses comandos abrindo a caixa de diálogo **Opções** e editando o posicionamento do comando na categoria **ambiente do teclado** . Esse sinalizador não afeta o posicionamento em menus de atalho, barras de ferramentas, controladores de menu ou submenus.<br /><br /> Válido para: `Button` , `Combo`|
|Defaultdesabilitoud|Por padrão, o comando será desabilitado se o VSPackage que o implementa não estiver carregado ou se o `QueryStatus` método não tiver sido chamado.<br /><br /> Válido para: `Button` , `Combo`|
|Defaultdocked|Encaixado por padrão. Essa configuração não se aplica mais às barras de ferramentas porque elas estão sempre encaixadas.|
|Invisible|Por padrão, o comando será invisível se o VSPackage que o implementa não estiver carregado ou se o `QueryStatus` método não tiver sido chamado.<br /><br /> É recomendável que você Combine isso com o `DynamicVisibility` sinalizador.<br /><br /> Válido para: `Button` , `Combo` , `Menu`|
|DontCache|O ambiente de desenvolvimento não armazena em cache os `QueryStatus` resultados do método para esse comando.<br /><br /> Para um menu, isso diz a um controlador de menu para não armazenar em cache o texto de seus itens de menu. Use esse sinalizador quando o menu contiver itens dinâmicos ou itens com texto dinâmico.<br /><br /> Válido para: `Button` , `Menu`|
|DynamicItemStart|Indica o início de uma lista dinâmica. Isso permite que o ambiente crie uma lista chamando sucessivamente o `QueryStatus` método em itens de lista até que o sinalizador de OLECMDERR_E_UNSUPPORTED seja retornado. Isso funciona bem para itens como listas MRU e listas de janelas usadas recentemente.<br /><br /> Válido para: `Button`|
|DynamicVisibility|A visibilidade do comando pode ser alterada por meio do `QueryStatus` método ou por meio de um GUID de contexto que está incluído na `VisibilityConstraints` seção.<br /><br /> Aplica-se a comandos que aparecem em menus e barras de ferramentas da janela de ferramentas, mas não em barras de ferramentas de nível superior que aparecem na janela principal. Itens de barra de ferramentas de nível superior podem ser desabilitados, mas não ocultos, quando o sinalizador de OLECMDF_INVISIBLE é retornado do `QueryStatus` método. Os comandos da barra de ferramentas que aparecem nas barras de ferramentas da janela de ferramentas podem ser ocultados.<br /><br /> Em um menu, esse sinalizador também indica que ele deve ser ocultado automaticamente quando todos os seus membros estiverem ocultos. Esse sinalizador é normalmente atribuído a submenus porque os menus de nível superior já têm esse comportamento.<br /><br /> Esse sinalizador deve ser combinado com o `DefaultInvisible` sinalizador.<br /><br /> Válido para: `Button` , `Combo` , `Menu`|
|Ativar|Consulte o tópico chaves de filtragem em [elemento de combinação](../extensibility/combo-element.md).<br /><br /> Válido para: `Combo`|
|FixMenuController|Se esse comando estiver posicionado em um controlador de menu, o comando será sempre o padrão; ou seja, o comando é selecionado sempre que o botão do controlador de menu é selecionado. Se o controlador de menu tiver o `TextIsAnchorCommand` sinalizador definido, o controlador de menu também usará o texto do comando que tem o `FixMenuController` sinalizador.<br /><br /> Somente um comando em um controlador de menu deve ter o `FixMenuController` sinalizador. Se mais de um comando estiver marcado, o último comando no menu se tornará o comando padrão.<br /><br /> Válido para: `Button`|
|IconAndText|Mostrar um ícone e um texto no menu e na barra de ferramentas.<br /><br /> Válido para: `Button` , `Combo` , `Menu`|
|NoAutoComplete|O recurso de conclusão automática está desabilitado.<br /><br /> Válido para: `Combo`|
|NoButtonCustomize|Não deixe que o usuário personalize esse botão.<br /><br /> Válido para: `Button` , `Combo`|
|NoKeyCustomize|Não habilite a personalização do teclado.<br /><br /> Válido para: `Button` , `Combo`|
|NoShowOnMenuController|Se esse comando estiver posicionado em um controlador de menu, o comando não aparecerá na lista suspensa.<br /><br /> Válido para: `Button`|
|NotInTBList|Não aparece na lista de barras de ferramentas disponíveis. Isso é válido somente para tipos de menu da barra de ferramentas.<br /><br /> Válido para: `Menu`|
|NoToolbarClose|O usuário não pode fechar a barra de ferramentas. Isso é válido somente para tipos de menu da barra de ferramentas.<br /><br /> Válido para: `Menu`|
|Otimizar|Mostrar apenas um ícone em uma barra de ferramentas, mas apenas texto em um menu. Se nenhum ícone for especificado, mostrará um espaço em branco clicável em uma barra de ferramentas.<br /><br /> Válido para: `Button`|
|Exec|Torna o comando sem bloqueio. O ambiente de desenvolvimento adia a execução até que todas as consultas de pré-processamento sejam concluídas.<br /><br /> Válido para: `Button`|
|RouteToDocs|O comando é roteado para o documento ativo.<br /><br /> Válido para: `Button`|
|StretchHorizontally|Quando esse sinalizador é definido, a largura se torna a largura mínima da caixa de combinação e, se houver espaço na barra de ferramentas, a caixa de combinação será ampliada para preencher o espaço disponível. Isso ocorrerá somente se a barra de ferramentas for encaixada horizontalmente e apenas uma caixa de combinação na barra de ferramentas puder usar o sinalizador (o sinalizador será ignorado em todos os exceto na primeira caixa de combinação).<br /><br /> Válido para: `Combo`|
|Textchanges|O comando ou o texto do menu pode ser alterado em tempo de execução, normalmente por meio do `QueryStatus` método.<br /><br /> Válido para: `Button` , `Menu`|
|TextChangesButton|Válido para: `Button`|
|TextIsAnchorCommand|Para um controlador de menu, o texto do menu é extraído do comando padrão (âncora). Um comando de âncora é o último comando selecionado ou travado. Se esse sinalizador não for definido, o controlador de menu usará seu próprio `MenuText` campo. No entanto, clicar no controlador de menu ainda habilita o último comando selecionado desse controlador.<br /><br /> Recomendamos que você combine esse sinalizador com o `TextChanges` sinalizador.<br /><br /> Esse sinalizador aplica-se somente a menus do tipo MenuController ou MenuControllerLatched.<br /><br /> Válido para: `Menu`|
|TextMenuCtrlUseMenu|Use o `MenuText` campo em controladores de menu. O campo padrão é `ButtonText` .<br /><br /> Válido para: `Button`|
|TextMenuUseButton|Use o `ButtonText` campo para menus. O campo padrão é `MenuText` se especificado.<br /><br /> Válido para: `Button`|
|TextOnly|Mostrar somente texto em uma barra de ferramentas ou em um menu, mas sem ícone, mesmo que o ícone seja especificado.<br /><br /> Válido para: `Button`|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento Buttons](../extensibility/buttons-element.md)|Fornece um grupo para elementos de [elemento de botão](../extensibility/button-element.md) .|
|[Elemento menus](../extensibility/menus-element.md)|Define todos os menus que um VSPackage implementa.|

## <a name="see-also"></a>Confira também
- [Tabela de comandos do Visual Studio (. Arquivos de vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
