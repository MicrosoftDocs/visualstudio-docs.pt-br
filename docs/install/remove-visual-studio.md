---
title: Remover o Visual Studio
titleSuffix: ''
description: Saiba como remover completamente Visual Studio do computador, passo a passo.
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
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 5af0cf31d3a53b12910ea8108c93a99cbaf3e87f
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306950"
---
# <a name="remove-visual-studio"></a>Remover o Visual Studio

Se você tiver um erro catastrófico e não puder reparar ou desinstalar o Visual Studio, poderá executar a ferramenta para remover arquivos de instalação e informações do produto para todas as `InstallCleanup.exe` instâncias instaladas do Visual Studio 2017, Visual Studio 2019 ou Visual Studio 2022.

> [!WARNING]
> Use a ferramenta InstallCleanup **somente como último recurso** se o reparo ou a desinstalação falharem. Essa ferramenta pode desinstalar recursos de outras Visual Studio ou outros produtos, que talvez também precisem ser reparados ou reinstalados.

## <a name="run-installcleanupexe"></a>Executar InstallCleanup.exe

Você pode usar qualquer uma das seguintes opções de linha de comando com a `InstallCleanup.exe` ferramenta:

| Comutador | Comportamento                                                                                                                                                                                                                                                                                                                 |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `-i`   | Essa opção será o padrão se nenhuma outra opção for passada. Ele remove apenas o diretório de instalação principal e as informações do produto. Use essa opção se você pretende reinstalar a mesma versão do Visual Studio depois de executar a `InstallCleanup.exe` ferramenta.                                                              |
| `-f`   | Essa opção remove o diretório de instalação principal, as informações do produto e a maioria dos outros recursos instalados fora do diretório de instalação, que também podem ser compartilhados com outras instalações Visual Studio ou outros produtos. Use essa opção se você pretende remover o Visual Studio sem reinstalá-lo posteriormente. |

Veja como executar a `InstallCleanup.exe` ferramenta:

1. Fechar o instalador do Visual Studio.
1. Abra um prompt de comando do administrador. Para abrir um prompt de comando de administrador, siga estas etapas:
   * Digite **cmd** na caixa "Digite aqui para pesquisar".
   * Clique com o botão direito do mouse em **Prompt de Comando** e escolha **Executar como administrador**.
1. Insira o caminho completo da ferramenta `InstallCleanup.exe` e adicione a opção de linha de comando que você preferir. Por padrão, o caminho da ferramenta é o seguinte. As aspas duplas contêm um comando que contém espaços:

   ```shell
   "C:\Program Files (x86)\Microsoft Visual Studio\Installer\resources\app\layout\InstallCleanup.exe"
   ```

   > [!NOTE]
   > Se você não encontrar no diretório Instalador do Visual Studio, que está sempre localizado `InstallCleanup.exe` em , veja o que fazer em `%ProgramFiles(x86)%\Microsoft Visual Studio` seguida. Siga as instruções para [instalar o Visual Studio](install-visual-studio.md). Em seguida, quando a tela de seleção da carga de trabalho for exibida, feche a janela e siga as etapas nesta página novamente.

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Instalar o Visual Studio](install-visual-studio.md)
* [Atualizar o Visual Studio](update-visual-studio.md)
* [Modificar o Visual Studio](modify-visual-studio.md)
* [Desinstalar o Visual Studio](uninstall-visual-studio.md)
