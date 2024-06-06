# Założenie Azure
1. Wejdź na stronę Azure Dev Tools for Teaching: [link](https://aka.ms/devtoolsforteaching)
2. Zaloguj się mailem studenckim i wypełnij formularz na weryfikację statusu studenta (jeśli nie działa Jagielloński, wybierz angielską wersję nazwy).
3. Powinno przekierować na stronę Azure Portal. Jeśli nie ma dostępnych "credits", to w "Education" > "Overview" można odnowić ponowną weryfikacją studenta.
4. Azure Portal powinien pokazywać €92 do wykorzystania.

# Stworzenie bazy CosmosDB
1. Jako student w "Education" > "Overview" w liście "Free services" kliknij "Explore all".
2. Wyszukaj "Azure Cosmos DB" i kliknij "Create".
3. Wybierz "Azure Cosmos DB for NoSQL" i kliknij "Create"
4. W "Resource Group" stwórz nową nazwę i ją wybierz.
5. Subscription musi być ustawione na "Azure for Students"
6. Reszta opcji może pozostać domyślna.
7. Po stworzeniu bazy danych powinien pojawić się ekran główny bazy.  Najważniejszą zakładką w całym projekcie jest "Data Explorer". Stamtąd będzie kontynuowana większość ćwiczeń.

# Ćwiczenia - Azure Portal
1. Stwórz nową bazę danych i kontener za pomocą "New Database" i odpowiednio go skonfiguruj (ustaw max RU/s i odpowiedni Partition key typu /weaponType).
2. Stwórz nowy item za pomocą "New Item". Kluczowe: wypełnij unikalnym id i najlepiej pasującym partition key. Reszta danych może być jakakolwiek. Kliknij "Save".
3. Zaimportuj JSON sampleWeapon.json za pomocą "Upload Item".
4. Zaimportuj resztę plików JSON, by mieć komplet bazy danych.
5. Ćwiczenia na kwerendy:
* Wyfiltruj wszystkie bronie typu ("weaponType") "greatsword" i "katana" bez używania `OR`.
* Wyfiltruj wszystkie bronie, które posiadają "uniqueArt" 
* Wyfiltruj wszystkie bronie, których "attackTypes" posiadają typ ataku magicznego "mag" (`JOIN`).
* Wyfiltruj wszystkie bronie, których "numbers" zawierają liczbę 3.
* Zsumuj wagę wszystkich broni.
* Wyfiltruj wszystkie bronie posiadające więcej niż dwa "requirements" i użyj paginacji po z limitem 2 (`OFFSET LIMIT`).
* Wypisz przedmiotu od najcięższego do najlżejszego.
* Zsumuj wagę wszystkich broni, których średnia "guardTypes" jest pomiędzy 40 a 50 (można użyć udf lub zapytania API).
6. Ćwiczenia UDF - za pomocą UDF (User Defined Functions) można modyfikować kwerendy z pomocą kodu JavaScript. Aby stworzyć UDF, należy w danym kontenerze (UDF są unikalne w obrębie kontenera) wybrać opcję "New UDF". W "User Defined Function Id" wpisz nazwe funkcji, a w body ją zaimplementuj z taką samą nazwą. W kwerendach używa się prefixu `udf.` by wywołać tę funkcję.
* Zaimplementuj funkcję podwajającą wagę przedmiotu i dodającą 3.5. Użyj jej w kwerendzie i pokaż razem z nazwą przedmiotu.
* Zaimplementuj funkcję sprawdzającą, czy element jest mniejszy od 10 lub większy od 20. Przefiltruj za pomocą niego wymagania na siłę "requirements".
* Zaimplementuj funkcję zwiększającą napis (UPPERCASE) i odwracającą go. Użyj jej w kwerendzie dla nazwy przedmiotu i pokaż razem z nim.
7. Ćwiczenia Triggery - za pomocą triggerów można przykładowo modyfikować ciało dodawanego przedmiotu. Istnieją dwa typy triggerów - pre, wykonywane przed operacją (np. dodaniem) do bazy danych, pozwalające np. dodać nowe pole oraz post, wykonywane po operacji bazodanowej, np. wysyłające request na stworzenie logu. Funkcje są pisane w JavaScripcie.
* Zaimplementuj trigger pre dodający nowe pole "addCreated" do każdego nowo dodanego przedmiotu. (pamiętaj o `getContext()`, `getRequest()` i `getBody()`).
* Zaimplementuj trigger pre modyfikujący jedno z pól string (oprócz partition id), dodając na końcu jakiś znak.
8. Ćwiczenia Stored Procedures - procedury składowane jest kod Javascript zapisany i wykonywany bezpośrednio na serwerze CosmosDB. Pozwalają one na wykonywanie złożonych operacji w jednym wywołaniu, co może zwiększyć wydajność przez redukcję operacji sieciowych.
* Stwórz Stored Procedure wyszukującą element po podanym w argumencie id i dodającą do niego jakieś pole.

# Ćwiczenia - Copilot
1. CosmosDB pozwala na korzystanie z Copilota przy tworzeniu zapytań.
2. Aby zarejestrować się do użytku, w "Data Explorer" powinna pojawić notyfikacja o Copilocie. Zarejestruj się w niej, by móc z niego korzystać.
3. Aby skorzystać z jego możliwości, kliknij "New SQL Query". Na górze powinno być okienko do wpisywania tekstu dla Copilota.
4. Spytaj Copilota o stworzenie kwerendy wykorzystującej udf do podwajania liczb i użyj jej na jednej ze statystyk "attackType" jeżeli taka broń ją posiada.
5. Spytaj Copilota o powyższe ćwiczenia i sprawdź jak różnią się wyniki i czy są w ogóle poprawne.

# Ćwiczenia - kod i API
1. Dostęp do bazy z poziomu API. Wejdź w "Quick start" z lewego paska.
2. Wybierz swoją platformę pośród .NET, Javy, Node.js i Pythonem. Możesz dodać przykładowy kontener "Items".
3. Stwórz aplikację lokalnie i wykonaj przykładowe zapytania z poprzednich ćwiczeń za pomocą kodu. Spróbuj skorzystać z funkcji udf.
4. Wykorzystaj triggery, stored procedures z poziomu kodu.


