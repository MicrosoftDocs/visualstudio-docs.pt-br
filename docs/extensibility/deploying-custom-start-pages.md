---
title: Implantar páginas iniciais personalizadas | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- package start page
- deploy start page
ms.assetid: 4a7eb360-de83-41d5-be53-3cfb160d19f9
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 81b4fb4938c1b87f4a9ca31cdc6035c4c6f124d1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49926456"
---
# <a name="deploy-custom-start-pages"></a>Implantar páginas de inicialização personalizada

Você pode implantar páginas de inicialização personalizada usando a implantação do VSIX ou copiando os arquivos nos locais corretos no computador de destino.

## <a name="vsix-deployment-by-using-the-start-page-project-template"></a>Implantação do VSIX usando o modelo de projeto de página inicial

Quando você cria uma página inicial, usando o modelo de projeto de página inicial e, em seguida, compile o projeto, o Visual Studio cria uma *VSIX* arquivo que você pode distribuir. Empacotando uma página inicial em um *VSIX* arquivo fornece as seguintes opções para a implantação, dependendo do seu público-alvo:

-   Você pode colocar o *VSIX* arquivo em um compartilhamento de rede ou em um site público. Quando alguém abre o arquivo, a página de início é instalada automaticamente.

-   Você pode carregar os *. VSIX* do arquivo para o [Galeria do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=123847) Web site para que os usuários podem instalá-lo usando **Gerenciador de extensões**.

O modelo de página inicial do projeto cria uma cópia da página de início do Visual Studio padrão para que você possa modificar a cópia e preservar o original.

Você pode obter o modelo de projeto de página inicial usando **Extension Manager** ou fazendo o download no site da Web.

## <a name="vsix-deployment-without-using-the-start-page-project-template"></a>Implantação do VSIX sem usar o modelo de projeto de página inicial
 Uma implantação bem-sucedida do VSIX requer uma extensão para ser instalado em pastas que são reconhecidas pelo processo de registro VSIX e pelo **Extension Manager**. Como o modelo de projeto de página inicial já especifica nas pastas corretas, é recomendável que você usá-lo sempre que você deseja empacotar uma extensão para a implantação do VSIX. No entanto, se você tiver um caso em que você não pode usar o modelo, você pode criar uma implantação de VSIX sem usá-lo.

 Para criar uma implantação de VSIX sem usar o modelo de projeto de página inicial, primeiro crie uma *VSIX* arquivo da página inicial em qualquer uma destas duas maneiras:

- Adicionando seus arquivos de página inicial personalizados para um projeto vazio do VSIX. Para obter mais informações, consulte [modelo de projeto do VSIX](../extensibility/vsix-project-template.md).

- Criando manualmente uma *VSIX* arquivo. Para criar uma *VSIX* arquivo manualmente:

  1.  Criar o *vsixmanifest* arquivo e o *[Content_Types]. XML* arquivo em uma nova pasta. Para obter mais informações, consulte [Anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md).

  2.  No Windows Explorer, clique com botão direito na pasta que contém os dois arquivos XML, clique em **enviar para**e, em seguida, clique em pasta compactada (zipada). Renomear resultante *. zip* arquivo *Filename.vsix*, onde Filename é o nome do arquivo redistribuível que instala o pacote.

  Para o Visual Studio reconhecer uma página inicial, o `Content Element` do manifesto do VSIX deve conter um `CustomExtension Element` que tem o `Type` atributo definido como `"StartPage"`. Uma extensão de página inicial que foi instalada usando a implantação do VSIX aparece na **Personalizar página inicial** lista o **inicialização** página de opções como **[instalado a extensão]** *Nome de extensão*.

  Se o seu pacote de página inicial inclui assemblies, você deve adicionar o registro do caminho de associação para que eles estejam disponíveis quando o Visual Studio é iniciado. Para fazer isso, certifique-se de que seu pacote inclui um *pkgdef* arquivo que tem as informações a seguir.

```
[$RootKey$\BindingPaths\{Insert a new GUID here}]
"$PackageFolder$"=""
```

### <a name="vsix-deployment-for-all-users"></a>Implantação do VSIX para todos os usuários
 Por padrão, as extensões implantadas em pacotes VSIX instalam somente para o usuário atual. Você pode fazer uma instalação de página de início para todos os usuários da máquina de destino com a criação de uma implantação de todos os usuários.

### <a name="to-create-an-all-users-deployment"></a>Para criar uma implantação de todos os usuários

1.  Abra o *vsixmanifest* arquivo na exibição de código.

2.  No `Identifier` elemento de manifesto do vsix, adicione uma `AllUsers` elemento que tem um valor de `true`.

    ```
    <AllUsers>true</AllUsers>
    ```

     Isso faz com que o instalador do vsix solicitar permissões de administrador e, em seguida, instale os arquivos a serem *\Common7\IDE\Extensions*.

3.  Abra o *pkgdef* arquivo.

4.  Modificar a *. pkgdef* para definir a página de início padrão em HKLM, adicionando o seguinte, onde *MyStartPage.xaml* é o nome da *. XAML* arquivo que contém seu início Página.

     [$RootKey$ \StartPage\Default]

     "Uri"="$PackageFolder$\\*MyStartPage.xaml*"

     Isso informa ao Visual Studio para examinar o novo local da página inicial.

## <a name="file-copy-deployment"></a>Implantação de cópia de arquivo
 Você não precisa criar uma *VSIX* arquivo para implantar uma página inicial personalizada. Em vez disso, você pode copiar a marcação e arquivos de suporte diretamente para o usuário <em>\StartPages\* pasta. O **Personalizar página inicial</em>*  lista o **inicialização** página de opções de listas de cada *. XAML* arquivo nessa pasta, junto com o caminho — por exemplo, *%USERPROFILE%\My Documents\Visual Studio {version} \StartPages\\. XAML de {nome do arquivo}*. Se sua página inicial inclui referências a assemblies particulares, você deve copiá-los e colá-los no * \PrivateAssemblies\* pasta.

 Para distribuir uma página inicial que você criou sem empacotá-la em uma *VSIX* arquivo, é recomendável que você usar uma estratégia de cópia do arquivo básico, por exemplo, um script em lotes, ou qualquer outra tecnologia de implantação que permite que você coloca os arquivos no diretórios necessários.

### <a name="to-manually-install-a-custom-start-page"></a>Para instalar manualmente uma página inicial personalizada

1.  Cópia de *. XAML* arquivo que contém a marcação de página inicial, junto com quaisquer arquivos de suporte que não seja de assemblies e colá-los no usuário * \StartPages\* pasta.

2.  Se a página de início requer que os assemblies, copiá-los e colá-los no *... \\{Pasta de instalação do visual Studio} \Common7\IDE\PrivateAssemblies\\*.

3.  No **Personalizar página inicial** lista os **inicialização** opções, selecione a nova página inicial. Para obter mais informações, consulte [personalizar a página de início](../ide/customizing-the-start-page-for-visual-studio.md).

## <a name="see-also"></a>Consulte também

- [Personalizar a Página Inicial](../ide/customizing-the-start-page-for-visual-studio.md)
- [Adicionar controle de usuário para a página de início](../extensibility/adding-user-control-to-the-start-page.md)