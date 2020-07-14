---
title: Adicionando opções de linha de comando | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- command-line switches, adding
- command-line switches, retrieving
- IVsAppCommandLine::GetOption method
- command line, switches
ms.assetid: 8bbbd87e-76fe-4fb5-8ef9-65f5e31967cf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bb4abf5352ac6ad78852bd3224df0b22784470db
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903478"
---
# <a name="add-command-line-switches"></a>Adicionar opções de linha de comando
Você pode adicionar opções de linha de comando que se aplicam ao seu VSPackage quando *devenv.exe* é executado. Use <xref:Microsoft.VisualStudio.Shell.ProvideAppCommandLineAttribute> para declarar o nome do comutador e suas propriedades. Neste exemplo, a opção mySwitch é adicionada a uma subclasse de VSPackage chamada **AddCommandSwitchPackage** sem argumentos e com o VSPackage carregado automaticamente.

```csharp
[ProvideAppCommandLine("MySwitch", typeof(AddCommandSwitchPackage), Arguments = "0", DemandLoad = 1)]
```

 Os parâmetros nomeados são mostrados nas descrições a seguir.

|Nome|Descrição|
|-|-|
| Argumentos | O número de argumentos para a opção. Pode ser "*" ou uma lista de argumentos. |
| À DEMANDLOAD | Carregue o VSPackage automaticamente se ele estiver definido como 1, caso contrário, definido como 0. |
| HelpString | A cadeia de caracteres de ajuda ou a ID de recurso da cadeia de caracteres a ser exibida com **devenv/?**. |
| Nome | A opção. |
| PackageGuid | O GUID do pacote. |

 O primeiro valor de argumentos é geralmente 0 ou 1. Um valor especial de ' * ' pode ser usado para indicar que todo o restante da linha de comando é o argumento. Isso pode ser útil para cenários de depuração em que um usuário deve passar uma cadeia de comando de depurador.

 O valor de À DEMANDLOAD é `true` (1) ou `false` (0) indica que o VSPackage deve ser carregado automaticamente.

 O valor de HelpString é a ID de recurso da cadeia de caracteres que aparece no **devenv/?** Exibição da ajuda. Esse valor deve estar no formato "#nnn", em que NNN é um inteiro. O valor da cadeia de caracteres no arquivo de recurso deve terminar em um caractere de nova linha.

 O nome valor é o nome da opção.

 O valor de PackageGuid é o GUID do pacote que implementa essa opção. O IDE usa esse GUID para localizar o VSPackage no registro ao qual a opção de linha de comando se aplica.

## <a name="retrieve-command-line-switches"></a>Recuperar opções de linha de comando
 Quando o pacote for carregado, você poderá recuperar as opções de linha de comando concluindo as etapas a seguir.

1. Na implementação do seu VSPackage <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> , chame `QueryService` <xref:Microsoft.VisualStudio.Shell.Interop.SVsAppCommandLine> para obter a <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine> interface.

2. Chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine.GetOption%2A> para recuperar as opções de linha de comando que o usuário inseriu.

   O código a seguir mostra como descobrir se a opção de linha de comando mySwitch foi inserida pelo usuário:

```csharp
IVsAppCommandLine cmdline = (IVsAppCommandLine)GetService(typeof(SVsAppCommandLine));

int isPresent = 0;
string optionValue = "";

cmdline.GetOption("MySwitch", out isPresent, out optionValue);
```

 É sua responsabilidade verificar se há opções de linha de comando sempre que seu pacote for carregado.

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>
- [Opções de linha de comando do Devenv](../ide/reference/devenv-command-line-switches.md)
- [Utilitário CreatePkgDef](../extensibility/internals/createpkgdef-utility.md)
- [. Arquivos pkgdef](https://devblogs.microsoft.com/visualstudio/whats-a-pkgdef-and-why/)
