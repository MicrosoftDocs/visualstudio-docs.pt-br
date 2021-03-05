---
title: Elemento VisibilityItem | Microsoft Docs
description: O elemento VisibilityItem determina a visibilidade estática de comandos e barras de ferramentas. As entradas identificam um comando ou menu e um contexto de interface do usuário de comando associado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VisibilityItem element (VSCT XML schema)
- VSCT XML schema elements, VisibilityItem
ms.assetid: 0932f551-972d-4194-84bb-426e3e4375e4
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3fa4c2910a1f694a822d2a31b5ad537c8104f99c
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221295"
---
# <a name="visibilityitem-element"></a>Elemento VisibilityItem
O `VisibilityItem` elemento determina a visibilidade estática de comandos e barras de ferramentas. Cada entrada identifica um comando ou menu e também um contexto de interface do usuário de comando associado. O Visual Studio detecta comandos, menus e barras de ferramentas e sua visibilidade, sem carregar o VSPackages que os define. O IDE usa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> método para determinar se um contexto de interface do usuário de comando está ativo.

 Depois que o VSPackage é carregado, o Visual Studio espera que a visibilidade do comando seja determinada pelo VSPackage em vez do `VisibilityItem` . Para determinar a visibilidade do comando, você pode implementar o <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> manipulador de eventos ou o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método, dependendo de como você implementou o comando.

 Um comando ou menu que tem um `VisibilityItem` elemento é exibido somente quando o contexto associado está ativo. Você pode associar um único comando, menu ou barra de ferramentas com um ou mais contextos de interface do usuário de comando, incluindo uma entrada para cada combinação de contexto de comando. Se um comando ou menu estiver associado a vários contextos de interface do usuário, o comando ou o menu ficará visível quando qualquer um dos contextos de interface do comando associados estiver ativo.

 O `VisibilityItem` elemento aplica-se somente a comandos, menus e barras de ferramentas, não a grupos. Um elemento que não tem um elemento relacionado `VisibilityItem` é visível sempre que seu menu pai está ativo.

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
|guid|Obrigatórios. O GUID do identificador do comando GUID/ID.|
|id|Obrigatórios. A ID do identificador de comando de GUID/ID.|
|contexto|Obrigatórios. O contexto de interface do usuário no qual o comando está visível.|
|Condição|Opcional. Consulte [atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|

### <a name="child-elements"></a>Elementos filho
 Nenhum

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento VisibilityConstraints](../extensibility/visibilityconstraints-element.md)|O `VisibilityConstraints` elemento determina a visibilidade estática de grupos de comandos e barras de ferramentas.|

## <a name="remarks"></a>Comentários
 Os contextos padrão da interface do usuário do Visual Studio são definidos no arquivo \VisualStudioIntegration\Common\Inc\vsshlids.h do *caminho de instalação do SDK do Visual Studio*, bem como nas <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids> <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> classes e. Um conjunto mais completo de contextos de interface do usuário é definido na <xref:Microsoft.VisualStudio.VSConstants> classe.

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
- [Tabela de comandos do Visual Studio (. Arquivos de vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
