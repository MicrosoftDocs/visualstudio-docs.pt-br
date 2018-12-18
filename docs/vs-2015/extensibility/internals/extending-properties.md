---
title: Estendendo propriedades | Microsoft Docs
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
- Properties window, providing support
ms.assetid: 68e2cbd4-861c-453f-8c9f-4ab6afc80e67
caps.latest.revision: 19
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 919b5a08f003d6e6c320edef4c1321af35f17388
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51777871"
---
# <a name="extending-properties"></a>Estendendo propriedades
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **Properties** janela é um navegador de propriedade universal para componentes COM e COM+ e dá suporte a todas [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] produtos. O **propriedades** janela funciona com `ITypeInfo` COM+ metadados para listar as propriedades de tempo de design para o objeto atualmente selecionado em outra janela no ambiente de desenvolvimento integrado (IDE) e informações de tipo.  
  
 O **propriedades** janela, que pode ser aberta pressionando F4 no teclado, ou selecionando **janela propriedades** sobre o **exibição** menu, é usado para exibir e editar Propriedades de configuração independente, o tempo de design e eventos dos objetos selecionados. Propriedades dependentes de configuração, associadas com soluções e projetos, são exibidas na [páginas de propriedade](../../extensibility/internals/property-pages.md). Para obter mais informações, consulte [propriedades do projeto: NIB](http://msdn.microsoft.com/en-us/fb126574-24ad-4c96-9b2b-6e1f3879ba50), [gerenciar opções de configuração](../../extensibility/internals/managing-configuration-options.md), e [gerenciamento NIB: Item em projetos](http://msdn.microsoft.com/en-us/762e606b-7f44-4b66-97a1-e30a703654a0).  
  
 ![Visão geral da janela de propriedades](../../extensibility/internals/media/vspropertieswindow.png "vsPropertiesWindow")  
Janela de Propriedades  
  
 Esta seção fornece informações detalhadas relacionadas às áreas individuais do **propriedades** janela e as interfaces que você deve implementar e chamar para preencher a janela.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Visão geral da janela de propriedades](../../extensibility/internals/properties-window-overview.md)  
 Explica a finalidade de **propriedades** janela em relação a janela de ferramentas e a janela do documento.  
  
 [Política de modelo e a janela Propriedades](../../extensibility/internals/template-policy-and-the-properties-window.md)  
 Discute como um projeto está contido em um projeto de modelo da empresa e como esse projeto de modelo empresarial pode impor a política.  
  
 [Interfaces e campos da janela Propriedades](../../extensibility/internals/properties-window-fields-and-interfaces.md)  
 Explica a base para a seleção que determina quais informações são exibidas na **propriedades** janela.  
  
 [Lista de objetos da janela Propriedades](../../extensibility/internals/properties-window-object-list.md)  
 Descreve a finalidade do **propriedades** lista de objetos de janela, que descreve como fazer isso, quando um objeto diferente desta lista dispara uma chamada, o ambiente é informado de que um novo objeto foi selecionado.  
  
 [Botões da janela Propriedades](../../extensibility/internals/properties-window-buttons.md)  
 Explica a finalidade dos botões de quatro padrão exibidos na **propriedades** de ferramentas da janela.  
  
 [Grade de exibição de propriedades](../../extensibility/internals/properties-display-grid.md)  
 Explica onde os nomes de propriedade e os campos de valores de propriedade são encontrados na grade.  
  
 [Anunciando o acompanhamento da seleção da janela Propriedades](../../misc/announcing-property-window-selection-tracking.md)  
 Descreve a seleção de acompanhamento para o **propriedades** janela.  
  
 [Ocultar propriedades que têm propriedades filho](../../misc/hiding-properties-that-have-child-properties.md)  
 Explica como ocultar propriedades que têm propriedades filho Implementando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> interface.  
  
 [Fornecendo uma janela Propriedades personalizada](../../misc/providing-a-custom-properties-window.md)  
 Detalha as etapas para fornecer seu próprio navegador de propriedade.  
  
 [Obtendo descrições dos campos na janela Propriedades](../../misc/getting-field-descriptions-from-the-properties-window.md)  
 Explica onde encontrar a área de descrição que exibe informações relacionadas ao campo de propriedade selecionada.  
  
 [Atualizando valores de propriedade na janela Propriedades](../../misc/updating-property-values-in-the-properties-window.md)  
 Fornece instruções passo a passo que mostram duas maneiras de manter o **propriedades** janela sincronizados com o valor da propriedade muda.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Tipos de projeto](../../extensibility/internals/project-types.md)  
 Discute os projetos como blocos de construção do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE.  
  
 [Compilando e criando](../../ide/compiling-and-building-in-visual-studio.md)  
 Descreve como você pode usar o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] plataforma para continuamente testar e depurar aplicativos, conforme você criá-los.  
  
 [Propriedades do documento HTML, janela de propriedades](http://msdn.microsoft.com/library/46e3d164-a1a7-42f9-87b0-344e10a37b62)  
 Fornece instruções sobre como editar um documento HTML diretamente na janela de propriedades e fornece uma tabela detalhando os campos em um documento HTML na janela Propriedades.  
  
 [IDispatch](http://msdn.microsoft.com/en-us/ebbff4bc-36b2-4861-9efa-ffa45e013eb5)  
 Descreve o `IDispatch` interface, que primeiro foi projetado para oferecer suporte à automação, fornecendo um mecanismo de associação tardia para acessar e recuperar informações sobre os métodos e propriedades de um objeto.  
  
 [NIB: Introdução a propriedades dinâmicas (Visual Studio)](http://msdn.microsoft.com/en-us/f5102027-1431-4195-ae40-9b991de46d3a)  
 Fornece uma visão geral das propriedades dinâmicas que permitem que você configure seu aplicativo para que os valores de propriedade são armazenados em um arquivo de configuração externo em vez de código compilado do aplicativo.  
  
 [NIB: projetos como contêineres](http://msdn.microsoft.com/en-us/87d40f63-f487-4767-8963-64beec27ba1b)  
 Descreve a função do projeto como um contêiner em uma solução para gerenciar logicamente, compilar e depurar os itens que compõem seu aplicativo.  
  
 [Propriedades do NIB: projeto](http://msdn.microsoft.com/en-us/fb126574-24ad-4c96-9b2b-6e1f3879ba50)  
 Descreve como o projeto gerencia configurações que permitem que você controle propriedades que se aplicam a todo o projeto e também propriedades que são limitadas a certas configurações de build do projeto.  
  
 [Soluções e projetos](../../ide/solutions-and-projects-in-visual-studio.md)  
 Explica como [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] gerencia com eficiência os itens como referências, conexões de dados, pastas e arquivos que são exigidos por seu esforço de desenvolvimento por meio de soluções e projetos.  
  
 [Estender outras partes do Visual Studio](../../extensibility/extending-other-parts-of-visual-studio.md)  
 Explica como usar [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] services para criar elementos de interface do usuário que correspondem ao restante do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].

