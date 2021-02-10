---
title: Exibição de classe ícones do Pesquisador de Objetos
description: Saiba mais sobre Modo de Exibição de Classe e o pesquisador de objetos exibe ícones que representam entidades de código, por exemplo, namespaces, classes, funções e variáveis.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- icons, in Object Browser
- signal icons
- Class View tool, symbols
- graphic symbols
- IntelliSense, icons
- icons, IntelliSense
- symbols, Object Browser icons
- Object Browser, icons in Class View
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 551033ce7dcd7b8755124b86734243470442b6e0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99939975"
---
# <a name="class-view-and-object-browser-icons"></a>Ícones do Pesquisador de Objetos e do Modo de Exibição de Classe

**Modo de exibição de classe** e o **pesquisador de objetos** exibem ícones que representam entidades de código, por exemplo, namespaces, classes, funções e variáveis. A tabela a seguir ilustra e descreve os ícones.

|ícone|Descrição|ícone|Descrição|
|----------|-----------------|----------|-----------------|
|![Símbolo de namespace](../ide/media/vxnamespace_icon.gif)|Namespace|![Símbolo de declaração](../ide/media/vxmethod_icon.gif)|Método ou função|
|![Ícone de classe](../ide/media/vxclass_icon.gif)|Classe|![Símbolo de operador](../ide/media/vxoperator_icon.gif)|Operador|
|![Símbolo de interface pirulito](../ide/media/vxinterface_icon.gif)|Interface|![Símbolo de propriedade](../ide/media/vxproperty_icon.gif)|Propriedade|
|![Símbolo de estrutura](../ide/media/vxstruct_icon.gif)|Estrutura|![Ícone de campo](../ide/media/vxfield_icon.gif)|Campo ou variável|
|![Símbolo de união](../ide/media/vxunion_icon.gif)|Union|![Símbolo de evento](../ide/media/vxevent_icon.gif)|Evento|
|![Símbolo de enumeração](../ide/media/vxenum_icon.gif)|Enumeração|![Ícone constante](../ide/media/vxconstant_icon.gif)|Constante|
|![Símbolo de definição de tipo](../ide/media/vxtypedef_icon.gif)|TypeDef|![Símbolo do item de enumeração](../ide/media/vxenumitem_icon.gif)|Item Enum|
|![Símbolo do módulo do Visual Studio](../ide/media/vxmodule_icon.gif)|Módulo|![Símbolo do item de mapa](../ide/media/vxmapitem_icon.gif)|Item de Mapa|
|![Símbolo do método de extensão](../ide/media/extensionmethod.gif)|Método de extensão|![Símbolo de declaração](../ide/media/vxmethod_icon.gif)|Declaração externa|
|![Símbolo de delegado](../ide/media/vxdelegate_icon.gif)|Delegar|![Ícone de erro para Modo de Exibição de Classe e Pesquisador de Objetos](../ide/media/erroricon.gif)|Erro|
|![Símbolo de exceção](../ide/media/vxexception_icon.gif)|Exceção|![Símbolo de modelo](../ide/media/vxtemplate_icon.gif)|Modelo|
|![Símbolo de mapa](../ide/media/vxmap_icon.gif)|Mapeamento|![Símbolo de ponto de exclamação de erro](../ide/media/vxerror_icon.gif)|Unknown|
|![Símbolo de encaminhamento de tipo](../ide/media/ob_type_forward.gif)|Encaminhamento de tipo|||

> [!TIP]
> Para exibir melhor os ícones nesta página, verifique se seu tema de Microsoft Docs está definido como **Light**. Você pode alternar esse tema de cores do controle localizado na parte inferior esquerda da página, conforme mostrado na seguinte captura de tela:
>
> ![Tema do docs](../ide/media/toggle-docs-color-theme.png "Ativar/desativar o tema de cores para Microsoft Docs páginas")

## <a name="signal-icons"></a>Ícones de sinal

Os ícones de sinal a seguir aplicam-se a todos os ícones anteriores e indicam sua acessibilidade.

|ícone|Descrição|
|----------|-----------------|
|\<No Signal Icon>|Público. Acessível de qualquer lugar neste componente e de qualquer componente que faça referência a ele.|
|![Símbolo protegido por sinal](../ide/media/vxsignal_icon_key.gif)|Protegido. Acessível da classe ou do tipo recipiente ou daqueles derivados da classe ou do tipo recipiente.|
|![Símbolo privado de sinal](../ide/media/vxsignal_icon_lock.gif)|Privado. Acessível somente na classe ou no tipo recipiente.|
|![Símbolo selado por sinal](../ide/media/vxsignal_icon_envelope.gif)|Lacrado.|
|![Símbolo de amigo&#47;interno de sinal](../ide/media/vxsignal_icon_diamond.gif)|Amigo/interno. Acessível somente no projeto.|
|![Seta do ícone de sinal](../ide/media/vxsignal_icon_arrow.gif)|Atalho. Um atalho para o objeto.|

> [!NOTE]
> Se seu projeto estiver incluído em um banco de dados de controle do código-fonte, ícones de sinal adicionais poderão ser exibidos para indicar o status de controle de origem, como check-in ou check-out.

> [!TIP]
> Para exibir mais imagens e ícones de aplicativos que aparecem no Visual Studio, baixe a [**biblioteca de imagens do Visual Studio**](https://www.microsoft.com/download/details.aspx?id=35825).

## <a name="see-also"></a>Confira também

- [Exibindo a estrutura do código](../ide/viewing-the-structure-of-code.md)
