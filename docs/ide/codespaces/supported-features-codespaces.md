---
title: Recursos do Visual Studio com suporte (versão prévia)
description: Saiba mais sobre os recursos do IDE do Visual Studio disponíveis ao trabalhar com o GitHub Codespaces.
ms.topic: how-to
ms.date: 09/21/2020
author: gregvanl
ms.author: gregvanl
manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.workload:
- multiple
monikerRange: vs-2019
ms.openlocfilehash: ebd64a314f1c4d6afd7b6e6fcc3b38148ff68225
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104672963"
---
# <a name="supported-visual-studio-features-preview"></a>Recursos do Visual Studio com suporte (versão prévia)

> [!Important] 
> A partir de 12 de abril de 2021, a conexão ao GitHub Codespaces do Visual Studio 2019 não será mais suportada e essa versão prévia privada terá sido concluída. Estamos concentrados em experiências em evolução para um loop interno baseado em nuvem e soluções de VDI otimizadas para um amplo conjunto de cargas de trabalho do Visual Studio. Incentivamos você a estar envolvido em nosso [Fórum da comunidade de desenvolvedores](https://developercommunity.visualstudio.com/home) para Visual Studio para obter informações sobre versões futuras e informações de roteiro. 


O Visual Studio fornece uma experiência de desenvolvimento rica ao se conectar a um codespace. Você Obtém as ferramentas de loop interno do Visual Studio com as quais está familiarizado para editar, depurar, testar e realizar a versão do código-fonte, bem como recursos de produtividade, como modelos de projeto, navegação de código avançada e IntelliSense.

Na [versão beta pública](https://github.com/features/codespaces)Codespaces do GitHub atual, alguns recursos do Visual Studio podem não ter suporte completo ou podem estar inicialmente ausentes. As seções a seguir descrevem o que você pode esperar com o Visual Studio e o GitHub Codespaces beta e o que você pode aguardar no futuro. 

Isso **não deve ser uma lista exaustiva**, mas para explicar os recursos gerais do Visual Studio quando conectados a um codespace.

> [!NOTE]
> Se houver um recurso que você está perdendo ao usar o codespaces com o Visual Studio, informe-nos abrindo um problema na [comunidade de desenvolvedores do Visual Studio](https://aka.ms/feedback/suggest?space=8). Isso nos ajuda a priorizar os recursos mais desejados.

> [!NOTE]
> Os recursos descritos abaixo são para o Visual Studio e não para os dois outros clientes do GitHub Codespaces; Visual Studio Code e o editor no navegador.

## <a name="edit-and-navigation"></a>Editar e navegar

Você deve notar pouca diferença no código-fonte de edição em um codespace à medida que obtém recursos de linguagem inteligente, como IntelliSense, navegação de código, diagnóstico e sugestões.

* IntelliSense
* Navegação de código *
* Formatação de código com documento de formato
* Realce de sintaxe
* Informações rápidas *
* HTML, CSS, editores do Razor *-suporte parcial.
* Editor de JavaScript e TypeScript *-suporte parcial.

Ainda não disponível:

* IntelliSense *-alguns dos filtros de AutoCompletar/lista de membros não estão disponíveis. A conclusão para tipos não importados e o IntelliSense na janela de observação ainda não está disponível.
* Navegação de código *-a maioria dos comandos com suporte. Ir para base e localizar em arquivos com especificação de caminho ainda não tem suporte.
* Informações rápidas *-a colorização em informações rápidas não é suportada.
* HTML, CSS, editores do Razor *-diagnóstico, conclusão do IntelliSense, informações rápidas, recuo inteligente. Atualmente não há suporte para colorização semântica, comandos de navegação, etc.
* Editor de JavaScript e TypeScript *-blocos de script (por exemplo, conteúdo JavaScript em arquivos HTML e CSHTML) e realce semântico ainda não têm suporte. Problemas conhecidos com recursos de lâmpada e refiapoing.
* Exibição de destinos de CMake
* Editor de configurações do projeto CMake
* CTRL + F7 (arquivo de compilação)
* CodeLens
* Snippets de código
* IntelliCode

## <a name="application-types-and-configuration"></a>Tipos de aplicativos e configuração

Há suporte para a maioria dos tipos de aplicativos e configurações de projeto, mas você precisará editar o código do projeto diretamente sem a ajuda dos designers visuais. Para obter mais diretrizes de configuração, consulte [como personalizar um codespace](customize-codespaces.md).

* Modelos de projeto e de item
* Projetos do .NET Core e do ASP.NET Core
* Aplicativos de console do C++-CMake e vcxproj com suporte
* Aplicativos C++ destinados ao Linux-principalmente suportados para não GUI. Capacidade de instalar e provisionar o WSL, o IntelliSense específico da plataforma e o Build.
* Edição de arquivo de projeto-com suporte na maioria das vezes. Faltam alguns recursos de conclusão, realce de sintaxe e edição avançada.
* Contas do GitHub – podem ser usadas para criar e conectar-se ao Codespaces e acessar os recursos disponíveis para a conta no GitHub.
* CLI do Azure-não compartilha as contas de identidade ou conjunto de chaves do Visual Studio conectadas. Não há suporte para o logon baseado em navegador, mas você pode autenticar dentro do terminal integrado usando: `az login --use-device-code` .

Ainda não disponível:

* Designers de interface do usuário – WinForms, WPF e designers de recursos
* A conversão de aplicativo WinForms e WPF Projects só está disponível em um sinalizador de recurso
* Projetos Visual Basic e F #
* Projetos de .NET Framework de destino
* Projetos de Docker Compose
* Página de propriedades do projeto
* Opções de autenticação em modelos de ASP.NET Core
* Aplicativos que exigem uma GUI para instalar – qualquer coisa que possa ser instalada com o terminal tem suporte (incluindo o instalador de Chocolatey), mas a GUI real não estará imediatamente disponível. Habilitar a Live Share de tela inteira para acessar a GUIs é uma solução alternativa atual. Os consoles de administração não estão acessíveis. Não há suporte para aplicativos que exigem uma reinicialização para instalação.
* Identidades gerenciadas para recursos do Azure no Visual Studio
* Recursos de intranet (rede privada)-atualmente, o codespaces não poderá se conectar a nenhum recurso que exija uma VPN.
* Extensões-não há suporte para extensões ao usar o Codespaces com o Visual Studio.

## <a name="debugging"></a>Depuração

Há suporte para a depuração de loop interno essencial, incluindo a definição de pontos de interrupção, a depuração básica no código, a inspeção de variáveis e as janelas local, automático e inspecionar. Não há suporte para algumas janelas, personalizações e visualizadores adicionais.

* Interrupção
* Depuração básica
* Locais, automáticos, Assista ao Windows *-suporte parcial.
* O servidor de símbolos, o servidor de origem e a importação/exportação de dicas de dados são todos parcialmente suportados.

Ainda não disponível:

* Pontos de interrupção *-rótulos de ponto de interrupção, pontos de interrupção de dados e definir ponto de interrupção na janela de desmontagem está em andamento. Há suporte parcial para importar e exportar pontos de interrupção.
* Locais, automáticos, inspecionar janelas * – algumas funcionalidades, como conclusão de instrução na caixa de pesquisa e navegação da caixa de pesquisa.
* Personalizações de interface do usuário-Propriedades fixas e ocultar parâmetros de modelo sem suporte.
* Visualizadores – há suporte parcial para C++ natvis. Janela de desmontagem, diagnóstico Visual XAML, visualizadores .NET personalizados e visualizadores de conjuntos de conjunto de os não são suportados.
* Janelas do depurador adicionais com suporte parcial do Windows. Janela de pilhas paralelas-a exibição tarefas, o Hub de diagnóstico e a caixa de diálogo Localizar fonte/símbolo não têm suporte.
* Alguns fluxos de trabalho do depurador – anexar ao processo, depurador JIT (just in time), depuração de despejo, criação de perfil e IntelliTrace não têm suporte. O C++ Apenas Meu Código Stepping tem suporte parcial.
* Editar e continuar – sem suporte para código gerenciado e nativo.
* Recursos de Threading – congelar/descongelar Threads, renomear thread e mostrar threads na fonte não têm suporte.
* Recursos de depuração adicionais – não há suporte para a etapa automática em relação a propriedades e operadores (.NET Core) e a depuração específica. 

## <a name="features"></a>Recursos

Ao trabalhar com o Visual Studio conectado a um codespace, você obtém os mesmos recursos de acessibilidade que ao trabalhar localmente.

* Controle do código-fonte-suporte completo do git por meio da nova [experiência de git integrada](../git-with-visual-studio.md). Para que os submódulos git sejam clonados em um codespace, talvez seja necessário executar `git submodule update` a partir do terminal.
* Acessibilidade – há um problema conhecido com a tecnologia assistencial que não consegue acessar o appcasting de um aplicativo depurado. Além dessa limitação, não acreditamos que haja outros problemas de compatibilidade que ainda não existam na experiência do Visual Studio local. Informe-nos se detectar bugs ao arquivar um problema na [comunidade de desenvolvedores](https://aka.ms/feedback/report?space=8).
* Publicação – publicar no Azure por meio de ações do GitHub tem suporte.
* Serviços conectados-não há suporte parcial para o app insights, o keyvault, o armazenamento, o SQL, o Redis, o cosmos, o openAPI e o gRPC.
* Gerenciador de testes *-com suporte na maioria das vezes.

Ainda não disponível:

* Gerenciador de testes *-alguns recursos, como seleção de arquitetura padrão, executam testes em paralelo, listas de reprodução, etc. Problemas conhecidos com a depuração de um teste de unidade, configurações de execução e alguns recursos empresariais adicionais. Não há suporte para testes de unidade de criação de perfil.
* Interface do usuário do Gerenciador de pacotes NuGet-a linha de comando do NuGet tem suporte.
* Recursos de teste empresarial-Live Unit Testing, falsificações da Microsoft, cobertura de código e IntelliTest não têm suporte.
* Cenários de publicação avançada-publicação seletiva, publicação de FTP, alterações de visualização, barra de ferramentas de publicação rápida, etc.

## <a name="see-also"></a>Veja também

* [O que é o GitHub Codespaces?](codespaces-overview.md)
* [Como usar o Visual Studio com um codespace](use-visual-studio-with-codespaces.md)
* [Como personalizar um codespace](customize-codespaces.md)
