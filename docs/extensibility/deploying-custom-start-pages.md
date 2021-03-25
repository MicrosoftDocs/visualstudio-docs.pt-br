---
title: Implantando páginas iniciais personalizadas | Microsoft Docs
description: Saiba como implantar páginas iniciais personalizadas usando a implantação do VSIX ou copiando os arquivos para os locais corretos no computador de destino.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- package start page
- deploy start page
ms.assetid: 4a7eb360-de83-41d5-be53-3cfb160d19f9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: a356fe3dadaf0eca4f0b4d0f2a7d17f0b475acfb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061401"
---
# <a name="deploy-custom-start-pages"></a>Implantar páginas iniciais personalizadas

Você pode implantar páginas iniciais personalizadas usando a implantação do VSIX ou copiando os arquivos para os locais corretos no computador de destino.

## <a name="vsix-deployment-by-using-the-start-page-project-template"></a>Implantação do VSIX usando o modelo de projeto de página inicial

Quando você cria uma página inicial usando o modelo de projeto de página inicial e, em seguida, compila o projeto, o Visual Studio cria um arquivo *. vsix* que você pode distribuir. Empacotar uma página inicial em um arquivo *. vsix* oferece as seguintes opções para implantação, dependendo do público-alvo:

- Você pode colocar o arquivo *. vsix* em um compartilhamento de rede ou em um site público. Quando alguém abre o arquivo, a página inicial é instalada automaticamente.

- Você pode carregar o arquivo *. vsix* no site da [Visual Studio Marketplace](https://marketplace.visualstudio.com/) para que os usuários possam instalá-lo usando o **Gerenciador de extensões**.

O modelo de projeto página inicial cria uma cópia da página inicial do Visual Studio padrão para que você possa modificar a cópia e preservar o original.

Você pode obter o modelo de projeto de página inicial usando o **Gerenciador de extensões** ou baixando-o do site da Web.

## <a name="vsix-deployment-without-using-the-start-page-project-template"></a>Implantação do VSIX sem usar o modelo de projeto de página inicial
 Uma implantação de VSIX bem-sucedida requer que uma extensão seja instalada em pastas que são reconhecidas pelo processo de registro do VSIX e pelo **Gerenciador de extensões**. Como o modelo de projeto de página inicial já especifica as pastas corretas, recomendamos usá-lo sempre que desejar empacotar uma extensão para a implantação do VSIX. No entanto, se você tiver um caso no qual não possa usar o modelo, poderá criar uma implantação do VSIX sem usá-lo.

 Para criar uma implantação do VSIX sem usar o modelo de projeto de página inicial, primeiro crie um arquivo *. vsix* para a página inicial de uma destas duas maneiras:

- Adicionando os arquivos de página inicial personalizados a um projeto VSIX vazio. Para obter mais informações, consulte [modelo de projeto VSIX](../extensibility/vsix-project-template.md).

- Criando manualmente um arquivo *. vsix* . Para criar um arquivo *. vsix* manualmente:

   1. Crie o arquivo *extension. vsixmanifest* e o arquivo *[Content_Types]. xml* em uma nova pasta. Para obter mais informações, consulte [anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md).

   2. No Windows Explorer, clique com o botão direito do mouse na pasta que contém os dois arquivos XML, clique em **Enviar para** e clique em pasta compactada (zipada). Renomeie o arquivo *. zip* resultante para *filename. vsix*, em que filename é o nome do arquivo redistribuível que instala o pacote.

Para que o Visual Studio reconheça uma página inicial, o `Content Element` do manifesto do VSIX deve conter um `CustomExtension Element` que tenha o `Type` atributo definido como `"StartPage"` . Uma extensão de página inicial que foi instalada usando a implantação do VSIX aparece na lista **Personalizar página inicial** na página opções de **inicialização** como o *nome da extensão* **[extensão instalada]** .

Se o pacote de página inicial incluir assemblies, você deverá adicionar o registro de caminho de associação para que eles fiquem disponíveis quando o Visual Studio for iniciado. Para fazer isso, certifique-se de que o pacote inclui um arquivo *. pkgdef* que contém as informações a seguir.

```
[$RootKey$\BindingPaths\{Insert a new GUID here}]
"$PackageFolder$"=""
```

### <a name="vsix-deployment-for-all-users"></a>Implantação do VSIX para todos os usuários
 Por padrão, as extensões implantadas em pacotes VSIX são instaladas somente para o usuário atual. Você pode fazer uma instalação de página inicial para todos os usuários do computador de destino criando uma implantação de All-Users.

### <a name="to-create-an-all-users-deployment"></a>Para criar uma implantação de All-Users

1. Abra o arquivo *extension. vsixmanifest* na exibição de código.

2. No `Identifier` elemento do manifesto do VSIX, adicione um `AllUsers` elemento que tenha um valor de `true` .

    ```
    <AllUsers>true</AllUsers>
    ```

     Isso faz com que o instalador VSIX solicite permissões de administrador e, em seguida, instale os arquivos em *\Common7\IDE\Extensions*.

3. Abra o arquivo *. pkgdef* .

4. Modifique o *. pkgdef* para definir a página inicial padrão em HKLM adicionando o seguinte, em que *mystartpage. XAML* é o nome do arquivo *. XAML* que contém a página inicial.

     [$RootKey $ \StartPage\Default]

     "URI" = "$PackageFolder $ \\ *mystartpage. XAML*"

     Isso diz ao Visual Studio para examinar o novo local da página inicial.

## <a name="file-copy-deployment"></a>Implantação de cópia de arquivo
 Você não precisa criar um arquivo *. vsix* para implantar uma página inicial personalizada. Em vez disso, você pode copiar a marcação e os arquivos de suporte diretamente na <em>pasta \StartPages do usuário \* . A lista **Personalizar página inicial</em>* na página opções de **inicialização** lista todos os arquivos *. XAML* nessa pasta, junto com o caminho — por exemplo, *%USERPROFILE%\My Documentos\visual Studio {Version} \StartPages \\ {File Name}. XAML*. Se a página inicial incluir referências a assemblies privados, você deverá copiá-los e colá-los na pasta * \PrivateAssemblies \*

 Para distribuir uma página inicial que você criou sem compactá-la em um arquivo *. vsix* , recomendamos que você use uma estratégia básica de cópia de arquivo, por exemplo, um script em lotes ou qualquer outra tecnologia de implantação que permita colocar os arquivos nos diretórios necessários.

### <a name="to-manually-install-a-custom-start-page"></a>Para instalar manualmente uma página inicial personalizada

1. Copie o arquivo *. XAML* que contém a marcação de página inicial, junto com quaisquer arquivos de suporte que não sejam assemblies e cole-os na pasta * \StartPages do usuário \* .

2. Se a página inicial exigir assemblies, copie-os e cole-os no *. \\ {Pasta de instalação do Visual Studio \\ } \Common7\IDE\PrivateAssemblies*.

3. Na lista **Personalizar página inicial** na página opções de **inicialização** , selecione a nova página inicial. Para obter mais informações, consulte [Personalizar a página inicial](../ide/customizing-the-start-page-for-visual-studio.md).

## <a name="see-also"></a>Confira também

- [Personalizar a página inicial](../ide/customizing-the-start-page-for-visual-studio.md)
- [Adicionar controle de usuário à página inicial](../extensibility/adding-user-control-to-the-start-page.md)
