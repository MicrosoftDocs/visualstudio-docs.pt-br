---
title: Grade de Exibição de Propriedades | Microsoft Docs
description: Saiba onde os nomes de propriedade e os campos de valores de propriedade são encontrados na grade no janela Propriedades e como trabalhar com a grade na extensão de propriedades.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- properties [Visual Studio SDK], grid
ms.assetid: 318e41b0-acf5-4842-b85e-421c9d5927c5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ee3d7d8d6277f9cfa0352cb4961644e4860b46bb
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899648"
---
# <a name="properties-display-grid"></a>Grade de exibição de propriedades

A **janela** Propriedades exibe campos dentro de uma grade. A coluna à esquerda contém os nomes de propriedade; a coluna à direita contém os valores de propriedade.

## <a name="work-with-the-grid"></a>Trabalhar com a grade

A lista de duas colunas mostra propriedades independentes de configuração que podem ser alteradas em tempo de design e suas configurações atuais. Observe que todas as propriedades podem não ser mostradas. Uma propriedade pode ser definida como oculta, por exemplo, implementando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A> método . Especificamente, para ocultar propriedades que têm propriedades filho:

1. De definir `pfDisplay` o parâmetro em como <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.DisplayChildProperties%2A> `FALSE` .

2. De definir `pfHide` o parâmetro em como <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A> `TRUE` .

Para fazer push de informações para **a janela Propriedades,** o IDE usa <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> . <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> é chamado pelo VSPackages para cada janela que contém objetos selecionáveis com propriedades relacionadas a serem exibidas na **janela** Propriedades. **Gerenciador de Soluções** implementação de chamadas <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> usando `GetProperty` [__VSHPROPID. VSHPROPID_BrowseObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>) na hierarquia do projeto para adquirir os objetos navegáveis na hierarquia.

Se o VSPackage não tiver suporte [para __VSHPROPID. VSHPROPID_BrowseObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>), o IDE tenta usar <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> o valor para [__VSHPROPID. VSHPROPID_SelContainer](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_SelContainer>) que o item de hierarquia ou itens fornecem.

Seu projeto VSPackage não precisa criar porque o pacote de janela fornecido pelo IDE que o implementa (por exemplo, Gerenciador de Soluções ) constrói em <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> seu  <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> nome.

<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> consiste em três métodos que são chamados pelo IDE:

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.CountObjects%2A> contém o número de objetos selecionados para serem exibidos na **janela** Propriedades.

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> retorna os `IDispatch` objetos selecionados para serem exibidos na **janela** Propriedades.

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> possibilita que qualquer um dos objetos retornados por <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> seja selecionado pelo usuário. Isso permite que o VSPackage atualize visualmente a seleção exibida para o usuário na interface do usuário.

A **janela** Propriedades extrai informações dos `IDispatch` objetos para recuperar as propriedades que estão sendo procuradas. O navegador Properties usa para perguntar ao objeto quais propriedades ele dá suporte `IDispatch` consultando `ITypeInfo` , que é obtido de `IDispatch::GetTypeInfo` . Em seguida, o navegador usa esses valores para preencher a **janela Propriedades** e alterar os valores das propriedades individuais exibidas na grade. As informações de propriedades são mantidas dentro do próprio objeto.

Como os objetos retornados são suportados, o chamador pode obter informações como o nome do objeto chamando ou com um DISPID (identificador de expedição) predefinido que representa as `IDispatch` `IDispatch::Invoke` informações `ITypeInfo::Invoke` desejadas. DispIDs declarados são negativos para garantir que não entre em conflito com identificadores definidos pelo usuário.

A **janela** Propriedades exibe diferentes tipos de campos, dependendo dos atributos de propriedades específicas de um objeto selecionado. Esses campos incluem caixas de edição, listas listadas e links para caixas de diálogo personalizadas do editor.

- Os valores contidos em uma lista enumerada são recuperados por <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> uma consulta para `IDispatch` . Os valores obtidos de uma lista enumerada podem ser alterados na grade de propriedades clicando duas vezes no nome do campo ou clicando no valor e selecionando o novo valor na listada. Para propriedades que têm configurações predefinida de listas enumeradas, clicar duas vezes no nome da propriedade na lista Propriedades passa pelas opções disponíveis. Para propriedades predefinidos com apenas duas opções, como true/false, clique duas vezes no nome da propriedade para alternar entre as opções.

- Se <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HasDefaultValue%2A> for `false` , indicando que o valor foi alterado, o valor será exibido em negrito. <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.CanResetPropertyValue%2A> é usado para determinar se o valor pode ser redefinido para o valor original. Nesse caso, você pode alterar de volta para o padrão clicando com o botão direito do mouse no valor e escolhendo Redefinir **no** menu exibido. Caso contrário, você precisa alterar o valor de volta para o padrão manualmente. <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> também permite que você localize e o hide os nomes das propriedades exibidas durante o tempo de design, mas não afeta os nomes de propriedade exibidos durante o tempo de operação.

- Clicar no botão de reellipse (...) exibe uma lista de valores de propriedade da qual o usuário pode selecionar (como um seletor de cores ou uma lista de fontes). <xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder> fornece esses valores.

## <a name="see-also"></a>Confira também

- [Estender propriedades](../../extensibility/internals/extending-properties.md)
