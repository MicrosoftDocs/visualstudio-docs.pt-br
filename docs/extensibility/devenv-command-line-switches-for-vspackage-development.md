---
title: Opções de linha de comando devenv para desenvolvimento de VSPackage | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- /setup command line switch
- /resetskippkgs command line switch
- /noVSIP command line switch
- /rootsuffix command line switch
- command-line switches
- registry, Visual Studio SDK
- command line, switches
- Visual Studio SDK, command-line switches
ms.assetid: d65d2c04-dd84-42b0-b956-555b11f5a645
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 8fd305133f913877f8d4ad4808a8c4efcab52af4
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49847052"
---
# <a name="devenv-command-line-switches-for-vspackage-development"></a>Opções de linha de comando devenv para desenvolvimento de VSPackage
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] permite que os desenvolvedores a automatizar tarefas da linha de comando ao executar *devenv.exe*, o arquivo que inicia o ambiente de desenvolvimento integrado (IDE) do Visual Studio.  

 As tarefas incluem:  

-   Implantando aplicativos em configurações predefinidas de fora do IDE.  

-   Compilando projetos usando a predefinição de configurações de build ou automaticamente configurações de depuração.  

-   Carregando o IDE em configurações específicas, tudo a partir de fora do IDE. Além disso, você pode personalizar o IDE durante a inicialização.  

## <a name="guidelines-for-switches"></a>Diretrizes para comutadores  
 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] documentação descreve as opções de linha de comando do devenv do nível de usuário. Para obter mais informações, consulte [opções de linha de comando do Devenv](../ide/reference/devenv-command-line-switches.md). Devenv também dá suporte a opções de linha de comando adicionais que são úteis com desenvolvimento VSPackage, implantação e depuração.  


| Opção de linha de comando | Descrição |
|---------------------| - |
| /SafeMode | Inicia [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] no modo de segurança, carregando apenas o padrão IDE e serviços. A opção /safemode impede que todos os VSPackages de terceiros carregados quando [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] é iniciado, garantindo assim uma execução estável.<br /><br /> Esta opção não aceita nenhum argumento. |
| /resetskippkgs | Limpa todos os ignorar opções de carregamento que foram adicionadas por usuários que desejam evitar carregar VSPackages problemáticos, em seguida, inicia [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. A presença de uma marcação SkipLoading desabilita o carregamento de um VSPackage. Limpar a marcação habilita novamente o carregamento do VSPackage.<br /><br /> Esta opção não aceita nenhum argumento. |
| /rootsuffix | Inicia [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] por meio de um local alternativo. O comando a seguir é executado pelo atalho criado pelo [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] instalador:<br /><br /> devenv /RootSuffix exp<br /><br /> Nesse caso, exp identifica um local com um sufixo específico, por exemplo 10.0Exp em vez de 10.0. A instância experimental permite que você depure um VSPackage separadamente da instância do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] que você está usando para escrever código.<br /><br /> Essa opção pode levar a qualquer cadeia de caracteres que identifica um local que você criou usando VSRegEx.exe. Para obter mais informações, consulte [a instância Experimental](../extensibility/the-experimental-instance.md). |
| /Splash | Mostra o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] tela inicial como de costume e, em seguida, mostra uma caixa de mensagem antes de mostrar o IDE principal. A caixa de mensagem permite que você estude a tela inicial, para verificar se há um ícone de produto de VSPackage, por exemplo.<br /><br /> Esta opção não aceita nenhum argumento. |

## <a name="see-also"></a>Consulte também  
 [Adicionar opções de linha de comando](../extensibility/adding-command-line-switches.md)   
 [Opções de linha de comando do Devenv](../ide/reference/devenv-command-line-switches.md)