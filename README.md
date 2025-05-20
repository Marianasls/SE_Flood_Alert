# Estação de Monitoramento de Enchente - Sistemas Multitarefas


## Descrição

Sistema de monitoramento e alerta de enchentes, desenvolvido para a plataforma Raspberry Pi Pico W utilizando FreeRTOS. O sistema lê sensores de nível de água e volume de chuva, que são representados pela leitura ADC com um joystick, e exibe as informações em um display OLED e aciona alertas visuais e sonoros em caso de risco de enchente.

## Funcionamento

O sistema opera em três tarefas principais, executadas em paralelo via FreeRTOS:

- **Leitura dos Sensores:** Realiza a leitura periódica dos sensores de nível de água e volume de chuva (simulados via ADC).
- **Exibição no Display:** Mostra os valores lidos no display OLED, atualizando a cada ciclo.
- **Alerta:** Monitora os valores dos sensores e, caso o nível de água seja maior ou igual a 70% ou o volume de chuva maior ou igual a 80%, aciona um alerta:
  - Liga o LED RGB na cor vermelha.
  - Ativa o buzzer.
  - Exibe um símbolo de alerta na matriz de LEDs WS2812.
  - Mostra a mensagem "ALERTA" no display OLED.
- Quando não há alerta, o sistema mantém o LED RGB verde, buzzer desligado e exibe "Monitoramento de enchente" no display.

O sistema também possui um botão (BOOTSEL) para reinicialização via USB.

## Componentes Utilizados

- **Raspberry Pi Pico W**
- **Display OLED SSD1306 (I2C)**
- **Matriz de LEDs WS2812 (NeoPixel)**
- **LED RGB (3 pinos: vermelho, verde, azul)**
- **Buzzer**
- **Dois sensores analógicos (simulados via entradas ADC)**
- **Botão físico (BOOTSEL)**
- **Resistores de pull-up para I2C**

## Como funciona

1. Inicialização dos periféricos (GPIO, I2C, PWM, ADC, PIO).
2. As tarefas FreeRTOS são criadas e iniciadas.
3. O sistema lê os sensores, atualiza o display e monitora condições de alerta.
4. Em caso de alerta, aciona os dispositivos de aviso visual e sonoro.
5. O botão BOOTSEL pode ser usado para reiniciar o dispositivo em modo USB.

## Dependências

- Raspberry Pi Pico SDK
- FreeRTOS
- Bibliotecas customizadas: `ssd1306`, `led_matrix`, `ws2812.pio`

## Compilação

O projeto utiliza CMake. Para compilar:

```sh
mkdir build
cd build
cmake ..
make