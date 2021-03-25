---
title: Grade de exibição de propriedades | Microsoft Docs
description: Saiba onde os campos nomes de propriedade e valores de propriedade são encontrados na grade na janela Propriedades e como trabalhar com a grade em Propriedades de extensão.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- properties [Visual Studio SDK], grid
ms.assetid: 318e41b0-acf5-4842-b85e-421c9d5927c5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9ccf8afd293c47a1eb55b0b57b8190c11492cfa8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061115"
---
# <a name="properties-display-grid"></a>Grade de exibição de propriedades

A janela **Propriedades** exibe os campos em uma grade. A coluna à esquerda contém os nomes das propriedades; a coluna da direita contém os valores de propriedade.

## <a name="work-with-the-grid"></a>Trabalhar com a grade

A lista de duas colunas mostra as propriedades independentes de configuração que podem ser alteradas em tempo de design e suas configurações atuais. Observe que todas as propriedades podem não ser mostradas. Uma propriedade pode ser definida como oculta, por exemplo, implementando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A> método. Especificamente, para ocultar propriedades que têm propriedades filho:

1. Defina o `pfDisplay` parâmetro em <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.DisplayChildProperties%2A> para `FALSE` .

2. Defina o `pfHide` parâmetro em <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A> para `TRUE` .

Para enviar informações por push para a janela **Propriedades** , o IDE usa <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> . <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> é chamado por VSPackages para cada janela que contém objetos selecionáveis com propriedades relacionadas a serem exibidas na janela **Propriedades** . **Gerenciador de soluções** a implementação de <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> chamadas `GetProperty` usando [__VSHPROPID. VSHPROPID_BrowseObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>) na hierarquia do projeto para adquirir os objetos navegáveis na hierarquia.

Se seu VSPackage não oferecer suporte a [__VSHPROPID. VSHPROPID_BrowseObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>), o IDE tenta usar <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> usando o valor para [__VSHPROPID. VSHPROPID_SelContainer](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_SelContainer>) que o item de hierarquia ou os itens são fornecidos.

Seu projeto VSPackage não precisa ser criado <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> porque o pacote de janela fornecido pelo IDE que o implementa (por exemplo, **Gerenciador de soluções**) constrói <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> em seu nome.

<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> consiste em três métodos que são chamados pelo IDE:

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.CountObjects%2A> contém o número de objetos selecionados a serem exibidos na janela **Propriedades** .

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> Retorna os `IDispatch` objetos selecionados para serem exibidos na janela **Propriedades** .

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> torna possível que qualquer um dos objetos retornados pelo <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> seja selecionado pelo usuário. Isso permite que o VSPackage atualize visualmente a seleção exibida para o usuário na interface de usuário.

A janela **Propriedades** extrai informações dos `IDispatch` objetos para recuperar as propriedades que estão sendo procuradas. O navegador de propriedades usa `IDispatch` para perguntar ao objeto quais propriedades ele dá suporte por meio `ITypeInfo` de consulta, que é obtido do `IDispatch::GetTypeInfo` . O navegador usa esses valores para preencher a janela **Propriedades** e alterar os valores de propriedades individuais exibidas na grade. As informações de propriedades são mantidas no próprio objeto.

Como os objetos retornados dão suporte `IDispatch` , o chamador pode obter informações como o nome do objeto chamando um `IDispatch::Invoke` ou `ITypeInfo::Invoke` com um DISPID (identificador de expedição predefinido) que representa as informações desejadas. Os DISPIDs declarados são negativos para garantir que não entrem em conflito com identificadores definidos pelo usuário.

A janela **Propriedades** exibe diferentes tipos de campos, dependendo dos atributos de propriedades específicas de um objeto selecionado. Esses campos incluem caixas de edição, listas suspensas e links para caixas de diálogo do editor personalizado.

- Os valores contidos em uma lista enumerada são recuperados por uma <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> consulta para `IDispatch` . Os valores obtidos de uma lista enumerada podem ser alterados na grade de propriedades clicando duas vezes no nome do campo ou clicando no valor e selecionando o novo valor na lista suspensa. Para propriedades que têm configurações predefinidas de listas enumeradas, clicar duas vezes no nome da propriedade na lista Propriedades percorre as opções disponíveis. Para propriedades predefinidas com apenas duas opções, como true/false, clique duas vezes no nome da propriedade para alternar entre as opções.

- Se <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HasDefaultValue%2A> estiver `false` , indicando que o valor foi alterado, o valor será exibido em negrito. <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.CanResetPropertyValue%2A> é usado para determinar se o valor pode ser redefinido para o valor original. Nesse caso, você pode alterar de volta para o padrão clicando com o botão direito do mouse no valor e escolhendo **Redefinir** no menu exibido. Caso contrário, você precisará alterar o valor de volta para o padrão manualmente. <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> também permite localizar e ocultar os nomes das propriedades exibidas durante o tempo de design, mas não afeta os nomes de propriedade exibidos durante o tempo de execução.

- Clicar no botão de reticências (...) exibe uma lista de valores de propriedade dos quais o usuário pode selecionar (como um seletor de cores ou uma lista de fontes). <xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder> fornece esses valores.

## <a name="see-also"></a>Confira também

- [Estender Propriedades](../../extensibility/internals/extending-properties.md)
