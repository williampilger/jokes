# Impedir acesso ao Spotify pelo SSH


Você precisará adicionar algumas entradas no arquivo de hosts do sistema:

*C:\Windows\System32\drivers\etc\hosts*
```
127.0.0.1 spotify.com
127.0.0.1 open.spotify.com
127.0.0.1 api.spotify.com
127.0.0.1 scdn.co
127.0.0.1 spotifycdn.com
```

Lembre-se de fazer uma cópia desse arquivo antes de mecher nele.
