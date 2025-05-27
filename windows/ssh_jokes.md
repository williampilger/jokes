# Brincadeiras para fazer via SSH (ou CMD, se tiver acesso)



## Abrir a gaveta de CD/DVD

> powershell -command "(New-Object -ComObject Shell.Application).Namespace(17).ParseName('E:').InvokeVerb('Eject')"

Trocar, obviamente, a unidade pela letra correta.
A letra da unidade pode ser vista com:

> wmic logicaldisk where "DriveType=5" get DeviceID, VolumeName


## Enviar um PopUp
 > msg * "ALERTA: O SISTEMA VAI REINICIAR EM 10 SEGUNDOS! 😈"



## Desligar a tela (até que o mouse seja movido) - *PowerShell*

```ps1
(Add-Type -MemberDefinition '[DllImport("user32.dll")] public static extern int SendMessage(int hWnd, int hMsg, int wParam, int lParam);' -Name "Win32SendMessage" -Namespace Win32Functions -PassThru)::SendMessage(0xFFFF, 0x0112, 0xF170, 2)
```

