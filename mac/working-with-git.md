---
title: Trabalhando com Git
description: Usando o Git no Visual Studio para Mac.
author: conceptdev
ms.author: crdun
ms.date: 05/06/2018
ms.assetid: 852B6A9D-AEFA-4EF4-A5DD-94A506019D20
ms.openlocfilehash: 10d5b34ece7d093a42bafc1f0e410b670dd342f1
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51296444"
---
# <a name="working-with-git"></a>Trabalhando com Git

O Git é um sistema de controle de versão distribuído que permite que as equipes trabalhem nos mesmos documentos simultaneamente. Isso significa que há um servidor central que contém todos os arquivos, mas quando um repositório passar por check-out nessa fonte central, todo o repositório será clonado para o computador local.

As seções a seguir explorarão como o Git pode ser usado para controle de versão no Visual Studio para Mac.

## <a name="git-version-control-menu"></a>Menu de controle de versão do Git

A imagem a seguir ilustra as opções fornecidas pelo Visual Studio para Mac pelo item de menu de Controle de Versão:

![Item de menu de Controle de Versão](media/version-control-gitVersionControlMenu.png)

## <a name="push-and-pull"></a>Push e Pull

Push e pull são duas das ações mais usadas no Git. Para sincronizar as alterações que outras pessoas fizeram no repositório remoto, você deverá **Efetuar pull** de lá. Isso é feito no Visual Studio para Mac selecionando **Controle de versão > Atualizar solução**.

Depois de atualizar, examinar e confirmar seus arquivos, você deverá **Efetuar push** neles para o repositório remoto a fim de permitir que outros usuários acessem suas alterações. Isso é feito no Visual Studio para Mac selecionando **Controle de versão > Efetuar push nas alterações**. Isso exibirá a caixa de diálogo de Push, permitindo que você exiba as alterações confirmadas e selecione o branch para o qual o push será efetuado:

![Caixa de diálogo mostrando o branch de confirmação](media/version-control-gitPush.png)

Você também poderá Confirmar e Efetuar push nas alterações ao mesmo tempo por meio da caixa de diálogo Confirmar:

![Opção que mostra como confirmar e efetuar push ao mesmo tempo.](media/version-control-commitPush.png)

## <a name="blame-log-and-merge"></a>Acusar, Registrar em log e Mesclar

Na parte inferior da janela são exibidas cinco guias, conforme ilustrado abaixo:

![Guias de Controle de versão](media/version-control-gitTabs.png)

Elas permitem executar as seguintes ações:

* **Código-fonte** – Exibe o arquivo de código-fonte.
* **Alterações** – Exibe a alteração no código entre o arquivo local e o arquivo de base. Você também pode comparar versões diferentes do arquivo em diferentes hashes:

    ![Guia Alterações](media/version-control-gitChange.png)

* **Acusar** – Exibe o nome do usuário associado a cada seção de código.
* **Registrar em log** – Exibe todas as confirmações, horas, datas, mensagens e usuários que são responsáveis pelo arquivo:

    ![Guia Log](media/version-control-gitLog.png)

* **Mesclar** – Pode ser usado em caso de conflito de mesclagem ao confirmar seu trabalho. Mostra uma representação visual das alterações feitas por você e por outros desenvolvedores, permitindo que você combine as duas seções de código corretamente.

## <a name="switching-branches"></a>Alternar os branches

Por padrão, o primeiro branch criado em um repositório é conhecido como o branch **Mestre** . Tecnicamente não há nada diferente entre o branch mestre e os demais, porém o branch mestre é aquele que geralmente é considerado “dinâmico” ou “produção” pelas equipes de desenvolvimento.

Uma linha independente de desenvolvimento pode ser criada derivando-a do Mestre (ou de qualquer outro branch). Isso fornece uma nova versão pontual do branch mestre, permitindo desenvolvimento independentemente de qual deles é “dinâmico”. É comum usar branches dessa forma para recursos no desenvolvimento de software

Os usuários podem criar tantos branches quanto desejarem para cada repositório, porém é recomendado que, após terminar de usar um branch, ele seja excluído para manter o repositório organizado.

Branches são exibidos no Visual Studio para Mac navegando para **Controle de versão > Gerenciar branches e remotos...**:

![Exibição Branches](media/version-control-gitBranch2.png)

Alterne para outro branch selecionando-o na lista e pressionando o botão **Alternar para o branch**.

Para criar um novo branch, selecione o botão **Novo** na caixa de diálogo Configuração de repositório Git. Digite o nome do novo branch:

![Criar um novo branch](media/version-control-gitBranch.png)

Você também pode definir um branch remoto como seu branch de _acompanhamento_. Leia mais sobre o acompanhamento de branches na [Documentação do Git](https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches#Tracking-Branches).

Consulte o branch atual no Painel de Soluções, ao lado do nome do projeto:

 ![Branch atual exibido no painel de soluções](media/version-control-gitBranchName.png)

## <a name="reviewing-and-committing"></a>Revisar e confirmar

Para examinar as alterações nos arquivos, use as guias Alterações, Acusar, Registro em log e Mesclar em cada documento, ilustrado anteriormente neste tópico.

Examine todas as alterações no seu projeto navegando para o item de menu **Controle de versão > Examinar solução e confirmar**:

![Exibição Examinar código](media/version-control-gitReviewCommit.png)

Isso permite exibir todas as alterações em cada arquivo de um projeto com a opção de Reverter, Criar um Patch ou Confirmar.

Para confirmar um arquivo no repositório remoto, pressione **Confirmar**, insira uma mensagem de confirmação e confirme com o botão Confirmar:

![Confirmando um arquivo](media/version-control-gitCommit.png)

Depois de ter confirmado suas alterações, efetue push nelas para o repositório remoto para permitir que outros usuários possam vê-los.

## <a name="see-also"></a>Consulte também

* [Compartilhar seu código com o Visual Studio 2017 e o GIT do Azure Repos](/azure/devops/repos/git/share-your-code-in-git-vs-2017)