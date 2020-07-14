---
title: Exemplo de Dia2dump | Microsoft Docs
ms.date: 07/24/2018
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- sample applications [DIA SDK]
- Dia2dump sample [DIA SDK]
ms.assetid: 492c0893-7043-452f-a020-890a47230d20
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 17fe6d65e70399ccac5b9ef4e2f1234ef4e3698e
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468682"
---
# <a name="dia2dump-sample"></a>Exemplo de Dia2dump

O exemplo Dia2dump mostra como usar o Microsoft Debug interface Access Software Development Kit (DIA SDK) para consultar um arquivo PDB para obter informações.

O exemplo de Dia2dump é instalado com o Visual Studio e contém a solução e os arquivos de origem. O executável compilado é executado na linha de comando. Ele pode exibir o conteúdo de um arquivo de banco de dados do programa inteiro (. pdb) ou apenas as seções nas quais você está interessado.

## <a name="install-the-sample"></a>Instalar o exemplo

O exemplo é instalado quando você escolhe o **desenvolvimento de desktop com carga de trabalho C++** no instalador do Visual Studio. Para obter informações sobre como instalar o Visual Studio e escolher cargas de trabalho específicas e componentes individuais, consulte [instalar o Visual Studio](../../install/install-visual-studio.md).

Quando instalado, o exemplo está no diretório de instalação do Visual Studio, em um subdiretório chamado \DIA SDK\Samples\DIA2Dump.

## <a name="build-the-sample"></a>Compilar o exemplo

Por padrão, o diretório de instalação é um diretório protegido. Isso significa que você deve usar um prompt de comando do desenvolvedor elevado ou instância do Visual Studio para criar e editar a solução de exemplo neste local. Para simplificar a compilação, recomendamos que você primeiro copie os arquivos do diretório de exemplo para outro diretório, como uma pasta na pasta documentos e, em seguida, compile o exemplo.

### <a name="to-build-the-dia2dump-sample-in-visual-studio"></a>Para criar o exemplo de Dia2Dump no Visual Studio

1. Abra o arquivo DIA2Dump. sln no Visual Studio. Se você não tiver copiado a solução para outro diretório, talvez seja solicitado que você reinicie o Visual Studio com permissões elevadas.

1. Em **Gerenciador de soluções**, selecione o projeto Dia2Dump (não a solução).

1. Abra a caixa de diálogo **Páginas de Propriedades** do projeto. Para obter detalhes, confira [Trabalhando com propriedades do projeto](/cpp/build/working-with-project-properties).

1. Abra a página de propriedades de **configuração**  >  geral do**C/C++**  >  **General** .

1. Na propriedade **incluir diretórios adicionais** , escolha o controle suspenso e escolha **Editar**.

1. Na caixa de diálogo **diretórios de inclusão adicionais** , no campo editar, insira o `$(VSInstallDir)DIA SDK\include` diretório. Adicione esse diretório para garantir que o compilador possa localizar o arquivo dia2. h. Escolha **OK** para salvar suas alterações.

1. Escolha **OK** para salvar as alterações nas propriedades do projeto.

1. No menu **Compilar** , escolha **Recompilar solução**. Por padrão, o Visual Studio cria uma versão de depuração do exemplo, localizada em um subdiretório de depuração do diretório da solução.

1. Feche o Visual Studio.

### <a name="to-build-the-dia2dump-sample-at-the-command-line"></a>Para criar o exemplo de Dia2Dump na linha de comando

1. Em uma janela de prompt de comando do desenvolvedor, altere para o diretório em que você copiou os arquivos de exemplo. Se você não tiver copiado o exemplo em outro diretório, deverá usar uma janela de prompt de comando do desenvolvedor com privilégios elevados (executar como administrador).

1. Insira o comando `nmake makefile` para criar a configuração de depuração padrão de dia2dump.exe.

## <a name="run-the-dia2dump-sample"></a>Executar o exemplo de Dia2Dump

Dia2Dump.exe se baseia no servidor COM do MSDIA*version*. dll para fornecer seus serviços. A partir do Visual Studio 2015, a versão é msdia140.dll. Se o servidor COM MSDIA*version*. dll não for inicializado, você deverá registrá-lo antes que dia2dump.exe possa funcionar. O diretório DIA SDK tem um subdiretório bin que contém a versão x86 da DLL. Uma versão para computadores com arquitetura x64 está em bin\amd64, e uma versão para ARM está em bin\arm. Para registrar a dll, abra uma janela de prompt de comando de desenvolvedor elevada e altere para o diretório que contém a versão da sua arquitetura de computador. Insira o comando `regsvr32 msdia140.dll` para registrar o servidor com.

### <a name="to-run-the-sample"></a>Para executar a amostra

1. Abra um prompt de comando e altere para o diretório que contém o dia2dump.exe que você criou.

1. Insira o comando `dia2dump filename` em que *filename* é o nome de um arquivo PDB a ser examinado. Se o arquivo PDB estiver em outro diretório, use o caminho completo para o arquivo como *filename*. Esse comando lista todos os dados no arquivo PDB.

1. Dia2Dump tem outras opções para exibir apenas as informações selecionadas. Use o `dia2dump -?` comando para listar todas as opções disponíveis.

## <a name="see-also"></a>Veja também

- [Portar, migrar e atualizar projetos do Visual Studio](../../porting/port-migrate-and-upgrade-visual-studio-projects.md)
