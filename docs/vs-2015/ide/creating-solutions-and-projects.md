---
title: Criando soluções e projetos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.openprojectfromweb
- vs.newproject
- VS.ToolsOptionsPages.Projects.General
- SolutionItemsProject
helpviewer_keywords:
- solutions [Visual Studio], deleting
- solutions [Visual Studio], creating
- projects [Visual Studio], creating
ms.assetid: 836f8ca0-3fc9-4f4b-9090-45f2e4d2e9c8
caps.latest.revision: 49
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 336fb41ee6a4c90e7065187b2805aefe9e6e6df7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49893689"
---
# <a name="creating-solutions-and-projects"></a>Criando soluções e projetos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os projetos são os contêineres lógicos para tudo que é necessário para criar seu aplicativo. Quando você cria um projeto escolhendo **Arquivo &#124; Novo &#124; Projeto** no menu principal, [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] cria uma solução para contê-lo. Em seguida, é possível adicionar projetos novos ou existentes à solução, se necessário. É possível criar projetos de arquivos de código existentes e criar projetos temporários (apenas .NET) que serão excluídos quando você não os quiser mais.  
  
> [!NOTE]
>  As descrições deste tópico baseiam-se na edição Visual Studio Community. As caixas de diálogo e comandos de menu que você vê podem ser diferentes dos descritos aqui, dependendo de suas configurações ou da edição Visual Studio. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="create-a-project-from-an-installed-project-template"></a>Criar um projeto com base em um modelo de projeto instalado  
 **Arquivo &#124; Novo &#124; Projeto** no menu principal para exibir a caixa de diálogo Novo projeto. No painel esquerdo em **Mencionado &#124; Modelos**, escolha a linguagem de programação e plataforma ou tecnologia, em seguida, escolha um dos modelos disponíveis no painel central.  
  
 Na caixa de diálogo **Novo Projeto**, o menu suspenso **Solução** oferece a opção de criar o novo projeto em uma solução nova ou existente ou em uma nova instância do Visual Studio.  
  
## <a name="create-a-project-from-existing-code-files"></a>Criar um projeto com base em arquivos de código existentes  
 Se você tiver uma coleção de arquivos de origem flexíveis, será possível criar facilmente um projeto que os contenha. Escolha **Arquivo &#124; Novo &#124;Projeto de Código Existente** para iniciar o **Assistente de Criação de Projeto de Arquivos de Código Existentes** e siga os prompts.  
  
> [!TIP]
>  Essa opção funciona melhor para coleções de arquivos relativamente simples.  
  
## <a name="create-a-temporary-project-c-and-visual-basic"></a>Criar um projeto temporário (C# e Visual Basic)  
 Trabalhando com projetos temporários, é possível criar e testar um projeto .NET sem especificar um local de disco. Quando você cria um projeto, basta selecionar um tipo e modelo de projeto e especificar um nome na caixa de diálogo **Novo Projeto**. A qualquer momento enquanto você está trabalhando com o projeto temporário, é possível salvá-lo ou descartá-lo.  
  
## <a name="create-a-net-project-that-targets-a-specific-version-of-the-net-framework"></a>Criar um projeto .NET que direciona uma versão específica do .NET Framework  
 É possível criar um projeto para direcionar versões anteriores do .NET Framework usando o menu suspenso de versão do **.NET Framework** na parte superior da caixa de diálogo **Novo Projeto**. Defina esse valor antes de selecionar um modelo de projeto, uma vez que apenas modelos compatíveis com essa versão do .NET Framework serão exibidos na lista.  
  
 É necessário ter o .NET Framework 3.5 instalado em seu sistema para acessar as versões de estrutura anteriores à versão 4.0.  
  
## <a name="downloading-sample-solutions"></a>Baixando soluções de amostra  
 É possível usar o Visual Studio para baixar e instalar soluções de amostra na [Galeria de Códigos do MSDN](http://go.microsoft.com/fwlink/?LinkId=254185).  
  
 É possível baixar as amostras individualmente ou baixar um Pacote de Amostras que contém amostras relacionadas que compartilham uma tecnologia ou tópico. Você receberá uma notificação quando as alterações no código-fonte forem publicadas para qualquer exemplo baixado.  
  
 Para obter mais informações, consulte [Amostras do Visual Studio](../ide/visual-studio-samples.md).  
  
## <a name="adding-single-files-at-the-solution-level"></a>Adicionando arquivos individuais no nível da solução  
 Às vezes, você pode ter um arquivo que vários projetos referenciam ou que contém dados de texto ou diversos que pertencem logicamente no nível da solução em vez de em um projeto específico.  Para adicionar um item individual a uma solução:  
  
1.  Clique com botão direito do mouse no nó da solução em **Gerenciador de Soluções** e escolha **Adicionar &#124; Novo Item** ou **Adicionar &#124; Item Existente**.  
  
## <a name="creating-empty-solutions"></a>Criando soluções vazias  
 Embora um projeto deva residir em uma solução, é possível criar uma solução que não tem projetos.  
  
#### <a name="to-create-an-empty-solution"></a>Para criar uma solução vazia  
  
1. No menu **Arquivo**, clique em **Novo** e, em seguida, clique em **Novo Projeto**.  
  
2. No painel esquerdo, selecione **Instalados**, selecione **Outros Tipos de Projeto** e, em seguida, selecione **Soluções do Visual Studio** na lista expandida.  
  
3. No painel central, selecione **Solução em Branco**.  
  
4. Veja os valores **Nome** e **Local** para sua solução e, em seguida, clique em **OK**.  
  
   Depois de criar uma solução vazia, é possível adicionar projetos novos ou existentes ou itens a ele clicando em **Adicionar Novo Item** ou **Adicionar Item Existente** no menu **Projeto**.  
  
### <a name="deleting-solutions"></a>Excluindo soluções  
 É possível excluir uma solução permanentemente, mas não usando [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Antes de excluir uma solução, mova os projetos que você pode deseja usar novamente em outra solução. Em seguida, use o Gerenciador de Arquivos para excluir o diretório que contém os arquivos de solução .sln e .suo.  
  
> [!NOTE]
>  O arquivo .suo é um arquivo oculto que não é exibido nas configurações do Gerenciador de Arquivos padrão.  
  
##### <a name="to-delete-a-solution"></a>Para excluir uma solução  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse na solução a ser excluída e selecione **Abrir pasta no Gerenciador de Arquivos**.  
  
2.  No Gerenciador de Arquivos, navegue um nível acima.  
  
3.  Selecione o diretório que contém a solução e pressione Excluir.  
  
## <a name="see-also"></a>Consulte também  
 [Soluções e projetos](../ide/solutions-and-projects-in-visual-studio.md)   
 [NIB Como criar soluções multiprojeto](http://msdn.microsoft.com/en-us/02ecd6dd-0114-46fe-b335-ba9c5e3020d6)



