---
title: 'Passo a passo: Baixando Assemblies sob demanda com a API de implantação do ClickOnce | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- assemblies, downloading [ClickOnce]
- ClickOnce deployment, on-demand download
- on-demand assemblies, ClickOnce
ms.assetid: d20e2789-8621-4806-b5b7-841122da1456
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d6338044dff5aa5b0555b15b689c04ddd406c50f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49887651"
---
# <a name="walkthrough-download-assemblies-on-demand-with-the-clickonce-deployment-api"></a>Passo a passo: Fazer o Download de assemblies por demanda com a API de implantação do ClickOnce
Por padrão, todos os assemblies incluídos em um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo são baixadas quando o aplicativo é executado pela primeira vez. No entanto, você pode ter partes de seu aplicativo que são usados por um pequeno conjunto de seus usuários. Nesse caso, você deseja baixar um assembly somente quando você cria um de seus tipos. A instrução a seguir demonstra como marcar determinados assemblies em seu aplicativo como "opcional", e como baixá-los usando as classes no <xref:System.Deployment.Application> namespace quando o common language runtime (CLR) requê-los.  
  
> [!NOTE]
>  Seu aplicativo precisará executar em confiança total para usar este procedimento.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Será necessário um dos seguintes componentes para concluir este passo a passo:  
  
-   O SDK do Windows. O SDK do Windows pode ser baixado do Microsoft Download Center.  
  
-   Visual Studio.  
  
## <a name="create-the-projects"></a>Crie os projetos  
  
#### <a name="to-create-a-project-that-uses-an-on-demand-assembly"></a>Para criar um projeto que usa um assembly sob demanda  
  
1. Crie um diretório chamado ClickOnceOnDemand.  
  
2. Abra o Prompt de comando do Windows SDK ou o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] Prompt de comando.  
  
3. Altere para o diretório de ClickOnceOnDemand.  
  
4. Gere um par de chaves pública/privada usando o seguinte comando:  
  
   ```cmd  
   sn -k TestKey.snk  
   ```  
  
5. Usando o bloco de notas ou outro editor de texto, definir uma classe denominada `DynamicClass` com uma única propriedade chamada `Message`.  
  
    [!code-vb[ClickOnceLibrary#1](../deployment/codesnippet/VisualBasic/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api_1.vb)]
    [!code-csharp[ClickOnceLibrary#1](../deployment/codesnippet/CSharp/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api_1.cs)]  
  
6. Salve o texto como um arquivo chamado *ClickOnceLibrary.cs* ou *ClickOnceLibrary.vb*, dependendo da linguagem que você usa, como o *ClickOnceOnDemand* directory.  
  
7. Compile o arquivo em um assembly.  
  
   ```csharp  
   csc /target:library /keyfile:TestKey.snk ClickOnceLibrary.cs  
   ```  
  
   ```vb  
   vbc /target:library /keyfile:TestKey.snk ClickOnceLibrary.vb  
   ```  
  
8. Para obter a chave pública token para o assembly, use o seguinte comando:  
  
   ```cmd  
   sn -T ClickOnceLibrary.dll  
   ```  
  
9. Criar um novo arquivo usando o texto de editor e insira o código a seguir. Esse código cria um aplicativo de formulários do Windows que baixa o assembly ClickOnceLibrary quando for necessário.  
  
     [!code-csharp[ClickOnceOnDemandCmdLine#1](../deployment/codesnippet/CSharp/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api_2.cs)]
     [!code-vb[ClickOnceOnDemandCmdLine#1](../deployment/codesnippet/VisualBasic/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api_2.vb)]  
  
10. No código, localize a chamada para <xref:System.Reflection.Assembly.LoadFile%2A>.  
  
11. Definir`PublicKeyToken` como o valor que você recuperou anteriormente.  
  
12. Salve o arquivo como *Form1.cs* ou *Form1.vb*.  
  
13. Compilá-lo em um executável usando o comando a seguir.  
  
    ```csharp  
    csc /target:exe /reference:ClickOnceLibrary.dll Form1.cs  
    ```  
  
    ```vb  
    vbc /target:exe /reference:ClickOnceLibrary.dll Form1.vb  
    ```  
  
## <a name="mark-assemblies-as-optional"></a>Marcar assemblies como opcional  
  
#### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-mageuiexe"></a>Marcar assemblies como opcionais no seu aplicativo ClickOnce usando MageUI.exe  
  
1.  Usando o *MageUI.exe*, crie um manifesto de aplicativo, conforme descrito em [passo a passo: implantar manualmente um aplicativo ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md). Use as seguintes configurações para o manifesto do aplicativo:  
  
    -   Nomeie o manifesto do aplicativo `ClickOnceOnDemand`.  
  
    -   No **arquivos** página, o *ClickOnceLibrary.dll* de linha, defina a **tipo de arquivo** coluna a ser **nenhum**.  
  
    -   No **arquivos** página, o *ClickOnceLibrary.dll* linha, digite `ClickOnceLibrary.dll` no **grupo** coluna.  
  
2.  Usando o *MageUI.exe*, crie um manifesto de implantação, conforme descrito em [passo a passo: implantar manualmente um aplicativo ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md). Use as seguintes configurações para o manifesto de implantação:  
  
    -   Nomeie o manifesto de implantação `ClickOnceOnDemand`.  
  
## <a name="testing-the-new-assembly"></a>Teste o novo assembly  
  
#### <a name="to-test-your-on-demand-assembly"></a>Para testar seu assembly sob demanda  
  
1. Carregue seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação em um servidor Web.  
  
2. Iniciar o aplicativo implantado com [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] em um navegador da Web, inserindo a URL e o manifesto de implantação. Se você chamar sua [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo `ClickOnceOnDemand`e carregá-lo para o diretório raiz da adatum.com, a URL teria esta aparência:  
  
   ```  
   http://www.adatum.com/ClickOnceOnDemand/ClickOnceOnDemand.application  
   ```  
  
3. Quando o formulário principal é exibida, pressione a <xref:System.Windows.Forms.Button>. Você deve ver uma cadeia de caracteres em uma janela de caixa de mensagem que diz "Olá, mundo!".  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Deployment.Application.ApplicationDeployment>