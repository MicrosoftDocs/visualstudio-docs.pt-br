---
title: Configurações de confiança de arquivos e pastas
description: Saiba como alterar as configurações de confiança de arquivos e pastas para proteger o Visual Studio.
author: abuchholtzau
ms.author: allisb
ms.date: 09/05/2018
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
f1_keywords:
- VS.ToolsOptionsPages.Environment.PathTrustOptions
helpviewer_keywords:
- file security
- folder security
- mark of the web
- trusted files
- trusted folders
ms.openlocfilehash: 08c4b08c33cd954aa427f158158f29cfbe50df94
ms.sourcegitcommit: 4708f0ba09b540424efcc344f8438f25432e3d51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/11/2018
ms.locfileid: "44384698"
---
# <a name="configure-trust-settings-for-files-and-folders"></a>Definir configurações de confiança de arquivos e pastas

O Visual Studio solicita a aprovação do usuário antes de abrir projetos que têm a [marca da Web](/previous-versions/windows/internet-explorer/ie-developer/compatibility/ms537628(v=vs.85)). Para aumentar a segurança, você também pode configurar o Visual Studio para solicitar a aprovação do usuário antes de abrir qualquer arquivo ou pasta que tenha a marca do atributo da Web ou que não esteja designado como *confiável*. Verificações de arquivos e de pastas estão desabilitadas por padrão.

> [!WARNING]
> Você ainda precisa garantir que o arquivo, pasta ou solução seja proveniente de uma pessoa ou de um local confiável antes de aprová-lo.

## <a name="configure-trust-settings"></a>Definir configurações de confiança

Para alterar as configurações de confiança, siga estas etapas:

1. Abra **Ferramentas** > **Opções** > **Configurações de Confiança** e selecione o link **Definir Configurações de Confiança** no painel direito.

2. Escolha o nível das verificações que você gostaria de ter para os arquivos e pastas. É possível ter verificações diferentes para cada um deles. As opções são:

   * **Nenhuma verificação**: o Visual Studio não executa nenhuma verificação.

   * **Verifique a marca do atributo da Web**: se o arquivo ou pasta tiver a marca do atributo Web, o Visual Studio o bloqueará e solicitará permissão para abrir.

   * **Verifique se o caminho é confiável**: se o arquivo ou pasta não fizer parte da lista **Caminhos Confiáveis**, o Visual Studio o bloqueará e solicitará permissão para abrir.

   ![Opções de verificação de confiança](media/trust-settings.png)

## <a name="add-trusted-paths"></a>Adicionar caminhos confiáveis

Para adicionar caminhos confiáveis, siga estas etapas:

1. Abra **Ferramentas** > **Opções** > **Configurações de Confiança** e selecione o link **Definir Configurações de Confiança** no painel direito.

2. Clique em **Adicionar** na caixa de diálogo **Configurações de Confiança** e, em seguida, selecione **Arquivo** ou **Pasta**.

3. Navegue até o arquivo ou pasta que deseja adicionar à lista de confiança e adicione-o.

   O caminho do arquivo ou pasta aparece na lista **Caminhos Confiáveis**.

   ![Caminhos confiáveis adicionados](media/trusted-paths.png)

## <a name="remove-trusted-paths"></a>Remover caminhos confiáveis

Para remover caminhos confiáveis, siga estas etapas:

1. Abra **Ferramentas** > **Opções** > **Configurações de Confiança** e selecione o link **Definir Configurações de Confiança** no painel direito.

2. Selecione o caminho que gostaria de remover na lista **Caminhos Confiáveis** e, em seguida, clique em **Remover**.

   > [!TIP]
   > Para selecionar várias entradas, mantenha pressionada a tecla **Shift** enquanto seleciona os caminhos.

   Os caminhos selecionados são removidos da lista **Caminhos Confiáveis**.
