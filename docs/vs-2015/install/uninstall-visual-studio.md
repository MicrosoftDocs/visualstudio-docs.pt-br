---
title: Desinstalar o Visual Studio 2015 | Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-install
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- uninstalling
- uninstalling visual studio
- uninstall
- uninstall Visual Studio
ms.assetid: 0e445255-b796-426d-ad93-a4d8e36da2c5
caps.latest.revision: 9
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.openlocfilehash: 71e1318444c0b03ee5b2b9024c13bfbeb51b5c41
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53050109"
---
# <a name="uninstall-visual-studio"></a>Desinstalar o Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente do Visual Studio 2017, consulte [desinstalar o Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/uninstall-visual-studio).

Essa página guia você pela desinstalação do Visual Studio 2015, uma versão anterior do nosso conjunto integrado de ferramentas de produtividade para desenvolvedores.

##  <a name="uninstalling"></a>
#### <a name="to-uninstall-visual-studio-by-using-the-standard-uninstallation-method"></a>Para desinstalar o Visual Studio usando o método de desinstalação "padrão"

1. No **Painel de Controle**, na página **Programas e Recursos**, escolha a edição do produto que você deseja desinstalar e, em seguida, escolha **Alterar**.

2. No Assistente de instalação, escolha **Desinstalar**, escolha **Sim** e, em seguida, siga as instruções restantes no assistente.

   Esse padrão ou o método padrão deixará alguns itens na primeira instalação do Visual Studio instalados originalmente (por exemplo, o Microsoft .NET Framework, Microsoft Visual C++ Redistributables, Microsoft SQL Server, etc.).   Deixamos eles instalados porque muitos outros aplicativos dependem deles. No entanto, se você quiser removê-los também, selecione a entrada em **programas e recursos**e, em seguida, remova cada um individualmente.

#### <a name="to-uninstall-visual-studio-and-all-other-related-files-that-is-to-uninstall-almost-everything"></a>Para desinstalar o Visual Studio e todos os outros arquivos relacionados (ou seja, para desinstalar quase tudo)

1.  Localize o arquivo de .exe do Visual Studio (por exemplo, localize "vs_enterprise.exe").

    > [!NOTE]
    >  O arquivo deve estar em uma subpasta de "%ProgramData%\Package Cache", por exemplo: Cache de C:\ProgramData\Package\\\vs_enterprise.exe {37e19555-e88d-4aed-9d42-82d0784d2b79}

2.  Execute o arquivo .exe usando a desinstalar /Force parâmetros de linha de comando.

     Por exemplo, executar ```vs_enterprise.exe /uninstall /force```, que removerá o Visual Studio e a maioria dos componentes principais que são deixados para trás em uma desinstalação padrão. No entanto, isso não removerá todo o conteúdo adicional que complementos do Visual Studio e extensões podem instalar (por exemplo, atualizações do Visual Studio e outros componentes opcionais).

    > [!TIP]
    > Como alternativa, você pode usar o "**desinstalador Total**" ferramenta para remover tudo o que o Visual Studio ou podem ter instalado as atualizações do Visual Studio. Ou seja, qualquer versão do Visual Studio 2013 ou posterior. Para obter mais informações, consulte o [ferramenta de desinstalação do Visual Studio](https://github.com/Microsoft/VisualStudioUninstaller/releases) no GitHub.

#### <a name="to-uninstall-visual-studio-in-silent-or-passive-modes-that-is-to-uninstall-from-source"></a>Para desinstalar o Visual Studio nos modos silencioso ou passivo (isto é, desinstalação da origem)

1.  No computador onde o Visual Studio está instalado, abra o prompt de comando do Windows.

2.  Digite os seguintes parâmetros:

     *1&gt;dvdroot&lt;1* \\< arquivo de instalação\> \</quiet&#124;/passive > [/norestart] /Uninstall

#### <a name="to-roll-back-to-a-previous-version-or-release-of--visual-studio"></a>Para reverter para uma versão anterior ou a versão do Visual Studio

1. Desinstale o Visual Studio, usando qualquer um dos métodos listados neste tópico.

   > [!WARNING]
   >  Desinstalando uma versão atual do Visual Studio (ou uma atualização do Visual Studio) e, em seguida, instalar uma versão anterior podem não funcionar conforme o esperado.
   >
   >  O resultado depende de qual versão ou versão do Visual Studio você instalou, quais versões de seus componentes estão instalados, quais produtos estão instalados que podem ter dependências ou a versão do Visual Studio ou seus componentes, e, finalmente, em qual versão anterior do Visual Studio que você planeja instalar ou reinstalar.  Devido a essas variáveis, uma desinstalação padrão será normalmente deixará componentes que podem não funcionar com as versões anteriores do Visual Studio.
   >
   >  Portanto, para obter melhores resultados, é recomendável usar o [ferramenta de desinstalação do Visual Studio](https://github.com/Microsoft/VisualStudioUninstaller/releases).

2. Instale ou reinstale a versão anterior do Visual Studio que você deseja usar.

   Mesmo se você instalar uma versão anterior do Visual Studio, o programa de instalação pode ainda tentar usar uma versão mais recente ou se houver uma disponível. Para obter mais informações, consulte o [como: Instalar uma versão específica do Visual Studio](../install/how-to-install-a-specific-release-of-visual-studio.md) tópico.

## <a name="see-also"></a>Consulte também
 [Instalar o Visual Studio](https://msdn.microsoft.com/library/e2h7fzkw.aspx)