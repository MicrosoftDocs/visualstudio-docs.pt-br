---
title: Como exportar uma textura que contenha mipmaps
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 3d1ad14b-44fb-4cf0-a995-5e2f60026524
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 67eb30f340afcd2f8e631170fc84fd00f5a9d43c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49831323"
---
# <a name="how-to-export-a-texture-that-contains-mipmaps"></a>Como exportar uma textura que contenha mipmaps

O Pipeline de conteúdo de imagem pode gerar mipmaps de uma imagem de origem como parte da fase de build do projeto. Para obter certos efeitos, às vezes, você precisa especificar o conteúdo da imagem de cada nível de MIP manualmente. Quando você não precisa especificar o conteúdo da imagem de cada nível de MIP manualmente, gerar mapas MIP no momento da criação assegura que o conteúdo do mapa MIP nunca fique fora de sincronia. Isso também elimina o custo de desempenho de gerar mapas MIP em tempo de execução.

Este artigo aborda:

- Configurando a imagem de origem a ser processada pelo Pipeline de conteúdo da imagem.

- Configurando o Pipeline de conteúdo de imagem para gerar mipmaps.

## <a name="export-mipmaps"></a>Exportar mipmaps

O mapeamento mip fornece o nível de detalhe do espaço de tela automático para superfícies com textura em um aplicativo ou jogo 3D. Ele aumenta o desempenho de renderização de um jogo ou aplicativo computando previamente versões com amostra reduzida de uma textura. Pré-computar versões reduzidas significa que a textura inteira não ter sua amostra reduzida cada vez que é amostrada.

### <a name="to-export-a-texture-that-has-mipmaps"></a>Para exportar uma textura que contenha mipmaps

1. Comece com uma textura básica. Carregue um arquivo de imagem existente ou crie um, conforme descrito em [Como criar uma textura básica](../designers/how-to-create-a-basic-texture.md). Para oferecer suporte a mipmaps, especifique uma textura que tenha uma largura e altura que sejam as mesmas, por exemplo, 64x64, 256x256 ou 512x512.

2. Configure o arquivo de textura que você acabou de criar para que ele seja processado pelo Pipeline de conteúdo de imagem. No **Gerenciador de Soluções**, abra o menu de atalho do arquivo de textura que você criou e selecione **Propriedades**. Na página **Propriedades de Configuração** > **Geral**, defina a propriedade **Tipo de Item** como **Pipeline de Conteúdo de Imagem**. Verifique se a propriedade **Conteúdo** está definida como **Sim** e se **Excluir do Build** está definido como **Não**. Selecione **Aplicar**.

   A página de propriedades de configuração **Pipeline de Conteúdo de Imagem** é exibida.

3. Configure o Pipeline de conteúdo de imagem para gerar mipmaps. Na página **Propriedades de Configuração** > **Pipeline de Conteúdo de Imagem** > **Geral**, defina a propriedade **Gerar mips** como **Sim (/generatemips)**.

4. Selecione **OK**.

Quando você cria o projeto, o Pipeline de conteúdo de imagem converte a imagem de origem do formato de trabalho para o formato de saída que você especificou, incluindo níveis de MIP. O resultado é copiado para o diretório de saída do projeto.