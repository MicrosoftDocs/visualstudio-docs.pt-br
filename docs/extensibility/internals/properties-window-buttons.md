---
title: Botões da janela Propriedades | Microsoft Docs
description: Saiba mais sobre os botões exibidos por padrão na barra de ferramentas para o janela Propriedades e sobre a implementação dos botões.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Properties window, buttons
ms.assetid: bdd2e3a7-ae6e-4e88-be1a-e0e3b7ddbbcc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a9c45d6cf0f271683c3c708bd71ef46377a5c5ca
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903444"
---
# <a name="properties-window-buttons"></a>Botões da janela Propriedades
Dependendo da linguagem de desenvolvimento e do tipo de produto, determinados botões são exibidos por padrão na barra de ferramentas da **janela** Propriedades. Em todos os casos, os **botões Categorizado,** Em **Ordem** Alfabética, **Propriedades** e **Páginas** de Propriedades são exibidos. No Visual C# e Visual Basic, **o botão** Eventos também é exibido. Em determinados Visual C++, as mensagens **VC++** e os **botões Substituições** de VC são exibidos. Botões adicionais podem ser exibidos para outros tipos de projeto. Para obter mais informações sobre botões na **janela Propriedades,** consulte [Janela Propriedades](../../ide/reference/properties-window.md).

## <a name="implementation-of-properties-window-buttons"></a>Implementação de botões da janela Propriedades
 Quando você clica no **botão Categorizado,** Visual Studio chama a interface no objeto que tem o foco para <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> classificar suas propriedades por categoria. <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> é implementado no `IDispatch` objeto que é apresentado à **janela** Propriedades.

 Há 11 categorias de propriedade predefinidos, que têm valores negativos. Você pode definir categorias personalizadas, mas recomendamos atribuí-las valores positivos para diferenciá-las das categorias predefinida.

 O <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.MapPropertyToCategory%2A> método retorna o valor de categoria de propriedade apropriado para a propriedade especificada. O <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.GetCategoryName%2A> método retorna uma cadeia de caracteres que contém o nome da categoria. Você só precisa fornecer suporte para valores de categoria personalizados porque Visual Studio os valores de categoria de propriedade padrão.

 Quando você clica no **botão Alfabético,** as propriedades são exibidas em ordem alfabética por nome. Os nomes são recuperados por `IDispatch` de acordo com um algoritmo de classificação localizado.

 Quando a **janela Propriedades** estiver aberta, o **botão** Propriedades será mostrado automaticamente conforme selecionado. Em outras partes do ambiente, o mesmo botão é exibido e você pode clicar nele para mostrar a **janela** Propriedades.

 O **botão Páginas de** Propriedades não estará disponível se não for implementado para o objeto `ISpecifyPropertyPages` selecionado. As páginas de propriedades exibem propriedades dependentes de configuração normalmente associadas a soluções e projetos, mas também podem ser associadas a itens de projeto (por exemplo, em Visual C++).

> [!NOTE]
> Não é possível adicionar botões de barra de ferramentas **à janela Propriedades** usando código nãomanagedo. Para adicionar um botão de barra de ferramentas, você deve criar um objeto gerenciado derivado de <xref:System.Windows.Forms.Design.PropertyTab> .

## <a name="see-also"></a>Confira também
- [Estendendo propriedades](../../extensibility/internals/extending-properties.md)
