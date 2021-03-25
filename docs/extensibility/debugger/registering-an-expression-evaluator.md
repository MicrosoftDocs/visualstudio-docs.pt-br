---
title: Registrando um avaliador de expressão | Microsoft Docs
description: Saiba como o avaliador de expressão deve se registrar como uma fábrica de classes com o ambiente COM do Windows e o Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluators, registering
ms.assetid: 236be234-e05f-4ad8-9200-24ce51768ecf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3cf6998a9dd8bc521d8d5c7b8bd3e598e9a4e3bc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070642"
---
# <a name="register-an-expression-evaluator"></a>Registrar um avaliador de expressão
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 O avaliador de expressão (EE) deve se registrar como uma fábrica de classes com o ambiente COM do Windows e o Visual Studio. Um EE é configurado como uma DLL para que seja injetado no espaço DE endereço do mecanismo de depuração (DE) ou no espaço de endereço do Visual Studio, dependendo de qual entidade instancia o EE.

## <a name="managed-code-expression-evaluator"></a>Avaliador de expressão de código gerenciado
 Um EE de código gerenciado é implementado como uma biblioteca de classes, que é uma DLL que se registra com o ambiente COM, normalmente iniciado por uma chamada para o programa VSIP, *regpkg.exe*. O processo real de gravar as chaves do registro para o ambiente COM é manipulado automaticamente.

 Um método da classe principal é marcado com <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> , indicando que o método deve ser chamado quando a dll está sendo registrada com com. Esse método de registro, geralmente chamado `RegisterClass` , executa a tarefa de registrar a dll com o Visual Studio. Um correspondente `UnregisterClass` (marcado com o <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute> ), desfaz os efeitos de `RegisterClass` quando a dll é desinstalada.
As mesmas entradas de registro são feitas como para um EE gravado em código não gerenciado; a única diferença é que não há nenhuma função auxiliar, como `SetEEMetric` fazer o trabalho para você. Veja a seguir um exemplo do processo de registro e cancelamento de registro.

### <a name="example"></a>Exemplo
 A função a seguir mostra como um código gerenciado EE registra e cancela o registro em si com o Visual Studio.

```csharp
namespace EEMC
{
    [GuidAttribute("462D4A3D-B257-4AEE-97CD-5918C7531757")]
    public class EEMCClass : IDebugExpressionEvaluator
    {
        #region Register and unregister.
        private static Guid guidMycLang = new Guid("462D4A3E-B257-4AEE-97CD-5918C7531757");
        private static string languageName = "MyC";
        private static string eeName = "MyC Expression Evaluator";

        private static Guid guidMicrosoftVendor = new Guid("994B45C4-E6E9-11D2-903F-00C04FA302A1");
        private static Guid guidCOMPlusOnlyEng = new Guid("449EC4CC-30D2-4032-9256-EE18EB41B62B");
        private static Guid guidCOMPlusNativeEng = new Guid("92EF0900-2251-11D2-B72E-0000F87572EF");

        /// <summary>
        /// Register the expression evaluator.
        /// Set "project properties/configuration properties/build/register for COM interop" to true.
        /// </summary>
         [ComRegisterFunctionAttribute]
        public static void RegisterClass(Type t)
        {
            // Get Visual Studio version (set by regpkg.exe)
            string hive = Environment.GetEnvironmentVariable("EnvSdk_RegKey");
            string s = @"SOFTWARE\Microsoft\VisualStudio\"
                        + hive
                        + @"\AD7Metrics\ExpressionEvaluator";

            RegistryKey rk = Registry.LocalMachine.CreateSubKey(s);
            if (rk == null)  return;

            rk = rk.CreateSubKey(guidMycLang.ToString("B"));
            rk = rk.CreateSubKey(guidMicrosoftVendor.ToString("B"));
            rk.SetValue("CLSID", t.GUID.ToString("B"));
            rk.SetValue("Language", languageName);
            rk.SetValue("Name", eeName);

            rk = rk.CreateSubKey("Engine");
            rk.SetValue("0", guidCOMPlusOnlyEng.ToString("B"));
            rk.SetValue("1", guidCOMPlusNativeEng.ToString("B"));
        }
        /// <summary>
        /// Unregister the expression evaluator.
        /// </summary>
         [ComUnregisterFunctionAttribute]
        public static void UnregisterClass(Type t)
        {
            // Get Visual Studio version (set by regpkg.exe)
            string hive = Environment.GetEnvironmentVariable("EnvSdk_RegKey");
            string s = @"SOFTWARE\Microsoft\VisualStudio\"
                        + hive
                        + @"\AD7Metrics\ExpressionEvaluator\"
                        + guidMycLang.ToString("B");
            RegistryKey key = Registry.LocalMachine.OpenSubKey(s);
            if (key != null)
            {
                key.Close();
                Registry.LocalMachine.DeleteSubKeyTree(s);
            }
        }
    }
}
```

## <a name="unmanaged-code-expression-evaluator"></a>Avaliador de expressão de código não gerenciado
 A DLL do EE implementa a `DllRegisterServer` função para se registrar com o ambiente com, bem como com o Visual Studio.

> [!NOTE]
> Você pode encontrar o código do registro de exemplo de código MyCEE no arquivo *Dllentry. cpp*, que está localizado na instalação do VSIP em EnVSDK\MyCPkgs\MyCEE.

### <a name="dll-server-process"></a>Processo do servidor DLL
 Ao registrar o EE, o servidor DLL:

1. Registra sua fábrica `CLSID` de classes de acordo com as convenções com normais.

2. Chama a função auxiliar `SetEEMetric` para registrar com o Visual Studio as métricas do EE mostradas na tabela a seguir. A função `SetEEMetric` e as métricas especificadas da seguinte maneira são parte da biblioteca *dbgmetric. lib* . Consulte [auxiliares do SDK para depuração](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) para obter detalhes.

    |Métrica|Descrição|
    |------------|-----------------|
    |`metricCLSID`|`CLSID` da fábrica de classes do EE|
    |`metricName`|Nome do EE como uma cadeia de caracteres de exibição|
    |`metricLanguage`|O nome do idioma que o EE foi projetado para avaliar|
    |`metricEngine`|`GUID`s dos mecanismos de depuração que funcionam com este EE|

    > [!NOTE]
    > O `metricLanguage``GUID` identifica o idioma por nome, mas é o `guidLang` argumento para `SetEEMetric` o que seleciona o idioma. Quando o compilador gera o arquivo de informações de depuração, ele deve gravar o apropriado `guidLang` para que o saiba qual EE usar. O DE normalmente solicita ao provedor de símbolos esse idioma `GUID` , que é armazenado no arquivo de informações de depuração.

3. Registra-se no Visual Studio criando chaves em HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\ *x. y*, em que *x. y* é a versão do Visual Studio com a qual se registrar.

### <a name="example"></a>Exemplo
 A função a seguir mostra como um código não gerenciado (C++) EE registra e cancela o registro em si com o Visual Studio.

```cpp
/*---------------------------------------------------------
  Registration
-----------------------------------------------------------*/
#ifndef LREGKEY_VISUALSTUDIOROOT
    #define LREGKEY_VISUALSTUDIOROOT L"Software\\Microsoft\\VisualStudio\\8.0"
#endif

static HRESULT RegisterMetric( bool registerIt )
{
    // check where we should register
    const ULONG cchBuffer = _MAX_PATH;
    WCHAR wszRegistrationRoot[cchBuffer];
    DWORD cchFreeBuffer = cchBuffer - 1;
    wcscpy(wszRegistrationRoot, LREGKEY_VISUALSTUDIOROOT_NOVERSION);
    wcscat(wszRegistrationRoot, L"\\");

    // this is Environment SDK specific
    // we check for  EnvSdk_RegKey environment variable to
    // determine where to register
    DWORD cchDefRegRoot = lstrlenW(LREGKEY_VISUALSTUDIOROOT_NOVERSION) + 1;
    cchFreeBuffer = cchFreeBuffer - cchDefRegRoot;
    DWORD cchEnvVarRead = GetEnvironmentVariableW(
        /* LPCTSTR */ L"EnvSdk_RegKey", // environment variable name
        /* LPTSTR  */ &wszRegistrationRoot[cchDefRegRoot],// buffer for variable value
        /* DWORD   */ cchFreeBuffer);// size of buffer
    if (cchEnvVarRead >= cchFreeBuffer)
        return E_UNEXPECTED;
    // If the environment variable does not exist then we must use
    // LREGKEY_VISUALSTUDIOROOT which has the version number.
    if (0 == cchEnvVarRead)
        wcscpy(wszRegistrationRoot, LREGKEY_VISUALSTUDIOROOT);

    if (registerIt)
    {
        SetEEMetric(guidMycLang,
                    guidMicrosoftVendor,
                    metricCLSID,
                    CLSID_MycEE,
                    wszRegistrationRoot );
        SetEEMetric(guidMycLang,
                    guidMicrosoftVendor,
                    metricName,
                    GetString(IDS_INFO_MYCDESCRIPTION),
                    wszRegistrationRoot );
        SetEEMetric(guidMycLang,
                    guidMicrosoftVendor,
                    metricLanguage, L"MyC",
                    wszRegistrationRoot);

        GUID engineGuids[2];
        engineGuids[0] = guidCOMPlusOnlyEng;
        engineGuids[1] = guidCOMPlusNativeEng;
        SetEEMetric(guidMycLang,
                    guidMicrosoftVendor,
                    metricEngine,
                    engineGuids,
                    2,
                    wszRegistrationRoot);
    }
    else
    {
        RemoveEEMetric( guidMycLang,
                        guidMicrosoftVendor,
                        metricCLSID,
                        wszRegistrationRoot);
        RemoveEEMetric( guidMycLang,
                        guidMicrosoftVendor,
                        metricName,
                        wszRegistrationRoot );
        RemoveEEMetric( guidMycLang,
                        guidMicrosoftVendor,
                        metricLanguage,
                        wszRegistrationRoot );
        RemoveEEMetric( guidMycLang,
                        guidMicrosoftVendor,
                        metricEngine,
                        wszRegistrationRoot );
    }

    return S_OK;
}
```

## <a name="see-also"></a>Confira também
- [Escrevendo um avaliador de expressão CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [Auxiliares do SDK para depuração](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
