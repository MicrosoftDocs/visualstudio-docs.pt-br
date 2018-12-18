---
title: Microsoft Language Interface Packs (LIPs) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-install
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- text [Visual Studio], multiple languages
- Multilingual User Interface [Visual Studio]
- language switching [Visual Studio]
- MUI [Visual Studio]
- multiple language support [Visual Studio SDK]
- Windows Multilingual User Interface
- UI text language [Visual Studio]
- languages, multiple language support
ms.assetid: dc86304b-65b7-47e6-9314-1dfd02ecfa65
caps.latest.revision: 28
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.openlocfilehash: 647935dce06d74b29271af130686a10fb8cfc1e9
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53065032"
---
# <a name="microsoft-language-interface-packs-lips-and-visual-studio"></a>Microsoft Language Interface Packs (LIPs) e Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Usando um Windows Language Interface Pack (LIP), você pode instalar uma versão de idioma do windows e então instalar diversos Pacotes de Idiomas da Interface do Usuário. Pacotes de idiomas da interface do usuário oferecem uma interface do usuário localizada (IU) do sistema operacional. Por exemplo, você pode instalar um Language Interface Pack em japonês sobre uma versão do Windows em inglês e então alternar o idioma da interface de usuário do Windows entre japonês e inglês. Usando os LIPs, você pode ter várias versões de idioma do Windows em um computador.

 Em computadores com os LIPs e versões de vários idiomas do Visual Studio instaladas, a alteração da configuração do idioma para exibição do Windows define o Windows e o Visual Studio quando pacotes de idiomas correspondentes são instalados.

## <a name="limitations-of-multi-language-installations"></a>Limitações de instalações multilíngues
 Quando você instala as versões de idioma diferente do Visual Studio no mesmo computador, você só poderá alternar idiomas entre edições correspondentes. Por exemplo, se você tiver uma Express Edition instalada em inglês, uma Express Edition instalada em alemão e uma Professional Edition instalada, só poderá alternar idiomas para as Express Editions, e não para a Professional Edition.

 O Visual Studio usa um pacote de idiomas unificado. Para instalar mais de uma versão de idioma desses produtos, você deve instalar um produto com todos os idiomas primeiro e então instalar um ou mais pacotes de idioma.

> [!NOTE]
>  Visual Studio não oferece suporte à instalação de várias versões de idioma do produto completo de idiomas no mesmo computador. Depois de instalar um produto com todos os idiomas, você deverá adicionar versões de idioma usando pacotes de idiomas. Você ainda pode instalar vários produtos de idiomas completos das edições Express no mesmo computador.

### <a name="support-for-code-pages"></a>Suporte para páginas de código
 Algumas ferramentas do Visual Studio não exibem o texto corretamente quando o texto contém caracteres que não estão na página de código atual. Em vez disso, os pontos de interrogação aparecem ou texto está corrompido. As seguintes ferramentas ou áreas são afetadas:

-   Sites implantados usando FTP.

-   Nomes de computador não ASCII em alguns controles.

-   Ferramentas de linha de comando executadas fora do Visual Studio.

-   Assistente de Migração do Visual Basic.

-   Contêiner de teste de controle ActiveX.

-   Visualizador de Objeto OLE/COM.

-   Ferramenta de depuração ISAPI Web.

-   Os projetos de aplicativos MFC que têm conteúdo da Ajuda HTML.

-   A interface do usuário do Visual SourceSafe/SCCI voltará para o inglês quando houver uma página de código incompatível.

-   O Visual SourceSafe não dá suporte para nomes de arquivo Unicode.

-   Caracteres Definidos pelo Usuário Final (zona de uso particular) não podem ser usados como tokens/identificadores.

-   Os caracteres Latinos Estendidos-B não podem ser exibidos em algumas janelas de ferramentas do Visual Studio quando a página de código do Windows estiver definida para um idioma do leste asiático.

-   As execuções de texto que consistem em caracteres de scripts de vários idiomas podem exibir o glifo padrão para alguns caracteres.

-   Copiar e colar cadeias de caracteres de script complexas para controles pode causar a perda do shaping de caractere. Em vez disso, use o teclado de idioma correspondente para inserir texto.

##### <a name="to-correctly-display-characters-that-are-not-included-in-the-current-code-page"></a>Para exibir corretamente caracteres que não estejam incluídos na página de código atual

1.  Clique em **Iniciar**, clique em **Painel de Controle** e, em seguida, abra **Opções regionais e de idiomas** (ou **Região** em [!INCLUDE[win8](../includes/win8-md.md)]).

    > [!NOTE]
    >  Você deve ser um administrador no computador para seguir estas etapas.

2.  Clique na aba **Avançado**.

3.  Na lista **Selecionar um idioma para corresponder à versão do idioma dos programas não Unicode que você deseja usar**, selecione o idioma que você está usando atualmente.

4.  Clique em **OK**.

## <a name="changing-the-language-used-for-the-ui-text-in-visual-studio"></a>Alterando o idioma usado para o texto da interface do usuário no Visual Studio
 Quando você instalar versões de vários idiomas do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] no mesmo computador, a interface do usuário do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] será padronizada para **O mesmo que o do Microsoft Windows**. Essa configuração indica que o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] exibirá o texto da interface do usuário no idioma especificado como o idioma do sistema operacional.

> [!NOTE]
>  Se o Visual Studio estiver definido como **Usar o idioma do Microsoft Windows** e se o pacote de idiomas do Visual Studio correspondente não estiver instalado, o Visual Studio usará o idioma da primeira instalação do Visual Studio.

#### <a name="to-set-the-language-that-is-used-for-the-ui-text-in-visual-studio"></a>Para definir o idioma usado para o texto da interface do usuário no Visual Studio

1. No menu **Ferramentas**, clique em **Opções**.

2. Na caixa de diálogo **Opções**, expanda **Ambiente** e depois clique em **Configurações Internacionais**.

3. Na lista **Idioma**, escolha o idioma em que o texto da interface do usuário deve aparecer no ambiente de desenvolvimento.

    Para que o texto de interface do usuário no IDE corresponda à configuração de idioma do sistema operacional, selecione **O mesmo que o do Microsoft Windows**.

   Você também pode usar o comando devenv para definir o idioma usado para interface do usuário. Para obter mais informações, consulte [/LCID (devenv.exe)](../ide/reference/lcid-devenv-exe.md).

## <a name="see-also"></a>Consulte também
 [Caixa de diálogo Configurações Internacionais, Ambiente, Opções](../ide/reference/international-settings-environment-options-dialog-box.md)