---
title: Como publicar um aplicativo WPF com estilos visuais habilitados | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 73b22b02-fc75-42aa-82d3-51fdcaf8e5c8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 21c94cc7ab97070b138cbae108c617094faf09b5
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382205"
---
# <a name="how-to-publish-a-wpf-application-with-visual-styles-enabled"></a>Como publicar um aplicativo WPF com estilos visuais habilitados

Os estilos visuais permitem a aparência de controles comuns a serem alterados com base no tema escolhido pelo usuário. Por padrão, os estilos visuais não são habilitados para aplicativos Windows Presentation Foundation (WPF), portanto, você deve habilitá-los manualmente. No entanto, a habilitação de estilos visuais para um aplicativo WPF e a publicação da solução causa um erro. Este tópico descreve como resolver esse erro e o processo de publicação de um aplicativo WPF com estilos visuais habilitados. Para obter mais informações sobre estilos visuais, consulte [visão geral de estilos visuais](/windows/desktop/Controls/visual-styles-overview). Para obter mais informações sobre a mensagem de erro, consulte [solucionar erros específicos em implantações do ClickOnce](../deployment/troubleshooting-specific-errors-in-clickonce-deployments.md).

 Para resolver o erro e publicar a solução, você deve executar as seguintes tarefas:

- [Publicar a solução sem estilos visuais habilitados](#publish-the-solution-without-visual-styles-enabled).

- [Crie um arquivo de manifesto](#create-a-manifest-file).

- [Insira o arquivo de manifesto no arquivo executável da solução publicada](#embed-the-manifest-file-into-the-executable-file-of-the-published-solution).

- [Assine os manifestos de aplicativo e implantação](#sign-the-application-and-deployment-manifests).

  Em seguida, você pode mover os arquivos publicados para o local do qual deseja que os usuários finais instalem o aplicativo.

## <a name="publish-the-solution-without-visual-styles-enabled"></a>Publicar a solução sem estilos visuais habilitados

1. Verifique se o projeto não tem estilos visuais habilitados. Primeiro, verifique o arquivo de manifesto do seu projeto para o seguinte XML. Em seguida, se o XML estiver presente, coloque o XML com uma marca de comentário.

     Por padrão, os estilos visuais não estão habilitados.

    ```xml
    <dependency>
        <dependentAssembly>
            <assemblyIdentity type="win32" name="Microsoft.Windows.Common-Controls" version="6.0.0.0" processorArchitecture="*" publicKeyToken="6595b64144ccf1df" language="*" />
        </dependentAssembly>
    </dependency>
    ```

     Os procedimentos a seguir mostram como abrir o arquivo de manifesto associado ao seu projeto.

    **Para abrir o arquivo de manifesto em um projeto Visual Basic**

    1. Na barra de menus, escolha **Project**, *ProjectName* **Propriedades**ProjectName, em que *ProjectName* é o nome do seu projeto do WPF.

         As páginas de propriedades do seu projeto WPF são exibidas.

    2. Na guia **aplicativo** , escolha **exibir configurações do Windows**.

         O arquivo app. manifest é aberto no **Editor de código**.

    **Para abrir o arquivo de manifesto em um projeto C#**

    1. Na barra de menus, escolha **Project**, *ProjectName* **Propriedades**ProjectName, em que *ProjectName* é o nome do seu projeto do WPF.

         As páginas de propriedades do seu projeto WPF são exibidas.

    2. Na guia **aplicativo** , anote o nome que aparece no campo manifesto. Este é o nome do manifesto associado ao seu projeto.

        > [!NOTE]
        > Se **Inserir manifesto com configurações padrão** ou **criar aplicativo sem o manifesto** aparecer no campo manifesto, os estilos visuais não serão habilitados. Se o nome de um arquivo de manifesto aparecer no campo manifesto, vá para a próxima etapa neste procedimento.

    3. Em **Gerenciador de soluções**, escolha **Mostrar todos os arquivos**.

         Esse botão mostra todos os itens de projeto, incluindo aqueles que foram excluídos e os que normalmente estão ocultos. O arquivo de manifesto aparece como um item de projeto.

2. Crie e publique sua solução. Para obter mais informações sobre como publicar a solução, consulte [como publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md).

## <a name="create-a-manifest-file"></a>Criar um arquivo de manifesto

1. Cole o XML a seguir em um arquivo do bloco de notas.

     Este XML descreve o assembly que contém controles que dão suporte a estilos visuais.

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <asmv1:assembly manifestVersion="1.0"
        xmlns="urn:schemas-microsoft-com:asm.v1"
        xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"
        xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <dependency>
            <dependentAssembly>
                <assemblyIdentity type="win32" name="Microsoft.Windows.Common-Controls" version="6.0.0.0" processorArchitecture="*" publicKeyToken="6595b64144ccf1df" language="*" />
            </dependentAssembly>
        </dependency>
    </asmv1:assembly>
    ```

2. No Bloco de Notas, clique em **Arquivo** e em **Salvar como.**

3. Na caixa de diálogo **salvar como** , na lista suspensa **salvar como tipo** , selecione **todos os arquivos**.

4. Na caixa **nome do arquivo** , nomeie o arquivo e acrescente *. manifest* ao final do nome do arquivo. Por exemplo: *Themes. manifest*.

5. Escolha o botão **procurar pastas** , selecione qualquer pasta e, em seguida, clique em **salvar**.

    > [!NOTE]
    > Os procedimentos restantes pressupõem que o nome desse arquivo seja *Themes. manifest* e que o arquivo seja salvo no diretório *C:\temp* do seu computador.

## <a name="embed-the-manifest-file-into-the-executable-file-of-the-published-solution"></a>Inserir o arquivo de manifesto no arquivo executável da solução publicada

1. Abra o **prompt de comando do Visual Studio**.

    Para obter mais informações sobre como abrir o **prompt de comando do Visual Studio**, consulte [prompts de comando](/dotnet/framework/tools/developer-command-prompt-for-vs).

   > [!NOTE]
   > As etapas restantes fazem as seguintes suposições sobre sua solução:
   >
   > - O nome da solução é **MyWPFProject**.
   > - A solução está localizada no seguinte diretório: `%UserProfile%\Documents\Visual Studio 2010\Projects\` .
   >
   > - A solução é publicada no seguinte diretório: `%UserProfile%\Documents\Visual Studio 2010\Projects\publish` .
   > - A versão mais recente dos arquivos de aplicativo publicados está localizada no seguinte diretório:`%UserProfile%\Documents\Visual Studio 2010\Projects\publish\Application Files\WPFApp_1_0_0_0`
   >
   > Você não precisa usar o nome ou os locais de diretório descritos acima. O nome e os locais descritos acima são usados apenas para ilustrar as etapas necessárias para publicar sua solução.

2. No prompt de comando, altere o caminho para o diretório que contém a versão mais recente dos arquivos de aplicativo publicados. O exemplo a seguir demonstra essa etapa.

   ```cmd
   cd "%UserProfile%\Documents\Visual Studio 2010\Projects\MyWPFProject\publish\Application Files\WPFApp_1_0_0_0"
   ```

3. No prompt de comando, execute o seguinte comando para inserir o arquivo de manifesto no arquivo executável do aplicativo.

   ```cmd
   mt -manifest c:\temp\themes.manifest -outputresource:MyWPFApp.exe.deploy
   ```

## <a name="sign-the-application-and-deployment-manifests"></a>Assinar os manifestos de aplicativo e implantação

1. No prompt de comando, execute o seguinte comando para remover a extensão *. Deploy* do arquivo executável no diretório atual.

   ```cmd
   ren MyWPFApp.exe.deploy MyWPFApp.exe
   ```

   > [!NOTE]
   > Este exemplo pressupõe que apenas um arquivo tem a extensão de arquivo *. Deploy* . Certifique-se de renomear todos os arquivos neste diretório que têm a extensão de arquivo *. Deploy* .

2. No prompt de comando, execute o comando a seguir para assinar o manifesto do aplicativo.

   ```cmd
   mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx
   ```

   > [!NOTE]
   > Este exemplo pressupõe que você assine o manifesto usando o arquivo *. pfx* do projeto. Se você não estiver assinando o manifesto, poderá omitir o `-cf` parâmetro usado neste exemplo. Se você estiver assinando o manifesto com um certificado que requer uma senha, especifique a `-password` opção ( `For example: mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx - password Password` ).

3. No prompt de comando, execute o seguinte comando para adicionar a extensão *. Deploy* ao nome do arquivo que você renomeou em uma etapa anterior deste procedimento.

   ```
   ren MyWPFApp.exe MyWPFApp.exe.deploy
   ```

   > [!NOTE]
   > Este exemplo pressupõe que apenas um arquivo tinha uma extensão de arquivo *. Deploy* . Certifique-se de renomear todos os arquivos nesse diretório que anteriormente tinham a extensão de nome de arquivo *. Deploy* .

4. No prompt de comando, execute o comando a seguir para assinar o manifesto de implantação.

   ```
   mage -u ..\..\MyWPFApp.application -appm MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx
   ```

   > [!NOTE]
   > Este exemplo pressupõe que você assine o manifesto usando o arquivo *. pfx* do projeto. Se você não estiver assinando o manifesto, poderá omitir o `-cf` parâmetro usado neste exemplo. Se você estiver assinando o manifesto com um certificado que requer uma senha, especifique a `-password` opção, como neste exemplo: `For example: mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx - password Password` .

   Depois de executar essas etapas, você pode mover os arquivos publicados para o local do qual deseja que os usuários finais instalem o aplicativo. Se você pretende atualizar a solução com frequência, pode mover esses comandos para um script e executar o script sempre que publicar uma nova versão.

## <a name="see-also"></a>Veja também

-[Solucionando problemas de erros específicos em implantações do ClickOnce](../deployment/troubleshooting-specific-errors-in-clickonce-deployments.md)
- [Visão geral dos estilos visuais](/windows/desktop/Controls/visual-styles-overview)
- [Habilitar estilos visuais](/windows/desktop/Controls/cookbook-overview)
- [Prompts de comando](/dotnet/framework/tools/developer-command-prompt-for-vs)
