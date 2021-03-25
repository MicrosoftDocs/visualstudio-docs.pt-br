---
title: Estendendo propriedades | Microsoft Docs
description: Saiba mais sobre as interfaces que você deve implementar e chame para estender a lista de propriedades no janela Propriedades do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, providing support
ms.assetid: 68e2cbd4-861c-453f-8c9f-4ab6afc80e67
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3b1006f74cd2de03b4fe74e090d7ffcd1c921e5d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069641"
---
# <a name="extend-properties"></a>Estender Propriedades
A [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] janela **Propriedades** é um navegador de propriedades universal para componentes com e com+ e dá suporte a todos os [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] produtos. A janela **Propriedades** funciona com `ITypeInfo` informações de tipo e metadados com+ para listar as propriedades de tempo de design para o objeto atualmente selecionado em qualquer outra janela no IDE (ambiente de desenvolvimento integrado).

 A janela **Propriedades** , que pode ser aberta pressionando-se **F4** no teclado, ou selecionando **janela Propriedades** no menu **Exibir** , é usada para exibir e editar propriedades de tempo de design, independentes de configuração e eventos de objetos selecionados. Propriedades dependentes de configuração, associadas a soluções e projetos, são exibidas em [páginas de propriedades](../../extensibility/internals/property-pages.md). Para obter mais informações, [Gerenciar opções de configuração](../../extensibility/internals/managing-configuration-options.md).

 ![Visão geral de janela Propriedades](../../extensibility/internals/media/vspropertieswindow.png "vsPropertiesWindow") janela Propriedades

 Esta seção fornece informações detalhadas relacionadas às áreas individuais da janela **Propriedades** e às interfaces que você deve implementar e chamar para popular a janela.

## <a name="in-this-section"></a>Nesta seção
- [Visão geral de janela Propriedades](../../extensibility/internals/properties-window-overview.md)

 Explica a finalidade da janela **Propriedades** em relação à janela de ferramentas e à janela do documento.

- [Política de modelo e o janela Propriedades](../../extensibility/internals/template-policy-and-the-properties-window.md)

 Discute como um projeto está contido em um projeto de modelo empresarial e como esse projeto de modelo corporativo pode impor a política.

- [janela Propriedades campos e interfaces](../../extensibility/internals/properties-window-fields-and-interfaces.md)

 Explica a base para a seleção que determina quais informações são exibidas na janela **Propriedades** .

- [Lista de objetos de janela Propriedades](../../extensibility/internals/properties-window-object-list.md)

 Descreve a finalidade da lista de objetos da janela **Propriedades** , descrevendo como, quando um objeto diferente dessa lista disparar uma chamada, o ambiente é informado de que um novo objeto foi selecionado.

- [Botões de janela Propriedades](../../extensibility/internals/properties-window-buttons.md)

 Explica a finalidade dos quatro botões padrão exibidos na barra de ferramentas da janela **Propriedades** .

- [Grade de exibição de propriedades](../../extensibility/internals/properties-display-grid.md)

 Explica onde os campos nomes de propriedade e valores de propriedade são encontrados na grade.

## <a name="related-sections"></a>Seções relacionadas
- [Tipos de projeto](../../extensibility/internals/project-types.md)

 Discute projetos como os blocos de construção do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE.

- [Compilar e criar](../../ide/compiling-and-building-in-visual-studio.md)

 Descreve como você pode usar a [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] plataforma para testar continuamente e depurar aplicativos à medida que os cria.

- [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)

 Descreve a `IDispatch` interface, que foi projetada primeiro para oferecer suporte à automação, fornecendo um mecanismo de ligação tardia para acessar e recuperar informações sobre os métodos e as propriedades de um objeto.

- [Gerenciar configurações de aplicativo (.NET)](../../ide/managing-application-settings-dotnet.md)

 Fornece uma visão geral das configurações do aplicativo que permitem configurar seu aplicativo para que os valores de propriedade sejam armazenados em um arquivo de configuração externo em vez do código compilado do aplicativo.

- [Soluções e projetos](../../ide/solutions-and-projects-in-visual-studio.md)

 Explica como [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o gerencia com eficiência os itens como referências, conexões de dados, pastas e arquivos que são necessários para seu esforço de desenvolvimento por meio de soluções e projetos.

- [Estender outras partes do Visual Studio](../../extensibility/extending-other-parts-of-visual-studio.md)

 Explica como usar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] os serviços do para criar elementos de interface do usuário que correspondam ao restante do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .
