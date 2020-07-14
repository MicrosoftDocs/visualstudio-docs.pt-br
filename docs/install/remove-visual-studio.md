---
title: Remover o Visual Studio
titleSuffix: ''
description: Saiba como remover completamente o Visual Studio do seu computador, passo a passo.
ms.date: 12/19/2019
ms.custom: seodec18
ms.topic: how-to
f1_keywords:
- uninstall
- uninstall Visual Studio
- remove
- remove Visual Studio
- cleanup
- cleanup Visual Studio
- clean up
- clean up Visual Studio
ms.assetid: 9c81a777-9c95-4934-b517-c60c6dc78799
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: b26e837ec2c4155c1be0b3639368c4315d2aecd3
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85418919"
---
# <a name="remove-visual-studio"></a>Remover o Visual Studio

Se você tiver um erro catastrófico e não puder reparar ou desinstalar o Visual Studio, poderá executar a `InstallCleanup.exe` ferramenta para remover arquivos de instalação e informações de produtos de todas as instâncias instaladas do visual studio 2017 ou do visual studio 2019.

> [!WARNING]
> Use a ferramenta InstallCleanup **somente como último recurso se a** reparação ou desinstalação falhar. Essa ferramenta pode desinstalar recursos de outras instalações do Visual Studio ou outros produtos que, em seguida, talvez também precisem ser reparadas ou reinstaladas.

## <a name="run-installcleanupexe"></a>Executar InstallCleanup.exe

Você pode usar qualquer uma das seguintes opções de linha de comando com a `InstallCleanup.exe` ferramenta:

| Alternar | Comportamento |
| ------ | -------- |
| `-i`   | Essa opção será o padrão se nenhuma outra opção for passada. Ele remove apenas o diretório de instalação principal e as informações do produto. Use essa opção se você pretende reinstalar a mesma versão do Visual Studio depois de executar a `InstallCleanup.exe` ferramenta. |
| `-f`   | Essa opção remove o diretório de instalação principal, as informações do produto e a maioria dos outros recursos instalados fora do diretório de instalação, que também podem ser compartilhados com outras instalações do Visual Studio ou outros produtos. Use esta opção se você pretende remover o Visual Studio sem reinstalá-lo mais tarde. |

Veja como executar a `InstallCleanup.exe` ferramenta:

1. Fechar o instalador do Visual Studio.
1. Abra um prompt de comando do administrador. Para abrir um prompt de comando de administrador, siga estas etapas:
   * Digite **cmd** na caixa "Digite aqui para pesquisar".
   * Clique com o botão direito do mouse em **Prompt de Comando** e escolha **Executar como administrador**.
1. Insira o caminho completo da `InstallCleanup.exe` ferramenta e adicione a opção de linha de comando que você preferir. Por padrão, o caminho da ferramenta é o seguinte. As aspas duplas delimitam um comando que contém espaços:

   ```
   "C:\Program Files (x86)\Microsoft Visual Studio\Installer\resources\app\layout\InstallCleanup.exe"
   ```

   > [!NOTE]
   > Se você não conseguir encontrar `InstallCleanup.exe` no diretório instalador do Visual Studio, que está sempre localizado em `%ProgramFiles(x86)%\Microsoft Visual Studio` , veja o que fazer em seguida. Siga as instruções para [instalar o Visual Studio](install-visual-studio.md). Em seguida, quando a tela de seleção de carga de trabalho for exibida, feche a janela e siga as etapas desta página novamente.

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Veja também

* [Instalar o Visual Studio](install-visual-studio.md)
* [Atualizar o Visual Studio](update-visual-studio.md)
* [Modificar o Visual Studio](modify-visual-studio.md)
* [Desinstalar o Visual Studio](uninstall-visual-studio.md)
