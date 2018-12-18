---
title: Visão geral da janela de propriedades | Microsoft Docs
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
- Properties window
ms.assetid: 289ed4f2-02ac-4899-855e-42dfe57ee05f
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8b733a6845a61a71f15d8574666b345dedbf6f50
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51752092"
---
# <a name="properties-window-overview"></a>Visão geral da janela Propriedades
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O **propriedades** janela é usada para exibir as propriedades de objetos selecionados os dois tipos principais do windows disponíveis no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE). Esses dois tipos de janelas são:  
  
-   Janelas de ferramentas como o Gerenciador de soluções, o modo de exibição de classe e o objeto de navegador  
  
-   Janelas de documento que contém tais editores e designers como o designer de formulários, o editor de XML e o editor de HTML  
  
## <a name="using-the-properties-window"></a>Usando a janela Propriedades  
 O **propriedades** janela exibe as propriedades de um único ou vários itens selecionados. Se forem selecionados vários itens, a interseção de todas as propriedades de todos os objetos selecionados é exibida.  
  
 Eventos relacionados a um objeto selecionado dentro de uma janela de design do formulário ou o editor de HTML usando metadados de COM+ são exibidos na **propriedades** janela. Por exemplo, você pode selecionar um botão e exibir os eventos associados, como um `OnClick` evento, que pode ser vinculado a esse botão.  
  
 Os eventos exibidos na **propriedades** janela são usados principalmente com objetos que estão vinculados ao código. Se você estiver editando um formato de arquivo que não tem nada a ver com o código, você não pretende ter todos os eventos. Eventos são exibidos apenas na **propriedades** janela quando há uma associação entre a execução de código e alguns eventos associados a objetos específicos. Um exemplo disso seria o código por trás de um objeto selecionado que é executado quando esse objeto é ativado.  
  
 A tabela a seguir lista as interfaces principais usadas pelos **propriedades** janela.  
  
|Nome da interface|Descrição|  
|--------------------|-----------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties>|Fornece uma lista de categorias para o **propriedades** janela e mapeia cada propriedade para uma categoria.|  
|[Interface IDispatch](http://msdn.microsoft.com/en-us/ebbff4bc-36b2-4861-9efa-ffa45e013eb5)|Expõe métodos e propriedades para ferramentas e outros aplicativos que oferecem suporte à automação de programação de um objeto.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder>|Fornece botões de reticências (...) chamados *construtores* que abrir janelas de caixa de diálogo modal implementadas pelo objeto em si. Usado quando um valor não é facilmente digitado pelo usuário em um campo de texto. Por exemplo, ele pode ser usado para abrir um seletor de cores que determina o valor RGB para você.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>|Fornece acesso a objetos usados para atualizar as informações exibidas na **propriedades** janela. <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> é implementado por VSPackages para cada janela que contém objetos selecionáveis com propriedades relacionadas a ser exibido.|  
|<xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo>|Fornece informações sobre o tipo de um objeto como métodos de uma interface e campos de uma estrutura.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>|Permite que os VSPackages para receber notificações de eventos de seleção e recuperar informações sobre a hierarquia de projeto atual, item, valor do elemento e o contexto de interface do usuário do comando.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiItemSelect>|Fornece o ambiente com acesso a várias seleções.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>|Usado para fornecer nomes localizados em algumas propriedades exibidas na **propriedades** janela.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents>|Notifica os VSPackages registrados de alterações para a seleção atual, o valor do elemento ou o contexto de interface do usuário do comando.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>|Notifica o ambiente de uma alteração na seleção atual e fornece acesso às informações de hierarquia e de item relacionado à nova seleção.|  
  
 Para obter mais informações sobre `IDispatch`, consulte a biblioteca MSDN.  
  
## <a name="see-also"></a>Consulte também  
 [Estendendo propriedades](../../extensibility/internals/extending-properties.md)   
 [Interfaces e campos da janela Propriedades](../../extensibility/internals/properties-window-fields-and-interfaces.md)

