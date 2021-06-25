---
title: Devenv Command-Line opções para o desenvolvimento de VSPackage | Microsoft Docs
description: Saiba como os desenvolvedores podem automatizar tarefas na linha de comando ao executar devenv.exe, o arquivo que inicia o IDE do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- /Setup command line switch
- /ResetSkipPkgs command line switch
- /RootSuffix command line switch
- /SafeMode command line switch
- /Splash command line switch
- command-line switches
- registry, Visual Studio SDK
- command line, switches
- Visual Studio SDK, command-line switches
ms.assetid: d65d2c04-dd84-42b0-b956-555b11f5a645
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4ea08b4714a79e09fce5933b67997a032532481f
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904237"
---
# <a name="devenv-command-line-switches-for-vspackage-development"></a>Opções de linha de comando do Devenv para desenvolvimento de VSPackage

O Visual Studio permite que os desenvolvedores automatizem tarefas da linha de comando durante a execução `devenv.exe` , o arquivo que inicia o IDE do Visual Studio.

 As tarefas incluem:

- Implantação de aplicativos em configurações predefinidos de fora do IDE.

- Criando projetos automaticamente usando configurações de compilação predefinidas ou configurações de depuração.

- Carregar o IDE em configurações específicas, tudo de fora do IDE. Você também pode personalizar o IDE na inicialização.

## <a name="guidelines-for-switches"></a>Diretrizes para opções

A documentação do Visual Studio descreve as opções de linha de comando no nível do usuário `devenv` . Para obter mais informações, consulte [Opções de linha de comando do devenv](../ide/reference/devenv-command-line-switches.md). A `devenv` ferramenta também dá suporte a opções de linha de comando adicionais que são úteis com o desenvolvimento, a implantação e a depuração do VSPackage.

| Opção de linha de comando | Descrição |
|---------------------| - |
| `/ResetSkipPkgs` | Desmarca todas as opções de ignorar carregamento que foram adicionadas por usuários que desejam evitar o carregamento de VSPackages problemáticas e, em seguida, inicia o Visual Studio. A presença de uma marca SkipLoading desabilita o carregamento de um VSPackage. Limpar a marca habilita novamente o carregamento do VSPackage.<br /><br /> Esta opção não aceita nenhum argumento. |
| `/RootSuffix` | Inicia o Visual Studio usando um local alternativo. O comando a seguir é executado pelo atalho criado pelo instalador do SDK do Visual Studio:<br /><br /> `devenv /RootSuffix exp`<br /><br /> Nesse caso, o `exp` identifica um local com um sufixo específico (por exemplo, `10.0Exp` em vez de `10.0` ). A instância experimental permite que você depure um VSPackage separadamente da instância do Visual Studio que você está usando para escrever código.<br /><br /> Essa opção pode usar qualquer cadeia de caracteres que identifique um local que você criou usando VSRegEx.exe. Para obter mais informações, consulte [a instância experimental](../extensibility/the-experimental-instance.md). |
| `/SafeMode` | Inicia o Visual Studio no modo de segurança, carregando apenas o IDE e os serviços padrão. A `/SafeMode` opção impede que todos os VSPackages de terceiros sejam carregados quando o Visual Studio é iniciado, garantindo a execução estável.<br /><br /> Esta opção não aceita nenhum argumento. |
| `/Setup` | Força o Visual Studio a Mesclar metadados de recursos que descrevem menus, barras de ferramentas e grupos de comandos de todos os VSPackages disponíveis. Você só pode executar este comando como administrador. <br /><br /> Esta opção não aceita nenhum argumento. O comando `devenv /Setup` geralmente é fornecido como a última etapa do processo de instalação. O uso da `/Setup` opção não inicia o IDE.|
| `/Splash` | Mostra a tela inicial do Visual Studio, como de costume, e mostra uma caixa de mensagem antes de mostrar o IDE principal. A caixa de mensagem permite que você estude a tela inicial (por exemplo, para verificar um ícone de produto VSPackage).<br /><br /> Esta opção não aceita nenhum argumento. |

## <a name="see-also"></a>Confira também

- [Adicionar opções de linha de comando](../extensibility/adding-command-line-switches.md)
- [Opções de linha de comando do Devenv](../ide/reference/devenv-command-line-switches.md)
