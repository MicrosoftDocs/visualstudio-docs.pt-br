---
title: Adicionando opções de linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- command-line switches, adding
- command-line switches, retrieving
- IVsAppCommandLine::GetOption method
- command line, switches
ms.assetid: 8bbbd87e-76fe-4fb5-8ef9-65f5e31967cf
caps.latest.revision: 22
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 5034e6bcb5aa878c16dbf9dadf478d68276c4fac
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51748279"
---
# <a name="adding-command-line-switches"></a>Adicionando opções de linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode adicionar opções de linha de comando que se aplicam ao seu VSPackage quando devenv.exe é executada. Use <xref:Microsoft.VisualStudio.Shell.ProvideAppCommandLineAttribute> para declarar o nome do comutador e suas propriedades. Neste exemplo, a opção MySwitch é adicionada para uma subclasse de VSPackage nomeado **AddCommandSwitchPackage** sem argumentos e com o VSPackage carregados automaticamente.  
  
```csharp  
[ProvideAppCommandLine("MySwitch", typeof(AddCommandSwitchPackage), Arguments = "0", DemandLoad = 1)]  
```  
  
 Os parâmetros nomeados são mostrados na tabela a seguir  
  
 Arguments  
 O número de argumentos para o comutador. Pode ser "*", ou uma lista de argumentos.  
  
 DemandLoad  
 Carrega o VSPackage automaticamente se isso estiver definido como 1, caso contrário, defina como 0.  
  
 HelpString  
 A cadeia de caracteres ou o recurso de ID de ajuda a cadeia de caracteres para exibir com **devenv /?**.  
  
 Nome  
 O comutador.  
  
 PackageGuid  
 O GUID do pacote.  
  
 O primeiro valor dos argumentos é geralmente 0 ou 1. Um valor especial de ' *' pode ser usado para indicar que o resto inteiro da linha de comando é o argumento. Isso pode ser útil para cenários onde um usuário deve passar em uma cadeia de caracteres de comando do depurador de depuração.  
  
 É o valor de DemandLoad `true` (1) ou `false` (0) indica que o VSPackage deve ser carregado automaticamente.  
  
 O valor de HelpString é a ID do recurso da cadeia de caracteres que aparece no devenv /? Exibição da Ajuda. Esse valor deve estar no formato "#nnn" em que nnn é um número inteiro. O valor de cadeia de caracteres no arquivo de recurso deve terminar com um caractere de nova linha.  
  
 O valor do nome é o nome do comutador.  
  
 O valor de PackageGuid é o GUID do pacote que implementa essa opção. O IDE usa esse GUID para localizar o VSPackage no registro ao qual se aplica a opção de linha de comando.  
  
## <a name="retrieving-command-line-switches"></a>Recuperando opções de linha de comando  
 Quando o pacote é carregado, você pode recuperar as opções de linha de comando ao concluir as etapas a seguir.  
  
1. Em seu VSPackage <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> implementação, chamada `QueryService` nos <xref:Microsoft.VisualStudio.Shell.Interop.SVsAppCommandLine> para obter o <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine> interface.  
  
2. Chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine.GetOption%2A> para recuperar as opções de linha de comando que o usuário inseriu.  
  
   O código a seguir mostra como descobrir se a opção de linha de comando MySwitch foi inserida pelo usuário:  
  
```csharp  
IVsAppCommandLine cmdline = (IVsAppCommandLine)GetService(typeof(SVsAppCommandLine));  
  
int isPresent = 0;  
string optionValue = "";  
  
cmdline.GetOption("MySwitch", out isPresent, out optionValue);  
```  
  
 É sua responsabilidade verificar suas opções de linha de comando sempre que o pacote é carregado.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>   
 [Opções de linha de comando devenv](../ide/reference/devenv-command-line-switches.md)   
 [Utilitário CreatePkgDef](../extensibility/internals/createpkgdef-utility.md)   
 [Arquivos .Pkgdef](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgdef-file.md)

