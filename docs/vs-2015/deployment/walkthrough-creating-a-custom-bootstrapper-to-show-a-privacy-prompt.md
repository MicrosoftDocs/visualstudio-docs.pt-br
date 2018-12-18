---
title: 'Passo a passo: Criando um Bootstrapper personalizado para mostrar uma privacidade Prompt | Microsoft Docs'
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
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, prerequisites
- dependencies [.NET Framework], custom bootstrapper package
- deploying applications [Visual Studio], custom prerequisites
- Windows Installer deployment, prerequisites
- prerequisites [.NET Framework], custom bootstrapper package
ms.assetid: 2f3edd6a-84d1-4864-a1ae-6a13c5732aae
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: e8bd1101647973a7a8f206159f8910a4e633e5da
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49893384"
---
# <a name="walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt"></a>Instruções passo a passo: criando um bootstrapper personalizado para mostrar um prompt de privacidade
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode configurar os aplicativos ClickOnce para atualizar automaticamente quando assemblies com versões do assembly e versões mais recentes do arquivo se tornam disponíveis. Para certificar-se de que seus clientes de consentimento para esse comportamento, você pode exibir um prompt de privacidade para eles. Então, eles podem escolher se deseja conceder permissão ao aplicativo para atualizar automaticamente. Se o aplicativo não tem permissão para atualizar automaticamente, ele não é instalado.  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   Visual Studio 2010.  
  
## <a name="creating-an-update-consent-dialog-box"></a>Criando uma caixa de diálogo de consentimento de atualização  
 Para exibir um prompt de privacidade, crie um aplicativo que solicita que o leitor a consentir com as atualizações automáticas para o aplicativo.  
  
#### <a name="to-create-a-consent-dialog-box"></a>Para criar uma caixa de diálogo de consentimento  
  
1. No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.  
  
2. No **novo projeto** caixa de diálogo, clique em **Windows**e, em seguida, clique em **WindowsFormsApplication**.  
  
3. Para o **nome**, digite **ConsentDialog**e, em seguida, clique em **Okey**.  
  
4. No designer, clique no formulário.  
  
5. No **propriedades** janela, altere o **texto** propriedade a ser **caixa de diálogo de consentimento atualização**.  
  
6. No **caixa de ferramentas**, expanda **todos os Windows Forms**e arraste uma **rótulo** controle ao formulário.  
  
7. No designer, clique no controle de rótulo.  
  
8. No **propriedades** janela, altere o **texto** propriedade sob **aparência** ao seguinte:  
  
    Verifica se o aplicativo que você está prestes a instalar as atualizações mais recentes na Web. Clicando em "Concordo", você deve autorizar o aplicativo para verificar e instalar atualizações automaticamente da Internet.  
  
9. No **caixa de ferramentas**, arraste um **caixa de seleção** controle para o meio do formulário.  
  
10. No **propriedades** janela, altere o **texto** propriedade sob **Layout** para **concordo**.  
  
11. No **caixa de ferramentas**, arraste um **botão** controle para o canto inferior esquerdo do formulário.  
  
12. No **propriedades** janela, altere o **texto** propriedade sob **Layout** para **continuar**.  
  
13. No **propriedades** janela, altere o **(nome)** propriedade sob **Design** para **ProceedButton**.  
  
14. No **caixa de ferramentas**, arraste um **botão** controle na parte inferior direita do formulário.  
  
15. No **propriedades** janela, altere o **texto** propriedade sob **Layout** para **Cancelar**.  
  
16. No **propriedades** janela, altere o **(nome)** propriedade sob **Design** para **CancelButton**.  
  
17. No designer, clique duas vezes o **concordo** caixa de seleção para gerar o manipulador de eventos CheckedChanged.  
  
18. No arquivo de código Form1, adicione o seguinte código para o manipulador de eventos CheckedChanged.  
  
     [!code-csharp[ConsentDialog#1](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs#1)]
     [!code-vb[ConsentDialog#1](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb#1)]  
  
19. Atualizar o construtor de classe para desabilitar o **prosseguir** botão por padrão.  
  
     [!code-csharp[ConsentDialog#6](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs#6)]
     [!code-vb[ConsentDialog#6](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb#6)]  
  
20. No arquivo de código Form1, adicione o seguinte código para uma variável booliana controlar se o usuário final tiver consentido atualizações online.  
  
     [!code-csharp[ConsentDialog#3](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs#3)]
     [!code-vb[ConsentDialog#3](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb#3)]  
  
21. No designer, clique duas vezes o **prosseguir** botão para gerar o manipulador de eventos de clique.  
  
22. No arquivo de código Form1, adicione o seguinte código para o manipulador de eventos para o **prosseguir** botão.  
  
     [!code-csharp[ConsentDialog#2](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs#2)]
     [!code-vb[ConsentDialog#2](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb#2)]  
  
23. No designer, clique duas vezes o **Cancelar** botão para gerar o manipulador de eventos de clique.  
  
24. No arquivo de código Form1, adicione o seguinte código para o manipulador de eventos para o **Cancelar** botão.  
  
     [!code-csharp[ConsentDialog#4](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs#4)]
     [!code-vb[ConsentDialog#4](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb#4)]  
  
25. Atualize o aplicativo para retornar um erro se o usuário final não consentiu a atualizações online.  
  
     Para desenvolvedores de Visual Basic somente:  
  
    1. Na **Gerenciador de soluções**, clique em **ConsentDialog**.  
  
    2. Sobre o **Project** menu, clique em **Adicionar módulo**e, em seguida, clique em **adicionar**.  
  
    3. No arquivo de código Module1.vb, adicione o código a seguir.  
  
        [!code-vb[ConsentDialog#7](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/module1.vb#7)]  
  
    4. Sobre o **projeto** menu, clique em **propriedades ConsentDialog**e, em seguida, clique no **aplicativo** guia.  
  
    5. Desmarque a opção **habilitar estrutura de aplicativo**.  
  
    6. No **objeto de inicialização** menu suspenso, selecione **Module1**.  
  
       > [!NOTE]
       >  Desabilitar a estrutura de aplicativo desabilita recursos, como estilos visuais do Windows XP, os eventos de aplicativo, tela inicial, aplicativo de instância única e muito mais. Para obter mais informações, consulte [Página de aplicativo, Designer de Projeto (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md).  
  
       Visual c# somente para desenvolvedores:  
  
       Abra o arquivo de código de Program.cs e adicione o seguinte código.  
  
       [!code-csharp[ConsentDialog#5](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/program.cs#5)]  
  
26. Sobre o **construir** menu, clique em **BuildSolution**.  
  
## <a name="creating-the-custom-bootstrapper-package"></a>Criando o pacote de Bootstrapper personalizado  
 Para mostrar o prompt de privacidade aos usuários finais, você pode criar um pacote de bootstrapper personalizado para o aplicativo de caixa de diálogo de consentimento atualização e incluí-lo como um pré-requisito em todos os aplicativos ClickOnce.  
  
 Este procedimento demonstra como criar um pacote de bootstrapper personalizado, criando os documentos a seguir:  
  
-   Arquivo para descrever o conteúdo do bootstrapper de manifesto de um Product.  
  
-   Um arquivo de manifesto Package. XML para listar os aspectos específicos de localização do seu pacote, como cadeias de caracteres e os termos de licença de software.  
  
-   Um documento para os termos de licença de software.  
  
#### <a name="step-1-to-create-the-bootstrapper-directory"></a>Etapa 1: Criar o diretório de bootstrapper  
  
1.  Crie um diretório chamado **UpdateConsentDialog** em %PROGRAMFILES%\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages.  
  
    > [!NOTE]
    >  Você pode precisar de privilégios administrativos para criar essa pasta.  
  
2.  No diretório UpdateConsentDialog, crie um subdiretório chamado en.  
  
    > [!NOTE]
    >  Crie um novo diretório para cada localidade. Por exemplo, você pode adicionar subdiretórios para as localidades fr e Alemanha. Esses diretórios conteria o francês e alemão cadeias de caracteres e os pacotes de idiomas, se necessário.  
  
#### <a name="step-2-to-create-the-productxml-manifest-file"></a>Etapa 2: Criar o arquivo de manifesto Product  
  
1.  Crie um arquivo de texto chamado `product.xml`.  
  
2.  No arquivo de Product, adicione o seguinte código XML. Certifique-se de que você não substitua o código XML existente.  
  
    ```  
    <Product  
      xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"  
      ProductCode="Microsoft.Sample.EULA">  
      <!-- Defines the list of files to be copied on build. -->  
      <PackageFiles CopyAllPackageFiles="false">  
        <PackageFile Name="ConsentDialog.exe"/>  
      </PackageFiles>  
  
      <!-- Defines how to run the Setup package.-->  
      <Commands >  
        <Command PackageFile = "ConsentDialog.exe" Arguments=''>  
          <ExitCodes>  
            <ExitCode Value="0" Result="Success" />  
            <ExitCode Value="-1" Result="Fail" String="AU_Unaccepted" />  
            <DefaultExitCode Result="Fail"   
              FormatMessageFromSystem="true" String="GeneralFailure" />  
          </ExitCodes>  
        </Command>  
      </Commands>  
  
    </Product>  
    ```  
  
3.  Salve o arquivo para o diretório de bootstrapper UpdateConsentDialog.  
  
#### <a name="step-3-to-create-the-packagexml-manifest-file-and-the-software-license-terms"></a>Etapa 3: Criar o manifesto Package. XML de arquivos e o software de termos de licença  
  
1.  Crie um arquivo de texto chamado `package.xml`.  
  
2.  No arquivo Package. XML, adicione o seguinte código XML para definir a localidade e incluem os termos de licença de software. Certifique-se de que você não substitua o código XML existente.  
  
    ```  
    <Package   
      xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"  
      Name="DisplayName"  
      Culture="Culture"  
      LicenseAgreement="eula.rtf">  
      <PackageFiles>  
        <PackageFile Name="eula.rtf"/>  
      </PackageFiles>  
  
      <!-- Defines a localizable string table for error messages. -->  
      <Strings>  
        <String Name="DisplayName">Update Consent Dialog</String>  
        <String Name="Culture">en</String>  
        <String Name="AU_Unaccepted">The automatic update agreement is not accepted.</String>  
        <String Name="GeneralFailure">A failure occurred attempting to launch the setup.</String>  
      </Strings>  
    </Package>  
    ```  
  
3.  Salve o arquivo para o subdiretório en no diretório UpdateConsentDialog bootstrapper.  
  
4.  Crie um documento chamado EULA. RTF para os termos de licença de software.  
  
    > [!NOTE]
    >  Os termos de licença de software devem incluir informações sobre licenciamento, garantias, responsabilidades e as leis locais. Esses arquivos devem ser específicos da localidade, portanto certifique-se de que o arquivo é salvo em um formato que oferece suporte a caracteres MBCS ou UNICODE. Consulte o departamento jurídico sobre o conteúdo dos termos de licença de software.  
  
5.  Salve o documento para o subdiretório en no diretório UpdateConsentDialog bootstrapper.  
  
6.  Se necessário, crie um novo arquivo de manifesto Package. XML e um novo documento de EULA. RTF para os termos de licença de software para cada localidade. Por exemplo, se você criou subdiretórios para as localidades fr e de, criar arquivos de manifesto Package. XML separado e os termos de licença de software e salvá-los para os subdiretórios fr e de.  
  
## <a name="setting-the-update-consent-application-as-a-prerequisite"></a>Configurando o aplicativo de consentimento de atualização como um pré-requisito  
 No Visual Studio, você pode definir o aplicativo de atualização de consentimento como um pré-requisito.  
  
#### <a name="to-set-the-update-consent-application-as-a-prerequisite"></a>Para definir o aplicativo de atualização de consentimento como um pré-requisito  
  
1.  Na **Gerenciador de soluções**, clique no nome do aplicativo que você deseja implantar.  
  
2.  Sobre o **Project** menu, clique em *ProjectName* **propriedades**.  
  
3.  Clique o **Publish** página e, em seguida, clique em **pré-requisitos**.  
  
4.  Selecione **atualizar caixa de diálogo de consentimento**.  
  
    > [!NOTE]
    >  Talvez você precise fechar e reabrir o Visual Studio para ver o diálogo de consentimento de atualização na caixa de diálogo pré-requisitos.  
  
5.  Clique em **OK**.  
  
## <a name="creating-and-testing-the-setup-program"></a>Criar e testar o programa de instalação  
 Depois de definir o aplicativo de atualização de consentimento como um pré-requisito, você pode gerar o instalador e o bootstrapper para seu aplicativo.  
  
#### <a name="to-create-and-test-the-setup-program-by-not-clicking-i-agree"></a>Para criar e testar o programa de instalação clicando não concordo  
  
1.  Na **Gerenciador de soluções**, clique no nome do aplicativo que você deseja implantar.  
  
2.  Sobre o **Project** menu, clique em *ProjectName* **propriedades**.  
  
3.  Clique o **Publish** página e, em seguida, clique em **publicar agora**.  
  
4.  Se a saída da publicação não abrir automaticamente, navegue até a saída da publicação.  
  
5.  Execute o programa Setup.exe.  
  
     O programa de instalação mostra o contrato de licença de software do diálogo de consentimento de atualização.  
  
6.  Leia o contrato de licença de software e, em seguida, clique em **Accept**.  
  
     O aplicativo de diálogo de consentimento de atualização é exibida e mostra o seguinte texto: verifica se o aplicativo que você está prestes a instalar as atualizações mais recentes na Web. Ao clicar em concordo, você deve autorizar o aplicativo para verificar se há atualizações automaticamente na Internet.  
  
7.  Feche o aplicativo ou clique em Cancelar.  
  
     O aplicativo mostra um erro: Ocorreu um erro durante a instalação de componentes do sistema do *ApplicationName*. A instalação não pode continuar até que todos os componentes do sistema foi instalados com êxito.  
  
8.  Clique em detalhes para exibir a seguinte mensagem de erro: componente atualizar diálogo de consentimento não foi instalado com a seguinte mensagem de erro: "o contrato de atualização automática não é aceito". Os seguintes componentes não conseguiu instalar:-atualização de caixa de diálogo de consentimento  
  
9. Clique em **Fechar**.  
  
#### <a name="to-create-and-test-the-setup-program-by-clicking-i-agree"></a>Para criar e testar o programa de instalação ao clicar em concordo  
  
1.  Na **Gerenciador de soluções**, clique no nome do aplicativo que você deseja implantar.  
  
2.  Sobre o **Project** menu, clique em *ProjectName* **propriedades**.  
  
3.  Clique o **Publish** página e, em seguida, clique em **publicar agora**.  
  
4.  Se a saída da publicação não abrir automaticamente, navegue até a saída da publicação.  
  
5.  Execute o programa Setup.exe.  
  
     O programa de instalação mostra o contrato de licença de software do diálogo de consentimento de atualização.  
  
6.  Leia o contrato de licença de software e, em seguida, clique em **Accept**.  
  
     O aplicativo de diálogo de consentimento de atualização é exibida e mostra o seguinte texto: verifica se o aplicativo que você está prestes a instalar as atualizações mais recentes na Web. Ao clicar em concordo, você deve autorizar o aplicativo para verificar se há atualizações automaticamente na Internet.  
  
7.  Clique em **concordo**e, em seguida, clique em **continuar**.  
  
     O aplicativo é iniciado instalar.  
  
8.  Se a caixa de diálogo de instalação do aplicativo for exibida, clique em **instalar**.  
  
## <a name="see-also"></a>Consulte também  
 [Pré-requisitos de implantação do aplicativo](../deployment/application-deployment-prerequisites.md)   
 [Criando pacotes de bootstrapper](../deployment/creating-bootstrapper-packages.md)   
 [Como: criar um manifesto de produto](../deployment/how-to-create-a-product-manifest.md)   
 [Como: criar um manifesto de pacote](../deployment/how-to-create-a-package-manifest.md)   
 [Referência de esquema de produto e pacote](../deployment/product-and-package-schema-reference.md)



