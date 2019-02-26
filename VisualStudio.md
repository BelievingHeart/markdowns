[//]: # (#vs #VisualStudio)

## unit test
1. Add a test project to the solution you want to test
2. Right click the test project -> add -> reference -> $project-to-test
3. Right click the test project -> add -> existing item -> the .h and .cpp file of the API to test
4. [Sample](https://docs.microsoft.com/en-us/visualstudio/test/microsoft-visualstudio-testtools-cppunittestframework-api-reference?view=vs-2017#create_test_classes_and_methods)
```cpp
#include "stdafx.h"
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
		TEST_PRIORITY(100)
		END_TEST_METHOD_ATTRIBUTE()

		TEST_METHOD(Method1)
	{
		Logger::WriteMessage("In Method1");
		Assert::AreEqual(0, 0);
	}

	TEST_METHOD(Method2)
	{
		//Assert::Fail(L"Fail");
		Logger::WriteMessage("In Method2");
	}
};
```