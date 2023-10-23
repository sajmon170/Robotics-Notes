
# Dodawanie ścieżek biblioteki do skryptu budującego
Pierwszym krokiem jest wykonanie czynności odpowiadających podaniu opcji `-I` i `-L` do kompilatora, z tym, że w unrealu nie bardzo mamy dostęp bezpośrednio do wywołania kompilatora, więc trzeba to zrobić poprzez skrypt w c#, który przygotowuje projekt. Otwieramy plik \<katalog projektu\>/Source/\<nazwa projektu\>/\<nazwa projektu\>.Build.cs

Do skryptu dodajemy dwie linijki w konstruktorze klasy nazywającej się tak jak nasz projekt:

```
PublicIncludePaths.AddRange(new string[]{
			"/usr/include",
			"/usr/include/python3.10",
			"/usr/include/x86_64-linux-gnu",
			"/usr/include/x86_64-linux-gnu/python3.10",
			"/usr/include/features.h"
		});
```
^ Dodanie ścieżek do nagłówków, jak -I

Ścieżki są przykładowe, u mnie działają takie, w większości przypadków jak masz python3.10 raczej powinny takie działać

```
PublicAdditionalLibraries.AddRange(new string[]{
			"/usr/lib/x86_64-linux-gnu/libpython3.10.so"
		});
```
^ Dodanie ścieżek do bibliotek: -L

Podobnie lepiej sprawdzić czy ta biblioteka rzeczywiście tu jest, u mnie działa taka ścieżka.

Ostatecznie skrypt może przykładowo wyglądać w ten sposób:
```
// Copyright Epic Games, Inc. All Rights Reserved.

using UnrealBuildTool;

public class MyProject4 : ModuleRules
{
	public MyProject4(ReadOnlyTargetRules Target) : base(Target)
	{
		PCHUsage = PCHUsageMode.UseExplicitOrSharedPCHs;

		PublicDependencyModuleNames.AddRange(new string[] { "Core", "CoreUObject", "Engine", "InputCore", "EnhancedInput" });
	
		// Dodanie ścieżek do nagłówków: -I
		PublicIncludePaths.AddRange(new string[]{
			"/usr/include",
			"/usr/include/python3.10",
			"/usr/include/x86_64-linux-gnu",
			"/usr/include/x86_64-linux-gnu/python3.10",
			"/usr/include/features.h"
		});
		// Dodanie ścieżek do bibliotek: -L
		PublicAdditionalLibraries.AddRange(new string[]{
			"/usr/lib/x86_64-linux-gnu/libpython3.10.so"
		});
	}
}

```

Po tych zmianach we wszystkich plikach nagłówkowych nowotworzonych klas w unrealu `#include <Python.h>` powinno includować nagłówki, a wywołanie funkcji z PyApi jak `Py_Initialize()` powinno być możliwe z metod klasy. 

# UWAGA
Bardzo nie polecam wywoływać metod z PyApi w `Konstruktorze` klasy, ponieważ jest on wywoływany już przy ładowaniu projektu niezależnie czy jakaś instancja tej klasy jest na mapie. Jeżeli coś w konstruktorze wywoła wyjątek to przy otwieraniu projekt będzie się natychmiast wywalał. Zamiast tego lepiej używać niepewnych funkcji w metodzie `BeginPlay`, która wywoływana jest tylko dla instancji obecnych na planszy i dopiero w momencie kliknięcia "play". Na ten moment większość funkcji z PyApi `powoduje segmentation fault`. Nie znam rozwiązania.