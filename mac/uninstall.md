---
title: Desinstalar o Visual Studio para Mac
description: Instruções para desinstalar o Visual Studio para Mac e as ferramentas relacionadas.
author: heiligerdankgesang
ms.author: dominicn
ms.date: 09/18/2019
ms.technology: vs-ide-install
ms.assetid: 4EB95F75-BC2E-4982-9564-2975805712D8
ms.topic: how-to
ms.openlocfilehash: ee30af4ed578bbc59924fcd8968b97dcf9306619
ms.sourcegitcommit: 5335a9864d5747bc917ed28d4ebeade3076b10e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85950030"
---
# <a name="uninstalling-visual-studio-for-mac"></a>Desinstalando o Visual Studio para Mac

Você pode usar este guia para desinstalar cada componente do Visual Studio para Mac individualmente navegando até a seção relevante ou usar os scripts fornecidos na seção [Script de Desinstalação](#uninstall-script) para desinstalar tudo.

> [!NOTE]
> Essas informações só removerão o Visual Studio 2019 ou 2017 para Mac do computador. para desinstalar o Visual Studio Code, confira [este problema](https://github.com/Microsoft/vscode/issues/52151) para obter detalhes.

## <a name="uninstall-script"></a>Scripts de Desinstalação

Há dois scripts que podem ser usados para desinstalar o Visual Studio para Mac e todos os componentes do seu computador:

- [Script do Visual Studio e do Xamarin](#visual-studio-for-mac-and-xamarin-script)
- [Script do .NET Core](#net-core-script)

As seções a seguir fornecem informações de como baixar e usar os scripts.

### <a name="visual-studio-for-mac-and-xamarin-script"></a>Script do Visual Studio para Mac e do Xamarin

Você pode desinstalar os componentes do Visual Studio e do Xamarin de uma só vez usando o [script de desinstalação](https://raw.githubusercontent.com/MicrosoftDocs/visualstudio-docs/master/mac/resources/uninstall-vsmac.sh).

Esse script de desinstalação contém a maioria dos comandos que você encontrará no artigo. Há três omissões principais do script que não estão incluídas devido a possíveis dependências externas. Para removê-las, vá para a seção relevante abaixo e remova manualmente:

- **[Desinstalando o mono](#uninstall-mono-sdk-mdk)**
- **[Desinstalando o Android AVD](#uninstall-android-avd)**
- **[Como desinstalar o SDK do Android e o SDK do Java](#uninstall-android-sdk-and-java-sdk)**

Para executar o script, execute as seguintes etapas:

1. Clique com o botão direito do mouse no script e selecione **Salvar Como** para salvar o arquivo no seu Mac.
2. Abra o Terminal e altere o diretório de trabalho para o local em que o script foi baixado:

    ```bash
    cd /location/of/file
    ```

3. Torne o script executável e execute-o com o **sudo**:

    ```bash
    chmod +x ./uninstall-vsmac.sh
    sudo ./uninstall-vsmac.sh
    ```

4. Por fim, exclua o script de desinstalação e remova o Visual Studio para Mac do dock (se estiver lá).

### <a name="net-core-script"></a>Script do .NET Core

O script de desinstalação do .NET Core está localizado no [repositório dotnet cli](https://raw.githubusercontent.com/dotnet/cli/master/scripts/obtain/uninstall/dotnet-uninstall-pkgs.sh)

Para executar o script, execute as seguintes etapas:

1. Clique com o botão direito do mouse no script e selecione **Salvar Como** para salvar o arquivo no seu Mac.
2. Abra o Terminal e altere o diretório de trabalho para o local em que o script foi baixado:

    ```bash
    cd /location/of/file
    ```

3. Torne o script executável e execute-o com o **sudo**:

    ```bash
    chmod +x ./dotnet-uninstall-pkgs.sh
    sudo ./dotnet-uninstall-pkgs.sh
    ```

4. Por fim, exclua o script de desinstalação do .NET Core.

## <a name="uninstall-visual-studio-for-mac"></a>Desinstalar o Visual Studio para Mac

A primeira etapa da desinstalação do Visual Studio em um Mac é localizar **Visual Studio.app** no diretório **/Aplicativos** e arrastá-lo para a **Lixeira**. Como alternativa, clique com botão direito do mouse e selecione **Mover para Lixeira** conforme é ilustrado na imagem a seguir:

![Mova o aplicativo do Visual Studio para a lixeira](media/uninstall-image1.png)

A exclusão desse lote de aplicativo removerá o Visual Studio para Mac, mesmo que outros arquivos relacionados ao Xamarin ainda permaneçam no sistema de arquivos.

Para remover todos os vestígios do Visual Studio para Mac, execute os comandos a seguir no Terminal:

```bash
sudo rm -rf "/Applications/Visual Studio.app"
rm -rf ~/Library/Caches/VisualStudio
rm -rf ~/Library/Preferences/VisualStudio
rm -rf ~/Library/Preferences/Visual\ Studio
rm -rf ~/Library/Logs/VisualStudio
rm -rf ~/Library/VisualStudio
rm -rf ~/Library/Preferences/Xamarin/
rm -rf ~/Library/Application\ Support/VisualStudio
rm -rf ~/Library/Application\ Support/VisualStudio/7.0/LocalInstall/Addins/
rm -rf ~/Library/Application\ Support/VisualStudio/8.0/LocalInstall/Addins/
```

Talvez você queira remover o seguinte diretório que contém vários arquivos e pastas do Xamarin. No entanto, antes de fazer isso, esteja ciente de que esse diretório contém as chaves de assinatura do Android. Para saber mais, consulte a seção **[Desinstalar o SDK do Android e o SDK do Java](#uninstall-android-sdk-and-java-sdk)**:

```bash
rm -rf ~/Library/Developer/Xamarin
```

## <a name="uninstall-mono-sdk-mdk"></a>Desinstalar o SDK do Mono (MDK)

O Mono é uma implementação de software livre do .NET Framework da Microsoft usado por todos os Produtos Xamarin – Xamarin.iOS, Xamarin.Android e Xamarin.Mac para permitir o desenvolvimento dessas plataformas em C#.

> [!WARNING]
> Há outros aplicativos fora do Visual Studio para Mac que também usam o Mono, como o Unity.
> Certifique-se de que não há outras dependências no Mono antes de desinstalá-lo.

Para remover a Estrutura Mono de um computador, execute os seguintes comandos no Terminal:

```bash
sudo rm -rf /Library/Frameworks/Mono.framework
sudo pkgutil --forget com.xamarin.mono-MDK.pkg
sudo rm -rf /etc/paths.d/mono-commands
```

## <a name="uninstall-xamarinandroid"></a>Desinstalar o Xamarin.Android

Há um número de itens necessários para a instalação e o uso do Xamarin.Android, como o SDK do Android e o SDK do Java.

Use os comandos a seguir para remover o Xamarin.Android:

```bash
sudo rm -rf /Developer/MonoDroid
rm -rf ~/Library/MonoAndroid
sudo pkgutil --forget com.xamarin.android.pkg
sudo rm -rf /Library/Frameworks/Xamarin.Android.framework
```

### <a name="uninstall-android-sdk-and-java-sdk"></a>Desinstalar o SDK do Android e o SDK do Java

O SDK do Android é necessário para o desenvolvimento de aplicativos Android. Para remover completamente todas as partes do SDK do Android, localize o arquivo em **~/Library/Developer/Xamarin/** e mova-o para a **Lixeira**.

> [!WARNING]
> Esteja ciente de que as chaves de assinatura do Android que são geradas pelo Visual Studio para Mac estão localizadas em `~/Library/Developer/Xamarin/Keystore`. Faça o backup delas de forma apropriada ou não remova esse diretório, caso queira manter seu repositório de chaves.

O SDK do Java (JDK) não precisa ser desinstalado, pois ele já é pré-empacotado como parte do Mac OS X / macOS.

### <a name="uninstall-android-avd"></a>Desinstalar o Android AVD

> [!WARNING]
> Há outros aplicativos fora do Visual Studio para Mac que também usam o Android AVD e esses componentes Android adicionais, como o Android Studio. Remover esse diretório pode causar falhas em projetos no Android Studio.

Para remover os Android AVDs e componentes Android adicionais, use o seguinte comando:

```bash
rm -rf ~/.android
```

Para remover apenas o Android AVDs, use o seguinte comando:

```bash
rm -rf ~/.android/avd
```

## <a name="uninstall-xamarinios"></a>Desinstalar o Xamarin.iOS

O Xamarin.iOS permite desenvolver aplicativos iOS usando C# ou F# com o Visual Studio para Mac.

Use os seguintes comandos no Terminal para remover todos os arquivos do Xamarin.iOS de um sistema de arquivos:

```bash
rm -rf ~/Library/MonoTouch
sudo rm -rf /Library/Frameworks/Xamarin.iOS.framework
sudo rm -rf /Developer/MonoTouch
sudo pkgutil --forget com.xamarin.monotouch.pkg
sudo pkgutil --forget com.xamarin.xamarin-ios-build-host.pkg
sudo pkgutil --forget com.xamarin.xamarin.ios.pkg
```

## <a name="uninstall-xamarinmac"></a>Desinstalar o Xamarin.Mac

O Xamarin.Mac pode ser removido do seu computador usando os dois comandos a seguir para eliminar o produto e a licença do seu Mac, respectivamente:

```bash
sudo rm -rf /Library/Frameworks/Xamarin.Mac.framework
rm -rf ~/Library/Xamarin.Mac
```

## <a name="uninstall-workbooks-and-inspector"></a>Desinstalar o Workbooks e o Inspector

A partir do 1.2.2, o Xamarin Workbooks e Inspector podem ser desinstalados de um terminal executando:

```bash
sudo /Library/Frameworks/Xamarin.Interactive.framework/Versions/Current/uninstall
```

Para as versões mais antigas, você precisa remover manualmente os seguintes artefatos:

* Exclua o aplicativo do Workbooks em `"/Applications/Xamarin Workbooks.app"`
* Exclua o aplicativo do Inspector em `"Applications/Xamarin Inspector.app"`
* Exclua os suplementos: `"~/Library/Application Support/XamarinStudio-6.0/LocalInstall/Addins/Xamarin.Interactive"` e `"~/Library/Application Support/XamarinStudio-6.0/LocalInstall/Addins/Xamarin.Inspector"`
* Exclua o Inspector e os arquivos de suporte aqui: `/Library/Frameworks/Xamarin.Interactive.framework` e `/Library/Frameworks/Xamarin.Inspector.framework`

## <a name="uninstall-the-xamarin-profiler"></a>Desinstale o Xamarin Profiler

```bash
sudo rm -rf "/Applications/Xamarin Profiler.app"
```

## <a name="uninstall-the-visual-studio-installer"></a>Desinstale o Instalador do Visual Studio

Use os comandos a seguir para remover todos os vestígios do Instalador Universal do Xamarin:

```bash
rm -rf ~/Library/Caches/XamarinInstaller/
rm -rf ~/Library/Caches/VisualStudioInstaller/
rm -rf ~/Library/Logs/XamarinInstaller/
rm -rf ~/Library/Logs/VisualStudioInstaller/
rm -rf ~/Library/Preferences/Xamarin/
rm -rf "~/Library/Preferences/Visual Studio/"
```

* * * 





## <a name="uninstall-visual-studio-2019-for-mac-preview"></a>Desinstalar a versão prévia do Visual Studio 2019 para Mac

A versão prévia do Visual Studio 2019 para Mac foi lançado como uma versão prévia separada, permitindo que você continue a trabalhar lado a lado com a instalação do Visual Studio 2017 para Mac.

Agora que o Visual Studio 2019 para Mac foi lançado, você pode remover com segurança o aplicativo de versão prévia do Visual Studio 2019 para Mac.

Para desinstalar o pacote de aplicativo de versão prévia, selecione **Visual Studio (Preview)** em sua pasta **Aplicativos** e clique em **Mover para a Lixeira**, conforme representado na imagem a seguir:

![selecionar a opção "mover para lixeira" no localizador](media/uninstall-remove-vspreview.png)

Você também pode remover o arquivo plist Preview com o seguinte comando:

```bash
rm -rf ~/Library/Preferences/com.microsoft.visual-studio-preview.plist
```

## <a name="see-also"></a>Veja também

- [Desinstalar Visual Studio (no Windows)](/visualstudio/install/uninstall-visual-studio)