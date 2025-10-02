# Termômetro sem fio – **EMISSOR** (lê e envia a temperatura)

## {Configurar o rádio}
Na categoria ``||radio:rádio||``, arraste **``||radio:definir grupo do rádio||``** e troque para **o número indicado pelo(a) professor(a)** (o **mesmo** do receptor).  
Depois, adicione **``||radio:conjunto de rádio transmite energia||``** e coloque **7** (máximo).

```blocks
radio.setGroup(12)
radio.setTransmitPower(7)
```

## {Criar um "LED de envio"}
Crie a variável ``||variables:blink||`` (``||variables:Variáveis||``) e defina **false** no ``||basic:no iniciar||``.  
Vamos usar um LED piscando para indicar cada envio, sem "brigar" com o display do receptor.

```blocks
let blink = false
```

## {Enviar temperatura periodicamente}
Em ``||basic:Básico||``, adicione **``||basic:sempre||``**.  
Dentro dele:
1. Use **``||input:temperatura (°C)||``** (``||input:Entrada||``) e guarde em uma variável local **``tempC``**.  
2. Envie pelo rádio usando **``||radio:rádio envia value||``**:
   - **name**: digite **``T``**  
   - **value**: ``tempC``  
3. Faça o LED "piscador":
   - **``||variables:definir blink para (não blink)||``** (``||logic:Lógica||`` → ``não``)  
   - Com ``||led:Matriz de LEDs||``, ligue/apague o LED do canto (0,0) de acordo com **blink**.  
4. **Pause** de **1000 ms** (1 segundo).

```blocks
basic.forever(function () {
    let tempC = input.temperature()
    radio.sendValue("T", tempC)
    blink = !blink
    if (blink) {
        led.plotBrightness(0, 0, 255)
    } else {
        led.unplot(0, 0)
    }
    basic.pause(1000)
})
```

## {Teste}
- Baixe no **Emissor**.  
- Observe o **LED piscando** a cada envio.  
- No Receptor, a temperatura deve aparecer como "23C", "24C"… no mesmo grupo.

```template
basic.forever(function () { })
```