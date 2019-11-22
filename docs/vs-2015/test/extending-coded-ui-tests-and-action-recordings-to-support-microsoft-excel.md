---
title: Estendendo testes de IU codificados e gravações da ação para dar suporte ao Microsoft Excel | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 6b0f72a4-70ca-4e55-b236-2ea1034fd8a7
caps.latest.revision: 32
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4e8e167f42a2f00553f1462db058e1b4e6d81b0f
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2019
ms.locfileid: "74302565"
---
# <a name="extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel"></a>Estendendo testes de IU codificado e gravações da ação para dar suporte ao Microsoft Excel
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A estrutura de teste para testes de IU codificados e gravações da ação não dá suporte a todas as interfaces do usuário possíveis. Ele pode não dar suporte à interface do usuário específica que você deseja testar. Por exemplo, você não pode criar imediatamente um teste de IU codificado ou uma gravação da ação para uma planilha [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)]. No entanto, você pode criar sua própria extensão para a estrutura de teste de IU codificado que dará suporte a interface do usuário específica, tirando proveito da extensibilidade da estrutura de teste de IU codificado. O tópico a seguir fornece um exemplo de como estender a estrutura para dar suporte à criação de testes de UI codificados e gravações da ação para [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)]. Para obter mais informações sobre as plataformas que têm suporte, consulte [Configurações e Plataformas com Suporte para Testes de IU Codificados e Gravações da Ação](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md).

 **Requisitos**

- Visual Studio Enterprise

  Esta seção apresenta uma extensão de teste de IU codificado que pode gravar e reproduzir testes de planilhas do Excel. Cada parte da extensão é explicada nesta seção e nos comentários do código para desenvolvedores que desejam criar uma extensão desse tipo.

  ![Arquitetura de teste da interface do usuário](../test/media/ui-testarch.png "UI_TestArch") Visão geral da arquitetura

## <a name="download-the-sample"></a>Baixar a amostra
 A amostra consiste de quatro projetos na solução `CodedUIExtensibilitySample.sln`:

- CodedUIextensibilitySample

- ExcelCodedUIAddInHelper

- ExcelUICommunicationHelper

- SampleTestProject

  Obtenha a amostra desta [postagem de blog](https://go.microsoft.com/fwlink/?LinkID=185592).

> [!NOTE]
> A amostra é destinada para uso com o Microsoft Excel 2010. A amostra pode funcionar com outras versões do Microsoft Excel, mas isso não tem suporte atualmente.

## <a name="details-about-the-sample"></a>Detalhes sobre a amostra
 As seções a seguir fornecem informações sobre a amostra e sua estrutura.

### <a name="microsoft-excel-add-in-excelcodeduiaddinhelper"></a>Suplemento do Microsoft Excel: ExcelCodedUIAddinHelper
 Este projeto inclui um suplemento que é executado no processo do Excel. Consulte [Suplemento de exemplo do Excel para testes de IU codificados](../test/sample-excel-add-in-for-coded-ui-testing.md) para obter uma visão geral sobre o projeto de suplemento.

 Para obter mais informações, consulte [Passo a passo: criando o primeiro suplemento do VSTO para Excel](https://msdn.microsoft.com/library/a855e2be-3ecf-4112-a7f5-ec0f7fad3b5f).

### <a name="excel-ui-communication-exceluicommunicationhelper"></a>Comunicação de interface do usuário do Excel: ExcelUIcommunicationHelper
 Esse projeto inclui a interface `IExcelUICommunication` e as classes de informações que são usadas para passar dados entre o Excel e estrutura de testes de IU codificados. Para obter mais informações, consulte [Interface de comunicador do Excel de amostra](../test/sample-excel-communicator-interface.md).

### <a name="coded-ui-test-extension-codeduiexentsibilitysample"></a>Extensão de teste de IU codificado: CodedUIExentsibilitySample
 Esse projeto inclui as classes personalizadas que são usadas em testes de uma planilha do Excel. O código para cada uma dessas classes é bastante autoexplicativo. No entanto, fornecemos uma breve descrição de cada classe personalizada. Para obter mais informações, consulte [Extensão de teste de IU codificado de exemplo para Excel](../test/sample-coded-ui-test-extension-for-excel.md).

### <a name="deploying-your-add-in-and-extension"></a>Implantando o suplemento e a extensão
 Depois de criar todos os projetos e objetos, execute o arquivo `CopyDrop.bat` fornecido como um administrador. Esse arquivo copia os arquivos DLL e PDB de `ExcelCodedUIAddinHelper` para:

 "`%CommonProgramFiles(x86)%\Microsoft Shared\VSTT\<version number>\UITestExtensionPackages\*.*`", em que o número de versão pode ser 11.0, 12.0, etc., com base em sua versão do Visual Studio.

 Os arquivos DLL e PDB `ExcelUICommunicationHelper` são copiados para `"%ProgramFiles(x86)%\Microsoft Visual Studio <version number>\Common7\IDE\PrivateAssemblies”`.

 Talvez você precise ajustar os caminhos de cópia exatos, mas nenhuma instalação adicional será necessária. Em um computador de 64 bits, use o prompt de comando do Visual Studio Enterprise de 32 bits para executar o arquivo `CopyDrop.bat`.

### <a name="testing-excel-with-the-sampletestproject"></a>Testando o Excel com o SampleTestProject
 Você pode executar o teste no projeto de teste fornecido que usa uma versão específica do Excel que talvez você não tenha ou então criar seu próprio projeto de teste e gravar um teste de sua preferência. Para obter mais informações, consulte [Criar um Teste de IU Codificado](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate).

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider>
- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement>
- [UITestActionFilter](/previous-versions/visualstudio/visual-studio-2012/dd985757(v=vs.110))
- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage>
- [Usar automação de interface do usuário para testar código](../test/use-ui-automation-to-test-your-code.md)
- [Melhores práticas para testes de IU codificados](../test/best-practices-for-coded-ui-tests.md)
- [Configurações e plataformas com suporte para testes de IU codificados e gravações das ações](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
