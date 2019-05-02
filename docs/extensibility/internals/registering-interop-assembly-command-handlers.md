---
title: Registrando manipuladores de comandos do Assembly de interoperabilidade | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, command handlers
- command handling with interop assemblies, registering
ms.assetid: 303cd399-e29d-4ea1-8abe-5e0b59c12a0c
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b07f018a35874e2ffc3f3be825abb227f2996aea
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63425466"
---
# <a name="registering-interop-assembly-command-handlers"></a>Registrando manipuladores de comando de assembly de interoperabilidade
Registre um VSPackage com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , de modo que o ambiente de desenvolvimento integrado (IDE) encaminha seus comandos corretamente.

 O registro pode ser atualizado por meio da edição manual ou por meio de um arquivo registrador (. rgs). Para obter mais informações, consulte [criação de Scripts do registrador](/cpp/atl/creating-registrar-scripts).

 Estrutura de pacote gerenciado (MPF) fornece essa funcionalidade por meio de <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> classe.

- [Referência de formato de tabela do comando](https://msdn.microsoft.com/library/09e9c6ef-9863-48de-9483-d45b7b7c798f) recursos estão localizados em dlls de interface do usuário do satélite não gerenciado.

## <a name="command-handler-registration-of-a-vspackage"></a>Registro do manipulador de comando de um VSPackage
 Um VSPackage que atua como um manipulador para a interface do usuário (IU)-comandos com base requer uma entrada de registro nomeada após o VSPackage `GUID`. Essa entrada de registro Especifica o local do arquivo de recurso de interface do usuário do VSPackage e do recurso de menu dentro desse arquivo. A entrada de registro está localizada em HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\*\<versão >* \Menus, onde  *\<versão >* é a versão do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], por exemplo 9.0.

> [!NOTE]
> O caminho raiz do HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*\<versão >* pode ser substituído por uma alternativa raiz quando o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] shell é inicializado. Para obter mais informações sobre o caminho raiz, consulte [instalando VSPackages com o Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md).

### <a name="the-ctmenu-resource-registry-entry"></a>A entrada de registro do recurso CTMENU
 A estrutura da entrada do registro é:

```
HKEY_LOCAL_MACHINE\Software\VisualStudio\<Version>\
  Menus\
    <GUID> = <Resource Information>
```

 \<*GUID*> é o `GUID` do VSPackage na forma {XXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX}.

 *\<Informações sobre o recurso >* consiste em três elementos separados por vírgulas. Esses elementos são, em ordem:

 \<*Caminho para a DLL de recurso*>, \< *ID de recurso de Menu*>, \< *Menu versão*>

 A tabela a seguir descreve os campos de \< *informações sobre o recurso*>.

| Elemento | Descrição |
|---------------------------| - |
| \<*Caminho para a DLL de recurso*> | Este é o caminho completo para a DLL que contém o recurso de menu de recursos ou estiver em branco, indicando que os recursos do VSPackage DLL deve ser usado (como especificado na subchave pacotes onde o VSPackage em si é registrado).<br /><br /> É comum deixar esse campo em branco. |
| \<*ID de recurso de menu*> | Esta é a ID de recurso do `CTMENU` recurso que contém todos os elementos de interface do usuário para o VSPackage conforme compiladas a partir de um [VSCT](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md) arquivo. |
| \<*Versão de menu*> | Este é um número usado como uma versão para o `CTMENU` recursos. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] usa esse valor para determinar se ele precisa remerge o conteúdo a `CTMENU` recursos com seu cache de todos os `CTMENU` recursos. Um remerge é disparado, executando o comando de instalação do devenv.<br /><br /> Esse valor deve ser inicialmente definido como 1 e incrementado após cada alteração no `CTMENU` recursos e antes que ocorra o remerge. |

### <a name="example"></a>Exemplo
 Aqui está um exemplo de um par de entradas de recurso:

```
HKEY_LOCAL_MACHINE\Software\VisualStudio\9.0Exp\
  Menus\
    {019971D6-4685-11D2-B48A-0000F87572EB} = ,1, 10
    {1b027a40-8f43-11d0-8d11-00a0c91bc942} = , 10211, 3
```

## <a name="see-also"></a>Consulte também
- [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Comandos e menus que usam assemblies de interoperabilidade](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)