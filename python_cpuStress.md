# Scripts para stress de CPU/Memória

*multiprocessing + math (Puro Python - Estresse de CPU)*
```py
import multiprocessing
import math

def stress_cpu():
    while True:
        math.factorial(100000)  # Cálculo pesado

if __name__ == "__main__":
    processes = []
    cores = multiprocessing.cpu_count()  # Usa todos os núcleos
    for _ in range(cores):
        p = multiprocessing.Process(target=stress_cpu)
        p.start()
        processes.append(p)
    
    input("Pressione Enter para parar...")  # Para quando quiser
    for p in processes:
        p.terminate()
```


*numpy (Para Cálculos Intensivos - Bom para CPU e RAM)*
```py
import numpy as np

def stress_ram_and_cpu():
    while True:
        # Aloca uma matriz gigante (consome RAM + CPU)
        big_matrix = np.random.rand(10000, 10000)
        np.linalg.inv(big_matrix)  # Operação pesada

stress_ram_and_cpu()
```

*psutil (Para Monitorar e Estressar Recursos)*
```py
import psutil
import os

# Estressa RAM (alocando memória)
def stress_ram():
    data = []
    try:
        while True:
            data.append(" " * 10**6)  # Aloca 1MB por iteração
    except MemoryError:
        print("RAM lotada!")

# Estressa CPU
def stress_cpu():
    while True:
        [x * x for x in range(10**6)]

stress_ram()  # Ou stress_cpu()
```


*pyautogui (Para Travar a Interface - Se Tiver Acesso Gráfico) [Não funciona via SSH!]*
```py
import pyautogui
import time

while True:
    pyautogui.press("capslock")  # Fica ligando/desligando o Caps Lock
    time.sleep(0.1)
```

**
```py

```
