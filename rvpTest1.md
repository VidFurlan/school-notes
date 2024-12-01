# Vprašanja za prvo ocenjevalno obdobje

> 1. Kako določimo, da bo digitalni I/O pin na krmilniku Arduino deloval kot vhod? (Arduino
> funkcija, direktno naslavljanje registra).

> [!NOTE]
> pinMode(pin, INPUT); // Arduino funkcija
> DDRx &= ~(1 << pin); // Register

---

> 2. Koliko registrov imajo digitalni vhodi/izhodi? Opiši njihove funkcije.

> [!CAUTION]
> 3 registri:
> - DDRx - Data Direction Register (0 - INPUT, 1 - OUTPUT) - doloca nacin delovanja
> - PORTx - Output Register (0 - LOW, 1 - HIGH), INPUT (0 - PULLUP OFF, 1 - PULLUP ON), OUTPUT (0 - LOW, 1 - HIGH)
> - PINx - Input Register (0 - LOW, 1 - HIGH) - prebere vrednost vhoda

---

> 3. Zakaj moramo digitalnemu vhodu na mikrokrmilniku dodati upor, ki ga povežemo na +5V ali
> na GND?

> [!NOTE]
> Da dobimo stabilen vhodni signal (brez upora ne moremo določiti potenciala na vhodu)

---

> 4. Kaj pomenita izraza PULLUP in PULLDOWN? Nariši povezavo upora v PULLDOWN načinu.

> [!NOTE]
> **PULLUP** - I/O na +5V
> ```
> +5V --- R --- I/O
>         |
>          /
>         |
>        GND
>```
>
> **PULLDOWN** - I/O na GND
>```
> GND --- R --- I/O
>         |
>          /
>         |
>        +5V
>```

---

> 5. Določi digitalni I/O pin kot PULLUP vhod in pri tem uporabi direktno naslavljanje registra.

> [!NOTE]
> DDRx &= ~(1 << pin); // INPUT
> PORTx |= (1 << pin); // PULLUP

---

> 6. Ali ima mikrokrmilnik Arduino vgrajen upor za PULLUP povezavo in s katerim ukazom to
> vezavo aktiviramo?

> [!NOTE]
> pinMode(pin, INPUT_PULLUP); // Arduino funkcija
> DDRx &= ~(1 << pin); // INPUT
> PORTx |= (1 << pin); // PULLUP

---

> 7. Nariši električno shemo svetleče diode, priključene v pozitivni logiki na PB4 in napiši program
> tako, da bo dioda svetila.

> [!NOTE]
> **Diagram:**
> ```
> PIN-12 --- 220R ---|>|--- GND
> ```
>
> **Koda:**
> ```cpp
> void setup() {
>     DDRB |= (1 << 4);  // OUTPUT
> }
> void loop() {
>     PORTB ^= (1 << 4); // TOGGLE LOW/HIGH
> }
> ```

---

> 8. Nariši električno shemo svetleče diode, priključene v negativni logiki na PB2 in napiši
> program tako, da bo dioda svetila.

> [!NOTE]
> **Diagram:**
> ```
> +5V --- 220R ---|>|--- PIN-12
> ```
>
> **Koda:**
> ```cpp
> void setup() {
>     DDRB &= ~(1 << 4); // INPUT
> }
> void loop() {
>     PORTB ^= (1 << 4); // TOGGLE PULLUP
> }
> ```

---

> 9. Zakaj uporabljamo upor pri vezavi diode na digitalni izhod mikrokrmilnika? Izračunaj zaščitni
> upor svetleče diode, ki ima nazivno napetost 2V, nazivni tok je 20mA in je priključena na
> napetost 5V.

> [!NOTE]
> Da omejimo tok skozi diodo in preprecimo preobremenitev diode in mikrokrmilnika
>
> **Zaščitni upor:**
> ```math
> V = 5V - 2V = 3V
> I = 20mA
> R = V / I = 3V / 0.02A = 150R
> ```

---

> 10. Napiši funkcijo za utripanje svetleče diode, priključene na PB3 (uporabi XOR bitni logični operator ^).

> [!NOTE]
> ```cpp
> setup() {
>     DDRB |= (1 << 3); // OUTPUT
> }
> loop() {
>     PORTB ^= (1 << 3); // TOGGLE
>     delay(500);
> }
> ```

---

> 11. Nariši matrično tipkovnico 3x2 tipk. Razloži programsko kako ugotovimo, katera tipka je pritisnjena.

> [!NOTE]
> 1. Pini 1 - 3 so OUTPUT, pina 4 - 5 sta INPUT
> 2. Iteriramo skozi pine 1 - 3 in trenutnega nastavimo na HIGH, preverimo vrednost pinov 4 - 5
> 3. Preberemo vrednost pinov 4 - 5 in preverimo ce je kje vrednost HIGH. Ce je vrednost HIGH je tipka, ki je povezana
>    z trenutnim OUTPUT pinom in INPUT pinom pritisnjena.
>
> **Diagram:**
> ```
>           |     |
> PIN-1 --- / --- / ---
>           |     |
> PIN-2 --- / --- / ---
>           |     |
> PIN-3 --- / --- / ---
>           |     |
>         PIN-4 PIN-5     
> ```

---

> 12. Nariši shemo za 4 tipke, priključene na analogni vhod.

> [!NOTE]
> Narisan je delilnik napetosti
>
> **Diagram:**
> ```
> +5V -|- R -|- R -|- R -|- R -|- R -|- GND
>      |     |     |     |     |
>      |- / -|- / -|- / -|- / -|- A0 
> ```

---

>[!WARNING] 
> 13. Razloži delovanje analognih vhodov mikrokrmilnika ATmega328.

---

> [!WARNING]
> 14. Ali ima mikrokrmilnik analogne izhode? Kakšna je oblika PWM signala in za kaj ga uporabljamo?

---

> [!WARNING]
> 15. Razloži delovanje pomikalnega registra.

---

> [!WARNING]
> 16. Razloži delovanje 7 segmentnega, 4 številčnega prikazovalnika.

---

> [!WARNING]
> 17. Zakaj uporabljamo multipleksiranje pri 7 segmentnem 4 številčnem prikazovalniku?

---

> [!WARNING]
> 18. Zakaj oz. kdaj uporabljamo prekinitve (interrupts)?

---

> [!WARNING]
> 19. Kaj je ISR funkcija?

---

> [!WARNING]
> 20. Razloži delovanje strojne prekinitve (Hardware Interrupt).

---

> [!WARNING]
> 21. Razloži delovanje časovne prekinitve (Timer Interrupt).

---

> [!WARNING]
> 22. Razloži princip delovanja časovnika/števca mikrokrmilnika ATmega328.

---

> [!WARNING]
> 23. Razloži delovanje časovnika/števca v CTC načinu.

---

> [!WARNING]
> 24. Razloži delovanje časovnika/števca v fast PWM načinu.
