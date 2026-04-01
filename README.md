# ⏱️ Relógio, Operações e Cronômetro em Python

Implementação de um **relógio analógico** com suporte a **operações aritméticas e comparações entre horários**, além de uma classe **Cronômetro** funcional com start, pause, restart e stop. Projeto desenvolvido em Python com Programação Orientada a Objetos (POO), explorando sobrecarga de operadores e o módulo `time`.

---

## 📋 Sobre o Projeto

O projeto é composto por duas classes independentes:

- **`Relogio`** — representa um horário no formato `HH:MM:SS`, com suporte completo a operações aritméticas (`+`, `-`) e comparações (`==`, `!=`, `>`, `<`, `>=`, `<=`) entre instâncias, tudo via sobrecarga de operadores dunder.
- **`Cronometro`** — simula o comportamento de um cronômetro real, com controlo de estado (a correr / pausado) e conversão para formato de relógio.

---

## 🗂️ Estrutura do Código

### `class Relogio`

Representa um horário com validação automática de limites (horas em ciclo de 24h, minutos e segundos em ciclo de 60).

**Atributos:**
- `horas` — valor entre 0 e 23 (`% 24`)
- `minutos` — valor entre 0 e 59 (`% 60`)
- `segundos` — valor entre 0 e 59 (`% 60`)

**Métodos especiais:**

| Método | Descrição |
|--------|-----------|
| `__str__` | Representação legível: `"04:20:00"` |
| `__repr__` | Representação técnica: `"Relogio(4, 20, 0)"` |
| `_para_segundos()` | Converte o horário para total de segundos |
| `_para_horas(total)` | *(estático)* Converte segundos de volta para um objeto `Relogio` |

**Operações aritméticas:**

| Operador | Método | Comportamento |
|----------|--------|---------------|
| `+` | `__add__` | Soma dois relógios; resultado em ciclo de 24h |
| `-` | `__sub__` | Diferença absoluta entre dois relógios |

**Operações de comparação:**

| Operador | Método |
|----------|--------|
| `==` | `__eq__` |
| `!=` | `__ne__` |
| `>` | `__gt__` |
| `<` | `__lt__` |
| `>=` | `__ge__` |
| `<=` | `__le__` |

> Todas as comparações são feitas convertendo os horários para segundos totais antes de comparar.

---

### `class Cronometro`

Simula um cronômetro com controlo preciso de estado, acumulando o tempo mesmo após pausas.

**Atributos internos:**
- `_inicio` — marca o instante em que o cronômetro foi (re)iniciado
- `_pausado` — acumula o tempo decorrido quando pausado
- `_a_correr` — booleano que indica se o cronômetro está activo

**Métodos:**

| Método | Descrição |
|--------|-----------|
| `start()` | Inicia ou retoma o cronômetro a partir do tempo acumulado |
| `pause()` | Pausa o cronômetro e guarda o tempo decorrido |
| `restart()` | Zera o contador e reinicia imediatamente |
| `stop()` | Para o cronômetro, exibe e retorna o tempo total em segundos |
| `show_time()` | Retorna o tempo atual em segundos (em execução ou pausado) |
| `__str__` | Exibe o tempo no formato `"HH:MM:SS"` |

---

## 💻 Exemplo de Uso

```python
from "Projeto Relogio e Cronometro" import Relogio, Cronometro
import time

# --- Relógio ---
r1 = Relogio(horas=4, minutos=20, segundos=0)
r2 = Relogio(horas=16, minutos=30, segundos=30)

print(r1)           # 04:20:00
print(r2)           # 16:30:30
print(r1 + r2)      # 20:50:30
print(r1 - r2)      # 12:10:30
print(r1 > r2)      # False
print(r1 < r2)      # True

# --- Cronômetro ---
c = Cronometro()

c.start()           # Cronometro INICIADO
time.sleep(0.5)
c.pause()           # Cronometro PAUSADO em 0.50 segundos
c.start()           # Retoma a partir de 0.50s
time.sleep(0.5)
c.stop()            # Cronometro PARADO. Tempo Total: ~1.00 segundos

c.restart()         # Zera e reinicia
time.sleep(0.5)
print(f"{c.show_time():.2f}")   # ~0.50
```

**Saída esperada:**
```
04:20:00
16:30:30
20:50:30
12:10:30
False
True
Cronometro INICIADO
Cronometro PAUSADO em 0.50 segundos
Cronometro INICIADO
Cronometro PARADO. Tempo Total: 1.00 segundos
Cronometro RENINCIADO
0.50
```

---

## ▶️ Como Executar

### Pré-requisitos

- Python 3.x instalado (sem dependências externas — usa apenas o módulo `time` da biblioteca padrão)

### Passos

```bash
# Clone o repositório
git clone https://github.com/talesreis27/Projeto-Relogio-e-Operacoes-e-Cronometro.git

# Acesse a pasta do projeto
cd Projeto-Relogio-e-Operacoes-e-Cronometro

# Execute o script
python "Projeto Relogio e Cronometro.py"
```

---

## 📁 Arquivos do Repositório

```
Projeto-Relogio-e-Operacoes-e-Cronometro/
├── Projeto Relogio e Cronometro.py   # Código-fonte principal
├── LICENSE                            # Licença MIT
└── README.md                          # Este arquivo
```

---

## 🛠️ Tecnologias Utilizadas

- **Python 3** — linguagem principal
- **Módulo `time`** (biblioteca padrão) — para medição de tempo no `Cronometro`

---

## 💡 Conceitos Praticados

- Programação Orientada a Objetos (POO)
- Sobrecarga de operadores com métodos dunder (`__add__`, `__sub__`, `__eq__`, `__gt__`, etc.)
- Métodos estáticos (`@staticmethod`)
- Controlo de estado com atributos internos (`_a_correr`, `_pausado`)
- Conversão entre representações de tempo (segundos ↔ HH:MM:SS)
- Formatação de strings com f-strings e zero-padding (`:02d`)

---

## 📄 Licença

Este projeto está licenciado sob a [Licença MIT](LICENSE) — sinta-se livre para usar, modificar e distribuir.

---

## 👤 Autor

**Tales Reis e Silva**  
GitHub: [@talesreis27](https://github.com/talesreis27)
