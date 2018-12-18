---
title: Adição de itens para a adicionar novo Item caixas de diálogo | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, adding items
ms.assetid: 2f70863b-425b-4e65-86b4-d6a898e29dc7
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b98e696def519cea6d3644d0ef3a48bc82c19136
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49812576"
---
# <a name="add-items-to-the-add-new-item-dialog-box"></a>Adicionar itens à caixa de diálogo Adicionar Novo Item
O processo para adicionar itens para o **Adicionar Novo Item** caixa de diálogo começa com as chaves do registro. Conforme mostrado nas entradas de registro a seguir, o **AddItemTemplates** seção contém o caminho e o nome do diretório em que os itens disponibilizados na **Adicionar Novo Item** caixa de diálogo são colocados.  

> [!NOTE]
>  A tabela imediatamente após o segmento de código contém informações adicionais sobre a entrada do registro.  

 Esta seção está localizada sob **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0Exp\Projects**.

 O primeiro GUID é o CLSID para projetos desse tipo; o segundo GUID indica o tipo de projeto registrados para os modelos de adicionar itens:  

 **\\{C061DB26-5833-11D2-96F5-000000000000} \\AddItemTemplates\\TemplatesDir\\{ACEF4EB2-57CF-11D2-96F4-000000000000}\\1**

 **@** = #6 

 **TemplatesDir** = \\&lt;caminho de instalação do SDK do Visual Studio&gt;\\VSIntegration\\&lt;SomeFolder&gt; \\ &lt;SomePackage&gt;\\&lt;SomeProject&gt;\\&lt;SomeProjectItems&gt;

 **SortPriority** = dword:00000064


| Nome | Tipo | Dados (de *rgs* arquivo) | Descrição |
|------------------|-----------| - | - |
| @ (Padrão) | REG_SZ | #% IDS_ADDITEM_TEMPLATES_ENTRY % | ID do recurso **Adicionar Item** modelos. |
| Val TemplatesDir | REG_SZ | % TEMPLATE_PATH\\&lt;SomeProjectItems&gt; | Caminho dos itens de projeto exibido na caixa de diálogo para o **Adicionar Novo Item** assistente. |
| Val SortPriority | REG_DWORD | 100 ([!INCLUDE[vcprx64](../../extensibility/internals/includes/vcprx64_md.md)]) | Determina a ordem de classificação no nó de árvore de arquivos exibidos na **Adicionar Novo Item** caixa de diálogo. |

> [!NOTE]
>  Os GUIDS para o Visual c# e tipos de projeto do Visual Basic são da seguinte maneira: 
> - [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]: {FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}
> - [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]: {F184B08F-C81C-45F6-A57F-5ABD9991F28F}  

 O diretório listado para **TemplatesDir**, que é *TEMPLATE_PATH %\\&lt;SomeProjectItems&gt;*, é o nó no lado esquerdo do **adicionar Novo Item** árvore da caixa de diálogo. Elementos adicionais da árvore baseiam-se no subdiretório do diretório raiz. Os arquivos disponíveis para serem adicionados ao projeto são os itens no painel à direita do **Adicionar Novo Item** caixa de diálogo.  

 Normalmente, essa pasta conterá os arquivos de modelo para seu projeto como um modelo HTML ou *. cpp* arquivo e qualquer *. vsz* arquivos para iniciar assistentes. Para controlar como os itens são exibidos, você também pode incluir *. vsdir* arquivos para localização de ícones e nomes de diretório. A cadeia de caracteres localizada é a legenda exibida na caixa de diálogo que representa esse nó na **Adicionar Novo Item** árvore da caixa de diálogo.  

 No entanto, você não precisa ter tudo em uma *. vsdir* arquivo. Você pode ter um *. vsdir* arquivo para cada item no diretório. Para obter mais informações, consulte [arquivo (. vsz) do assistente](../../extensibility/internals/wizard-dot-vsz-file.md) e [arquivos de descrição (. vsdir) do diretório de modelo](../../extensibility/internals/template-directory-description-dot-vsdir-files.md).  

> [!NOTE]
>  O *. vsdir* arquivos nos diretórios de modelo são opcionais. Se você apenas deseja colocar um elemento do projeto no diretório e exibi-lo na **Adicionar Novo Item** caixa de diálogo, você pode colocar esse arquivo no diretório de modelos especificado na **TemplatesDir** instrução. O arquivo, em seguida, será exibido no painel à direita do **Adicionar Novo Item** caixa de diálogo para o projeto. No entanto, se você quiser exibir uma legenda localizada para o arquivo ou um ícone, você deve incluir pelo menos um *. vsdir* arquivo no diretório de modelos.  

## <a name="group-project-items"></a>Itens de projeto de grupo  
 Se você quer incluir grupos de modelos em pastas na **Adicionar Novo Item** árvore da caixa de diálogo, você deve ter os subdiretórios no diretório raiz de modelo com os itens nelas. Quando o **Adicionar Novo Item** caixa de diálogo é exibida aos usuários, eles também verá as subpastas e ser capaz de selecionar os elementos do projeto deles.  

 A prioridade de classificação no segmento de código determina onde esse diretório de modelo será criado na árvore de em relação a outros elementos da árvore do nó. Para o **Adicionar Novo Item** caixa de diálogo, a prioridade de classificação é tudo o que você precisa incluir para que os itens serão exibidos no local correto na caixa de diálogo.  

 Você também pode implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2> interface para filtrar o que é exibido o **Adicionar Novo Item** caixa de diálogo. Ao implementar essa interface, você pode configurar o diretório de um modelo em disco que contém, por exemplo, 50 arquivos de modelo e o assistente. Dessa forma, você pode ter diferentes tipos de projetos com 20 arquivos que pertencem a um tipo de projeto, os 30 arquivos pertencentes a outro tipo de projeto e todos os arquivos disponíveis em um tipo geral do projeto. Dessa maneira, dependendo de qual projeto modelo for criado, você pode exibir um conjunto diferente de arquivos de modelo.  

 Por exemplo, em um projeto do Visual Basic, você pode ter projetos da Web e projetos de cliente. Formulários da Web não são itens úteis a serem adicionados a um projeto de cliente e do windows forms não são itens úteis para adicionar a um projeto do servidor Web. Portanto, você pode criar um diretório de modelo que contém todos os arquivos para os dois tipos de projeto. Em seguida, implementando <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>, você pode ocultar itens que não devem ser exibidos com base no tipo de projeto ou configurações do projeto no projeto.  

## <a name="filter-project-items"></a>Filtrar itens de projeto  
 `IVsFilterAddProjectItemDlg2` fornece para filtragem dos elementos na árvore (painel esquerdo) e arquivos de projeto (painel direito) das seguintes maneiras:  

- Por nomes localizados (legendas exibidas na caixa de diálogo que está contida na *. vsdir* arquivo) fornecida pelo `IVsFilterAddProjectItemDlg`.  

- Por que os nomes reais dos arquivos e pastas no disco (não localizado — nenhuma *. vsdir* arquivo) fornecida pelo `IVsFilterAddProjectItemDlg`.  

- Por categoria, fornecida pelo `IVsFilterAddProjectItemDlg2`.  

  Para filtrar por categoria, forneça uma cadeia de caracteres para um item na categoria de *. vsdir* do arquivo, como *formulário da Web* ou *item cliente* no Visual Basic. O código da caixa de diálogo, em seguida, recupera a classificação de categoria do *. vsdir* de arquivo e o passa para você. Você pode passar essas informações para sua implementação de `IVsFilterAddProjectItemDlg2` para filtrar o **Adicionar Novo Item** caixa de diálogo por categorias. Você também pode filtrar itens para páginas da Web ou como casos de aplicativo do Win32 de cliente. Além disso, você pode identificar [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] marcado itens como Microsoft Foundation Classes (MFC) ou itens do modelo do Active Directory library (ATL). Ao identificar esses itens, o sistema de projeto pode definir suas próprias classificações de forma que o sistema pode ser filtrado com base nas categorias e classificações.  

  Se você implementar essa funcionalidade de filtro, você não precisa mapear uma tabela de cada item que deve ser ocultada. Você pode classificar itens em tipos e coloque as classificações em simplesmente a *. vsdir* arquivo ou arquivos. Em seguida, você pode ocultar qualquer um dos itens que têm uma classificação específica, Implementando a interface. Dessa forma, você pode tornar os itens a **Adicionar Novo Item** dinâmico da caixa de diálogo, de acordo com o estado dentro do projeto.  

## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>   
 [Registrar os modelos de projeto e de item](../../extensibility/internals/registering-project-and-item-templates.md)   
 [CATIDs para objetos que normalmente são usados para estender projetos](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)   
 [Adicione o projeto e modelos de item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md)   
 [Arquivos de descrição (. vsdir) do diretório de modelo](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)   
 [Arquivo do assistente (. vsz)](../../extensibility/internals/wizard-dot-vsz-file.md)