---
title: 'Como: criar uma solução de linguagem específica do domínio | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.dsltools.designerwizard
helpviewer_keywords:
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools], creating domain-specific language
- Domain-Specific Language Tools, creating solutions
ms.assetid: e585b63b-34d2-405a-8d81-39ea22317975
caps.latest.revision: 43
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 2650afc2172cdcceca892d4ad19a05becac3e472
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49908896"
---
# <a name="how-to-create-a-domain-specific-language-solution"></a>Como criar uma solução de linguagem específica do domínio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Uma linguagem específica de domínio (DSL) é criada usando especializado [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] solução.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Antes de iniciar este procedimento, você deve primeiro instalar esses componentes:  
  
|||  
|-|-|  
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[http://go.microsoft.com/fwlink/?LinkID=185579](http://go.microsoft.com/fwlink/?LinkID=185579)|  
|[!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]|[http://go.microsoft.com/fwlink/?LinkID=185580](http://go.microsoft.com/fwlink/?LinkID=185580)|  
|SDK de Visualização e Modelagem do Visual Studio|[http://go.microsoft.com/fwlink/?LinkID=185581](http://go.microsoft.com/fwlink/?LinkID=185581)|  
  
## <a name="creating-a-domain-specific-language-solution"></a>Criando uma solução de linguagem específica do domínio  
  
#### <a name="to-create-a-domain-specific-language-solution"></a>Para criar uma solução de linguagem específica do domínio  
  
1. Inicie o assistente DSL.  
  
   1. No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.  
  
   2. A caixa de diálogo **Novo Projeto** é exibida.  
  
   3. Sob **tipos de projeto**, expanda o **Other Project Types** nó e clique em **extensibilidade**.  
  
   4. Clique em **Designer de linguagem específica do domínio**.  
  
   5. No **nome** , digite um nome para a solução. Clique em **OK**.  
  
       O **Assistente de Designer de linguagem específica do domínio** é exibida.  
  
      > [!NOTE]
      >  De preferência, o nome que você digita deve ser um Visual C# identificador válido, porque ele pode ser usado para gerar código.  
  
      ![Criar caixa de diálogo DSL](../modeling/media/create-dsldialog.png "Create_DSLDialog")  
  
2. Escolha um modelo DSL.  
  
    Sobre o **selecionar opções de linguagem específica do domínio** , selecione um dos modelos de solução, como **linguagem mínima**. Escolha um modelo que é semelhante a DSL que você deseja criar.  
  
    Para obter mais informações sobre modelos de solução, consulte [escolhendo um modelo de solução de linguagem específica do domínio](../modeling/choosing-a-domain-specific-language-solution-template.md).  
  
3. Digite uma extensão de nome de arquivo **extensão de arquivo** página. Ele deve ser exclusivo no seu computador e, em todos os computadores nos quais você deseja instalar a DSL. Você deve ver a mensagem **nenhum aplicativo ou os editores do Visual Studio usam esta extensão**.  
  
   -   Se você usou a extensão de nome de arquivo no anteriores DSLs experimentais que não foram totalmente instaladas, você pode desmarcá-las fora usando o **redefinir a instância Experimental** ferramenta, que pode ser encontrada no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] menu SDK.  
  
   -   Se outro [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensão que usa esta extensão de arquivo tiver sido totalmente instalado em seu computador, considere desinstalá-lo. Sobre o **ferramentas** menu, clique em **Gerenciador de extensões**.  
  
4. Inspecione e ajustar se necessário, os campos nas páginas restantes do assistente. Quando estiver satisfeito com as configurações, clique em **concluir**. Para obter mais informações sobre as configurações, consulte [páginas do Assistente de Designer de DSL](#settings).  
  
    O assistente cria uma solução que tem dois projetos, que são nomeados **Dsl** e **DslPackage**.  
  
   > [!NOTE]
   >  Se você vir uma mensagem que o alerta não executar modelos de texto de fontes não confiáveis, clique em **Okey**. Você pode definir essa mensagem não seja exibido novamente.  
  
##  <a name="settings"></a> As páginas do Assistente de Designer de DSL  
 Você pode deixar vários campos inalterados de seus valores padrão. No entanto, certifique-se de que você defina o campo de extensão de arquivo.  
  
### <a name="solution-settings-page"></a>Página de configurações de solução  
 **Qual modelo você deseja basear sua linguagem específica de domínio?**  
 Escolha um modelo que é semelhante a DSL que você deseja criar. Os modelos diferentes oferecem pontos de partida. Quando você seleciona um modelo de solução, o assistente exibe uma descrição. Para obter mais informações sobre modelos de solução, consulte [escolhendo um modelo de solução de linguagem específica do domínio](../modeling/choosing-a-domain-specific-language-solution-template.md).  
  
 **O que você deseja nomear sua linguagem específica de domínio?**  
 O padrão é o nome da solução. Código é gerado a partir esse valor. Ele deve ser válido como um nome de classe c#.  
  
### <a name="file-extension-page"></a>Página de extensão de arquivo  
 **Use arquivos de modelo do qual extensão deve?**  
 Digite uma nova extensão de arquivo.  
  
 Verifique se que essa extensão de arquivo não já foi registrado para uso neste computador, da seguinte maneira:  
  
 Procure **outras ferramentas e aplicativos registrados para manipular esta extensão**. Se você vir a mensagem **nenhum aplicativo ou os editores do Visual Studio usam esta extensão**, em seguida, você pode usar essa extensão de arquivo.  
  
 Se você vir uma lista de ferramentas ou pacotes, você deve fazer o seguinte:  
  
-   Digite uma extensão de arquivo diferente.  
  
     \- ou -  
  
-   Redefinir o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] instância Experimental. Isso cancelará todas as DSLs que você tiver criado anteriormente. Sobre o **iniciar** menu, clique em **todos os programas**, **SDK do Microsoft Visual Studio 2010**, **ferramentas**e, em seguida, **redefinir o Instância do Microsoft Visual Studio 2010 Experimental**. Você pode recriar a outras DSLs que você deseja usar novamente.  
  
     \- ou -  
  
-   Se um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensão que usa esta extensão de arquivo tiver sido totalmente instalado em seu computador, desinstalá-lo. Sobre o **ferramentas** menu, clique em **Gerenciador de extensões**.  
  
### <a name="product-settings-page"></a>Página de configurações do produto  
 **O que é o nome do produto que a nova linguagem específica de domínio pertence?**  
 O padrão é o nome DSL.  
  
 Esse valor é usado no Windows Explorer (ou Explorador de arquivos) para descrever os arquivos que têm essa extensão de arquivo.  
  
 **O que é o nome da empresa que o produto pertence?**  
 Nome da sua empresa.  
  
 Esse valor é incorporado nas propriedades de AssemblyInfo do seu pacote DSL.  
  
 **O que é o namespace raiz para projetos nesta solução?**  
 Esse padrão é um nome composto de sua empresa e nomes de produto.  
  
### <a name="signing-page"></a>Página Assinatura  
 **Criar um arquivo de chave de nome forte**  
 A opção padrão é criar uma nova chave para assinar seu assembly DSL.  
  
 **Usar a chave de nome forte existente**  
 Use esta opção se você quiser integrar sua DSL com outro assembly.  
  
 Para obter mais informações sobre nomes fortes, consulte [criando e usando Assemblies nomes fortes](http://go.microsoft.com/fwlink/?LinkId=186073).  
  
## <a name="see-also"></a>Consulte também  
 [Como definir uma linguagem específica de domínio](../modeling/how-to-define-a-domain-specific-language.md)   
 [Glossário de ferramentas de linguagem específica do domínio](http://msdn.microsoft.com/en-us/ca5e84cb-a315-465c-be24-76aa3df276aa)



