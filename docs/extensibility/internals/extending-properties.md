---
title: Estendendo propriedades | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Properties window, providing support
ms.assetid: 68e2cbd4-861c-453f-8c9f-4ab6afc80e67
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 77b5861dd084098e561f3642b5738dd0279d4b52
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39512103"
---
# <a name="extend-properties"></a>Estender propriedades
O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **Properties** janela é um navegador de propriedade universal para componentes COM e COM+ e dá suporte a todas [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] produtos. O **propriedades** janela funciona com `ITypeInfo` COM+ metadados para listar as propriedades de tempo de design para o objeto atualmente selecionado em outra janela no ambiente de desenvolvimento integrado (IDE) e informações de tipo.  
  
 O **propriedades** janela, que pode ser aberta pressionando **F4** no teclado, ou selecionando **janela propriedades** sobre a **exibição** menu, é usado para exibir e editar as propriedades de configuração independente, o tempo de design e eventos dos objetos selecionados. Propriedades dependentes de configuração, associadas com soluções e projetos, são exibidas na [páginas de propriedade](../../extensibility/internals/property-pages.md). Para obter mais informações, [gerenciar opções de configuração](../../extensibility/internals/managing-configuration-options.md).  
  
 ![Visão geral da janela de propriedades](../../extensibility/internals/media/vspropertieswindow.png "vsPropertiesWindow")  
Janela de Propriedades  
  
 Esta seção fornece informações detalhadas relacionadas às áreas individuais do **propriedades** janela e as interfaces que você deve implementar e chamar para preencher a janela.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Visão geral da janela de propriedades](../../extensibility/internals/properties-window-overview.md)  
 Explica a finalidade de **propriedades** janela em relação a janela de ferramentas e a janela do documento.  
  
 [Política de modelo e na janela Propriedades](../../extensibility/internals/template-policy-and-the-properties-window.md)  
 Discute como um projeto está contido em um projeto de modelo da empresa e como esse projeto de modelo empresarial pode impor a política.  
  
 [Interfaces e campos da janela Propriedades](../../extensibility/internals/properties-window-fields-and-interfaces.md)  
 Explica a base para a seleção que determina quais informações são exibidas na **propriedades** janela.  
  
 [Lista de objetos de janela de propriedades](../../extensibility/internals/properties-window-object-list.md)  
 Descreve a finalidade do **propriedades** lista de objetos de janela, que descreve como fazer isso, quando um objeto diferente desta lista dispara uma chamada, o ambiente é informado de que um novo objeto foi selecionado.  
  
 [Botões da janela Propriedades](../../extensibility/internals/properties-window-buttons.md)  
 Explica a finalidade dos botões de quatro padrão exibidos na **propriedades** de ferramentas da janela.  
  
 [Grade de exibição de propriedades](../../extensibility/internals/properties-display-grid.md)  
 Explica onde os nomes de propriedade e os campos de valores de propriedade são encontrados na grade.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Tipos de projeto](../../extensibility/internals/project-types.md)  
 Discute os projetos como blocos de construção do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE.  
  
 [Compilação e build](../../ide/compiling-and-building-in-visual-studio.md)  
 Descreve como você pode usar o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] plataforma para continuamente testar e depurar aplicativos, conforme você criá-los.  
  
 [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)  
 Descreve o `IDispatch` interface, que primeiro foi projetado para oferecer suporte à automação, fornecendo um mecanismo de associação tardia para acessar e recuperar informações sobre os métodos e propriedades de um objeto.  
  
 [Gerenciar configurações do aplicativo (.NET)](../../ide/managing-application-settings-dotnet.md)  
 Fornece uma visão geral das configurações do aplicativo que permitem que você configure seu aplicativo para que os valores de propriedade são armazenados em um arquivo de configuração externo em vez de código compilado do aplicativo.  
  
 [Soluções e Projetos](../../ide/solutions-and-projects-in-visual-studio.md)  
 Explica como [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] gerencia com eficiência os itens como referências, conexões de dados, pastas e arquivos que são exigidos por seu esforço de desenvolvimento por meio de soluções e projetos.  
  
 [Estender outras partes do Visual Studio](../../extensibility/extending-other-parts-of-visual-studio.md)  
 Explica como usar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] services para criar elementos de interface do usuário que correspondem ao restante do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].