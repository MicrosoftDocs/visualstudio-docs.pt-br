---
title: Elemento VisibilityItem | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VisibilityItem element (VSCT XML schema)
- VSCT XML schema elements, VisibilityItem
ms.assetid: 0932f551-972d-4194-84bb-426e3e4375e4
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3abf3a93db79ac347931acf9275065eb0d085ca4
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49920166"
---
# <a name="visibilityitem-element"></a>Elemento VisibilityItem
O `VisibilityItem` elemento determina a visibilidade estática de comandos e barras de ferramentas. Cada entrada identifica um comando ou menu e um contexto de interface do usuário do comando associado. Visual Studio detecta os comandos, menus e as barras de ferramentas e sua visibilidade, sem carregar os VSPackages que defini-los. O IDE usa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> método para determinar se um contexto de interface do usuário do comando está ativo.  
  
 Depois que o VSPackage é carregado, o Visual Studio espera visibilidade do comando seja determinado pelo VSPackage, em vez do `VisibilityItem`. Para determinar a visibilidade do seu comando, você pode implementar o <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> manipulador de eventos ou o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método, dependendo de como você implementou seu comando.  
  
 Um comando ou um menu que tem um `VisibilityItem` elemento aparece somente quando o contexto associado está ativo. Você pode associar um único comando, menu ou barra de ferramentas com um ou mais contextos de interface do usuário de comando com a inclusão de uma entrada para cada combinação de contexto do comando. Se um comando ou o menu estiver associado a vários contextos de interface do usuário do comando, em seguida, o comando ou o menu está visível quando qualquer um dos contextos de interface do usuário do comando associado está ativo.  
  
 O `VisibilityItem` elemento se aplica somente aos comandos, menus e barras de ferramentas, não para grupos. Um elemento que não tem um relacionados `VisibilityItem` elemento estiver visível, sempre que seu menu pai está ativa.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<VisibilityItem  
  guid ="="cmdGuidMyProductCommands"  
  id=="cmdidAddWidget"  
  context="guidNotViewSourceMode"/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|GUID|Necessário. O GUID do identificador de comando/ID de GUID.|  
|id|Necessário. A ID do identificador de comando/ID de GUID.|  
|contexto|Necessário. O contexto de interface do usuário em que o comando está visível.|  
|Condição|Opcional. Ver [atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|  
  
### <a name="child-elements"></a>Elementos filho  
 Nenhum  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Element visibilityconstraints](../extensibility/visibilityconstraints-element.md)|O `VisibilityConstraints` elemento determina a visibilidade estática dos grupos de comandos e barras de ferramentas.|  
  
## <a name="remarks"></a>Comentários  
 Os contextos de interface de usuário do Visual Studio padrão são definidos na *caminho de instalação do SDK do Visual Studio*\VisualStudioIntegration\Common\Inc\vsshlids.h arquivo, bem como na <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids> e <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> classes. Um conjunto mais completo de contextos de interface do usuário é definido no <xref:Microsoft.VisualStudio.VSConstants> classe.  
  
## <a name="example"></a>Exemplo  
  
```xml  
<VisibilityConstraints>  
  <VisibilityItem guid="cmdSetGuidMyProductCommands"     id="cmdidAddWidget"  
    context="guidNotViewSourceMode"/>  
</VisibilityConstraints>  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>   
 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>   
 <xref:Microsoft.VisualStudio.VSConstants>   
 <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids>   
 <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>   
 [Element visibilityconstraints](../extensibility/visibilityconstraints-element.md)   
 [Tabela de comando do Visual Studio (. Arquivos de VSCT)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)