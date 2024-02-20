# [roadmap.cameramonit.com](http://roadmap.cameramonit.com)

+ [cameramonit.com](http://www.cameramonit.com)
+ [docs](http://docs.cameramonit.com)
+ [logo](http://logo.cameramonit.com)
+ [roadmap](http://roadmap.cameramonit.com)
+ [identity](http://identity.cameramonit.com)
+ [contribution](http://contribution.softreck.dev)


Questions:

1. Showcase
2. MVP - 
3. How to interact, User experience
4. how interaction will work
5. what the benfit will be


MVP będzie polegało na zrobieniu interfejsu tekstowego z powiadamianiem o tym co dzieje się na video, gdzie tak jak chatgpt będziesz pisał co chesz zobaczyć

1. Panel instalatora
+ wykonanie w python, django + sqlite do konfiguracji 
+ instalator może dodawać dane za pomocą kanału email wysyłając wiadomość z nazwą kamery adresem i hasłem
+ instalator może używać aplikacji chat, np whatsapp do wysłania danych dostępowowych
+ wszystkie dane dotyczące kamer są dostępne do wglądu i bazując na nich admin wybiera które chce podłączyć do konkretnej aplikacji
+ baza danych jest osobno, gdyż można wykorzystać inna formę przehcowywania danych kamer 
+ interfejsem wymiany z panelem aplikacji jest API


2. Panel aplikacji dla @admina w oparciu o dane z Panelu instalatora
+ wykonanie w python, django + sqlite do konfiguracji + FTP/webdav do pobierania danych przez usługę VideoToText
+ dodawanie URL streamu z kamer + auth
+ wartość ile ma być zapisywanych minut video na bieżąco jako bufor, np 5 sekund do opisania tego co się  w tym czasie działo
+ zapisywanie video do maksymalnie do X minut
+ zapisywanie obrazów jako animacji do udostępnienia do przeglądania: X Sekund
+ dodawanie i zarządzanie integracjami 
+ interfejsem wymiany z panelem managera i interfesjem webowym jest API


3. Panel managera dla kontrioli dostępu
+ lista projektów 
+ lista grup i userów
+ określenie czasu dostępu
+ lista zdarzeń jakie mają być udostępnione dla konkretnego grupy usera


4. Usługa VideoToText
Przetwarzanie video i zapisywaniu zauważonych obiektów i zdarzeń do bazy mariaDB: obiekty, cechy, zdarzenia
Biblioteki Python i API w pierwszym etapie ułatwiające analizę krótkich video.
Na początku będzie zgrubna lokalna analiza a następnie dosyłanie do wyspecjalizowanej usługi na innym serwerze.
Dane konfiguracyjne muszą najpierw zostać pobrane z panelu aplikacji i zwrócone w postaci krótkich filmów na serwerze FTP/WEBDAV
Filmy są udostępniane dla usera z interfejsu webowego przez http



5. Interfejs webowy
strona webowa do wizualizacji zdarzeń i możliwości przeglądania w formie chat
każda kamera ma osobny chat tak jakbyś rozmawiał z różnymi ludźmi
z dodatkowymi opcjami, których nie można zaimplementować na zwykłej apce jak podpowiedzi.


6. Integracja API
z popularnymi komunikatorami z pisaniem bezpośrednio na smartphone usera o tym co dzieje się na kamerze + poprzez url możliwość wejścia na interfejs webowy aby zobaczyć więcej


7. Storage
dostepny poprzez FTP/Webdav


W skrócie mamy 3 typy użytkowników + instalator, który dodaje kamery
- admin, który definiuje projekt/aplikację i wykorzystuje kamery dodane przez instalatora
- manager, który dodaje userów i prawa do projektu/aplikacji 
- supervisor, który nazywa obiekty, określa korelacje, istnieje tylko na początku, ale może być odpytywany przez system o nazywanie sytuacji na wniosek customer-a 
- customer, który korzysta z WebUI/chat do przeglądania zdarzeń  



Trzeba stworzyć makietę na docker compose, każda usługa osobno przez dedykowany IP wewnątrz sieci
Kolejna implementacja na proxmox:
+ router openwrt
+ VPS per service
+ Mysql dla panelu admina, managera, interfejsu webowego
+ Storage ftp/webdav
+ Integracje API dla:
	+ VideoToText
	+ ImageToText
	+ SpeechToText
	+ TextToSpeech

Prezentacja dla użytkownika



## ROADMAP


### Offline upload video - 1 kanał
Przygotowanie docker compose lokalnie
+ FastAPI
+ Django, ORM
+ mariadb/sqlite
frontend:
+ admin: auth, usługi, api
+ kamera: upload, ftp
+ user: powiadamianie, web, email

Funkcje
Upload:
+ poprzez stronę 
+ webdav
Powiadamianie:
+ www
+ e-mail
+ chat

1. jedna baza danych konfiguracji + administracji 
2. ftp/webdav do wgrania video i pobierania video
3. Generowanie w oparciu o upload, poprzez połączenie do API videototext
4. Generowanie rozpoznanych obiektów w oparciu o bazę danych
5. Wysyłanie danych do bazy danych a z niej bezpośrednio na powiadamianie 
6. Na stronie www
7. Na API chat/Email

Statycznie przygotowane + z już przetworzonymi danymi oraz chat webowy dla usera do przeglądania wcześniej nagranego video z jednej kamery

### Live, 60 sekund - 1 kanał

Przygotowanie docker compose z runner na gitlab w VPS w proxmox
1. Panel konfiguracji + administracji + chat webowy dla usera do otrzymywania informacji z aktualnego streamu video z jednej kamery
2. Usługa videototext w oparciu o API do przetwarzania filmów 60 sekundowych
3. Chat webowy dla usera do przeglądania nagrywanych danych z ostatnich 60 sekund w pętli z 1 kamery
3. Zarządzanie użytkownikami: dodanie panelu instalatora i użytkownika
4. Rozszerzenie możliwości przetwarzania i obsługa panelu dla supervisora
5. Integracja chatów


### Live, 24h - 10 kanałów

Przygotwanie na wirtualiazji proxmox

+ Każda usługa jako odrębny VPS
+ Powiększenie storage do 24h
+ możliwość dodawania nie tylko strumieni ale własnych video do analizy







---

+ [issue](https://github.com/cameramonit/roadmap/issues/new)
+ [edit](https://github.com/cameramonit/roadmap/edit/main/README.md)
+ [git](https://github.com/cameramonit/) 
