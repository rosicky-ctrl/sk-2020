## Konfiguracja route


* routing
    * dodaj trasę default
    * dodaj trasę przez bramę
    * dodaj trasę przez interfejs
    * usuń trasę
    * zmień trasę
    * pobierz trasę dla adresu
     
### ip 
| subcommand    |  polecenie   | opis  |
| ------------- |:-------------| :---------------| 
|       | ip route add default via 10.0.10.1 | wszystkie adresy ktorych nie zna zostana wyslane do routera via 10.0.10.1 |
|               | ip route get 10.0.10.10 | droga jaką "pofrunie" routing dla 10.0.10.10 |
|  | ip route add 10.0.10.0/24 via 172.16.100.1 | router który ma przyłączony eth1 10.0.10.1 bedzie wiedział co z tym zrobić, dodanie do tablicy routingu |
|  |  ip route show  | tablica routingu |
| sysctl net.ipv4.ip_forward=1 | echo 1 > /proc/sys/net/ipv4/ip_forward | włączenie tej opcji, pingi między pctami z dwóch oddzielnych sieci zaczęły przechodzić, flaga mówiąca o przekazywaniu pakietów między interfejsami |


### Zastosowania

* Wydzielenie osobnej sieci dla urządzeń sieciowych
* Separacja urządzeń gościnnej sieci WIFI do osobnej sieci
* Zapewnienie komunikacji pomiędzy odrębnymi sieciami lokalnymi z wykorzystaniem VPN

![zadanie 4](example-network.svg)

### Zadanie

![zadanie 4](cwiczenia4.svg)

1.
   * Przygotuj konfigurację sieci zgodnie z powyższym diagramem, 
   * Przetestuj połączenie pomiędzy wszystkimi elementami sieci
   * Dlaczego połączenie może nie działać
2. Przygotuj konfigurację tak aby została załadowana poprawnie po ponownym uruchomieniu systemu
   * Patrz ``utrwalanie statycznej konfiguracji cwiczenia 2``
   * zwróć uwagę na różnice pomiędzy dydtrybucjami systemu
3. Zainstaluj, uruchom i przetestuj działanie aplikacji ``chat``
   * aplikacja dostępna w serwisie github ``https://github.com/jkanclerz/client-server-chat`` lub preinstalowana na maszynie dostępnej w zasobach kursu

### Zadanie do domu

1. Przygotuj konfigurację z zadania 1 wykorzystując inny system operacyjny na komputerze pełniącym rolę routera.
  * debian / centos / inny
  * zapewnij poprawną komunikację pomiędzy PC3 -> PC1
  
2. Dodaj kolejną sieć do komputera pełniącego funkcję routera
   * Sprawdź poprawność komunikacji pomiędzy innymi obszarami sieci
   * Zweryfikuj działanie programu chat pomiędzy różnymi segmentami sieci

![zadanie 4](todo.svg)
