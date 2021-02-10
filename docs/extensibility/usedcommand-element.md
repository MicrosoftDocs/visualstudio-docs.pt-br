---
title: Elemento UsedCommand | Microsoft Docs
description: O elemento UsedCommand permite que um VSPackage acesse um comando que é definido em outro arquivo. vsct.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- UsedCommands element (VSCT XML schema)
- VSCT XML schema elements, UsedCommands
ms.assetid: 99cd05d3-644a-42ff-b289-8458cd1b20c0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3c3f4a5f39e7cb999d9b3a86aa791464fca25645
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99934097"
---
# <a name="usedcommand-element"></a>Elemento UsedCommand
Permite que um VSPackage acesse um comando que é definido em outro arquivo. vsct. Por exemplo, se o VSPackage usar o comando de **cópia** padrão, que é definido pelo [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] shell, você poderá adicionar o comando a um menu ou barra de ferramentas sem implementá-lo novamente.

## <a name="syntax"></a>Sintaxe

```
<UsedCommand guid="guidMyCommandGroup" id="MyCommand" />
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|guid|Obrigatório. O GUID do par de IDs de GUID que identifica o comando.|
|id|Obrigatório. A ID do par de IDs de GUID que identifica o comando.|
|Condição|Opcional. Consulte [atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|Nenhum||

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento UsedCommands](../extensibility/usedcommands-element.md)|Agrupa elementos UsedCommand e outros agrupamentos do UsedCommands.|

## <a name="remarks"></a>Comentários
 Ao adicionar um comando ao `<UsedCommands>` elemento, um VSPackage informa ao [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ambiente que o VSPackage requer o comando. Você deve adicionar um `<UsedCommand>` elemento para qualquer comando que seu pacote exigir que talvez não seja incluído em todas as versões e configurações do Visual Studio. Por exemplo, se o pacote chamar um comando específico para Visual C++, o comando não estará disponível para os usuários do Visual Web Developer, a menos que você inclua um `<UsedCommand>` elemento para o comando.

## <a name="example"></a>Exemplo

```
<UsedCommands>
  <UsedCommand guid="guidVSStd97" id="cmdidCut"/>
  <UsedCommand guid="guidVSStd97" id="cmdidCopy"/>
  <UsedCommand guid="guidVSStd97" id="cmdidPaste"/>
</UsedCommands>
```

## <a name="see-also"></a>Confira também
- [Elemento UsedCommands](../extensibility/usedcommands-element.md)
- [Arquivos .Vsct (Visual Studio Command Table)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
