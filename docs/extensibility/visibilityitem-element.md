---
title: Elemento VisibilityItem | Microsoft Docs
description: O elemento VisibilityItem determina a visibilidade estática de comandos e barras de ferramentas. As entradas identificam um comando ou menu e um contexto de interface do usuário de comando associado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VisibilityItem element (VSCT XML schema)
- VSCT XML schema elements, VisibilityItem
ms.assetid: 0932f551-972d-4194-84bb-426e3e4375e4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 025e05dd0346c7da0a70985aa579d1673f2ffcaa
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905430"
---
# <a name="visibilityitem-element"></a>Elemento VisibilityItem
O `VisibilityItem` elemento determina a visibilidade estática de comandos e barras de ferramentas. Cada entrada identifica um comando ou menu e também um contexto de interface do usuário de comando associado. Visual Studio detecta comandos, menus e barras de ferramentas e sua visibilidade, sem carregar os VSPackages que os definem. O IDE usa o método para determinar se um contexto de interface do usuário <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> de comando está ativo.

 Depois que o VSPackage for carregado, Visual Studio espera que a visibilidade do comando seja determinada pelo VSPackage em vez do `VisibilityItem` . Para determinar a visibilidade do comando, você pode implementar o manipulador de eventos ou o método , dependendo de como você <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> implementou o comando.

 Um comando ou menu que tem um `VisibilityItem` elemento aparece somente quando o contexto associado está ativo. Você pode associar um único comando, menu ou barra de ferramentas a um ou mais contextos de interface do usuário de comando, incluindo uma entrada para cada combinação de contexto de comando. Se um comando ou menu estiver associado a vários contextos de interface do usuário de comando, o comando ou o menu será visível quando qualquer um dos contextos de interface do usuário de comando associados estiver ativo.

 O `VisibilityItem` elemento se aplica somente a comandos, menus e barras de ferramentas, não a grupos. Um elemento que não tem um elemento `VisibilityItem` relacionado fica visível sempre que seu menu pai está ativo.

## <a name="syntax"></a>Sintaxe

```xml
<VisibilityItem
  guid="cmdGuidMyProductCommands"
  id="cmdidAddWidget"
  context="guidNotViewSourceMode"/>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|guid|Obrigatórios. O GUID do identificador de comando GUID/ID.|
|id|Obrigatórios. A ID do identificador de comando GUID/ID.|
|contexto|Obrigatórios. O contexto da interface do usuário no qual o comando está visível.|
|Condição|Opcional. Consulte [Atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|

### <a name="child-elements"></a>Elementos filho
 Nenhum

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento VisibilityConstraints](../extensibility/visibilityconstraints-element.md)|O `VisibilityConstraints` elemento determina a visibilidade estática de grupos de comandos e barras de ferramentas.|

## <a name="remarks"></a>Comentários
 Os contextos de interface do usuário padrão Visual Studio são definidos no caminho de instalação do *SDK* do Visual Studio \VisualStudioIntegration\Common\Inc\vsshlids.h, bem como nas classes <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids> e <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> . Um conjunto mais completo de contextos de interface do usuário é definido na <xref:Microsoft.VisualStudio.VSConstants> classe .

## <a name="example"></a>Exemplo

```xml
<VisibilityConstraints>
  <VisibilityItem guid="cmdSetGuidMyProductCommands"     id="cmdidAddWidget"
    context="guidNotViewSourceMode"/>
</VisibilityConstraints>
```

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>
- <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>
- <xref:Microsoft.VisualStudio.VSConstants>
- <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids>
- <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>
- [Elemento VisibilityConstraints](../extensibility/visibilityconstraints-element.md)
- [Visual Studio de comando (. Vsct) Arquivos](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
