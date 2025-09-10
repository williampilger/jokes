# Impedir acesso ao Spotify pelo SSH

## Método 1: Usando o Firewall

*Bloquear*
```ps1
# 1. Lista de domínios do Spotify a serem bloqueados
$dominiosSpotify = @(
    "accounts.spotify.com",
    "scdn.co",
    "spotifycdn.com",
    "spclient.wg.spotify.com",
    "audio-ak-spotify-com.akamaized.net",
    "heads-fa.scdn.co",
    "https://community.spotify.com/t5/Desktop-Windows/Spotify-exe-location/td-p/5260104",
    "http://download.spotify.com/SpotifyFullSetup.exe",
    "ap.spotify.com"
)

# 2. Resolve os endereços IP para cada domínio e armazena em uma lista
$ipsParaBloquear = foreach ($dominio in $dominiosSpotify) {
    # Usamos -ErrorAction SilentlyContinue para ignorar domínios que não possam ser resolvidos
    (Resolve-DnsName -Name $dominio -Type A -ErrorAction SilentlyContinue).IPAddress
}

# 3. Cria a regra de firewall com a lista de IPs (removendo duplicados)
if ($ipsParaBloquear) {
    New-NetFirewallRule -DisplayName "Bloquear Domínios Spotify" -Direction Outbound -RemoteAddress ($ipsParaBloquear | Select-Object -Unique) -Action Block
    Write-Host "Regra de firewall 'Bloquear Domínios Spotify' criada com sucesso."
} else {
    Write-Error "Não foi possível resolver nenhum dos domínios do Spotify. A regra não foi criada."
}
```

*Desfazer*
```ps1
Remove-NetFirewallRule -DisplayName "Bloquear Domínios Spotify"
```

---

## Método 2: Usando o arquivo hosts (precisa de reinicio)

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
