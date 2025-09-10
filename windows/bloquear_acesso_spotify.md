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

---

### Scripts prontos

*Bloquear*
```ps1
cd C:\Windows\System32\drivers\etc
copy hosts hosts.old

echo 127.0.0.1 spotify.com >> hosts
echo 127.0.0.1 open.spotify.com >> hosts
echo 127.0.0.1 api.spotify.com >> hosts
echo 127.0.0.1 scdn.co >> hosts
echo 127.0.0.1 spotifycdn.com >> hosts
```

*Desfazer*
```
cd C:\Windows\System32\drivers\etc
copy hosts.old hosts
rm hosts.old
```
