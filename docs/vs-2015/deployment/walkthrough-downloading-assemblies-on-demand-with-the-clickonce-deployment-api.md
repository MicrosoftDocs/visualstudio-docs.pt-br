---
title: 'Passo a passo: Baixando Assemblies sob demanda com a API de implantação do ClickOnce | Microsoft Docs'
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
- ClickOnce deployment, on-demand download
- on-demand assemblies, ClickOnce
ms.assetid: d20e2789-8621-4806-b5b7-841122da1456
caps.latest.revision: 18
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 6e1f9e1a2115e61e46e0050c1e6504e73c0180fe
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49199128"
---
# <a name="walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api"></a>Instruções passo a passo: baixando assemblies por demanda com a API de implantação do ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Por padrão, todos os assemblies incluídos em um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo são baixadas quando o aplicativo é executado pela primeira vez. No entanto, você pode ter partes de seu aplicativo que são usados por um pequeno conjunto de seus usuários. Nesse caso, você deseja baixar um assembly somente quando você cria um de seus tipos. A instrução a seguir demonstra como marcar determinados assemblies em seu aplicativo como "opcional", e como baixá-los usando as classes no <xref:System.Deployment.Application> namespace quando o common language runtime (CLR) requê-los.  
  
> [!NOTE]
>  Seu aplicativo precisará executar em confiança total para usar este procedimento.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Será necessário um dos seguintes componentes para concluir este passo a passo:  
  
-   O SDK do Windows. O SDK do Windows pode ser baixado do Microsoft Download Center.  
  
-   Visual Studio.  
  
## <a name="creating-the-projects"></a>Criando os Projetos  
  
#### <a name="to-create-a-project-that-uses-an-on-demand-assembly"></a>Para criar um projeto que usa um assembly sob demanda  
  
1.  Crie um diretório chamado ClickOnceOnDemand.  
  
2.  Abra o Prompt de comando do Windows SDK ou o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Prompt de comando.  
  
3.  Altere para o diretório de ClickOnceOnDemand.  
  
4.  Gere um par de chaves pública/privada usando o seguinte comando:  
  
    ```  
    sn -k TestKey.snk  
    ```  
  
5.  Usando o bloco de notas ou outro editor de texto, definir uma classe denominada `DynamicClass` com uma única propriedade chamada `Message`.  
  
     [!code-csharp[ClickOnceLibrary#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnceLibrary/CS/Class1.cs#1)]
     [!code-vb[ClickOnceLibrary#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceLibrary/VB/Class1.vb#1)]  
  
6.  Salve o texto como um arquivo chamado `ClickOnceLibrary.cs` ou `ClickOnceLibrary.vb`, dependendo da linguagem usar, para o diretório ClickOnceOnDemand.  
  
7.  Compile o arquivo em um assembly.  
  
    ```csharp  
    csc /target:library /keyfile:TestKey.snk ClickOnceLibrary.cs  
    ```  
  
    ```vb  
    vbc /target:library /keyfile:TestKey.snk ClickOnceLibrary.vb  
    ```  
  
8.  Para obter a chave pública token para o assembly, use o seguinte comando:  
  
    ```  
    sn -T ClickOnceLibrary.dll  
    ```  
  
9. Criar um novo arquivo usando o texto de editor e insira o código a seguir. Esse código cria um aplicativo de formulários do Windows que baixa o assembly ClickOnceLibrary quando for necessário.  
  
     [!code-csharp[ClickOnceOnDemandCmdLine#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnceOnDemandCmdLine/CS/Form1.cs#1)]
     [!code-vb[ClickOnceOnDemandCmdLine#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceOnDemandCmdLine/VB/Form1.vb#1)]  
  
10. No código, localize a chamada para <xref:System.Reflection.Assembly.LoadFile%2A>.  
  
11. Definir`PublicKeyToken` como o valor que você recuperou anteriormente.  
  
12. Salve o arquivo como `Form1.cs` ou `Form1.vb`.  
  
13. Compilá-lo em um executável usando o comando a seguir.  
  
    ```csharp  
    csc /target:exe /reference:ClickOnceLibrary.dll Form1.cs  
    ```  
  
    ```vb  
    vbc /target:exe /reference:ClickOnceLibrary.dll Form1.vb  
    ```  
  
## <a name="marking-assemblies-as-optional"></a>Marcar Assemblies como opcional  
  
#### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-mageuiexe"></a>Marcar assemblies como opcionais no seu aplicativo ClickOnce usando MageUI.exe  
  
1.  Usando MageUI.exe, crie um manifesto de aplicativo, conforme descrito em [instruções passo a passo: Implantando um aplicativo ClickOnce manualmente](../deployment/walkthrough-manually-deploying-a-clickonce-application.md). Use as seguintes configurações para o manifesto do aplicativo:  
  
    -   Nomeie o manifesto do aplicativo `ClickOnceOnDemand`.  
  
    -   Sobre o **arquivos** página, na linha ClickOnceLibrary.dll, defina o **tipo de arquivo** coluna para **nenhum**.  
  
    -   Sobre o **arquivos** página, na linha ClickOnceLibrary.dll, tipo de `ClickOnceLibrary.dll` no **grupo** coluna.  
  
2.  Usando MageUI.exe, crie um manifesto de implantação, conforme descrito em [instruções passo a passo: Implantando um aplicativo ClickOnce manualmente](../deployment/walkthrough-manually-deploying-a-clickonce-application.md). Use as seguintes configurações para o manifesto de implantação:  
  
    -   Nomeie o manifesto de implantação `ClickOnceOnDemand`.  
  
## <a name="testing-the-new-assembly"></a>Teste o novo Assembly  
  
#### <a name="to-test-your-on-demand-assembly"></a>Para testar seu assembly sob demanda  
  
1.  Carregue seu [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantação em um servidor Web.  
  
2.  Iniciar o aplicativo implantado com [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] em um navegador da Web, inserindo a URL e o manifesto de implantação. Se você chamar sua [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo `ClickOnceOnDemand`e carregá-lo para o diretório raiz da adatum.com, a URL teria esta aparência:  
  
    ```  
    http://www.adatum.com/ClickOnceOnDemand/ClickOnceOnDemand.application  
    ```  
  
3.  Quando o formulário principal é exibida, pressione a <xref:System.Windows.Forms.Button>. Você deve ver uma cadeia de caracteres em uma janela de caixa de mensagem que diz "Olá, mundo!".  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Deployment.Application.ApplicationDeployment>



