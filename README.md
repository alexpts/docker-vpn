# IpSec

Контейнер запувкается и прокидывает все секереты через ENV, на хосте ничего не храним

# OpenVPN

Требуется иницилизация. Хранит конфигурацию на хосте через volume.

Создаем конфиги, указав ip адрес хоста:
`docker-compose run --rm openvpn ovpn_genconfig -u udp://138.201.190.100`

Создаем ключи, отвечая в интерактивном режиме
`docker-compose run --rm openvpn ovpn_initpki`

Создаем ключ клиента
`docker-compose run --rm openvpn easyrsa build-client-full name@host.com nopass`

Копируем в хост систему ключ клиента для openvpn клиента
`docker-compose run --rm openvpn ovpn_getclient name@host.com > alex@vpn_2.ovpn`

Запускам сервер
`docker-compose up openvpn`
