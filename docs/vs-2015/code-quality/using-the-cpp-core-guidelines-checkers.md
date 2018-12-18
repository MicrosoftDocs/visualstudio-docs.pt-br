---
title: Usando os verificadores de diretrizes principais do C++ | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a2098fd9-8334-4e95-9b8d-bc3da689d9e3
caps.latest.revision: 11
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: 1153f7a32c26946fafb1230699c4afcae976cd9e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51799555"
---
# <a name="using-the-c-core-guidelines-checkers"></a>Usando os verificadores de diretrizes principais do C++
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Diretrizes principais do C++ são um conjunto portátil de diretrizes, regras e as práticas recomendadas sobre como codificar em C++ criado pelos designers e especialistas em C++.  Visual Studio agora oferece suporte a pacotes suplemento que criar regras adicionais para o código de ferramentas de análise para verificar seu código quanto à conformidade com diretrizes principais do C++ e sugerir melhorias.  
  
## <a name="the-c-core-guidelines-project"></a>O projeto de diretrizes principais do C++  
 Diretrizes principais do C++ criado por Bjarne Stroustrup e outros, são um guia para usar o C++ moderno com segurança e eficácia. As diretrizes enfatizam a segurança de tipo estático e segurança de recursos. Eles identificarem maneiras de eliminar ou minimizar as partes mais propensas a erro da linguagem e sugerem como tornar seu código mais simples e mais eficaz de forma confiável. Essas diretrizes são mantidas pelo Standard C++ Foundation. Para obter mais informações, consulte a documentação [diretrizes principais do C++](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)e acessar os arquivos de projeto de documentação de diretrizes principais do C++ no [GitHub](https://github.com/isocpp/CppCoreGuidelines).  
  
 A Microsoft suporta o esforço de diretrizes principais do C++, fazendo a verificação principal do C++ define de regra de análise de código que você pode adicionar aos seus projetos usando um pacote do Nuget. O pacote é chamado Microsoft.CppCoreCheck e está disponível em [ http://www.nuget.org/packages/Microsoft.CppCoreCheck ](http://www.nuget.org/packages/Microsoft.CppCoreCheck). Este pacote requer que você tem pelo menos o Visual Studio 2015 com atualização 1 instalado.  
  
 O pacote também instala outro pacote como uma dependência, uma biblioteca de suporte diretriz (GSL) somente de cabeçalho. A GSL também está disponível no GitHub em [ https://github.com/Microsoft/GSL ](https://github.com/Microsoft/GSL).  
  
## <a name="enable-the-c-core-check-guidelines-in-code-analysis"></a>Habilitar as diretrizes da verificação principal do C++ na análise de código  
 Para habilitar as ferramentas de análise do código de verificação principal do C++, instale o pacote do Microsoft.CppCoreCheck NuGet para cada projeto de C++ que você deseja verificar no Visual Studio.  
  
#### <a name="to-add-the-microsoftcppcorecheck-package-to-your-project"></a>Para adicionar o pacote de Microsoft.CppCoreCheck ao seu projeto  
  
1. Na **Gerenciador de soluções**, clique com botão direito para abrir o menu de contexto do seu projeto na solução que você deseja adicionar o pacote. Escolher **gerenciar pacotes NuGet** para abrir o **Gerenciador de pacotes NuGet**.  
  
2. No **Gerenciador de pacotes NuGet** janela, procure Microsoft.CppCoreCheck.  
  
    ![Janela Gerenciador de pacotes do NuGet mostra o pacote de CppCoreCheck](../code-quality/media/cppcorecheck-nuget-window.PNG "CPPCoreCheck_Nuget_Window")  
  
3. Selecione o pacote Microsoft.CppCoreCheck e, em seguida, escolha o **instalar** botão para adicionar as regras ao seu projeto.  
  
   O pacote NuGet adiciona um arquivo. targets do MSBuild adicional ao seu projeto que é invocado quando você habilita a análise de código em seu projeto. Esse arquivo. targets adiciona as regras de verificação principal do C++ como uma extensão adicional para a ferramenta de análise de código do Visual Studio.  
  
   Você pode habilitar a análise de código em seu projeto, selecionando o **habilitar análise de código no Build** caixa de seleção na **análise de código** seção o **páginas de propriedade** caixa de diálogo para seu projeto.  
  
   ![Página de propriedades para configurações gerais de análise de código](../code-quality/media/cppcorecheck-codeanalysis-general.png "CPPCoreCheck_CodeAnalysis_General")  
  
   As regras de verificação principal do C++ se tornam parte dos conjuntos de regras padrão que são executados quando a análise de código está habilitada. Como as regras de verificação principal do C++ estão em desenvolvimento, algumas regras podem não estar prontas para uso em todo o código, mas podem ser informativas durante o desenvolvimento. Essas regras são lançadas como experimental. Você pode optar por executar as regras de lançamento ou experimentais nas propriedades de seu projeto.  
  
   ![Página de propriedades para configurações de extensões de análise de código](../code-quality/media/cppcorecheck-codeanalysis-extensions.png "CPPCoreCheck_CodeAnalysis_Extensions")  
  
   Para habilitar ou desabilitar os conjuntos de regra de verificação principal do C++, abra o **páginas de propriedade** caixa de diálogo para seu projeto. Sob **propriedades de configuração**, expanda **análise de código**, **extensões**. Na lista suspensa próxima ao controle **habilitar a verificação principal do C++ (liberados)** ou **Habilitar verificação principal do C++ (Experimental)**, escolha **Sim** ou **não**. Escolher **Okey** ou **aplicar** para salvar suas alterações.  
  
## <a name="check-types-bounds-and-lifetimes"></a>Verifique os tipos, limites e tempos de vida  
 Atualmente, o pacote de verificação principal do C++ contém verificadores para o [segurança de tipo](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#SS-type), [delimita safety](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#SS-bounds), e [segurança de tempo de vida](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#SS-lifetime) perfis.  
  
 Aqui está um exemplo do tipo de problemas que as regras de verificação principal do C++ podem encontrar:  
  
```cpp  
// CoreCheckExample.cpp  
// Add CppCoreCheck package and enable code analysis in build for warnings.  
  
int main()  
{  
    int arr[10];           // warning C26494  
    int* p = arr;          // warning C26485  
  
    [[gsl::suppress(bounds.1)]] // This attribute suppresses Bounds rule #1  
    {  
        int* q = p + 1;    // warning C26481 (suppressed)  
        p = q++;           // warning C26481 (suppressed)  
    }  
  
    return 0;  
}  
```  
  
 Este exemplo demonstra alguns dos avisos que as regras de verificação principal do C++ podem encontrar:  
  
- C26494 é regra Type.5: sempre inicialize um objeto.  
  
- C26485 é regra Bounds.3: decaimento nenhum ponteiro de matriz.  
  
- C26481 é regra Bounds.1: não use aritmética de ponteiro. Use `span` em seu lugar.  
  
  Se o rulesets de análise do código de verificação principal do C++ estão instalado e habilitado quando você compila esse código, os dois primeiros avisos forem gerados, mas o terceiro é suprimido. Aqui está a saída da compilação do código de exemplo:  
  
  **1 >---compilação iniciada: projeto: CoreCheckExample, configuração: Debug Win32 -**  
**----**  
**1 > CoreCheckExample.cpp**  
**1 > CoreCheckExample.vcxproj -> C:\Users\username\documents\visual studio 2015\P**  
**rojects\CoreCheckExample\Debug\CoreCheckExample.exe**  
**1 > CoreCheckExample.vcxproj -> C:\Users\username\documents\visual studio 2015\P**  
**rojects\CoreCheckExample\Debug\CoreCheckExample.PDB (PDB completo)**  
**c:\users\username\documents\visual studio 2015\projects\corecheckexample\coreche**  
**ckexample\corecheckexample.cpp(6): aviso C26494: a variável 'arr' é uninitializ**  
**Ed. sempre inicialize um objeto. (type.5: http://go.microsoft.com/fwlink/p/?Link**  
**ID = 620421)**  
**c:\users\username\documents\visual studio 2015\projects\corecheckexample\coreche**  
**ckexample\corecheckexample.cpp(7): aviso C26485: expressão 'arr': sem matriz para**  
 **ponteiro de decaimento. (bounds.3: http://go.microsoft.com/fwlink/p/?LinkID=620415)**  
**= = = Compilação: 1 com êxito, 0 com falha, 0 atualizada, 0 ignorado = = =** as diretrizes do C++ Core existem para ajudar você a escrever código melhor e mais seguro. No entanto, se você tiver uma instância em que uma regra ou um perfil não deve ser aplicado, é fácil suprimi-lo diretamente no código. Você pode usar o `gsl::suppress` atributo para manter a verificação principal do C++ de detectar e relatar qualquer violação de uma regra no bloco de código a seguir. Você pode marcar instruções individuais para suprimir regras específicas. Você pode até mesmo suprimir todo o perfil limites escrevendo `[[gsl::suppress(bounds)]]` sem incluir um número específico de regra.  
  
## <a name="use-the-guideline-support-library"></a>Use a biblioteca de suporte de diretriz  
 O pacote do Microsoft.CppCoreCheck NuGet também instala um pacote que contém a implementação da Microsoft da biblioteca de suporte de diretriz (GSL). A GSL também está disponível na forma independente em [ http://www.nuget.org/packages/Microsoft.Gsl ](http://www.nuget.org/packages/Microsoft.Gsl). Essa biblioteca é útil se você quiser seguir as diretrizes de núcleo. O GSL inclui definições que permitem que você substitua construções propenso a erro alternativas mais seguras. Por exemplo, você pode substituir uma `T*, length` par de parâmetros com o `span<T>` tipo. O GSL é um software livre, portanto, se você quiser dar uma olhada fontes da biblioteca, comentário ou contribuir com, o projeto pode ser encontrado em [ https://github.com/Microsoft/GSL ](https://github.com/Microsoft/GSL).



