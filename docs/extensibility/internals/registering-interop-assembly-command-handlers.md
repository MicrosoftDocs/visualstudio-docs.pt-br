---
title: Registrando manipuladores de comando de assembly de interoperabilidade | Microsoft Docs
description: Saiba mais sobre o contrato de comando básico usado por todos os VSPackages implementando comandos usando assemblies de interoperabilidade.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, command handlers
- command handling with interop assemblies, registering
ms.assetid: 303cd399-e29d-4ea1-8abe-5e0b59c12a0c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 641a21658e490f94a27cbd9120d044539a7ec284
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062753"
---
# <a name="registering-interop-assembly-command-handlers"></a>Registrando manipuladores de comando de assembly de interoperabilidade
Um VSPackage deve se registrar no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] para que o IDE (ambiente de desenvolvimento integrado) roteia seus comandos corretamente.

 O registro pode ser atualizado por edição manual ou por meio de um arquivo de registrador (. rgs). Para obter mais informações, consulte [Criando scripts de registrador](/cpp/atl/creating-registrar-scripts).

 A MPF (estrutura de pacote gerenciada) fornece essa funcionalidade por meio da <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> classe.

- Os recursos de [referência de formato de tabela de comando](/previous-versions/bb164647(v=vs.100)) estão localizados em DLLs de interface do usuário satélite não gerenciadas.

## <a name="command-handler-registration-of-a-vspackage"></a>Registro de manipulador de comando de um VSPackage
 Um VSPackage atuando como um manipulador para comandos baseados na interface do usuário requer uma entrada de registro nomeada após o VSPackage `GUID` . Essa entrada de registro especifica o local do arquivo de recurso de interface do usuário do VSPackage e o recurso de menu dentro desse arquivo. A própria entrada do registro está localizada em HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\ *\<Version>* \Menus, em que *\<Version>* é a versão do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , por exemplo, 9,0.

> [!NOTE]
> O caminho raiz de HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\ *\<Version>* pode ser substituído por uma raiz alternativa quando o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] shell é inicializado. Para obter mais informações sobre o caminho raiz, consulte [Installing VSPackages With Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md).

### <a name="the-ctmenu-resource-registry-entry"></a>A entrada do registro de recurso CTMENU
 A estrutura da entrada do registro é:

```
HKEY_LOCAL_MACHINE\Software\VisualStudio\<Version>\
  Menus\
    <GUID> = <Resource Information>
```

 \<*GUID*> é o `GUID` do VSPackage no formato {XXXXXX-XXXX-XXXX-XXXX-xxxxxxxxx}.

 *\<Resource Information>* consiste em três elementos separados por vírgulas. Esses elementos são, em ordem:

 \<*Path to Resource DLL*>, \<*Menu Resource ID*>, \<*Menu Version*>

 A tabela a seguir descreve os campos de \<*Resource Information*> .

| Elemento | Descrição |
|---------------------------| - |
| \<*Path to Resource DLL*> | Este é o caminho completo para a DLL de recursos que contém o recurso de menu ou que é deixado em branco, indicando que a DLL de recurso do VSPackage deve ser usada (conforme especificado na subchave pacotes em que o VSPackage em si está registrado).<br /><br /> É personalizado deixar esse campo em branco. |
| \<*Menu Resource ID*> | Essa é a ID de recurso do `CTMENU` recurso que contém todos os elementos da interface do usuário para o VSPackage como compilado de um arquivo [. vsct](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md) . |
| \<*Menu Version*> | Este é um número usado como uma versão para o `CTMENU` recurso. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] usa esse valor para determinar se ele precisa remesclar o conteúdo do `CTMENU` recurso com seu cache de todos os `CTMENU` recursos. Uma remesclagem é disparada executando o comando de instalação do devenv.<br /><br /> Esse valor deve inicialmente ser definido como 1 e incrementado após cada alteração no `CTMENU` recurso e antes que a remesclagem ocorra. |

### <a name="example"></a>Exemplo
 Aqui está um exemplo de algumas entradas de recurso:

```
HKEY_LOCAL_MACHINE\Software\VisualStudio\9.0Exp\
  Menus\
    {019971D6-4685-11D2-B48A-0000F87572EB} = ,1, 10
    {1b027a40-8f43-11d0-8d11-00a0c91bc942} = , 10211, 3
```

## <a name="see-also"></a>Confira também
- [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Comandos e menus que usam assemblies de interoperabilidade](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)