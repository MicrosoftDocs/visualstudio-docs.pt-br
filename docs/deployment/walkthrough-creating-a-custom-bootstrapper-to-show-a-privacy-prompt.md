---
title: Criar um bootstrapper personalizado com um aviso de privacidade
description: Saiba como configurar aplicativos ClickOnce para atualizar automaticamente quando os assemblies com versões de arquivo e versões de assembly mais recentes estiverem disponíveis.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
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
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 96cfbf8693ce23dbc0b0584c7742607224aeab4f
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216937"
---
# <a name="walkthrough-create-a-custom-bootstrapper-with-a-privacy-prompt"></a>Passo a passo: Criar um bootstrapper personalizado com um aviso de privacidade
Você pode configurar aplicativos ClickOnce para atualizar automaticamente quando os assemblies com versões de arquivo mais recentes e versões de assembly ficarem disponíveis. Para garantir que seus clientes consentim nesse comportamento, você pode exibir um aviso de privacidade para eles. Em seguida, eles podem escolher se deseja conceder permissão ao aplicativo para atualizar automaticamente. Se o aplicativo não tiver permissão para ser atualizado automaticamente, ele não será instalado.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- Visual Studio 2010.

## <a name="create-an-update-consent-dialog-box"></a>Criar uma caixa de diálogo de consentimento de atualização
 Para exibir um aviso de privacidade, crie um aplicativo que peça ao leitor para consentir as atualizações automáticas do aplicativo.

#### <a name="to-create-a-consent-dialog-box"></a>Para criar uma caixa de diálogo de consentimento

1. No menu **Arquivo** , aponte para **Novo** e clique em **Projeto**.

2. Na caixa de diálogo **novo projeto** , clique em **Windows** e em **WindowsFormsApplication**.

3. Para o **nome**, digite **ConsentDialog** e clique em **OK**.

4. No designer, clique no formulário.

5. Na janela **Propriedades** , altere a propriedade **texto** para **atualizar a caixa de diálogo de consentimento**.

6. Na **caixa de ferramentas**, expanda **todos os Windows Forms** e arraste um controle **rótulo** para o formulário.

7. No designer, clique no controle rótulo.

8. Na janela **Propriedades** , altere a propriedade **Text** em **aparência** para o seguinte:

    O aplicativo que você está prestes a instalar verifica as atualizações mais recentes na Web. Ao clicar em "concordo", você autoriza o aplicativo a verificar e instalar atualizações automaticamente da Internet.

9. Na **caixa de ferramentas**, arraste um controle de **caixa de seleção** para o meio do formulário.

10. Na janela **Propriedades** , altere a propriedade **Text** em **layout** para **concordo**.

11. Na **caixa de ferramentas**, arraste um controle de **botão** para a parte inferior esquerda do formulário.

12. Na janela **Propriedades** , altere a propriedade **Text** em **layout** para **continuar**.

13. Na janela **Propriedades** , altere a propriedade **(Name)** em **design** para **ProceedButton**.

14. Na **caixa de ferramentas**, arraste um controle de **botão** para a parte inferior direita do formulário.

15. Na janela **Propriedades** , altere a propriedade **Text** em **layout** para **Cancelar**.

16. Na janela **Propriedades** , altere a propriedade **(Name)** em **design** para **CancelButton**.

17. No designer, clique duas vezes na caixa de seleção **concordo** para gerar o manipulador de eventos Checked-Changed.

18. No arquivo de código Form1, adicione o código a seguir para o manipulador de eventos CheckedChanged.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb" id="Snippet1":::

19. Atualize o construtor de classe para desabilitar o botão **continuar** por padrão.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb" id="Snippet6":::

20. No arquivo de código Form1, adicione o código a seguir para uma variável booliana para controlar se o usuário final consentiu em atualizações online.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb" id="Snippet3":::

21. No designer, clique duas vezes no botão **continuar** para gerar o manipulador de eventos de clique.

22. No arquivo de código Form1, adicione o código a seguir ao manipulador de eventos de clique para o botão **continuar** .

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb" id="Snippet2":::


23. No designer, clique duas vezes no botão **Cancelar** para gerar o manipulador de eventos de clique.

24. No arquivo de código Form1, adicione o código a seguir para o manipulador de eventos de clique para o botão **Cancelar** .

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs" id="Snippet4":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb" id="Snippet4":::

25. Atualize o aplicativo para retornar um erro se o usuário final não consentir com atualizações online.

     Somente para desenvolvedores de Visual Basic:

    1. Em **Gerenciador de soluções**, clique em **ConsentDialog**.

    2. No menu **projeto** , clique em **Adicionar módulo** e, em seguida, clique em **Adicionar**.

    3. No arquivo de código *Module1. vb* , adicione o código a seguir.

       :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/module1.vb" id="Snippet7":::

    4. No menu **projeto** , clique em **ConsentDialog Propriedades** e, em seguida, clique na guia **aplicativo** .

    5. Desmarque **habilitar estrutura do aplicativo**.

    6. No menu suspenso **objeto de inicialização** , selecione **Module1**.

       > [!NOTE]
       > Desabilitar a estrutura do aplicativo desabilita recursos como estilos visuais do Windows XP, eventos de aplicativo, tela inicial, aplicativo de instância única e muito mais. Para obter mais informações, consulte [Página de aplicativo, Designer de Projeto (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md).

       Somente para desenvolvedores do Visual C#:

       Abra o arquivo de código *Program. cs* e adicione o código a seguir.

       :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/program.cs" id="Snippet5":::

26. No menu **Compilar** , clique em **BuildSolution**.

## <a name="create-the-custom-bootstrapper-package"></a>Criar o pacote de bootstrapper personalizado
 Para mostrar a solicitação de privacidade aos usuários finais, você pode criar um pacote de bootstrapper personalizado para o aplicativo de caixa de diálogo de consentimento de atualização e incluí-lo como um pré-requisito em todos os seus aplicativos ClickOnce.

 Este procedimento demonstra como criar um pacote de bootstrapper personalizado criando os seguintes documentos:

- Um *product.xml* arquivo de manifesto para descrever o conteúdo do bootstrapper.

- Um *package.xml* arquivo de manifesto para listar os aspectos específicos à localização do seu pacote, como cadeias de caracteres e os termos de licença de software.

- Um documento para os termos de licença de software.

#### <a name="step-1-to-create-the-bootstrapper-directory"></a>Etapa 1: para criar o diretório bootstrapper

1. Crie um diretório chamado **UpdateConsentDialog** no *%ProgramFiles%\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages*.

    > [!NOTE]
    > Talvez você precise de privilégios administrativos para criar essa pasta.

2. No diretório *UpdateConsentDialog* , crie um subdiretório chamado *en*.

    > [!NOTE]
    > Crie um novo diretório para cada localidade. Por exemplo, você pode adicionar subdiretórios para as localidades fr e de. Esses diretórios contêm as cadeias de caracteres e os pacotes de idiomas em francês e alemão, se necessário.

#### <a name="step-2-to-create-the-productxml-manifest-file"></a>Etapa 2: criar o arquivo de manifesto product.xml

1. Crie um arquivo de texto chamado *product.xml*.

2. No arquivo *product.xml* , adicione o código XML a seguir. Certifique-se de não substituir o código XML existente.

    ```xml
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

3. Salve o arquivo no diretório bootstrapper UpdateConsentDialog.

#### <a name="step-3-to-create-the-packagexml-manifest-file-and-the-software-license-terms"></a>Etapa 3: criar o arquivo de manifesto package.xml e os termos de licença de software

1. Crie um arquivo de texto chamado *package.xml*.

2. No arquivo *package.xml* , adicione o seguinte código XML para definir a localidade e incluir os termos de licença de software. Certifique-se de não substituir o código XML existente.

    ```xml
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

3. Salve o arquivo no subdiretório en no diretório bootstrapper UpdateConsentDialog.

4. Crie um documento chamado *EULA. rtf* para os termos de licença de software.

    > [!NOTE]
    > Os termos de licença de software devem incluir informações sobre licenciamento, garantias, passivos e leis locais. Esses arquivos devem ser específicos da localidade, portanto, certifique-se de que o arquivo seja salvo em um formato que dê suporte a caracteres MBCS ou UNICODE. Consulte seu departamento jurídico sobre o conteúdo dos termos de licença de software.

5. Salve o documento no subdiretório en no diretório bootstrapper *UpdateConsentDialog* .

6. Se necessário, crie um novo arquivo de manifesto *package.xml* e um novo documento *EULA. rtf* para os termos de licença de software para cada localidade. Por exemplo, se você criou subdiretórios para as localidades fr e de, Crie arquivos de manifesto de package.xml separados e termos de licença de software e salve-os nos subdiretórios fr e de.

## <a name="set-the-update-consent-application-as-a-prerequisite"></a>Definir o aplicativo de consentimento de atualização como um pré-requisito
 No Visual Studio, você pode definir o aplicativo de consentimento de atualização como um pré-requisito.

#### <a name="to-set-the-update-consent-application-as-a-prerequisite"></a>Para definir o aplicativo de consentimento de atualização como um pré-requisito

1. Em **Gerenciador de soluções**, clique no nome do aplicativo que você deseja implantar.

2. No menu **Projeto**, clique em *ProjectName* **Propriedades**.

3. Clique na página **publicar** e clique em **pré-requisitos**.

4. Selecione a **caixa de diálogo de consentimento de atualização**.

    > [!NOTE]
    > Talvez seja necessário fechar e reabrir o Visual Studio para ver a caixa de diálogo de consentimento de atualização na caixas de diálogo de pré-requisitos.

5. Clique em **OK**.

## <a name="create-and-test-the-setup-program"></a>Criar e testar o programa de instalação
 Depois de definir o aplicativo de consentimento de atualização como um pré-requisito, você pode gerar o instalador e o bootstrapper para seu aplicativo.

#### <a name="to-create-and-test-the-setup-program-by-not-clicking-i-agree"></a>Para criar e testar o programa de instalação, não clicando em Concordo

1. Em **Gerenciador de soluções**, clique no nome do aplicativo que você deseja implantar.

2. No menu **Projeto**, clique em *ProjectName* **Propriedades**.

3. Clique na página **publicar** e, em seguida, clique em **Publicar agora**.

4. Se a saída de publicação não abrir automaticamente, navegue até a saída de publicação.

5. Execute o programa *Setup.exe* .

     O programa de instalação mostra o contrato de licença de software de caixa de diálogo de consentimento de atualização.

6. Leia o contrato de licença de software e clique em **aceitar**.

     O aplicativo de caixa de diálogo de consentimento de atualização aparece e mostra o seguinte texto: o aplicativo que você está prestes a instalar verifica se há atualizações mais recentes na Web. Ao clicar em Concordo, você autoriza o aplicativo a verificar se há atualizações automaticamente na Internet.

7. Feche o aplicativo ou clique em cancelar.

     O aplicativo mostra um erro: ocorreu um erro ao instalar os componentes do sistema para *ApplicationName*. A instalação não pode continuar até que todos os componentes do sistema tenham sido instalados com êxito.

8. Clique em detalhes para mostrar a seguinte mensagem de erro: a caixa de diálogo de consentimento de atualização de componentes falhou ao instalar com a seguinte mensagem de erro: "o contrato de atualização automática não é aceito". Falha ao instalar os seguintes componentes:-caixa de diálogo de consentimento de atualização

9. Clique em **fechar**

#### <a name="to-create-and-test-the-setup-program-by-clicking-i-agree"></a>Para criar e testar o programa de instalação clicando em Concordo

1. Em **Gerenciador de soluções**, clique no nome do aplicativo que você deseja implantar.

2. No menu **Projeto**, clique em *ProjectName* **Propriedades**.

3. Clique na página **publicar** e, em seguida, clique em **Publicar agora**.

4. Se a saída de publicação não abrir automaticamente, navegue até a saída de publicação.

5. Execute o programa *Setup.exe* .

     O programa de instalação mostra o contrato de licença de software de caixa de diálogo de consentimento de atualização.

6. Leia o contrato de licença de software e clique em **aceitar**.

     O aplicativo de caixa de diálogo de consentimento de atualização aparece e mostra o seguinte texto: o aplicativo que você está prestes a instalar verifica se há atualizações mais recentes na Web. Ao clicar em Concordo, você autoriza o aplicativo a verificar se há atualizações automaticamente na Internet.

7. Clique em **concordo** e em **continuar**.

     O aplicativo começa a ser instalado.

8. Se a caixa de diálogo instalação do aplicativo for exibida, clique em **instalar**.

## <a name="see-also"></a>Confira também
- [Pré-requisitos de implantação do aplicativo](../deployment/application-deployment-prerequisites.md)
- [Criar pacotes de bootstrapper](../deployment/creating-bootstrapper-packages.md)
- [Como criar um manifesto de produto](../deployment/how-to-create-a-product-manifest.md)
- [Como criar um manifesto de pacote](../deployment/how-to-create-a-package-manifest.md)
- [Referência de esquema de produto e pacote](../deployment/product-and-package-schema-reference.md)