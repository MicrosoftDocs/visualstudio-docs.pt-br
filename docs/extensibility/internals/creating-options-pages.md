---
title: Criando páginas de opções | Microsoft Docs
description: Saiba como criar uma página de opções no menu ferramentas no Visual Studio implementando uma classe DialogPage da estrutura de pacote gerenciado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed package framework, creating Tools Options pages
- Tools Options pages [Visual Studio SDK], creating using managed package framework
ms.assetid: 1bf11fec-dece-4943-8053-6de1483c43eb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2e7513617ab4ee4a051dd48cd110ecb2c5e22495
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056825"
---
# <a name="create-options-pages"></a>Criar páginas de opções
Na [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] estrutura de pacote gerenciado, as classes derivadas de <xref:Microsoft.VisualStudio.Shell.DialogPage> estender o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE adicionando as páginas de **Opções** no menu **ferramentas** .

 Um objeto que implementa uma determinada página de **opção de ferramentas** é associado a VSPackages específicos pelo <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> objeto.

 Como o ambiente cria uma instância do objeto que implementa uma página de **Opções de ferramentas** em particular quando essa página específica é exibida pelo IDE:

- Uma página de **Opções de ferramentas** deve ser implementada em seu próprio objeto e não no objeto que implementa um VSPackage.

- Um objeto não pode implementar várias páginas de **Opções de ferramentas** .

## <a name="register-as-a-tools-options-page-provider"></a>Registrar como um provedor de páginas de opções de ferramentas
 Um VSPackage que dá suporte à configuração de usuário por meio das páginas de **Opções de ferramentas** indica os objetos que fornecem as páginas de **Opções de ferramentas** aplicando instâncias do <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> aplicadas à <xref:Microsoft.VisualStudio.Shell.Package> implementação.

 Deve haver uma instância do <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> para cada <xref:Microsoft.VisualStudio.Shell.DialogPage> tipo derivado que implemente uma página de **Opções de ferramentas** .

 Cada instância do <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> usa o tipo que implementa a página **Opções de ferramentas** , cadeias de caracteres que contêm a categoria e a subcategoria usadas para identificar uma página de opções de **ferramentas** e informações de recurso para registrar o tipo como fornecendo uma página de **Opções de ferramentas** .

## <a name="persist-tools-options-page-state"></a>Opções das ferramentas de persistência estado da página
 Se uma implementação de página de **Opções de ferramentas** estiver registrada com o suporte de automação habilitado, o IDE persiste o estado da página junto com todas as outras páginas de **Opções de ferramentas** .

 Um VSPackage pode gerenciar sua própria persistência usando o <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> . Somente um ou outro método de persistência deve ser usado.

## <a name="implement-dialogpage-class"></a>Implementar classe DialogPage
 Um objeto que fornece a implementação de um tipo derivado de um VSPackage <xref:Microsoft.VisualStudio.Shell.DialogPage> pode aproveitar os seguintes recursos herdados:

- Uma janela de interface do usuário padrão.

- Um mecanismo de persistência padrão disponível se <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> for aplicado à classe ou se a <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute.SupportsProfiles%2A> propriedade for definida como `true` para o <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> que é aplicado à classe.

- Suporte à automação.

  O requisito mínimo para um objeto que implementa uma página de **Opções de ferramentas** usando <xref:Microsoft.VisualStudio.Shell.DialogPage> é a adição de propriedades públicas.

  Se a classe estiver devidamente registrada como um provedor de páginas de **Opções de ferramentas** , suas propriedades públicas estarão disponíveis na seção **Opções** do menu **ferramentas** na forma de uma grade de propriedades.

  Todos esses recursos padrão podem ser substituídos. Por exemplo, para criar uma interface de usuário mais sofisticada, é necessário substituir apenas a implementação padrão do <xref:Microsoft.VisualStudio.Shell.DialogPage.Window%2A> .

## <a name="example"></a>Exemplo
 O que vem a seguir é uma implementação simples de "Olá mundo" de uma página de opções. Adicionar o código a seguir a um projeto padrão criado pelo modelo de pacote do Visual Studio com a opção de **comando de menu** selecionada irá demonstrar adequadamente a funcionalidade da página de opções.

### <a name="description"></a>Descrição
 A classe a seguir define uma página de opções mínima "Olá, mundo". Quando aberto, o usuário pode definir a `HelloWorld` propriedade pública em uma grade de propriedades.

### <a name="code"></a>Código
 [!code-csharp[UI_UserSettings_ToolsOptionPages#11](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_1.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#11](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_1.vb)]

### <a name="description"></a>Descrição
 Aplicar o atributo a seguir à classe de pacote disponibiliza a página opções quando o pacote é carregado. Os números são IDs de recursos arbitrários para a categoria e a página, e o valor booliano no final especifica se a página oferece suporte à automação.

### <a name="code"></a>Código
 [!code-csharp[UI_UserSettings_ToolsOptionPages#07](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_2.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#07](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_2.vb)]

### <a name="description"></a>Descrição
 O manipulador de eventos a seguir exibe um resultado, dependendo do valor do conjunto de propriedades na página opções. Ele usa o <xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A> método com o resultado convertido explicitamente no tipo de página de opção personalizada para acessar as propriedades expostas pela página.

 No caso de um projeto gerado pelo modelo de pacote, chame essa função da `MenuItemCallback` função para anexá-la ao comando padrão adicionado ao menu **ferramentas** .

### <a name="code"></a>Código
 [!code-csharp[UI_UserSettings_ToolsOptionPages#08](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_3.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#08](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_3.vb)]

## <a name="see-also"></a>Confira também
- [Estender as configurações e opções de usuário](../../extensibility/extending-user-settings-and-options.md)
- [Suporte de automação para páginas de opções](../../extensibility/internals/automation-support-for-options-pages.md)
