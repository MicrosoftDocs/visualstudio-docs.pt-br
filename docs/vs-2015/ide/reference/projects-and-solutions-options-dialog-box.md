---
title: Caixa de diálogo Projetos e Soluções, Opções | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Projects and Solutions Options dialog box
- Options dialog box, Projects and Solutions
ms.assetid: 2801f24e-a138-488a-ae3c-e1f99a678ac0
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4230f99b78809594d65da991c65c11d7dc30efd4
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49246188"
---
# <a name="projects-and-solutions-options-dialog-box"></a>Soluções e Projetos, caixa de diálogo Opções
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Define o caminho padrão das pastas do projeto [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e determina o comportamento padrão da Janela de **Saída**, da **Lista de Tarefas** e do **Gerenciador de Soluções**, conforme os projetos são desenvolvidos e compilados. Para acessar essa caixa de diálogo, clique em **Ferramentas/Opções**, expanda **Projetos e Soluções** e clique em **Geral**.  
  
> [!NOTE]
>  As opções disponíveis nas caixas de diálogo e os nomes os locais dos comandos de menu que você vê podem diferir do que é descrito na Ajuda, dependendo de suas configurações ativas ou da edição. Esta página de Ajuda foi escrita considerando as **Configurações gerais de desenvolvimento**. Para exibir ou alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="settings"></a>Configurações  
 **Local dos projetos**  
 Define o local padrão em que as novas pastas de projetos e da solução e os diretórios são criados. Várias caixas de diálogo também usam o local definido nessa opção para os pontos iniciais da pasta. Por exemplo, a caixa de diálogo Abrir Projeto usa esse local para o atalho Meus Projetos.  
  
 **Local dos modelos de projeto do usuário**  
 Define o local padrão usado pela caixa de diálogo **Novo Projeto** para criar a lista de **Meus Modelos**. Para obter mais informações, consulte [Como localizar e organizar modelos](../../ide/how-to-locate-and-organize-project-and-item-templates.md).  
  
 **Local dos modelos de item do usuário**  
 Define o local padrão usado pela caixa de diálogo **Adicionar Novo Item** para criar a lista de **Meus Modelos**. Para obter mais informações, consulte [Como localizar e organizar modelos](../../ide/how-to-locate-and-organize-project-and-item-templates.md).  
  
 **Sempre mostrar a Lista de Erros se houver erros após a conclusão do build**  
 Abre a janela **Lista de Erros** após a conclusão do build, somente se houve falha de build de um projeto. Os erros que ocorrem durante o processo de build são exibidos. Quando essa opção estiver desmarcada, os erros ainda ocorrerão, mas a janela não será aberta quando o build for concluído. Essa opção é habilitada por padrão.  
  
 **Acompanhar item ativo no Gerenciador de Soluções**  
 Quando essa opção estiver selecionada, o **Gerenciador de Soluções** será aberto automaticamente e o item ativo será selecionado. O item selecionado é alterado conforme você trabalha com arquivos diferentes em um projeto ou uma solução, ou com componentes diferentes em um designer. Quando essa opção estiver desmarcada, a seleção no **Gerenciador de Soluções** não será alterada automaticamente. Essa opção é habilitada por padrão.  
  
 **Mostrar configurações de build avançadas**  
 Quando estiverem marcadas, as opções de configuração de build serão exibidas nas caixas de diálogo **Páginas de Propriedades do Projeto** e **Páginas de Propriedades da Solução**. Quando estiverem desmarcadas, as opções de configuração de build não serão exibidas nas caixas de diálogo **Páginas de Propriedades do Projeto** e **Páginas de Propriedades da Solução** para projetos do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] e do [!INCLUDE[csprcs](../../includes/csprcs-md.md)] que contêm uma configuração ou as duas configurações de depuração e versão. Se um projeto tiver uma configuração definida pelo usuário, as opções de configuração de build serão mostradas.  
  
 Quando estiverem desmarcados, os comandos do menu **Build**, como **Compilar Solução**, **Recompilar Solução** e **Limpar Solução** serão executados na configuração de Versão e os comandos do menu **Depurar**, como **Iniciar Depuração** e **Iniciar Sem Depuração**, serão executados na configuração de Depuração.  
  
 **Sempre mostrar solução**  
 Quando essa opção estiver selecionada, a solução e todos os comandos que atuam em soluções sempre serão mostrados no IDE. Quando estiver desmarcada, todos os projetos serão criados como projetos independentes e você não verá a solução no Gerenciador de Soluções nem os comandos que atuam em soluções no IDE se a solução contiver apenas um projeto.  
  
 **Salvar novos projetos quando criados**  
 Quando essa opção estiver selecionada, será possível especificar um local para o projeto na caixa de diálogo **Novo Projeto**. Quando estiver desmarcada, todos os novos projetos serão criados como projetos temporários. Quando você estiver trabalhando com projetos temporários, poderá criar e testar um projeto sem a necessidade de especificar um local de disco.  
  
 **Avisar o usuário quando o local do projeto não for confiável**  
 Se você tentar criar um novo projeto ou abrir um projeto existente em um local que não é totalmente confiável (por exemplo, em um caminho UNC ou um caminho HTTP), uma mensagem será exibida. Use essa opção para especificar se a mensagem será exibida sempre que você tentar criar ou abrir um projeto em um local que não é totalmente confiável.  
  
 **Mostrar Janela de Saída no início do build**  
 Exibe a Janela de Saída automaticamente no IDE no início dos builds da solução. Para obter mais informações, consulte [Como controlar a Janela de Saída](http://msdn.microsoft.com/library/91aebd15-8854-4a7a-9f7d-57376fb4e858). Essa opção é habilitada por padrão.  
  
 **Solicitar renomeação simbólica ao renomear arquivos**  
 Quando estiver selecionada, exibirá uma caixa de mensagem solicitando se [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] também deverá renomear ou não todas as referências no projeto com o elemento de código.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo Opções, Projetos e Soluções, Compilar e Executar](../../ide/reference/options-dialog-box-projects-and-solutions-build-and-run.md)



