---
title: 'Passo a passo: Baixando Assemblies sob demanda com a implantação do ClickOnce usando o Designer de API | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- assemblies, downloading [ClickOnce]
- Windows applications, ClickOnce deployments
- ClickOnce deployment, on-demand download
- on-demand assemblies, ClickOnce
ms.assetid: 59a0dd5f-1cab-4f2f-b780-0ab7399905d5
caps.latest.revision: 20
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 923951196487c9dc3f08b61879271fc71be373e4
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49245057"
---
# <a name="walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer"></a>Instruções passo a passo: baixando assemblies por demanda com a API de implantação do ClickOnce usando o designer
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Por padrão, todos os assemblies incluídos em um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo são baixadas quando o aplicativo é executado pela primeira vez. No entanto, pode haver partes do seu aplicativo que são usados por um pequeno conjunto de usuários. Nesse caso, você deseja baixar um assembly somente quando você cria um de seus tipos. A instrução a seguir demonstra como marcar determinados assemblies em seu aplicativo como "opcional", e como baixá-los usando as classes no <xref:System.Deployment.Application> namespace quando o common language runtime requê-los.  
  
> [!NOTE]
>  Seu aplicativo precisará executar em confiança total para usar este procedimento.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, clique em **Importar e exportar configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="creating-the-projects"></a>Criando os Projetos  
  
#### <a name="to-create-a-project-that-uses-an-on-demand-assembly-with-visual-studio"></a>Para criar um projeto que usa um assembly sob demanda com o Visual Studio  
  
1.  Criar um novo projeto Windows Forms no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. No menu **Arquivo**, aponte para **Adicionar** e clique em **Novo Projeto**. Escolha uma **biblioteca de classes** na caixa de diálogo do projeto e nomeie-o `ClickOnceLibrary`.  
  
    > [!NOTE]
    >  No Visual Basic, é recomendável que você modifique as propriedades do projeto para alterar o namespace raiz para este projeto para `Microsoft.Samples.ClickOnceOnDemand` ou a um namespace de sua escolha. Para simplificar, os dois projetos neste passo a passo estão no mesmo namespace.  
  
2.  Definir uma classe denominada `DynamicClass` com uma única propriedade chamada `Message`.  
  
     [!code-csharp[ClickOnceLibrary#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnceLibrary/CS/Class1.cs#1)]
     [!code-vb[ClickOnceLibrary#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceLibrary/VB/Class1.vb#1)]  
  
3.  Selecione o projeto de formulários do Windows no **Gerenciador de soluções**. Adicione uma referência para o <xref:System.Deployment.Application> referenciarem de assembly e um projeto para o `ClickOnceLibrary` projeto.  
  
    > [!NOTE]
    >  No Visual Basic, é recomendável que você modifique as propriedades do projeto para alterar o namespace raiz para este projeto para `Microsoft.Samples.ClickOnceOnDemand` ou a um namespace de sua escolha. Para simplificar, os dois projetos neste passo a passo estão localizados no mesmo namespace.  
  
4.  Clique com botão direito do formulário, clique em **Exibir código** no menu e adicione as seguintes referências ao formulário.  
  
     [!code-csharp[ClickOnceOnDemand#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnceOnDemand/CS/Form1.cs#1)]
     [!code-vb[ClickOnceOnDemand#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceOnDemand/VB/Form1.vb#1)]  
  
5.  Adicione o código a seguir para baixar esse assembly sob demanda. Este código mostra como mapear um conjunto de módulos (assemblies) para um nome de grupo usando um genérico <xref:System.Collections.DictionaryBase.Dictionary%2A> classe. Porque estamos apenas estiver baixando um único assembly neste passo a passo, há apenas um assembly em nosso grupo. Um aplicativo real, você provavelmente deseja baixar todos os assemblies relacionados a um único recurso em seu aplicativo ao mesmo tempo. A tabela de mapeamento permite que você faça isso com facilidade por meio da associação todas as DLLs que pertencem a um recurso com um nome de grupo de download.  
  
     [!code-csharp[ClickOnceOnDemand#2](../snippets/csharp/VS_Snippets_Winforms/ClickOnceOnDemand/CS/Form1.cs#2)]
     [!code-vb[ClickOnceOnDemand#2](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceOnDemand/VB/Form1.vb#2)]  
  
6.  Sobre o **modo de exibição** menu, clique em **caixa de ferramentas**. Arraste uma <xref:System.Windows.Forms.Button> do **caixa de ferramentas** para o formulário. Clique duas vezes no botão e adicione o seguinte código para o <xref:System.Windows.Forms.Control.Click> manipulador de eventos.  
  
     [!code-csharp[ClickOnceOnDemand#3](../snippets/csharp/VS_Snippets_Winforms/ClickOnceOnDemand/CS/Form1.cs#3)]
     [!code-vb[ClickOnceOnDemand#3](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceOnDemand/VB/Form1.vb#3)]  
  
## <a name="marking-assemblies-as-optional"></a>Marcar Assemblies como opcional  
  
#### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-visual-studio"></a>Marcar assemblies como opcionais no seu aplicativo ClickOnce usando o Visual Studio  
  
1.  Clique com botão direito no projeto de formulários do Windows no **Gerenciador de soluções** e clique em **propriedades**. Selecione o **publicar** guia.  
  
2.  Clique o **arquivos de aplicativo** botão.  
  
3.  Localize a listagem para ClickOnceLibrary.dll. Definir a **Status da publicação** caixa de lista suspensa **Include**.  
  
4.  Expanda o **grupo** caixa de lista suspensa e selecione **New**. Insira o nome `ClickOnceLibrary` como o novo nome de grupo.  
  
5.  Continuar publicando seu aplicativo, conforme descrito em [como: publicar um aplicativo ClickOnce usando o Assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md).  
  
#### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-manifest-generation-and-editing-tool--graphical-client-mageuiexe"></a>Marcar assemblies como opcionais no seu aplicativo ClickOnce usando o Manifest Generation and Editing Tool, cliente gráfico (MageUI.exe)  
  
1.  Criar seu [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifestos conforme descrito em [passo a passo: Implantando um aplicativo ClickOnce manualmente](../deployment/walkthrough-manually-deploying-a-clickonce-application.md).  
  
2.  Antes de fechar MageUI.exe, selecione a guia que contém o manifesto do aplicativo da implantação e, nessa guia, selecione a **arquivos** guia.  
  
3.  Encontre ClickOnceLibrary.dll na lista de arquivos do aplicativo e defina suas **tipo de arquivo** coluna a ser **None**. Para o **grupo** coluna, digite `ClickOnceLibrary.dll`.  
  
## <a name="testing-the-new-assembly"></a>Teste o novo Assembly  
  
#### <a name="to-test-your-on-demand-assembly"></a>Para testar seu assembly sob demanda  
  
1.  Iniciar o aplicativo implantado com [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)].  
  
2.  Quando o formulário principal é exibida, pressione a <xref:System.Windows.Forms.Button>. Você deve ver uma cadeia de caracteres em uma janela de caixa de mensagem que se lê "Olá, mundo!"  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Deployment.Application.ApplicationDeployment>



