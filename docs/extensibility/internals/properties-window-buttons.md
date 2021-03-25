---
title: Botões da janela Propriedades | Microsoft Docs
description: Saiba mais sobre os botões exibidos por padrão na barra de ferramentas para o janela Propriedades e sobre a implementação dos botões.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, buttons
ms.assetid: bdd2e3a7-ae6e-4e88-be1a-e0e3b7ddbbcc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 88eacbdbcc50dc843769cdcf4701ba1a2bfe895a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061063"
---
# <a name="properties-window-buttons"></a>Botões da janela Propriedades
Dependendo da linguagem de desenvolvimento e do tipo de produto, determinados botões são exibidos por padrão na barra de ferramentas da janela **Propriedades** . Em todos os casos, os botões **Categorizado**, em **ordem alfabética**, **Propriedades** e **páginas de propriedades** são exibidos. No Visual C# e Visual Basic, o botão **eventos** também é exibido. Em determinados projetos de Visual C++, as **mensagens do vc + +** e os botões de **substituições do vc** são exibidos. Botões adicionais podem ser exibidos para outros tipos de projeto. Para obter mais informações sobre os botões na janela **Propriedades** , consulte [janela Propriedades](../../ide/reference/properties-window.md).

## <a name="implementation-of-properties-window-buttons"></a>Implementação de botões da janela Propriedades
 Quando você clica no botão **Categorizado** , o Visual Studio chama a <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> interface no objeto que tem o foco para classificar suas propriedades por categoria. <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> é implementado no `IDispatch` objeto que é apresentado à janela **Propriedades** .

 Há 11 categorias de propriedades predefinidas, que têm valores negativos. Você pode definir categorias personalizadas, mas é recomendável atribuí-las a valores positivos para diferenciá-las das categorias predefinidas.

 O <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.MapPropertyToCategory%2A> método retorna o valor da categoria de propriedade apropriado para a propriedade especificada. O <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.GetCategoryName%2A> método retorna uma cadeia de caracteres que contém o nome da categoria. Você só precisa fornecer suporte para valores de categoria personalizados porque o Visual Studio conhece os valores de categoria de propriedade padrão.

 Quando você clica no botão em **ordem alfabética** , as propriedades são exibidas em ordem alfabética por nome. Os nomes são recuperados de `IDispatch` acordo com um algoritmo de classificação localizado.

 Quando a janela **Propriedades** estiver aberta, o botão **Propriedades** será mostrado automaticamente como selecionado. Em outras partes do ambiente, o mesmo botão é exibido e você pode clicar nele para mostrar a janela **Propriedades** .

 O botão **páginas de propriedades** não estará disponível se `ISpecifyPropertyPages` não estiver implementado para o objeto selecionado. As páginas de propriedades exibem propriedades dependentes da configuração que normalmente são associadas a soluções e projetos, mas também podem ser associadas a itens de projeto (por exemplo, em Visual C++).

> [!NOTE]
> Não é possível adicionar botões da barra de ferramentas à janela **Propriedades** usando código não gerenciado. Para adicionar um botão da barra de ferramentas, você deve criar um objeto gerenciado que derive de <xref:System.Windows.Forms.Design.PropertyTab> .

## <a name="see-also"></a>Confira também
- [Estendendo propriedades](../../extensibility/internals/extending-properties.md)
