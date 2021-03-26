---
title: Adicionando itens às caixas de diálogo Adicionar novo item | Microsoft Docs
description: Saiba como adicionar itens à caixa de diálogo Adicionar novo item no Visual Studio, para que você possa exibir modelos e elementos de projeto para uso em seus projetos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, adding items
ms.assetid: 2f70863b-425b-4e65-86b4-d6a898e29dc7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 574cc5384018d14fdc05a834876002bbcbdbaaf7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079092"
---
# <a name="add-items-to-the-add-new-item-dialog-box"></a>Adicionar itens à caixa de diálogo Adicionar novo item
O processo para adicionar itens à caixa de diálogo **Adicionar novo item** começa com as chaves do registro. Conforme mostrado nas entradas de registro a seguir, a seção **Additemtemplates** contém o caminho e o nome do diretório no qual os itens disponibilizados na caixa de diálogo **Adicionar novo item** são colocados.

> [!NOTE]
> A tabela imediatamente após o segmento de código contém informações adicionais sobre a entrada do registro.

 Esta seção está localizada em **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0Exp\Projects**.

 O primeiro GUID é o CLSID para projetos desse tipo; o segundo GUID indica o tipo de projeto registrado para os modelos adicionar itens:

 **\\{C061DB26-5833-11D2-96F5-000000000000} \\ Additemtemplates \\ TemplatesDir \\ {ACEF4EB2-57CF-11D2-96F4-000000000000} \\ 1**

 **@** = #6

   =  \\ TemplatesDir &lt; Caminho de instalação do SDK do Visual Studio &gt; \\ VSIntegration \\ &lt; SomeFolder &gt; \\ &lt; SomePackage &gt; \\ &lt; SomeProject &gt; \\ &lt; SomeProjectItems&gt;

 **SortPriority** = DWORD: 00000064

| Nome | Type | Dados (do arquivo *. rgs* ) | Descrição |
|------------------|-----------| - | - |
| @ (Padrão) | REG_SZ | #% IDS_ADDITEM_TEMPLATES_ENTRY% | ID do recurso para adicionar modelos de **Item** . |
| Valor TemplatesDir | REG_SZ | % TEMPLATE_PATH% \\ &lt; SomeProjectItems&gt; | Caminho dos itens de projeto exibidos na caixa de diálogo para o assistente para **Adicionar novo item** . |
| Valor SortPriority | REG_DWORD | 100 ( [!INCLUDE[vcprx64](../../extensibility/internals/includes/vcprx64_md.md)] ) | Determina a ordem de classificação no nó de árvore dos arquivos exibidos na caixa de diálogo **Adicionar novo item** . |

> [!NOTE]
> Os GUIDs para os tipos de projeto do Visual C# e Visual Basic são os seguintes:
> - [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]: {FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}
> - [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]: {F184B08F-C81C-45F6-A57F-5ABD9991F28F}

 O diretório listado para **TemplatesDir**, que é *% TEMPLATE_PATH% \\ &lt; SomeProjectItems &gt;*, é o nó no lado esquerdo da árvore da caixa de diálogo **Adicionar novo item** . Elementos adicionais na árvore são baseados no subdiretório dentro desse diretório raiz. Os arquivos disponíveis para serem adicionados ao projeto são os itens no painel direito da caixa de diálogo **Adicionar novo item** .

 Normalmente, essa pasta conterá os arquivos de modelo para seu projeto, como um arquivo de modelo HTML ou *. cpp* , e quaisquer arquivos *. vsz* para iniciar os assistentes. Para controlar como os itens são exibidos, você também pode incluir arquivos *. vsdir* para localizar nomes de diretório e ícones. A cadeia de caracteres localizada é a legenda que aparece na caixa de diálogo que representa esse nó na árvore da caixa de diálogo **Adicionar novo item** .

 No entanto, você não precisa ter tudo em um arquivo *. vsdir* . Você pode ter um arquivo *. vsdir* para cada item no diretório. Para obter mais informações, consulte [arquivo do assistente (. vsz)](../../extensibility/internals/wizard-dot-vsz-file.md) e [arquivos de descrição do diretório de modelo (. vsdir)](../../extensibility/internals/template-directory-description-dot-vsdir-files.md).

> [!NOTE]
> Os arquivos *. vsdir* nos diretórios de modelo são opcionais. Se você apenas deseja colocar um elemento de projeto no diretório e exibi-lo na caixa de diálogo **Adicionar novo item** , você pode colocar esse arquivo no diretório templates especificado na instrução **TemplatesDir** . O arquivo será exibido no painel direito da caixa de diálogo **Adicionar novo item** para esse projeto. No entanto, se você quiser exibir uma legenda localizada para o arquivo ou um ícone, deverá incluir pelo menos um arquivo *. vsdir* no diretório de modelos.

## <a name="group-project-items"></a>Agrupar itens de projeto
 Se você quiser conter grupos de modelos em pastas na árvore da caixa de diálogo **Adicionar novo item** , deverá ter subdiretórios no diretório do modelo raiz com os itens neles. Quando a caixa de diálogo **Adicionar novo item** for exibida aos usuários, elas também verão as subpastas e poderão selecionar elementos do projeto a partir delas.

 A prioridade de classificação no segmento de código determina onde esse diretório de modelo será criado na árvore em relação a outros elementos do nó de árvore. Para a caixa de diálogo **Adicionar novo item** , a prioridade de classificação é tudo o que você deve incluir para que os itens sejam exibidos no local correto na caixa de diálogo.

 Você também pode implementar a <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2> interface para filtrar o que é exibido na caixa de diálogo **Adicionar novo item** . Ao implementar essa interface, você pode configurar um diretório de modelo no disco que contém, por exemplo, os arquivos de modelo e de assistente 50. Dessa forma, você pode ter diferentes tipos de projeto com 20 arquivos que pertencem a um tipo de projeto, os outros 30 arquivos que pertencem a outro tipo de projeto e todos os arquivos disponíveis em um tipo geral de projeto. Dessa maneira, dependendo de qual modelo de projeto é criado, você pode exibir um conjunto diferente de arquivos de modelo.

 Por exemplo, em um projeto Visual Basic, você pode ter projetos Web e projetos de cliente. Os Web Forms não são itens úteis para adicionar a um projeto de cliente e o Windows Forms não são itens úteis para adicionar a um projeto de servidor Web. Portanto, você pode criar um diretório de modelo que contém todos os arquivos para os dois tipos de projeto. Em seguida, implementando <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2> , você pode ocultar itens que não devem ser exibidos com base no tipo de projeto ou nas configurações de projeto no projeto.

## <a name="filter-project-items"></a>Filtrar itens de projeto
 `IVsFilterAddProjectItemDlg2` fornece filtragem de elementos na árvore (painel esquerdo) e arquivos de projeto (painel direito) das seguintes maneiras:

- Pelos nomes localizados (legendas exibidas na caixa de diálogo contida no arquivo *. vsdir* ) fornecida pelo `IVsFilterAddProjectItemDlg` .

- Pelos nomes reais dos arquivos e pastas no disco (não localizado — no arquivo *. vsdir* ) fornecido pelo `IVsFilterAddProjectItemDlg` .

- Por categoria, fornecido por `IVsFilterAddProjectItemDlg2` .

  Para filtrar por categoria, forneça uma cadeia de caracteres de categoria para um item no arquivo *. vsdir* , como *formulário da Web* ou *item de cliente* em Visual Basic. O código da caixa de diálogo recupera a classificação de categoria do arquivo *. vsdir* e a transmite para você. Em seguida, você pode passar essas informações para a implementação do `IVsFilterAddProjectItemDlg2` para filtrar a caixa de diálogo **Adicionar novo item** por categorias. Você também pode filtrar itens para páginas da Web ou como casos de aplicativo Win32 do cliente. Além disso, você pode identificar [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] itens marcados como MFC (MFC) ou itens da ATL (Active Template Library). Quando você identifica esses itens, o sistema de projeto pode definir suas próprias classificações para que o sistema possa ser filtrado com base em categorias e classificações.

  Se você implementar essa funcionalidade de filtro, não precisará mapear uma tabela de todos os itens que devem estar ocultos. Você pode simplesmente classificar itens em tipos e colocar as classificações no arquivo *. vsdir* ou nos arquivos. Em seguida, você pode ocultar qualquer um dos itens que têm uma classificação específica implementando a interface. Dessa forma, você pode tornar os itens na caixa de diálogo **Adicionar novo item** dinâmicos com base no estado dentro do projeto.

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [Registrar modelos de projeto e item](../../extensibility/internals/registering-project-and-item-templates.md)
- [CATIDs para objetos que normalmente são usados para estender projetos](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
- [Adicionar projeto e modelos de item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [Arquivos de descrição do diretório de modelo (. vsdir)](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
- [Arquivo do assistente (. vsz)](../../extensibility/internals/wizard-dot-vsz-file.md)
