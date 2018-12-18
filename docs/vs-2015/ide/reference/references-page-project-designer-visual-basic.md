---
title: Página Referências, Designer de Projeto (Visual Basic) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vb.ProjectPropertiesReference
- vb.ProjectPropertiesUnusedReference
- vb.ProjectPropertiesReferencePaths
helpviewer_keywords:
- References page in Project Designer
- Project Designer, References page
- Unused References dialog box
ms.assetid: 5a47c595-e084-401c-86e1-74e0bf74fd86
caps.latest.revision: 40
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 0dabf5b84eb1adde1d6e579b7ec5ad6a6c443723
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49859051"
---
# <a name="references-page-project-designer-visual-basic"></a>Página Referências, Designer de Projeto (Visual Basic)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Use a página **Referências** do **Designer de Projeto** para gerenciar referências, referências Web e namespaces importados em seu projeto. Projetos podem conter referências a componentes COM, serviços Web XML, assemblies ou bibliotecas de classes do .NET Framework ou outras bibliotecas de classes. Para obter mais informações sobre o uso de referências, consulte [Gerenciando referências em um projeto](../../ide/managing-references-in-a-project.md).  
  
 Para acessar a página **Referências**, escolha um nó de projeto (não o nó **Solução**) no **Gerenciador de Soluções**. Em seguida, escolha **Projeto**, **Propriedades** na barra de menus. Quando o Designer de Projeto for exibido, clique na guia **Referências**.  
  
## <a name="uielement-list"></a>Lista UIElement  
 As opções a seguir permitem selecionar ou remover referências e namespaces importados em seu projeto.  
  
 **Referências Não Utilizadas**  
 Clique neste botão para acessar a caixa de diálogo **Referências Não Utilizadas**.  
  
 A caixa de diálogo **Referências Não Utilizadas** permite remover referências que estão incluídas em seu projeto, mas na verdade não são usadas pelo código. Ela contém uma grade que lista o **Nome da Referência**, o **Caminho** e outras informações sobre as referências de namespace não utilizadas em seu projeto. Na grade, selecione as referências de namespace que você deseja remover de seu projeto e clique em **Remover**.  
  
 **Caminhos de Referência**  
 Clique neste botão para acessar a caixa de diálogo **Caminhos de Referência**.  
  
> [!NOTE]
>  Quando o sistema do projeto encontra uma referência de assembly, o sistema resolve a referência examinando os seguintes locais, na seguinte ordem:  
> 
> 1. A pasta do projeto. Os arquivos da pasta do projeto aparecem no **Gerenciador de Soluções** quando **Mostrar Todos os Arquivos** não está em vigor.  
>    2.  Pastas especificadas na caixa de diálogo **Caminhos de Referência**.  
>    3.  Pastas que exibem arquivos na caixa de diálogo **Adicionar Referência**.  
>    4.  A pasta obj do projeto. (Quando você adiciona uma referência COM a seu projeto, um ou mais assemblies podem ser adicionados à pasta obj do projeto.)  
  
 **Referências**  
 Esta lista mostra todas as referências no projeto, utilizadas ou não utilizadas.  
  
 **Adicionar**  
 Clique neste botão para adicionar uma referência ou uma referência Web à lista **Referências**.  
  
 Escolha **Referência** para adicionar uma referência ao seu projeto usando a caixa de diálogo Adicionar Referência.  
  
 Escolha **Referência Web** para adicionar uma referência Web ao seu projeto usando a caixa de diálogo Adicionar Referência Web.  
  
 **Removerr**  
 Selecione uma ou mais referências na lista **Referências** e clique nesse botão para excluí-las.  
  
 **Atualizar Referência Web**  
 Selecione uma referência Web na lista **Referências** e clique nesse botão para atualizá-la.  
  
 **Namespaces importados**  
 Você pode digitar seu próprio namespace nesta caixa e clicar em **Adicionar Importação de Usuário** para adicioná-lo à lista de namespaces.  
  
 Você pode criar aliases para namespaces importados pelo usuário. Para fazer isso, digite o alias e o namespace no formato *alias*=*namespace*. Isso é útil se você estiver usando namespaces longos, por exemplo: `Http= MyOrg.ObjectLib.Internet.WebRequestMethods.Http`.  
  
 **Adicionar Importação de Usuário**  
 Clique neste botão para adicionar o namespace especificado na caixa **Namespaces importados** à lista de namespaces importados. O botão fica ativo somente se o namespace especificado ainda não estiver na lista.  
  
 **Lista de namespaces**  
 Esta lista mostra todos os namespaces disponíveis. As caixas de seleção dos namespaces incluídos em seu projeto são selecionadas.  
  
 **Atualizar Importação de Usuário**  
 Selecione um namespace especificado pelo usuário na lista de namespaces, digite o nome com o qual deseja substituí-lo na caixa **Namespaces importados** e, em seguida, clique neste botão para alterar para o novo namespace. O botão fica ativo somente se o namespace selecionado for aquele que você adicionou à lista usando o botão **Adicionar Importação de Usuário**. Você pode adicionar:  
  
-   Classes ou namespaces, como <xref:System.Math?displayProperty=fullName>.  
  
-   Importações com alias, como `VB=Microsoft.VisualBasic`.  
  
-   Namespaces XML, como `<xmlns:xsl="http://www.w3.org/1999/XSL/Transform">`.  
  
## <a name="see-also"></a>Consulte também  
 [NIB: como adicionar ou remover referências usando a caixa de diálogo Adicionar Referência](http://msdn.microsoft.com/en-us/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)   
 [Como adicionar ou remover namespaces importados (Visual Basic)](../../ide/how-to-add-or-remove-imported-namespaces-visual-basic.md)   
 [NIB: caixa de diálogo Adicionar Referência Web](http://msdn.microsoft.com/en-us/bdf05776-c591-40af-bfd7-e1e2aa1e87b5)   
 [Instrução Imports (Namespace de XML)](http://msdn.microsoft.com/library/1f4d50a6-08c7-4c2e-8206-ccae35fcd1b4)



