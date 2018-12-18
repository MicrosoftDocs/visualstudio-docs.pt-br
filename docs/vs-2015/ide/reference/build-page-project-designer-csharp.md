---
title: Página Build, Designer de Projeto (C#) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- cs.ProjectPropertiesBuild
helpviewer_keywords:
- Build options [C#]
- Project Designer, Build page
ms.assetid: 77ff1bfc-d633-4634-ba29-9afdb6d7e362
caps.latest.revision: 47
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: a377db0ac82b672d053e59c621714945fa9b515c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49837172"
---
# <a name="build-page-project-designer-c"></a>Página de Build, Designer de Projeto (C#)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Use a página **Compilar** do **Designer de Projeto** para especificar as propriedades de configuração de build do projeto. Essa página se aplica somente a projetos do [!INCLUDE[csprcs](../../includes/csprcs-md.md)].  
  
 Para acessar a página **Build**, escolha um nó do projeto (não o nó **Solução**) no **Gerenciador de Soluções**. Em seguida, escolha **Projeto**, **Propriedades** na barra de menus. Quando o Designer de Projeto for exibido, clique na guia **Build**.  
  
 [!INCLUDE[note_settings_general](../../includes/note-settings-general-md.md)]  
  
## <a name="configuration-and-platform"></a>Configuração e plataforma  
 As opções a seguir permitem selecionar a configuração e a plataforma a ser exibida ou modificada.  
  
> [!NOTE]
>  Com configurações de build simplificadas, o sistema do projeto determina se é necessário compilar uma versão de depuração ou de liberação. Portanto, essas opções não são exibidas. Para obter mais informações, consulte [Configurações de projeto de depuração e versão](http://msdn.microsoft.com/en-us/0440b300-0614-4511-901a-105b771b236e).  
  
 **Configuração**  
 Especifica quais definições de configuração exibir ou modificar. As configurações podem ser **Ativa (Depuração)** (esse é o padrão), **Depuração**, **Versão** ou **Todas as Configurações**.  
  
 **Plataforma**  
 Especifica quais configurações de plataforma exibir ou modificar. A configuração padrão é **Ativo (Qualquer CPU)**. É possível alterar a plataforma ativa usando o **Configuration Manager**. Para obter mais informações, consulte [Como criar e editar configurações](../../ide/how-to-create-and-edit-configurations.md).  
  
## <a name="general"></a>Geral  
 As opções a seguir permitem definir várias configurações do compilador do C#.  
  
 **Símbolos de compilação condicional**  
 Especifica símbolos nos quais a compilação condicional é executada. Separe símbolos com um ponto-e-vírgula (“;”). Para obter mais informações, consulte [/define (opções do compilador C#)](http://msdn.microsoft.com/library/f17d7b4d-82d0-4133-8563-68cced1cac6e).  
  
 **Definir a constante DEBUG**  
 Define DEBUG como um símbolo em todos os arquivos de código-fonte do aplicativo. Selecionar essa opção equivale a usar a opção de linha de comando `/define:DEBUG`.  
  
 **Definir a constante TRACE**  
 Define TRACE como um símbolo em todos os arquivos de código-fonte do aplicativo. Selecionar essa opção equivale a usar a opção de linha de comando `/define:TRACE`.  
  
 **CPU de Destino**  
 Especifica o processador de destino do arquivo de saída. Escolha **x86** para qualquer processador compatível com Intel de 32 bits, **x64** para qualquer processador compatível com Intel de 64 bits, **ARM** para processadores ARM ou **Qualquer CPU** para especificar que qualquer processador é aceitável. **Qualquer CPU** é o valor padrão para projetos, pois permite que o aplicativo seja executado em uma ampla variedade de hardwares.  
  
 Para obter mais informações, consulte [/platform (opções do compilador C#)](http://msdn.microsoft.com/library/c290ff5e-47f4-4a85-9bb3-9c2525b0be04).  
  
 **Preferir 32 bits**  
 Se a caixa de seleção **Preferir 32 bits** estiver marcada, o aplicativo será executado como um aplicativo de 32 bits em versões de 32 e 64 bits do Windows. Se a caixa de seleção estiver desmarcada, o aplicativo será executado como um aplicativo de 32 bits em versões de 32 bits do Windows e como um aplicativo de 64 bits em versões de 64 bits do Windows.  
  
 Se você executar um aplicativo como um aplicativo de 64 bits, o ponteiro duplicará de tamanho e poderão ocorrer problemas de compatibilidade com outras bibliotecas que são exclusivamente de 32 bits. É útil executar um aplicativo de 64 bits somente se ele precisa de mais de 4 GB de memória ou se as instruções de 64 bits fornecem uma melhoria de desempenho significativa.  
  
 Essa caixa de seleção estará disponível somente se todas as seguintes condições forem verdadeiras:  
  
- Na **Página Build**, a lista **Destino da plataforma** é definida com **Qualquer CPU**.  
  
- Na **Página Aplicativo**, a lista **Tipo de saída** especifica que o projeto é um aplicativo.  
  
- Na **Página Aplicativo**, a lista **Estrutura de destino** especifica o .NET Framework 4.5.  
  
  **Permitir código não seguro**  
  Permite a compilação do código que usa a palavra-chave [unsafe](http://msdn.microsoft.com/library/7e818009-1c6e-4b9e-b769-3728a01586a0). Para obter mais informações, consulte [/unsafe (opções do compilador C#)](http://msdn.microsoft.com/library/fdb77ed9-da03-45bd-bb7f-250704da1bcc).  
  
  **Otimizar código**  
  Habilita ou desabilita as otimizações executadas pelo compilador para tornar o arquivo de saída menor, mais rápido e mais eficiente. Para obter mais informações, consulte [/optimize (opções do compilador C#)](http://msdn.microsoft.com/library/6dd5b6f2-cd1d-4593-a9f4-1c2ed9404ca0).  
  
## <a name="errors-and-warnings"></a>Erros e Avisos  
 As configurações a seguir são usadas para configurar as opções de erro e de aviso para o processo de build.  
  
 **Nível de aviso**  
 Especifica o nível a ser exibido para avisos do compilador. Para obter mais informações, consulte [/warn (opções do compilador C#)](http://msdn.microsoft.com/library/5f80ff59-4991-4382-9f9a-77da18446e71).  
  
 **Suprimir avisos**  
 Bloqueia a capacidade do compilador de gerar um ou mais avisos. Separe vários números de aviso com uma vírgula ou um ponto-e-vírgula. Para obter mais informações, consulte [/nowarn (opções do compilador C#)](http://msdn.microsoft.com/library/6dcbc5e8-ae67-4566-9df3-f63cfdd9c4e4).  
  
## <a name="treat-warnings-as-errors"></a>Tratar Avisos como Erros  
 As configurações a seguir são usadas para especificar quais avisos são tratados como erros. Selecione uma das opções a seguir para indicar em quais condições um erro é retornado quando o build recebe um aviso. Para obter mais informações, consulte [/warnaserror (opções do compilador C#)](http://msdn.microsoft.com/library/04680ec3-08d6-4e2e-a274-38310e10e33c).  
  
 **Nenhum**  
 Não trata nenhum aviso como erro.  
  
 **Avisos específicos**  
 Trata os avisos especificados como erros. Separe vários números de aviso com uma vírgula ou um ponto-e-vírgula.  
  
 **All**  
 Trata todos os avisos como erros.  
  
## <a name="output"></a>Saída  
 As configurações a seguir são usadas para configurar as opções de saída para o processo de build.  
  
 **Caminho de saída**  
 Especifica o local dos arquivos de saída para a configuração deste projeto. Insira o caminho da saída do build nessa caixa ou escolha o botão **Procurar** para especificar um caminho. Observe que o caminho é relativo; se você inserir um caminho absoluto, ele será salvo como relativo. O caminho padrão é bin\Debug ou bin\Release\\. Para obter mais informações, consulte [Configurações de projeto de depuração e versão](http://msdn.microsoft.com/en-us/0440b300-0614-4511-901a-105b771b236e).  
  
 Com configurações de build simplificadas, o sistema do projeto determina se é necessário compilar uma versão de depuração ou de liberação. O comando **Build** do menu **Depurar** (F5) colocará o build no local de depuração, independentemente do **Caminho de saída** você especificar. No entanto, o comando **Build** do menu **Build** o coloca no local especificado. Para obter mais informações, consulte [Configurações de projeto de depuração e versão](http://msdn.microsoft.com/en-us/0440b300-0614-4511-901a-105b771b236e).  
  
 **Arquivo de documentação XML**  
 Especifica o nome de um arquivo no qual os comentários da documentação serão processados. Para obter mais informações, consulte [/doc (opções do compilador C#)](http://msdn.microsoft.com/library/849eea59-c936-4311-bad8-d07404480f2a).  
  
 **Registrar para interoperabilidade COM**  
 Indica que o aplicativo gerenciado exporá um objeto COM (um COM Callable Wrapper) que permite que um objeto COM interaja com o aplicativo gerenciado. A propriedade **Tipo de saída** da [página Aplicativo](../../ide/reference/application-page-project-designer-visual-basic.md) do **Designer de Projeto** desse aplicativo deve ser definida como **Biblioteca de Classes** para que a propriedade **Registrar para a interoperabilidade COM** esteja disponível. Para obter uma classe de exemplo que pode ser incluída no aplicativo [!INCLUDE[csprcs](../../includes/csprcs-md.md)] e exposta como um objeto COM, consulte [Classe COM de exemplo](http://msdn.microsoft.com/library/6504dea9-ad1c-4993-a794-830fec5270af).  
  
 **Gerar assembly de serialização**  
 Especifica se o compilador usará a ferramenta Gerador de Serializador XML (Sgen.exe) para criar assemblies de serialização XML. Os assemblies de serialização poderão melhorar o desempenho da inicialização de <xref:System.Xml.Serialization.XmlSerializer> se você tiver usado essa classe para serializar os tipos no código. Por padrão, essa opção é definida como **Automático**, que especifica que os assemblies de serialização serão gerados apenas se você tiver usado <xref:System.Xml.Serialization.XmlSerializer> para codificar tipos no código em XML. **Desativado** especifica que os assemblies de serialização nunca devem ser gerados, independentemente de o código usar <xref:System.Xml.Serialization.XmlSerializer>. **Ativado** especifica que os assemblies de serialização sempre devem ser gerados. Os assemblies de serialização são chamados `TypeName`.XmlSerializers.dll. Para obter mais informações, consulte [Ferramenta Gerador de Serializador XML (Sgen.exe)](http://msdn.microsoft.com/library/cc1d1f1c-fb26-4be9-885a-3fe84c81cec6).  
  
 **Avançado**  
 Clique para exibir a caixa de diálogo [Configurações de Build Avançadas (C#)](../../ide/reference/advanced-build-settings-dialog-box-csharp.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de propriedades do projeto](../../ide/reference/project-properties-reference.md)   
 [Opções do compilador de C#](http://msdn.microsoft.com/library/d3403556-1816-4546-a782-e8223a772e44)



