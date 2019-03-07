---
title: Botões da janela Propriedades | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, buttons
ms.assetid: bdd2e3a7-ae6e-4e88-be1a-e0e3b7ddbbcc
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e7726fe13c90c3a2732b7a6131ae4093a9051a62
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56625641"
---
# <a name="properties-window-buttons"></a>Botões da janela Propriedades
Dependendo da linguagem de desenvolvimento e o tipo de produto, determinados botões são exibidos por padrão na barra de ferramentas para o **propriedades** janela. Em todos os casos, o **categorizado**, **Alphabetized**, **propriedades**, e **páginas de propriedade** botões são exibidos. No Visual c# e Visual Basic, o **eventos** botão também é exibido. Em determinados projetos do Visual C++, o **mensagens do VC + +** e o **VC substitui** botões são exibidos. Botões adicionais podem ser exibidas para outros tipos de projeto. Para obter mais informações sobre os botões na **propriedades** janela, consulte [janela propriedades](../../ide/reference/properties-window.md).

## <a name="implementation-of-properties-window-buttons"></a>Implementação de botões da janela Propriedades
 Quando você clica o **categorizado** botão, o Visual Studio chama o <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> interface no objeto que tem o foco para classificar suas propriedades por categoria. <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> é implementado para o `IDispatch` objeto que é apresentado ao **propriedades** janela.

 Há 11 categorias de propriedade predefinidos, que têm valores negativos. Você pode definir as categorias personalizadas, mas é recomendável que você atribua-os valores positivos para distingui-las das categorias predefinidas.

 O <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.MapPropertyToCategory%2A> método retorna o valor de categoria de propriedade apropriada para a propriedade especificada. O <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.GetCategoryName%2A> método retorna uma cadeia de caracteres que contém o nome da categoria. Você só precisará fornecer suporte para valores de categoria personalizada porque o Visual Studio sabe os valores de categoria de propriedade padrão.

 Quando você clica o **Alphabetized** botão, as propriedades são exibidas em ordem alfabética por nome. Os nomes são recuperados pelo `IDispatch` acordo com um algoritmo de classificação localizado.

 Quando o **propriedades** janela estiver aberta, o **propriedades** botão automaticamente é mostrado como selecionado. Em outras partes do ambiente, o mesmo botão é exibido e você pode clicar nele para mostrar o **propriedades** janela.

 O **páginas de propriedades** botão não estará disponível se `ISpecifyPropertyPages` não está implementado para o objeto selecionado. Propriedades dependentes de configuração de exibição que são normalmente associadas com projetos e soluções de páginas de propriedade, mas eles ser também podem ser associadas a itens de projeto (por exemplo, no Visual C++).

> [!NOTE]
>  Não é possível adicionar botões de barra de ferramentas para o **propriedades** janela usando código não gerenciado. Para adicionar um botão de barra de ferramentas, você deve criar um objeto gerenciado que deriva de <xref:System.Windows.Forms.Design.PropertyTab>.

## <a name="see-also"></a>Consulte também
- [Estender as propriedades](../../extensibility/internals/extending-properties.md)