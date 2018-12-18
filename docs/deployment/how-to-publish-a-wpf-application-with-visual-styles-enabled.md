---
title: 'Como: publicar um aplicativo WPF com estilos visuais habilitados | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
ms.assetid: 73b22b02-fc75-42aa-82d3-51fdcaf8e5c8
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4dc45c624d44ed550fb491fc57638ba033090346
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52388102"
---
# <a name="how-to-publish-a-wpf-application-with-visual-styles-enabled"></a>Como publicar um aplicativo WPF com estilos visuais habilitados
Estilos visuais permitem a aparência dos controles comuns para mudar com base no tema escolhido pelo usuário. Por padrão, os estilos visuais estiverem habilitados não para aplicativos do Windows Presentation Foundation (WPF), portanto, você deve habilitá-los manualmente. No entanto, habilitar estilos visuais para um aplicativo WPF e, em seguida, publicar a solução causa um erro. Este tópico descreve como resolver esse erro e o processo para publicar um aplicativo WPF com estilos visuais habilitados. Para obter mais informações sobre estilos visuais, consulte [visão geral de estilos visuais](/windows/desktop/Controls/visual-styles-overview). Para obter mais informações sobre a mensagem de erro, consulte [solucionar problemas de erros específicos nas implantações do ClickOnce](../deployment/troubleshooting-specific-errors-in-clickonce-deployments.md).  
  
 Para resolver o erro e publicar a solução, você deve executar as seguintes tarefas:  
  
- [Publicar a solução sem estilos visuais habilitados](#publish-the-solution-without-visual-styles-enabled).  
  
- [Criar um arquivo de manifesto](#create-a-manifest-file).  
  
- [Inserir o arquivo de manifesto no arquivo executável da solução publicado](#embed-the-manifest-file-into-the-executable-file-of-the-published-solution).  
  
- [Assinar os manifestos de aplicativo e implantação](#sign-the-application-and-deployment-manifests).  
  
  Em seguida, você pode mover os arquivos publicados para o local do qual você deseja que os usuários finais instalarem o aplicativo.  
  
##  <a name="publish-the-solution-without-visual-styles-enabled"></a>Publicar a solução sem estilos visuais habilitados  
  
1.  Certifique-se de que seu projeto não tem estilos visuais habilitados. Primeiro, verifique o arquivo de manifesto do projeto para o XML a seguir. Em seguida, se o XML estiver presente, coloque o XML com uma marca de comentário.  
  
     Por padrão, os estilos visuais não estão habilitados.  
  
    ```xml  
    <dependency>
        <dependentAssembly>
            <assemblyIdentity type="win32" name="Microsoft.Windows.Common-Controls" version="6.0.0.0" processorArchitecture="*" publicKeyToken="6595b64144ccf1df" language="*" />
        </dependentAssembly>
    </dependency>
    ```  
  
     Os procedimentos a seguir mostram como abrir o arquivo de manifesto associado ao seu projeto.  
  
    ###### <a name="to-open-the-manifest-file-in-a-visual-basic-project"></a>Para abrir o arquivo de manifesto em um projeto do Visual Basic  
  
    1.  Na barra de menus, escolha **Project**, *ProjectName* **propriedades**, onde *ProjectName* é o nome do seu projeto WPF.  
  
         As páginas de propriedades para o seu projeto WPF são exibidos.  
  
    2.  Sobre o **Application** guia, escolha **exibir configurações do Windows**.  
  
         O arquivo App. manifest é aberto na **Editor de códigos**.  
  
    ###### <a name="to-open-the-manifest-file-in-a-c-project"></a>Para abrir o arquivo de manifesto em um projeto c#  
  
    1.  Na barra de menus, escolha **Project**, *ProjectName* **propriedades**, onde *ProjectName* é o nome do seu projeto WPF.  
  
         As páginas de propriedades para o seu projeto WPF são exibidos.  
  
    2.  Sobre o **aplicativo** guia, anote o nome que aparece no campo de manifesto. Esse é o nome do manifesto que está associado com seu projeto.  
  
        > [!NOTE]
        >  Se **Inserir manifesto com configurações padrão** ou **criar aplicativo sem um manifesto** aparecem no campo de manifesto, os estilos visuais não estão habilitados. Se o nome de um arquivo de manifesto é exibido no campo de manifesto, vá para a próxima etapa neste procedimento.  
  
    3.  Na **Gerenciador de soluções**, escolha **Mostrar todos os arquivos**.  
  
         Esse botão mostra todos os itens de projeto, incluindo aqueles que foram excluídos e aqueles que normalmente estão ocultas. O arquivo de manifesto é exibido como um item de projeto.  
  
2.  Criar e publicar sua solução. Para obter mais informações sobre como publicar a solução, consulte [como: publicar um aplicativo ClickOnce usando o Assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md).  
  
## <a name="create-a-manifest-file"></a>Criar um arquivo de manifesto  
  
1.  Cole o seguinte XML em um arquivo do bloco de notas.  
  
     Esse XML descreve o assembly que contém controles que dão suporte a estilos visuais.  
  
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
  
2.  No bloco de notas, clique em **arquivo**e, em seguida, clique em **Salvar como**.  
  
3.  No **Salvar como** na caixa de **Salvar como tipo** lista suspensa, selecione **todos os arquivos**.  
  
4.  No **nome do arquivo** caixa, nomeie o arquivo e acrescentar *. manifest* até o final do nome do arquivo. Por exemplo: *themes.manifest*.  
  
5.  Escolha o **procurar nas pastas** botão, selecione qualquer pasta e, em seguida, clique em **salvar**.  
  
    > [!NOTE]
    >  Os procedimentos restantes supõem que o nome desse arquivo está *themes.manifest* e que o arquivo é salvo para o *C:\temp* diretório em seu computador.  
  
## <a name="embed-the-manifest-file-into-the-executable-file-of-the-published-solution"></a>Inserir o arquivo de manifesto no arquivo executável da solução publicada  
  
1. Abra o **Prompt de comando do Visual Studio**.  
  
    Para obter mais informações sobre como abrir o **Prompt de comando do Visual Studio**, consulte [prompts de comando](/dotnet/framework/tools/developer-command-prompt-for-vs).  
  
   > [!NOTE]
   >  As etapas restantes fazem as seguintes suposições sobre sua solução:  
   > 
   > - É o nome da solução **MyWPFProject**.  
   >   -   A solução está localizada no seguinte diretório: `%UserProfile%\Documents\Visual Studio 2010\Projects\`.  
   > 
   >   A solução é publicada no seguinte diretório: `%UserProfile%\Documents\Visual Studio 2010\Projects\publish`.  
   >   -   A versão mais recente dos arquivos do aplicativo publicado está localizada no seguinte diretório: `%UserProfile%\Documents\Visual Studio 2010\Projects\publish\Application Files\WPFApp_1_0_0_0`  
   > 
   >   Não é preciso usar o nome ou os locais de diretório descritos acima. O nome e localizações descritas acima são usadas apenas para ilustrar as etapas necessárias para publicar sua solução.  
  
2. No prompt de comando, altere o caminho para o diretório que contém a versão mais recente dos arquivos do aplicativo publicado. O exemplo a seguir demonstra essa etapa.  
  
   ```cmd  
   cd "%UserProfile%\Documents\Visual Studio 2010\Projects\MyWPFProject\publish\Application Files\WPFApp_1_0_0_0"  
   ```  
  
3. No prompt de comando, execute o seguinte comando para inserir o arquivo de manifesto no arquivo executável do aplicativo.  
  
   ```cmd
   mt -manifest c:\temp\themes.manifest -outputresource:MyWPFApp.exe.deploy  
   ```  
  
## <a name="sign-the-application-and-deployment-manifests"></a>Assinar os manifestos de aplicativo e implantação  
  
1. No prompt de comando, execute o seguinte comando para remover o *Deploy* extensão do arquivo executável no diretório atual.  
  
   ```cmd  
   ren MyWPFApp.exe.deploy MyWPFApp.exe  
   ```  
  
   > [!NOTE]
   >  Este exemplo presume que apenas um arquivo tem o *Deploy* extensão de arquivo. Certifique-se de que você renomeie todos os arquivos nesse diretório com o *Deploy* extensão de arquivo.  
  
2. No prompt de comando, execute o seguinte comando para assinar o manifesto do aplicativo.  
  
   ```cmd  
   mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx  
   ```  
  
   > [!NOTE]
   >  Este exemplo supõe que você assina o manifesto usando o *. pfx* arquivo do projeto. Se você não estiver se conectando o manifesto, você pode omitir o `-cf` parâmetro que é usado neste exemplo. Se você está assinando o manifesto com um certificado que exige uma senha, especifique o `-password` opção (`For example: mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx - password Password`).  
  
3. No prompt de comando, execute o seguinte comando para adicionar o *Deploy* extensão para o nome do arquivo que você renomeou na etapa anterior deste procedimento.  
  
   ```  
   ren MyWPFApp.exe MyWPFApp.exe.deploy  
   ```  
  
   > [!NOTE]
   >  Este exemplo presume que apenas um arquivo tivesse uma *Deploy* extensão de arquivo. Certifique-se de que você renomeie todos os arquivos neste diretório que anteriormente tinha o *Deploy* extensão de nome de arquivo.  
  
4. No prompt de comando, execute o seguinte comando para assinar o manifesto de implantação.  
  
   ```  
   mage -u ..\..\MyWPFApp.application -appm MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx  
   ```  
  
   > [!NOTE]
   >  Este exemplo supõe que você assina o manifesto usando o *. pfx* arquivo do projeto. Se você não estiver se conectando o manifesto, você pode omitir o `-cf` parâmetro que é usado neste exemplo. Se você está assinando o manifesto com um certificado que exige uma senha, especifique o `-password` opção, como neste exemplo:`For example: mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx - password Password`.  
  
   Depois de realizar essas etapas, você pode mover os arquivos publicados para o local do qual você deseja que os usuários finais instalarem o aplicativo. Se você pretende atualizar a solução muitas vezes, você pode mover esses comandos em um script e execute o script a cada vez que você publica uma nova versão.  
  
## <a name="see-also"></a>Consulte também

-[Solução de problemas com erros específicos nas implantações do ClickOnce](../deployment/troubleshooting-specific-errors-in-clickonce-deployments.md)
- [Visão geral de estilos visuais](/windows/desktop/Controls/visual-styles-overview)
- [Habilitando Estilos Visuais](/windows/desktop/Controls/cookbook-overview)
- [Prompts de Comando](/dotnet/framework/tools/developer-command-prompt-for-vs)
