---
title: Usando Microsoft.VisualStudio.TestTools.CppUnitTestFramework | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d1ac9188-d79f-407e-9f3a-80dbefa66317
caps.latest.revision: 10
ms.author: gewarren
manager: douge
ms.openlocfilehash: 68f083bf6aa99177f6b9e697be8affa5d29804a8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49889601"
---
# <a name="using-microsoftvisualstudiotesttoolscppunittestframework"></a>Usando Microsoft.VisualStudio.TestTools.CppUnitTestFramework
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico lista os membros públicos do namespace `Microsoft::VisualStudio::CppUnitTestFramework`.  
  
 Os arquivos de cabeçalho estão localizados na pasta _VisualStudio2012[x86]InstallFolder_**\VC\UnitTest\include**.  
  
 Os arquivos lib estão localizados na pasta _VisualStudio2012[x86]InstallFolder_**\VC\UnitTest\lib**.  
  
##  <a name="BKMK_In_this_topic"></a> Neste tópico  
 [CppUnitTest.h](#BKMK_CppUnitTest_h)  
  
- [Criar classes de teste e métodos](#BKMK_Create_test_classes_and_methods)  
  
- [Inicialização e limpeza](#BKMK_Initialize_and_cleanup)  
  
  -   [Métodos de teste](#BKMK_Test_methods)  
  
  -   [Classes de teste](#BKMK_Test_classes)  
  
  -   [Módulos de teste](#BKMK_Test_modules)  
  
- [Criar atributos de teste](#BKMK_Create_test_attributes)  
  
  - [Atributos de método de teste](#BKMK_Test_method_attributes)  
  
  - [Atributos de classe de teste](#BKMK_Test_class_attributes)  
  
  - [Atributos de módulo de teste](#BKMK_Test_module_attributes)  
  
  - [Atributos predefinidos](#BKMK_Pre_defined_attributes)  
  
    [CppUnitTestAssert.h](#BKMK_CppUnitTestAssert_h)  
  
  - [Declarações Gerais](#BKMK_General_Asserts)  
  
    -   [São iguais](#BKMK_General_Are_Equal)  
  
    -   [Não são iguais](#BKMK_General_Are_Not_Equal)  
  
    -   [São os mesmos](#BKMK_General_Are_Same)  
  
    -   [Não são os mesmos](#BKMK_General_Are_Not_Same)  
  
    -   [É nulo](#BKMK_General_Is_Null)  
  
    -   [Não é nulo](#BKMK_General_Is_Not_Null)  
  
    -   [É True](#BKMK_General_Is_True)  
  
    -   [É False](#BKMK_General_Is_False)  
  
    -   [Falha](#BKMK_General_Fail)  
  
  - [Declarações do Windows Runtime](#BKMK_WinRT_Asserts)  
  
    -   [São iguais](#BKMK_WinRT_Are_Equal)  
  
    -   [São os mesmos](#BKMK_WinRT_Are_Same)  
  
    -   [Não são iguais](#BKMK_WinRT_Are_Not_Equal)  
  
    -   [Não são os mesmos](#BKMK_WinRT_Are_Not_Same)  
  
    -   [É nulo](#BKMK_WinRT_Is_Null)  
  
    -   [Não é nulo](#BKMK_WinRT_Is_Not_Null)  
  
  - [Declarações de Exceção](#BKMK_Exception_Asserts)  
  
    - [Exceção de Espera](#BKMK_Expect_Exception)  
  
      [CppUnitTestLogger.h](#BKMK_CppUnitTestLogger_h)  
  
    - [Logger](#BKMK_Logger)  
  
    - [Gravar Mensagem](#BKMK_Write_Message)  
  
##  <a name="BKMK_CppUnitTest_h"></a> CppUnitTest.h  
  
###  <a name="BKMK_Create_test_classes_and_methods"></a> Criar classes de teste e métodos  
  
```cpp  
TEST_CLASS(className)  
```  
  
 Necessário para cada classe que contém métodos de teste. Identifica *className* como uma classe de teste. `TEST_CLASS` deve ser declarado no escopo do namescape.  
  
```cpp  
TEST_METHOD(methodName)   
{  
    // test method body  
}  
  
```  
  
 Define *methodName* como um método de teste. `TEST_METHOD` deve ser declarado no escopo da classe do método.  
  
###  <a name="BKMK_Initialize_and_cleanup"></a> Inicialização e limpeza  
  
####  <a name="BKMK_Test_methods"></a> Métodos de teste  
  
```cpp  
TEST_METHOD_INITIALIZE(methodName)   
{  
    // method initialization code  
}  
  
```  
  
 Define *methodName* como um método executado antes de cada método de teste ser executado. `TEST_METHOD_INITIALIZE` só pode ser definido uma vez em uma classe de teste e deve ser definido na classe de teste.  
  
```cpp  
TEST_METHOD_CLEANUP(methodName)   
{  
    // test method cleanup  code  
}  
  
```  
  
 Define *methodName* como um método executado após de cada método de teste ser executado. `TEST_METHOD_CLEANUP` só pode ser definido uma vez em uma classe de teste e deve ser definido no escopo da classe de teste.  
  
####  <a name="BKMK_Test_classes"></a> Classes de teste  
  
```cpp  
TEST_CLASS_INITIALIZE(methodName)   
{  
    // test class initialization  code  
}  
  
```  
  
 Define *methodName* como um método executado após de cada classe de teste ser executada. `TEST_CLASS_INITIALIZE` só pode ser definido uma vez em uma classe de teste e deve ser definido no escopo da classe de teste.  
  
```cpp  
TEST_CLASS_CLEANUP(methodName)   
{  
    // test class cleanup  code  
}  
  
```  
  
 Define *methodName* como um método executado após de cada classe de teste ser executada. `TEST_CLASS_CLEANUP` só pode ser definido uma vez em uma classe de teste e deve ser definido no escopo da classe de teste.  
  
####  <a name="BKMK_Test_modules"></a> Módulos de teste  
  
```cpp  
TEST_MODULE_INITIALIZE(methodName)  
{  
    // module initialization code  
}  
```  
  
 Define o método *methodName* executado quando um módulo é carregado. `TEST_MODULE_INITIALIZE` só pode ser definido uma vez em um módulo de teste e deve ser declarado no escopo do namespace.  
  
```cpp  
TEST_MODULE_CLEANUP(methodName)  
```  
  
 Define o método *methodName* executado quando um módulo é descarregado. `TEST_MODULE_CLEANUP` só pode ser definido uma vez em um módulo de teste e deve ser declarado no escopo do namespace.  
  
###  <a name="BKMK_Create_test_attributes"></a> Criar atributos de teste  
  
####  <a name="BKMK_Test_method_attributes"></a> Atributos de método de teste  
  
```cpp  
BEGIN_TEST_METHOD_ATTRIBUTE(testMethodName)   
    TEST_METHOD_ATTRIBUTE(attributeName, attributeValue)  
    ...  
END_TEST_METHOD_ATTRIBUTE()  
```  
  
 Adiciona os atributos definidos com um ou mais macros `TEST_METHOD_ATTRIBUTE` ao método de teste *testClassName*.  
  
 Uma macro `TEST_METHOD_ATTRIBUTE` define um atributo com o nome *attributeName* e o valor *attributeValue*.  
  
####  <a name="BKMK_Test_class_attributes"></a> Atributos de classe de teste  
  
```cpp  
BEGIN_TEST_CLASS_ATTRIBUTE(testClassName)   
    TEST_CLASS_ATTRIBUTE(attributeName, attributeValue)  
    ...  
END_TEST_CLASS_ATTRIBUTE()  
```  
  
 Adiciona os atributos definidos com um ou mais macros `TEST_CLASS_ATTRIBUTE` à classe de teste *testClassName*.  
  
 Uma macro `TEST_CLASS_ATTRIBUTE` define um atributo com o nome *attributeName* e o valor *attributeValue*.  
  
####  <a name="BKMK_Test_module_attributes"></a> Atributos de módulo de teste  
  
```cpp  
BEGIN_TEST_MODULE_ATTRIBUTE(testModuleName)   
    TEST_MODULE_ATTRIBUTE(attributeName, attributeValue)  
    ...  
END_TEST_MODULE_ATTRIBUTE()  
```  
  
 Adiciona os atributos definidos com um ou mais macros `TEST_MODULE_ATTRIBUTE` ao módulo de teste *testModuleName*.  
  
 Uma macro `TEST_MODULE_ATTRIBUTE` define um atributo com o nome *attributeName* e o valor *attributeValue*.  
  
####  <a name="BKMK_Pre_defined_attributes"></a> Atributos predefinidos  
 Essas macros de atributo predefinidas podem ser substituídas pelas macros `TEST_METHOD_ATTRIBUTE`, `TEST_CLASS_ATTRIBUTE` OU `TEST_MODULE_ATTRIBUTE` descritas anteriormente.  
  
```cpp  
TEST_OWNER(ownerAlias)  
```  
  
 Define um atributo com o nome `Owner` e o valor de atributo de *ownerAlias*.  
  
```cpp  
TEST_DESCRIPTION(description)  
```  
  
 Define um atributo com o nome `Description` e o valor de atributo de *description*.  
  
```cpp  
TEST_PRIORITY(priority)  
```  
  
 Define um atributo com o nome `Priority` e o valor de atributo de *priority*.  
  
```cpp  
TEST_WORKITEM(workitem)  
```  
  
 Define um atributo com o nome `WorkItem` e o valor de atributo de *workItem*.  
  
```cpp  
TEST_IGNORE()  
```  
  
 Define um atributo com o nome `Ignore` e o valor de atributo de `true`.  
  
##  <a name="BKMK_CppUnitTestAssert_h"></a> CppUnitTestAssert.h  
  
###  <a name="BKMK_General_Asserts"></a> Declarações Gerais  
  
####  <a name="BKMK_General_Are_Equal"></a> São iguais  
 Verifica se dois objetos são iguais  
  
```cpp  
template<typename T>   
static void AreEqual(  
    const T& expected,   
    const T& actual,   
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
 Verifica se dois duplos são iguais  
  
```cpp  
static void AreEqual(  
    double expected,   
    double actual,   
    double tolerance,   
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
 Verifica se dois floats são iguais  
  
```cpp  
static void AreEqual(  
    float expected,   
    float actual,   
    float tolerance,   
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
 Verifica se duas cadeias de caracteres char* são iguais  
  
```cpp  
static void AreEqual(  
    const char* expected,   
    const char* actual,   
    bool ignoreCase = false,   
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
 Verifica se duas cadeias de caracteres w_char* são iguais  
  
```cpp  
static void AreEqual(  
    const wchar_t* expected,   
    const wchar_t* actual,   
    bool ignoreCase = false,   
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
####  <a name="BKMK_General_Are_Not_Equal"></a> Não são iguais  
 Verifica se dois duplos não são iguais  
  
```cpp  
static void AreNotEqual(  
    double notExpected,   
    double actual,   
    double tolerance,   
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
 Verifica se dois floats não são iguais  
  
```cpp  
static void AreNotEqual(  
    float notExpected,   
    float actual,   
    float tolerance,   
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
 Verifica se duas cadeias de caracteres char* não são iguais  
  
```cpp  
static void AreNotEqual(  
    const char* notExpected,   
    const char* actual,   
    bool ignoreCase = false,   
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
 Verifica se duas cadeias de caracteres w_char* não são iguais  
  
```cpp  
static void AreNotEqual(  
    const wchar_t* notExpected,   
    const wchar_t* actual,   
    bool ignoreCase = false,   
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
 Verifique se duas referências não são iguais com base em operator==.  
  
```cpp  
template<typename T>   
static void AreNotEqual(  
    const T& notExpected,   
    const T& actual,   
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
####  <a name="BKMK_General_Are_Same"></a> São os mesmos  
 Verifica se duas referências indicam a mesma instância de objeto (identidade).  
  
```cpp  
template<typename T>   
static void AreSame(  
    const T& expected,   
    const T& actual,   
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
####  <a name="BKMK_General_Are_Not_Same"></a> Não são os mesmos  
 Verifica se duas referências não indicam a mesma instância de objeto (identidade).  
  
```cpp  
template<typename T>   
static void AreNotSame (  
    const T& notExpected,   
    const T& actual,   
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
####  <a name="BKMK_General_Is_Null"></a> É nulo  
 Verifica se um ponteiro é NULO.  
  
```cpp  
template<typename T>   
static void IsNull(  
    const T* actual,  
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
####  <a name="BKMK_General_Is_Not_Null"></a> Não é nulo  
 Verifica se um ponteiro não é NULO  
  
```cpp  
template<typename T>   
static void IsNotNull(  
    const T* actual,   
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
####  <a name="BKMK_General_Is_True"></a> É True  
 Verifica se uma condição é true  
  
```cpp  
static void IsTrue(  
    bool condition,   
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
####  <a name="BKMK_General_Is_False"></a> É False  
 Verifica se uma condição é false  
  
```cpp  
static void IsFalse(  
    bool condition,   
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
####  <a name="BKMK_General_Fail"></a> Falha  
 Força a falha do resultado do caso de teste  
  
```cpp  
static void Fail(  
    const wchar_t* message = NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
###  <a name="BKMK_WinRT_Asserts"></a> Declarações do Windows Runtime  
  
####  <a name="BKMK_WinRT_Are_Equal"></a> São iguais  
 Verifica se dois ponteiros do Windows Runtime são iguais.  
  
```  
template<typename T>   
static void AreEqual(  
    T^ expected,   
    T^ actual,   
    Platform::String^ message = nullptr,   
    const __LineInfo* pLineInfo= nullptr)  
```  
  
 Verifica se duas cadeias de caracteres Platform::String^ são iguais.  
  
```  
template<typename T>   
static void AreEqual(  
    T^ expected,   
    T^ actual,   
    Platform::String^ message= nullptr,   
    const __LineInfo* pLineInfo= nullptr)  
```  
  
####  <a name="BKMK_WinRT_Are_Same"></a> São os mesmos  
 Verifica se duas referências do Windows Runtime referenciam o mesmo objeto.  
  
```  
template<typename T>   
static void AreSame(  
    T% expected,   
    T% actual,   
    Platform::String^ message= nullptr,   
    const __LineInfo* pLineInfo= nullptr)  
```  
  
####  <a name="BKMK_WinRT_Are_Not_Equal"></a> Não são iguais  
 Verifica se dois ponteiros do Windows Runtime não são iguais.  
  
```  
template<typename T>   
static void AreNotEqual(  
    T^ notExpected,   
    T^ actual,   
    Platform::String^ message = nullptr,   
    const __LineInfo* pLineInfo= nullptr)  
```  
  
 Verifica se duas cadeias de caracteres Platform::String^ não são iguais.  
  
```  
static void AreNotEqual(  
    Platform::String^ notExpected,   
    Platform::String^ actual,   
    bool ignoreCase = false,   
    Platform::String^ message= nullptr,   
    const __LineInfo* pLineInfo= nullptr)  
```  
  
####  <a name="BKMK_WinRT_Are_Not_Same"></a> Não são os mesmos  
 Verifica se duas referências do Windows Runtime não referenciam o mesmo objeto.  
  
```  
template<typename T>   
static void AreNotSame(  
    T% notExpected,   
    T% actual,   
    Platform::String^ message= nullptr,   
    const __LineInfo* pLineInfo= nullptr)  
```  
  
####  <a name="BKMK_WinRT_Is_Null"></a> É nulo  
 Verifica se um ponteiro do Windows Runtime é um nullptr.  
  
```  
template<typename T>   
static void IsNull(  
    T^ actual,  
    Platform::String^ message = nullptr,   
    const __LineInfo* pLineInfo= nullptr)  
```  
  
####  <a name="BKMK_WinRT_Is_Not_Null"></a> Não é nulo  
 Verifica se um ponteiro do Windows Runtime não é um nullptr.  
  
```  
template<typename T>   
static void IsNotNull(  
    T^ actual,   
    Platform::String^ message= nullptr,   
    const __LineInfo* pLineInfo= nullptr)  
```  
  
###  <a name="BKMK_Exception_Asserts"></a> Declarações de Exceção  
  
####  <a name="BKMK_Expect_Exception"></a> Exceção de Espera  
 Verifica se uma função gera uma exceção:  
  
```  
template<typename _EXPECTEDEXCEPTION, typename _FUNCTOR>   
static void ExpectException(  
    _FUNCTOR functor,   
    const wchar_t* message= NULL,   
    const __LineInfo* pLineInfo= NULL)  
```  
  
 Verifica se uma função gera uma exceção:  
  
```  
template<typename _EXPECTEDEXCEPTION, typename _RETURNTYPE>   
    static void ExpectException(  
    _RETURNTYPE (*func)(),   
    const wchar_t* message= NULL,   
    const __LineInfo* pLineInfo = NULL)  
```  
  
##  <a name="BKMK_CppUnitTestLogger_h"></a> CppUnitTestLogger.h  
  
###  <a name="BKMK_Logger"></a> Logger  
 A classe Logger contém métodos estáticos para gravar  
  
```  
class Logger  
```  
  
###  <a name="BKMK_Write_Message"></a> Gravar Mensagem  
  
```  
static void   
Logger::WriteMessage(const wchar_t* message)  
```  
  
```  
static void   
Logger::WriteMessage(const char* message)  
```  
  
## <a name="example"></a>Exemplo  
 Esse código é um exemplo de  
  
```  
////////////////////////////////////////////////////////////  
/* USAGE EXAMPLE  
// The following is an example of VSCppUnit usage.  
// It includes examples of attribute metadata, fixtures,  
// unit tests with assertions, and custom logging.  
  
#include <CppUnitTest.h>  
  
using namespace Microsoft::VisualStudio::CppUnitTestFramework;  
  
BEGIN_TEST_MODULE_ATTRIBUTE()  
    TEST_MODULE_ATTRIBUTE(L"Date", L"2010/6/12")  
END_TEST_MODULE_ATTRIBUTE()  
  
TEST_MODULE_INITIALIZE(ModuleInitialize)  
{  
    Logger::WriteMessage("In Module Initialize");  
}  
  
TEST_MODULE_CLEANUP(ModuleCleanup)  
{  
    Logger::WriteMessage("In Module Cleanup");  
}  
  
TEST_CLASS(Class1)  
{  
  
public:  
  
    Class1()  
    {  
        Logger::WriteMessage("In Class1");  
    }  
  
    ~Class1()  
    {  
        Logger::WriteMessage("In ~Class1");  
    }  
  
    TEST_CLASS_INITIALIZE(ClassInitialize)  
    {  
        Logger::WriteMessage("In Class Initialize");  
    }  
  
    TEST_CLASS_CLEANUP(ClassCleanup)  
    {  
        Logger::WriteMessage("In Class Cleanup");  
    }  
  
    BEGIN_TEST_METHOD_ATTRIBUTE(Method1)  
        TEST_OWNER(L"OwnerName")  
        TEST_PRIORITY(1)  
    END_TEST_METHOD_ATTRIBUTE()  
  
    TEST_METHOD(Method1)  
    {     
        Logger::WriteMessage("In Method1");  
        Assert::AreEqual(0, 0);  
    }  
  
    TEST_METHOD(Method2)  
    {  
        Assert::Fail(L"Fail");  
    }  
};  
```  
  
## <a name="see-also"></a>Consulte também  
 [Efetuar teste de unidade em seu código](../test/unit-test-your-code.md)   
 [Código nativo de testes de unidade com o Gerenciador de Testes](http://msdn.microsoft.com/en-us/8a09d6d8-3613-49d8-9ffe-11375ac4736c)   
 [Adicionando testes de unidade a aplicativos do C++ existentes](../test/unit-testing-existing-cpp-applications-with-test-explorer.md)



