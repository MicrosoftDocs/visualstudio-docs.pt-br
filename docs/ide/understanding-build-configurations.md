---
title: Noções sobre configurações de build
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-compile
ms.topic: conceptual
f1_keywords:
- SolutionProperties.ActiveConfig
- vs.build.newprojectconfiguration
- vc.proj.configurationsctrl.multipleconfigs
- vs.build.editsolutionconfigurations
- vs.build.editprojectconfigurations
- vs.multipleconfigurations
- vs.build.newsolutionconfiguration
- VS.ConfigurationManager
- VS.MultipleConfig
helpviewer_keywords:
- solution build configurations, about build configurations
- build configurations
- project build configurations
- build configurations, advanced
- projects [Visual Studio], build configuration
- solutions [Visual Studio], build configuration
ms.assetid: 934c727d-3a22-429c-bd13-3552cecf2e24
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a3e361b407d013f27f3cf76d1ff0da98aa36c3c8
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349043"
---
# <a name="understand-build-configurations"></a>Noções sobre configurações de build

É possível armazenar diferentes configurações de propriedades de solução e de projeto para usar em diferentes tipos de builds. Para criar, selecionar, modificar ou excluir uma configuração, é possível usar o **Configuration Manager**. Para abri-lo, na barra de menus, escolha **Build** > **Configuration Manager** ou apenas digite **Configuração** na caixa **Início Rápido**. Também é possível usar a lista **Configurações de Solução** na barra de ferramentas **Padrão** para selecionar uma configuração ou para abrir o **Configuration Manager**.

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Configurações de build no Visual Studio para Mac](/visualstudio/mac/configurations).

> [!NOTE]
> Se não for possível localizar as definições de configuração da solução na barra de ferramentas nem acessar o **Configuration Manager**, as configurações de desenvolvimento [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] poderão ser aplicadas. Para obter mais informações, consulte [Como gerenciar configurações com as configurações para desenvolvedores do Visual Basic aplicadas](../ide/how-to-manage-build-configurations-with-visual-basic-developer-settings-applied.md).

Por padrão, as configurações de Depuração e Versão são incluídas nos projetos criados usando modelos [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Uma configuração de depuração dá suporte à depuração de um aplicativo, e uma configuração de Versão cria uma versão do aplicativo que pode ser implantada. Para saber mais, consulte [Como definir configurações de depuração e versão](../debugger/how-to-set-debug-and-release-configurations.md). Também é possível criar configurações de solução e de projeto personalizadas. Para obter mais informações, consulte [Como criar e editar configurações](../ide/how-to-create-and-edit-configurations.md).

## <a name="solution-configurations"></a>Configurações da solução

Uma configuração de solução especifica como os projetos na solução devem ser criados e implantados. Para modificar uma configuração de solução ou definir uma nova, no **Configuration Manager**, em **Configuração da solução ativa**, escolha **Editar** ou **Novo**.

Cada entrada na caixa **Contextos do Projeto** em uma configuração de solução representa um projeto na solução. Para cada combinação de **Configuração da solução ativa** e **Plataforma da solução ativa**, é possível definir como cada projeto é usado. (Para obter mais informações sobre as plataformas de solução, consulte [Noções básicas sobre plataformas de build](../ide/understanding-build-platforms.md).)

> [!NOTE]
> Quando você define uma nova configuração de solução e marca a caixa de seleção **Criar novas configurações de projeto**, o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] atribui automaticamente a nova configuração a todos os projetos. Da mesma forma, quando você define uma nova plataforma de solução e marca a caixa de seleção **Criar novas plataformas de projeto**, o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] atribui automaticamente a nova plataforma a todos os projetos. Além disso, se você adicionar um projeto que define como destino uma nova plataforma, o Visual Studio adiciona essa plataforma à lista de plataformas de solução e a atribui a todos os projetos.
>
> Ainda é possível modificar as configurações para cada projeto.

A configuração da solução ativa também fornece contexto ao IDE. Por exemplo, se você estiver trabalhando em um projeto e a configuração especificar que ele será criado para um dispositivo móvel, a **Caixa de Ferramentas** exibirá apenas os itens que podem ser usados em um projeto de dispositivo móvel.

## <a name="project-configurations"></a>Configurações de projeto
 A configuração e a plataforma que um projeto define como destino serão usadas conjuntamente para especificar as propriedades a serem usadas quando ele for criado. Um projeto pode ter um conjunto diferente de definições de propriedade para cada combinação de configuração e de plataforma. Para modificar as propriedades de um projeto, é possível usar as Páginas de Propriedades. (No **Gerenciador de Soluções**, abra o menu de atalho do projeto e, em seguida, escolha **Propriedades**.)

 Para cada configuração de projeto, é possível definir propriedades dependentes de configuração, conforme necessário. Por exemplo, para um determinado build, é possível definir quais itens de projeto serão incluídos, quais arquivos de saída serão criados, onde eles serão colocados e como eles serão otimizados.

 As configurações de projeto podem ter diferenças consideráveis. Por exemplo, as propriedades de uma configuração podem especificar que seu arquivo de saída seja otimizado para ocupar o mínimo espaço, enquanto outra configuração pode especificar que seu executável seja executado na velocidade máxima.

 As configurações de projeto são armazenadas pela solução, não pelo usuário, para que possam ser compartilhadas por uma equipe.

 Embora as dependências do projeto não dependam de configuração, somente os projetos especificados na configuração da solução ativa serão criados.

## <a name="how-visual-studio-assigns-project-configurations"></a>Como o Visual Studio atribui configurações de projeto
 Quando você define uma nova configuração de solução e não copia as configurações de uma já existente, o Visual Studio usa os seguintes critérios para atribuir configurações de projeto padrão. Os critérios são avaliados na ordem mostrada.

1.  Se um projeto tiver um nome de configuração (*\<nome de configuração> \<nome de plataforma>*) que corresponda exatamente ao nome da nova configuração de solução, essa configuração será atribuída. Nomes de configuração não diferenciam maiúsculas de minúsculas.

2.  Se o projeto tiver um nome de configuração no qual a parte configuração-nome corresponda à nova configuração de solução, essa configuração será atribuída, independentemente se a parte da plataforma for correspondente ou não.

3.  Se ainda não houver correspondência, a primeira configuração listada no projeto será atribuída.

## <a name="how-visual-studio-assigns-solution-configurations"></a>Como o Visual Studio atribui configurações de solução
 Quando você cria uma configuração de projeto (no **Configuration Manager**, escolhendo **Novo** no menu suspenso na coluna **Configuração** desse projeto) e marca a caixa de seleção **Criar novas configurações de solução** o Visual Studio procura uma configuração de solução com nome semelhante para compilar o projeto em cada plataforma à que ele dá suporte. Em alguns casos, o Visual Studio renomeia as configurações de solução existentes ou define novas configurações.

 O Visual Studio usa os seguintes critérios para atribuir configurações de solução.

-   Se uma configuração de projeto não especificar uma plataforma ou especificar apenas uma delas, então a configuração de solução cujo nome corresponder ao da nova configuração de projeto será localizada ou adicionada. O nome padrão dessa configuração de solução não inclui um nome de plataforma; ele assume a forma *\<nome de configuração do projeto>*.

-   Se um projeto der suporte a várias plataformas, uma configuração de solução será localizada ou adicionada para cada plataforma com suporte. O nome de cada configuração de solução inclui tanto o nome de configuração do projeto quanto o nome da plataforma e tem a forma *\<nome de configuração do projeto> \<nome da plataforma>*.

## <a name="see-also"></a>Consulte também

- [Passo a passo: Compilar um aplicativo](../ide/walkthrough-building-an-application.md)
- [Compilação e build](../ide/compiling-and-building-in-visual-studio.md)
- [Soluções e Projetos](../ide/solutions-and-projects-in-visual-studio.md)
- [Referência de build do C/C++](/cpp/build/reference/c-cpp-building-reference)
- [Opções de linha de comando do Devenv](../ide/reference/devenv-command-line-switches.md)
- [Configurações de build (Visual Studio para Mac)](/visualstudio/mac/configurations)