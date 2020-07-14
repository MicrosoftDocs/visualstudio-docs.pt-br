---
title: Criando uma extensão com um VSPackage | Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
ms.assetid: c0cc5e08-4897-44f2-8309-e3478f1f999e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 68ade2f8d334c1f93349e396d910fa300f6b5417
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903848"
---
# <a name="create-an-extension-with-a-vspackage"></a>Criar uma extensão com um VSPackage

Este tutorial mostra como criar um projeto VSIX e adicionar um item de projeto VSPackage. Usaremos o VSPackage para obter o serviço de Shell da interface do usuário para mostrar uma caixa de mensagem.

## <a name="prerequisites"></a>Pré-requisitos

A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-vspackage"></a>Criar um VSPackage

1. Crie um projeto VSIX chamado **FirstPackage**. Você pode encontrar o modelo de projeto VSIX na caixa de diálogo **novo projeto** pesquisando por "VSIX".

2. Quando o projeto for aberto, adicione um modelo de item de pacote do Visual Studio chamado **FirstPackage**. Na **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar**  >  **novo item**. Na caixa de diálogo **Adicionar novo item** , vá para extensibilidade do **Visual C#**  >  **Extensibility** e selecione **pacote do Visual Studio**. No campo **nome** na parte inferior da janela, altere o nome do arquivo de comando para *FirstPackage.cs*.

3. Compile o projeto e comece a depuração.

    A instância experimental do Visual Studio é exibida. Para obter mais informações sobre a instância experimental, consulte [a instância experimental](../extensibility/the-experimental-instance.md).

4. Na instância experimental, abra a janela **ferramentas**  >  **extensões e atualizações** . Você deve ver a extensão **FirstPackage** aqui. (Se você abrir **extensões e atualizações** em sua instância de trabalho do Visual Studio, não verá **FirstPackage**).

## <a name="load-the-vspackage"></a>Carregar o VSPackage

Neste ponto, a extensão não é carregada porque não há nada que faça com que ela seja carregada. Geralmente, é possível carregar uma extensão quando você interage com sua interface do usuário (clicando em um comando de menu, abrindo uma janela de ferramentas) ou especificando que o VSPackage deve ser carregado em um contexto de interface do usuário específico. Para obter mais informações sobre como carregar VSPackages e contextos de interface do usuário, consulte [carregando VSPackages](../extensibility/loading-vspackages.md). Para este procedimento, mostraremos como carregar um VSPackage quando uma solução estiver aberta.

1. Abra o arquivo *FirstPackage.cs* . Procure a declaração da `FirstPackage` classe. Substitua os atributos existentes pelos seguintes atributos:

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]
    [Guid(FirstPackage.PackageGuidString)]
    public sealed class FirstPackage : Package
    ```

2. Vamos adicionar uma mensagem que nos permite saber que o VSPackage foi carregado. Usamos o `Initialize()` método VSPackage para fazer isso, pois você pode obter os serviços do Visual Studio somente depois que o VSPackage tiver sido site. (Para obter mais informações sobre como obter serviços, consulte [como: obter um serviço](../extensibility/how-to-get-a-service.md).) Substitua o `Initialize()` método de `FirstPackage` pelo código que obtém o <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> serviço, obtenha a <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> interface e chame seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowMessageBox%2A> método.

    ```csharp
    protected override void Initialize()
    {
        base.Initialize();

        IVsUIShell uiShell = (IVsUIShell)GetService(typeof(SVsUIShell));
        Guid clsid = Guid.Empty;
        int result;
        Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(uiShell.ShowMessageBox(
            0,
            ref clsid,
            "FirstPackage",
             string.Format(CultureInfo.CurrentCulture, "Inside {0}.Initialize()", this.GetType().FullName),
            string.Empty,
            0,
            OLEMSGBUTTON.OLEMSGBUTTON_OK,
            OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST,
            OLEMSGICON.OLEMSGICON_INFO,
            0,
            out result));
    }
    ```

3. Compile o projeto e comece a depuração. A instância experimental é exibida.

4. Abra uma solução na instância experimental. Você deverá ver uma caixa de mensagem que diz **primeiro pacote dentro de Initialize ()**.
