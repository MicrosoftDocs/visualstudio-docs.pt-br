---
title: Adicionando itens às caixas de diálogo Adicionar Novo Item | Microsoft Docs
description: Saiba como adicionar itens à caixa de diálogo Adicionar Novo Item no Visual Studio, para que você possa exibir modelos e elementos de projeto para uso em seus projetos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Add New Item dialog box, adding items
ms.assetid: 2f70863b-425b-4e65-86b4-d6a898e29dc7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 70bc1a0c4d90d8cab0b2193550773745fc2dd47e
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904403"
---
# <a name="add-items-to-the-add-new-item-dialog-box"></a>Adicionar itens à caixa de diálogo Adicionar Novo Item
O processo para adicionar itens à **caixa de diálogo Adicionar Novo Item** começa com as chaves do Registro. Conforme mostrado nas entradas do Registro a seguir, a seção **AddItemTemplates** contém o caminho e o nome do diretório no qual os itens disponibilizados na caixa de diálogo Adicionar Novo **Item** são colocados.

> [!NOTE]
> A tabela imediatamente após o segmento de código contém informações adicionais sobre a entrada do Registro.

 Esta seção está localizada em **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0Exp\Projects**.

 O primeiro GUID é o CLSID para projetos desse tipo; o segundo GUID indica o tipo de projeto registrado para os modelos Adicionar Itens:

 **\\{C061DB26-5833-11D2-96F5-0000000000} \\ Modelos AddItemTemplatesDir \\ \\ {ACEF4EB2-57CF-11D2-96F4-00000000000} \\ 1**

 **@** = #6

 **TemplatesDir**  =  \\ &lt; Visual Studio caminho de instalação do SDK &gt; \\ VSIntegration \\ &lt; SomeFolder &gt; \\ &lt; SomePackage &gt; \\ &lt; &gt; \\ &lt; SomeProject SomeProjectItems&gt;

 **SortPriority** = dword:00000064

| Nome | Tipo | Dados (do *arquivo .rgs)* | Descrição |
|------------------|-----------| - | - |
| @ (Padrão) | REG_SZ | #%IDS_ADDITEM_TEMPLATES_ENTRY% | ID do recurso para **adicionar modelos** de item. |
| Val TemplatesDir | REG_SZ | %TEMPLATE_PATH% \\ &lt; SomeProjectItems&gt; | Caminho dos itens de projeto exibidos na caixa de diálogo para o **assistente Adicionar Novo** Item. |
| Val SortPriority | REG_DWORD | 100 ( [!INCLUDE[vcprx64](../../extensibility/internals/includes/vcprx64_md.md)] ) | Determina a ordem de classificação no nó de árvore de arquivos exibidos na **caixa de diálogo** Adicionar Novo Item. |

> [!NOTE]
> Os GUIDS para os tipos de projeto visual C# e Visual Basic são os exemplos a seguir:
> - [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]: {LTD04EC0-301F-11D3-BF4B-00C04F79EFBC}
> - [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]: {F184B08F-C81C-45F6-A57F-5ABD9991F28F}

 O diretório listado para **TemplatesDir**, que é *%TEMPLATE_PATH% \\ &lt; SomeProjectItems &gt;*, é o nó no lado esquerdo da árvore da caixa de diálogo Adicionar Novo **Item.** Elementos adicionais na árvore são baseados no subdiretório dentro desse diretório raiz. Os arquivos disponíveis para serem adicionados ao projeto são os itens no painel direito da caixa de diálogo Adicionar **Novo** Item.

 Normalmente, essa pasta conterá os arquivos de modelo para seu projeto, como um arquivo HTML ou *.cpp* de modelo, bem como qualquer arquivo *.vsz* para assistentes de início. Para controlar como os itens são exibidos, você também pode incluir arquivos *.vsdir* para localização de nomes e ícones de diretório. A cadeia de caracteres localizada é a legenda que aparece na caixa de diálogo que representa esse nó na árvore **da** caixa de diálogo Adicionar Novo Item.

 No entanto, você não precisa ter tudo em um *arquivo .vsdir.* Você pode ter um *arquivo .vsdir* para cada item no diretório. Para obter mais informações, consulte [Arquivo do Assistente (.vsz)](../../extensibility/internals/wizard-dot-vsz-file.md) e Arquivos de descrição do [diretório de modelo (.vsdir).](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)

> [!NOTE]
> Os *arquivos .vsdir* nos diretórios de modelo são opcionais. Se você quiser apenas colocar um elemento de projeto no diretório e exibi-lo na caixa de diálogo Adicionar Novo **Item,** poderá colocar esse arquivo no diretório templates especificado na instrução **TemplatesDir.** O arquivo será exibido no painel direito da caixa de diálogo Adicionar Novo **Item** para esse projeto. No entanto, se você quiser exibir uma legenda localizada para o arquivo ou um ícone, deverá incluir pelo menos um arquivo *.vsdir* no diretório templates.

## <a name="group-project-items"></a>Itens do projeto de grupo
 Se você quiser conter grupos de modelos em pastas na árvore de caixa de diálogo Adicionar Novo **Item,** deverá ter subdireções no diretório do modelo raiz com os itens neles. Quando a **caixa de diálogo** Adicionar Novo Item for exibida aos usuários, eles também verão as subpastas e poderão selecionar elementos de projeto deles.

 A prioridade de classificação no segmento de código determina onde esse diretório de modelo será criado na árvore em relação a outros elementos do nó de árvore. Para a caixa de diálogo Adicionar Novo **Item,** a prioridade de classificação é tudo o que você deve incluir para que seus itens sejam exibidos no local correto na caixa de diálogo.

 Você também pode implementar a <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2> interface para filtrar o que é exibido na **caixa de diálogo Adicionar Novo** Item . Ao implementar essa interface, você pode configurar um diretório de modelo no disco que contém, por exemplo, 50 arquivos de modelo e de assistente. Dessa forma, você pode ter diferentes tipos de projeto com 20 arquivos que pertencem a um tipo de projeto, os outros 30 arquivos que pertencem a outro tipo de projeto e todos os arquivos disponíveis em um tipo geral de projeto. Dessa maneira, dependendo de qual modelo de projeto é criado, você pode exibir um conjunto diferente de arquivos de modelo.

 Por exemplo, em um projeto Visual Basic, você pode ter projetos Web e projetos de cliente. Os formulários da Web não são itens úteis para adicionar a um projeto cliente e os formulários do Windows não são itens úteis para adicionar a um projeto de servidor Web. Portanto, você pode criar um diretório de modelo que contém todos os arquivos para ambos os tipos de projeto. Em seguida, implementando , você pode ocultar itens que não devem ser exibidos com base no tipo de configurações de projeto ou <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2> projeto no projeto.

## <a name="filter-project-items"></a>Filtrar itens de projeto
 `IVsFilterAddProjectItemDlg2` fornece filtragem de elementos na árvore (painel esquerdo) e arquivos de projeto (painel direito) das seguintes maneiras:

- Pelos nomes localizados (legendas exibidas na caixa de diálogo contidas no *arquivo .vsdir)* fornecidos pelo `IVsFilterAddProjectItemDlg` .

- Pelos nomes reais dos arquivos e pastas no disco (não localizados – nenhum *arquivo .vsdir)* fornecido pelo `IVsFilterAddProjectItemDlg` .

- Por categoria, fornecido por `IVsFilterAddProjectItemDlg2` .

  Para filtrar por categoria, forneça uma cadeia de caracteres de categoria para um item no *arquivo .vsdir,* como Formulário da *Web* ou *Item* de cliente no Visual Basic. O código da caixa de diálogo recupera a classificação de categoria do *arquivo .vsdir* e a passa para você. Em seguida, você pode passar essas informações para sua implementação do para filtrar a caixa de diálogo Adicionar `IVsFilterAddProjectItemDlg2` Novo **Item** por categorias. Você também pode filtrar itens para páginas da Web ou como casos de aplicativo Win32 do cliente. Além disso, você pode identificar itens marcados como MFC (MFC) ou itens da ATL (biblioteca de modelos [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] ativos). Quando você identifica esses itens, o sistema de projeto pode definir suas próprias classificações para que o sistema possa ser filtrado com base em categorias e classificações.

  Se você implementar essa funcionalidade de filtro, não será preciso mapear uma tabela de cada item que deve ser ocultado. Você pode simplesmente classificar itens em tipos e colocar as classificações no arquivo ou arquivos *.vsdir.* Em seguida, você pode ocultar qualquer um dos itens que têm uma classificação específica implementando a interface . Dessa forma, você pode tornar os itens na caixa de diálogo Adicionar Novo **Item** dinâmicos com base no estado dentro do projeto.

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [Registrar modelos de projeto e item](../../extensibility/internals/registering-project-and-item-templates.md)
- [CATIDs para objetos que normalmente são usados para estender projetos](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
- [Adicionar modelos de projeto e item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [Arquivos de descrição do diretório de modelo (.vsdir)](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
- [Arquivo do assistente (.vsz)](../../extensibility/internals/wizard-dot-vsz-file.md)
