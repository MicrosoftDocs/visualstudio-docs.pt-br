---
title: Alterando as configurações de exibição usando a API herdada | Microsoft Docs
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
- editors [Visual Studio SDK], legacy - changing view settings
ms.assetid: 12c9b300-0894-4124-96a1-764326176d77
caps.latest.revision: 19
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: df84fa92cb0da8dd408b1cc8717628afa3d5ba19
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51730628"
---
# <a name="changing-view-settings-by-using-the-legacy-api"></a>Alterando as configurações de exibição usando a API herdada
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As configurações para recursos do editor de núcleo, como quebra automática de linha, margem de seleção e espaço virtual, podem ser alteradas pelo usuário por meio das **opções** caixa de diálogo. No entanto, também é possível alterar essas configurações programaticamente.  
  
## <a name="changing-settings-by-using-the-legacy-api"></a>Alterar as configurações usando a API herdada  
 O <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer> interface expõe um conjunto de propriedades do editor de texto. A exibição de texto contém uma categoria de propriedades (GUID_EditPropCategory_View_MasterSettings) que representa o grupo de configurações alteradas por meio de programação para a exibição de texto. Depois de exibir as configurações foram alteradas dessa maneira, eles não podem ser alterados a **opções** caixa de diálogo até que elas são redefinidas.  
  
 Veja a seguir o processo típico para alterar as configurações de exibição para uma instância do editor de núcleo.  
  
1.  Chame `QueryInterface` sobre o (<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>) para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer> interface.  
  
2.  Chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer.GetPropertyCategory%2A> método, especificando um valor de GUID_EditPropCategory_View_MasterSettings para o `rguidCategory` parâmetro.  
  
     Isso retorna um ponteiro para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer> interface, que contém o conjunto de propriedades forçados para o modo de exibição. Todas as configurações nesse grupo são forçadas permanentemente. Se uma configuração não está nesse grupo, ele seguirá as opções especificadas na **opções** caixa de diálogo ou os comandos do usuário.  
  
3.  Chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.SetProperty%2A> método, especificando o valor de configurações apropriadas no `idprop` parâmetro.  
  
     Por exemplo, para forçar a quebra automática de linha, chamar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.SetProperty%2A> e especifique um valor de VSEDITPROPID_ViewLangOpt_WordWrap, `vt` para o `idprop` parâmetro. Nessa chamada `vt` é uma VARIANTE do tipo VT_BOOL e `vt.boolVal` é VARIANT_TRUE.  
  
## <a name="resetting-changed-view-settings"></a>Redefinir as configurações de exibição alterada  
 Para redefinir a qualquer exibição alterada definindo-se para uma instância do editor de núcleo, chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.RemoveProperty%2A> método e especifique o valor de configuração apropriada no `idprop` parâmetro.  
  
 Por exemplo, para permitir que a quebra automática de flutuando livremente, você deve removê-lo da categoria de propriedade chamando <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.RemoveProperty%2A> e especificando um valor de VSEDITPROPID_ViewLangOpt_WordWrap para o `idprop` parâmetro.  
  
 Para remover configurações tudo isso mudou para o editor de núcleo de uma vez, especifique um valor de VSEDITPROPID_ViewComposite_AllCodeWindowDefaults, vt para o `idprop` parâmetro. Nessa chamada, vt é uma VARIANTE do tipo VT_BOOL e vt.boolVal é VARIANT_TRUE.  
  
## <a name="see-also"></a>Consulte também  
 [Dentro do Editor de núcleo](../extensibility/inside-the-core-editor.md)   
 [Acessando o theText exibição usando a API herdada](../extensibility/accessing-thetext-view-by-using-the-legacy-api.md)   
 [Caixa de diálogo Opções](../ide/reference/options-dialog-box-visual-studio.md)

