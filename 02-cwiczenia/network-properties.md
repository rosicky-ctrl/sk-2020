## Ustawianie parametrów sieci

### Zadania

0. Z wykorzystaniem dowolnych systemów operacyjnych na których potrafisz uruchomić interpreter ``python`` oraz oprogramowania virtualbox odwzoruj poniższy schemat sieci:

![alt text][network]

[network]: ./network.png "Logo Title Text 2"

1. na 1 z komputerów zainstaluj i uruchom program ``server.py`` dostępne pod adresem ``https://github.com/jkanclerz/client-server-chat``
2. na 2 z komputerów zainstaluj i uruchom program ``client.py`` dostępne pod adresem ``https://github.com/jkanclerz/client-server-chat``
3. Manipulując konfiguracją sieci na poziomie virtualbox, uruchom serwer czatu, oraz udostępnij go na wybranym porcie oraz adresie tak aby istniała możliwość połączenia przez inne osoby w obrębie pracowni
4. Zainstaluj oprogramowanie serwera HTTP ``nginx`` lub innego, skonfiguruj plik index.html wg instrukcji, sprawdź dostępność strony z wykorzystaniem dowolnego klienta protokołu ``HTTP`` z różnych konfiguracji IP
5. Posługując się programami tj: ``netstat`` lub ``lsof`` sprawdź na jakich portach zostały uruchomione serwery czatu czy HTTP

Wejściowe parametry sieci
-------------------------
| Parametr | wartość | komentarz(opcionalny) |
| ------------- |:-------------:| -----:|
|   PC 1 |  
| IP - address  | 10.0.15.4 | ip addr add 10.0.15.4/24 |
| MASKA  | /24 (255.255.255.0) | maska - ilosc jedynek od lewej strony |
|   |  | |
| PC 2  |  | |
| IP - address  | 10.0.15.6 | ip addr add 10.0.15.4/24 |
| MASKA  | /24 (255.255.255.0 )| maska - ilosc jedynek od lewej strony |

Weryfikacja połączenia

Polecenie

* ip addr add 10.0.15.4/24 dev eth0 na pierwszej maszynie - ustawienie adresu IP i maski na PC1
* ip addr add 10.0.15.6/24 dev eth0 na drugiej maszynie - ustawienie adresu IP i maski na PC2
* ip addr show eth0 - pokazuje dane interfejsu
* apk add git python3 curl - zainstalowanie pakietu pozwalającego na korzystanie z githuba, pythona, curla
* git clone https://github.com/jkanclerz/client-server-chat - sklonowanie na PCty programów
* ping - najprostsza metoda sprawdzenia czy host po drugiej stronie odpowie, czy jest komunikacja, polaczenie miedzy dwiema maszynami
* python3 server.py / python3 client.py 9999 - odpalenie na jednym PC serwera, na drugim klienta z portem 9999

Efekt:
* PCty w tej samej sieci, ta sama maska, połączenie za pomocą ping i server-client działa.

Statyczna konfiguracja parametrów połączenia
Wejściowe parametry sieci
-------------------------
| Parametr | wartość | komentarz(opcionalny) |
| ------------- |:-------------:| -----:|
|   PC 1 |  
| IP - address  | 192.168.10.10 | ip addr add 192.168.10.10/24 |
| MASKA  | 255.255.255.0 | /24 |
|   |  | |
| PC 2  |  | |
| IP - address  | 192.168.10.11 | ip addr add 192.168.10.11/17 |
| MASKA  | 255.255.128.0 | 8+8+1=17 |
| PC 2  |  | |
| IP - address  | 172.16.100.100 | ip addr add 172.16.100.100/16 |
| MASKA  | 255.255.0.0 | 8+8=16 |

Polecenie ping działa między PC1 a PC2, jeżeli pingujemy adres 1, tj. 192.168.10.11, zatem maska nie miała na to wpływu. Natomiast w przypadku połączenia z drugim adresem, 172... "Network unreachable". Zgaduję, że do połączenie będzie potrzebny routing.


Nowa statyczna konfiguracja 

-------------------------
| Parametr | wartość | komentarz(opcionalny) |
| ------------- |:-------------:| -----:|
|   PC 1 |  
| IP - address  |  | |
| MASKA  |  | |
|   |  | |
| PC 2  |  | |
| IP - address  |  | |
| MASKA  |  | |

Weryfikacja połączenia

Polecenie
vi /etc/networks/interfaces - edytowanie statycznej konfiguracji

``iface eth0 inet dhcp --> iface eth0 inet static`` zmiana z dhcp na statyczną konfigurację <br>
``address 192.168.10.10`` podajemy adres <br>
``netmask 255.255.255.0`` podajemy maske <br>
``hostname localhost`` <br>
i np. reboot lub rc-service networking restart (przeładowanie sieci), komunikacja zadziała i zostanie utrwalona <br>

Efekt

### Utrwalenie konfiguracji

* Pamiętać o podłączeniu do jednej sieci Lan
* Ustawienie adresów za pomocą ip addr add adres/maska dev eth0/1/..
* Sprawdzenie połączenia za pomocą ping
* PCty muszą znajdować się w tej samej sieci
* vi /etc/network/interfaces - plik, w którym następuje edycja konifugracji
* iface eth0 inet dhcp --> iface eth0 inet static

Stosowane, aby nie ustawiać przy każdym ponownym włączeniu/awarii/braku prądu ponownie adresów, masek, połączeń etc.

### Warto wiedzieć

-------------------------
| Parametr | wartość | komentarz(opcionalny) |
| ------------- |:-------------:| -----:|
| Lokalizacja pliku z konfiguracją sieci| /etc/networks/interfaces | cat |
| UP -> Wyłączenie interfejsu sieciowego| ip link set eth1 down |  |
| DOWN -> Włączenie interfejsu sieciowego| ip link set eth1 up | |
| Sprawdzenie obecnych parametrów | cat /etc/networks/interfaces lub ip addr show | nie jestem pewien o które parametry chodzi |
| lista wszystkich interfejsów | ip addr show | |
| Które interfejsy jakie porty słuchają | netstat | -ltnp przydatne |

