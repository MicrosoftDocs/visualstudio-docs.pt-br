---
title: Elemento de sinalizador de comando | Microsoft Docs
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
- CommandFlag element (VSCT XML schema)
- VSCT XML schema elements, CommandFlag
ms.assetid: 5ef63399-d2db-4dc1-97ce-be1bd4ef4e39
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 98140c90288d8a65d22996940300a82b5e070308
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51809916"
---
# <a name="command-flag-element"></a>Elemento Command Flag
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Modifica seu elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<CommandFlag>DynamicVisibility</CommandFlag>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 A seção a seguir descreve os valores de elemento válido.  
  
### <a name="attributes"></a>Atributos  
 nenhuma.  
  
### <a name="child-elements"></a>Elementos filho  
  
|Valor|Descrição|  
|-----------|-----------------|  
|AllowParams|Indica que os usuários podem inserir parâmetros de comando na **comando** janela ao digitar o nome canônico do comando.<br /><br /> Válido para: `Button`|  
|AlwaysCreate|Menu é criado, mesmo se ele não possui grupos ou botões.<br /><br /> Válido para: `Menu`|  
|CaseSensitive|As entradas de usuário diferenciam maiusculas de minúsculas.<br /><br /> Válido para: `Combo`|  
|CommandWellOnly|Aplica esse sinalizador se o comando não aparecer no menu de nível superior e você deseja torná-lo disponível para personalização do shell adicionais, por exemplo, para associá-la a um atalho de teclado. Depois que o VSPackage é instalado, você pode personalizar esses comandos, abrindo o **opções** caixa de diálogo e, em seguida, editando o posicionamento do comando sob o **teclado ambiente** categoria. Este sinalizador não afeta o posicionamento em menus de atalho, barras de ferramentas, os controladores de menu ou submenus.<br /><br /> Válido para: `Button`, `Combo`|  
|DefaultDisabled|Por padrão, o comando está desabilitado se o VSPackage que implementa a ele não está carregado ou o `QueryStatus` método não tiver sido chamado.<br /><br /> Válido para: `Button`, `Combo`|  
|DefaultDocked|Encaixado por padrão. Essa configuração não se aplica a barras de ferramentas, porque eles sempre estão encaixados.|  
|DefaultInvisible|Por padrão, o comando é invisível se o VSPackage que implementa a ele não está carregado ou o `QueryStatus` método não tiver sido chamado.<br /><br /> É recomendável que você combine isso com o `DynamicVisibility` sinalizador.<br /><br /> Válido para: `Button`, `Combo`, `Menu`|  
|DontCache|O ambiente de desenvolvimento não armazena em cache o `QueryStatus` resultados do método para esse comando.<br /><br /> Para um menu, isso informa um controlador de menu não armazenar em cache o texto de seus itens de menu. Use esse sinalizador quando o menu contém itens dinâmicos ou itens que têm texto dinâmico.<br /><br /> Válido para: `Button`, `Menu`|  
|DynamicItemStart|Indica o início de uma lista dinâmica. Isso permite que o ambiente criar uma lista sucessivamente chamando o `QueryStatus` método nos itens de lista até que o sinalizador OLECMDERR_E_UNSUPPORTED seja retornado. Isso funciona bem para itens, como usado mais recentemente (MRU) listas e listas de janela.<br /><br /> Válido para: `Button`|  
|DynamicVisibility|A visibilidade do comando pode ser alterada por meio de `QueryStatus` método ou por meio de um GUID que é incluído no contexto o `VisibilityConstraints` seção.<br /><br /> Aplica-se aos comandos que aparecem nos menus e barras de ferramentas de janela de ferramenta, mas não em barras de ferramentas de nível superior que aparecem na janela principal. Itens de nível superior da barra de ferramentas podem ser desabilitados, mas não ocultas, quando o sinalizador OLECMDF_INVISIBLE é retornado do `QueryStatus` método. Comandos da barra de ferramentas que aparecem nas barras de ferramentas de janela de ferramenta podem ser ocultados.<br /><br /> Em um menu, esse sinalizador indica também que ele deve ser automaticamente ocultado quando todos os seus membros estão ocultos. Esse sinalizador normalmente é atribuído à submenus como menus de nível superior já têm esse comportamento.<br /><br /> Este sinalizador deve ser combinado com o `DefaultInvisible` sinalizador.<br /><br /> Válido para: `Button`, `Combo`, `Menu`|  
|Teclas de filtragem|Consulte o tópico de filtragem chaves sob [elemento Combo](../extensibility/combo-element.md).<br /><br /> Válido para: `Combo`|  
|FixMenuController|Se esse comando é posicionado em um controlador de menu, o comando sempre é o padrão; ou seja, o comando é selecionado sempre que o próprio botão de controlador de menu é selecionado. Se o controlador de menu tem o `TextIsAnchorCommand` sinalizador definido, em seguida, o controlador de menu também usa o texto do comando que tem o `FixMenuController` sinalizador.<br /><br /> Somente um comando em um controlador de menu deve ter o `FixMenuController` sinalizador. Se mais de um comando é marcado assim, o último comando no menu torna-se o comando padrão.<br /><br /> Válido para: `Button`|  
|IconAndText|Mostra um ícone e texto em menus e barra de ferramentas.<br /><br /> Válido para: `Button`, `Combo`, `Menu`|  
|NoAutoComplete|O recurso de preenchimento automático está desabilitado.<br /><br /> Válido para: `Combo`|  
|NoButtonCustomize|Não permitir que o usuário personalize esse botão.<br /><br /> Válido para: `Button`, `Combo`|  
|NoKeyCustomize|Não habilite a personalização de teclado.<br /><br /> Válido para: `Button`, `Combo`|  
|NoShowOnMenuController|Se esse comando é posicionado em um controlador de menu, o comando não aparecer na lista suspensa.<br /><br /> Válido para: `Button`|  
|NotInTBList|Não aparece na lista de barras de ferramentas disponíveis. Isso é válido somente para tipos de menu da barra de ferramentas.<br /><br /> Válido para: `Menu`|  
|NoToolbarClose|O usuário não é possível fechar a barra de ferramentas. Isso é válido somente para tipos de menu da barra de ferramentas.<br /><br /> Válido para: `Menu`|  
|PICT|Mostra apenas um ícone em uma barra de ferramentas, mas apenas o texto em um menu. Se nenhum ícone for especificado, mostra um espaço em branco que pode ser clicado em uma barra de ferramentas.<br /><br /> Válido para: `Button`|  
|PostExec|Faz com que o comando sem bloqueio. O ambiente de desenvolvimento adia a execução até que todas as consultas de pré-processamento são concluídas.<br /><br /> Válido para: `Button`|  
|RouteToDocs|O comando é roteado para o documento ativo.<br /><br /> Válido para: `Button`|  
|StretchHorizontally|Quando esse sinalizador estiver definido, a largura torna-se a largura mínima da caixa de combinação e, se houver espaço na barra de ferramentas, caixa de combinação é alongado para preencher o espaço disponível. Isso ocorre somente se a barra de ferramentas horizontal está encaixada e apenas uma caixa de combinação na barra de ferramentas pode usar o sinalizador (o sinalizador é ignorado em todos, exceto a primeira caixa de combinação).<br /><br /> Válido para: `Combo`|  
|TextMenuUseButton|Use o `ButtonText` field para menus. O campo padrão é `MenuText` se for especificado.<br /><br /> Válido para: `Button`|  
|TextoAltera|O texto de comando ou o menu pode ser alterado em tempo de execução normalmente por meio de `QueryStatus` método.<br /><br /> Válido para: `Button`, `Menu`|  
|TextChangesButton|Válido para: `Button`|  
|TextIsAnchorCommand|Para um controlador de menu, o texto do menu é obtido do comando padrão (âncora). Um comando de âncora é o último comando selecionado ou travada. Se este sinalizador não for definido, o controlador de menu usa seu próprio `MenuText` campo. No entanto, clicando no controlador de menu ainda permite que o último comando selecionado do controlador em questão.<br /><br /> Recomendamos que você combine esse sinalizador com a `TextChanges` sinalizador.<br /><br /> Esse sinalizador aplica-se somente aos menus do tipo MenuController ou MenuControllerLatched.<br /><br /> Válido para: `Menu`|  
|TextMenuCtrlUseMenu|Use o `MenuText` campo nos controladores de menu. O campo padrão é `ButtonText`.<br /><br /> Válido para: `Button`|  
|TextMenuUseButton|Use o `ButtonText` field para menus. O campo padrão é `MenuText` se for especificado.<br /><br /> Válido para: `Button`|  
|TextOnly|Mostra somente o texto em uma barra de ferramentas ou um menu, mas nenhum ícone mesmo se o ícone for especificado.<br /><br /> Válido para: `Button`|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Elemento Buttons](../extensibility/buttons-element.md)|Fornece um grupo para [elemento Button](../extensibility/button-element.md) elementos.|  
|[Elemento Menus](../extensibility/menus-element.md)|Define todos os menus que implementa um VSPackage.|  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos da tabela de comandos do Visual Studio (.Vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)

