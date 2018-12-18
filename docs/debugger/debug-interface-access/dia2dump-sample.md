---
title: Exemplo de Dia2dump | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- sample applications [DIA SDK]
- Dia2dump sample [DIA SDK]
ms.assetid: 492c0893-7043-452f-a020-890a47230d20
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e2e44abdce737df335133d5e54b6b022c97f639a
ms.sourcegitcommit: 71b307ce86c4079cc7ad686d8d5f96a6a123aadd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2018
ms.locfileid: "39252275"
---
# <a name="dia2dump-sample"></a>Exemplo de Dia2dump

O exemplo de Dia2dump mostra como usar o Microsoft depurar Interface acesso Software Development Kit (DIA SDK) para consultar um arquivo PDB para obter informações.

O exemplo de Dia2dump é instalado com o Visual Studio e contém os arquivos de solução e código-fonte. O executável compilado é executado da linha de comando. Ele pode exibir o conteúdo de um arquivo de banco de dados (. PDB) do programa inteiro ou apenas as seções que você está interessado.

## <a name="install-the-sample"></a>Instalar o exemplo

O exemplo é instalado quando você escolhe a **desenvolvimento para Desktop com C++** carga de trabalho no instalador do Visual Studio. Para obter informações sobre como instalar o Visual Studio e escolha as cargas de trabalho específicas e componentes individuais, consulte [instalar o Visual Studio](../../install/install-visual-studio.md).

Quando instalado, o exemplo está em seu diretório de instalação do Visual Studio, em um subdiretório chamado \DIA SDK\Samples\DIA2Dump.

## <a name="build-the-sample"></a>Criar o exemplo

Por padrão, o diretório de instalação é um diretório protegido. Isso significa que você deve usar um prompt de comando do desenvolvedor ou a instância do Visual Studio para criar e editar a solução de exemplo nesse local. Para simplificar a compilação, é recomendável primeiro copiar os arquivos do diretório de exemplo para outro diretório, como uma pasta na pasta documentos e, em seguida, criar o exemplo.

### <a name="to-build-the-dia2dump-sample-in-visual-studio"></a>Para criar o exemplo de Dia2Dump no Visual Studio

1. Abra o arquivo DIA2Dump.sln no Visual Studio. Se você não tiver copiado a solução para outro diretório, você pode ser solicitado a reiniciar o Visual Studio com permissões elevadas.

1. Na **Gerenciador de soluções**, selecione o projeto de Dia2Dump (não na solução).

1. Abra a caixa de diálogo **Páginas de Propriedades** do projeto. Para obter detalhes, confira [Trabalhando com propriedades do projeto](/cpp/ide/working-with-project-properties).

1. Abra o **propriedades de configuração** > **C/C++** > **geral** página de propriedades.

1. No **diretórios de inclusão adicionais** propriedade, escolha o controle de lista suspensa e escolha **editar**.

1. No **diretórios de inclusão adicionais** Inserir caixa de diálogo, no campo de edição, o `$(VSInstallDir)DIA SDK\include` directory. Adicione o diretório para garantir que o compilador pode localizar o arquivo de dia2.h. Escolher **Okey** para salvar suas alterações.

1. Escolher **Okey** para salvar suas alterações às propriedades do projeto.

1. Sobre o **construir** menu, escolha **recompilar solução**. Por padrão, o Visual Studio cria uma versão de depuração da amostra, localizada em um subdiretório de depuração do diretório da solução.

1. Feche o Visual Studio.

### <a name="to-build-the-dia2dump-sample-at-the-command-line"></a>Para criar o exemplo de Dia2Dump na linha de comando

1. Em uma janela de prompt de comando do desenvolvedor, altere para o diretório onde você copiou os arquivos de exemplo. Se você não copiar o exemplo para outro diretório, você deve usar com privilégios elevados (Executar como administrador) janela de prompt de comando do desenvolvedor.

1. Digite o comando `nmake makefile` para compilar a configuração de depuração padrão do dia2dump.exe.

## <a name="run-the-dia2dump-sample"></a>Executar o exemplo de Dia2Dump

Dia2Dump.exe depende do msdia*versão*. dll COM o servidor para fornecer seus serviços. No Visual Studio 2015 e Visual Studio 2017, a versão é msdia140.dll. Se o msdia*versão*. dll COM servidor não é inicializado, você deve registrá-lo antes de dia2dump.exe pode trabalhar. O diretório de DIA SDK tem um subdiretório bin que contém o x86 versão da DLL. Uma versão para x64 máquinas de arquitetura está em bin\amd64 e uma versão para ARM está em bin\arm. Para registrar a dll, abra uma janela elevada de prompt de comando do desenvolvedor e altere o diretório que contém a versão para a sua arquitetura de máquina. Digite o comando `regsvr32 msdia140.dll` para registrar o servidor COM.

### <a name="to-run-the-sample"></a>Para executar a amostra

1. Abra um prompt de comando e altere para o diretório que contém o dia2dump.exe que você criou.

1. Digite o comando `dia2dump filename` onde *filename* é o nome de um arquivo PDB para examinar. Se o arquivo PDB estiver em outro diretório, use o caminho completo para o arquivo como *filename*. Esse comando lista todos os dados no arquivo PDB.

1. Dia2Dump tem outras opções para exibir apenas as informações selecionadas. Use o `dia2dump -?` comando para listar todas as opções disponíveis.

## <a name="see-also"></a>Consulte também

- [Portar, migrar e atualizar projetos do Visual Studio](../../porting/port-migrate-and-upgrade-visual-studio-projects.md)  
