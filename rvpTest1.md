# Vprašanja za prvo ocenjevalno obdobje

> [!NOTE]
> 1. Kako določimo, da bo digitalni I/O pin na krmilniku Arduino deloval kot vhod? (Arduino
> funkcija, direktno naslavljanje registra).

> ```cpp
> pinMode(pin, INPUT); // Arduino funkcija
> DDRx &= ~(1 << pin); // Register
> ```

---

> [!IMPORTANT]
> 2. Koliko registrov imajo digitalni vhodi/izhodi? Opiši njihove funkcije.

> 3 registri:
> - DDRx - Data Direction Register (0 - INPUT, 1 - OUTPUT) - doloca nacin delovanja
> - PORTx - Output Register (0 - LOW, 1 - HIGH), INPUT (0 - PULLUP OFF, 1 - PULLUP ON), OUTPUT (0 - LOW, 1 - HIGH)
> - PINx - Input Register (0 - LOW, 1 - HIGH) - prebere vrednost vhoda

---

> [!NOTE]
> 3. Zakaj moramo digitalnemu vhodu na mikrokrmilniku dodati upor, ki ga povežemo na +5V ali
> na GND?

> Da dobimo stabilen vhodni signal (brez upora ne moremo določiti potenciala na vhodu)

---

> [!NOTE]
> 4. Kaj pomenita izraza PULLUP in PULLDOWN? Nariši povezavo upora v PULLDOWN načinu.

> **PULLUP** - I/O na +5V
> ```
> +5V --- R -|- I/O
>            |
>             /
>            |
>           GND
>```
>
> **PULLDOWN** - I/O na GND
>```
> GND --- R -|- I/O
>            |
>             /
>            |
>           +5V
>```

---

> [!NOTE]
> 5. Določi digitalni I/O pin kot PULLUP vhod in pri tem uporabi direktno naslavljanje registra.

> ```cpp
> DDRx &= ~(1 << pin); // INPUT
> PORTx |= (1 << pin); // PULLUP
> ```

---

> [!NOTE]
> 6. Ali ima mikrokrmilnik Arduino vgrajen upor za PULLUP povezavo in s katerim ukazom to
> vezavo aktiviramo?

> ```cpp
> pinMode(pin, INPUT_PULLUP); // Arduino funkcija
> DDRx &= ~(1 << pin); // INPUT
> PORTx |= (1 << pin); // PULLUP
> ```

---

> [!WARNING]
> 7. Nariši električno shemo svetleče diode, priključene v pozitivni logiki na PB4 in napiši program
> tako, da bo dioda svetila.

> **Diagram:**
> ```
> PIN-12 --- 220R ---|>|--- GND
> ```
>
> **Koda:**
> ```cpp
> void setup() {
>     DDRB |= (1 << 4);  // OUTPUT
>     PORTB |= (1 << 4); // Set OUTPUT to HIGH
> }
> ```

---

> [!WARNING]
> 8. Nariši električno shemo svetleče diode, priključene v negativni logiki na PB2 in napiši
> program tako, da bo dioda svetila.

> **Diagram:**
> ```
> +5V --- 220R ---|>|--- PIN-10
> ```
>
> **Koda:**
> ```cpp
> void setup() {
>     DDRB |= (1 << 2);
>     PORTB &= ~(1 << 2);
> }
> ```

---

> [!NOTE]
> 9. Zakaj uporabljamo upor pri vezavi diode na digitalni izhod mikrokrmilnika? Izračunaj zaščitni
> upor svetleče diode, ki ima nazivno napetost 2V, nazivni tok je 20mA in je priključena na
> napetost 5V.

> Da omejimo tok skozi diodo in preprecimo preobremenitev diode in mikrokrmilnika
>
> **Zaščitni upor:**
> ```math
> V = 5V - 2V = 3V
> I = 20mA
> R = V / I = 3V / 0.02A = 150R
> ```

---

> [!NOTE]
> 10. Napiši funkcijo za utripanje svetleče diode, priključene na PB3 (uporabi XOR bitni logični operator ^).

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

> [!NOTE]
> 11. Nariši matrično tipkovnico 3x2 tipk. Razloži programsko kako ugotovimo, katera tipka je pritisnjena.

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

> [!NOTE]
> 12. Nariši shemo za 4 tipke, priključene na analogni vhod.

> **Diagram:**
> ```
> +5V -|- R -|- R -|- R -|- R -|- R -|- GND
>      |     |     |     |     |
>      |- / -|- / -|- / -|- / -|- A0 
> ```

---

>[!NOTE] 
> 13. Razloži delovanje analognih vhodov mikrokrmilnika ATmega328.

> Najprej z analognega vhoda preberemo trenutno napetost, ki jo s pomocjo kvantizacije pretvorimo v digitalno vrednost.
> Kvantizacija je postopek, kjer izberemo najblizjo vrednost digitalnega signala ki najustrezneje predstavlja analogno vrednost.
> ATmega328 ima za to vgrajen 10-bitni ADC. To pomeni da pri branju iz analognega vhoda dobimo vrednost med 0 in 1023 (0V - 5V).

---

> [!NOTE]
> 14. Ali ima mikrokrmilnik analogne izhode? Kakšna je oblika PWM signala in za kaj ga uporabljamo?

> Nima analognih izhodov. Nadomestiomo jih z generiranjem PWM signala.
> PWM je signal s kvadratno valovno obliko (square wave). Analogne vrednosti z njim simuliramo tako, 
> da spreminjamo razmerje med časom, ko je signal HIGH in LOW.
> Uporabimo ga za npr. svetlost LED diode, hitrost motorja...

---

> [!NOTE]
> 15. Razloži delovanje pomikalnega registra.

> Pomikalni register je serijsko paralelni pretvornik. Ta serijsko prejema po 1 bit, ko na clock pinu zazna signal.
> Najprej premakne trenutno shranjene bite za 1 mesto naprej, nato pa na prvo mesto shrani prejeti bit. Glede na vrednosti trenutno shranjenih bitov bo na svojih output pinih dajav vstrezno napetost.
> Funkcija shiftOut(dataPin, clockPin, bitOrder, value)

---

> [!NOTE]
> 16. Razloži delovanje 7 segmentnega, 4 številčnega prikazovalnika.

> Imamo 8 segmentov (7 + decimalna pika). Vsa 4 stevila si delijo 8 pinov za segmente. 
> Imamo se 4 pine za izbiro stevila oz. mesta ki ga zelimo prikazati, kar nam omogoca
> neodvisen vklop posameznih stevil.

---

> [!NOTE]
> 17. Zakaj uporabljamo multipleksiranje pri 7 segmentnem 4 številčnem prikazovalniku?

> Ce bi hkrati vklopili pine za vsa stevila bi se na vseh pokazalo isto stevilo, saj imajo
> skupne pine za segmente. S pomocjo casovnega multiplexiranja bomo hkrati vklopili samo eno stevilo, 
> ter na njem prikazali zeljeno stevilo. Nato izklopimo trenutno stevilo in vklopimo naslednje.
> Ker med izbranimi stevili preklapljamo dovolj hitro, ne bomo mogli zaznali utripanja posameznih stevil.

---

> [!NOTE]
> 18. Zakaj oz. kdaj uporabljamo prekinitve (interrupts)?

> Uporaljamo jih, da ne rabimo stalno previrjati stanja vhoda ali preteklega casa, 
> v situacijah kjer hocemo takoj ob spremembi nek odziv.
> Primer uporabe bi biv casovni interrupt ce imamo v kodi delay, za casovnik pa zelimo,
> da deluje neodvisno od casa ki ga porabi koda.

---

> [!NOTE]
> 19. Kaj je ISR funkcija?

> IRS funkcije so funkcije, ki se izvedejo ob dolocenem interruptu.
> Za nih velja, da ob izvajanju ustavijo izvajanje glavne kode, ter da med izvajanjem
> ene ISR funkcije so klici drugih ISR funkcij ignorirani.
> Zelimo da so te cim krajse saj hocemo cim hitreje nadaljevanje glavne kode.

---

> [!IMPORTANT]
> 20. Razloži delovanje strojne prekinitve (Hardware Interrupt).

> Strojne prekinitve povzrocijo spremembe na pinih, ki to podpirajo.
> Ce na pinu vklopimo interrupt, bo mikrokrmilnik samostojno vs cas
> stanje na pinu opazoval in ob zeljeni spremembi (npr. rising ali falling) 
> izvedel specifirano ISR funkcijo.
> attachInterrupt(digitalPinToInterrupt(pin), ISR, mode);

---

> [!IMPORTANT]
> 21. Razloži delovanje časovne prekinitve (Timer Interrupt).

> Arduino ima 3 casovnike, ki jih lahko uporabimo za generiranje casovnih prekinitv.
> Casovnik ima lahko razlicne pogoje za sporzitev prekinitve (npr. overflow ali compare match).


---

> [!IMPORTANT]
> 22. Razloži princip delovanja časovnika/števca mikrokrmilnika ATmega328.

> Casovnik deluje s frekvenco 16MHz. To pomeni 1 signal na 1/16MHz = 62.5ns.
> Nas casovnik ima 8 ali 16 bitov. Ce je maksimalno mozno stevilo do katerega lahko stejemo
> premajhno za naso casovno periodo, lahko uporabimo prescaler, ki ponuja upocasnitev stevca, 
> tako da stevec upocasni za x1, x8, x64, x256, x1024. To nastavimo v TCCRxB registru.
> Ce smo nastavili casovnik v compare match nacin, bomo trenutno vrednost TCNTx primerjali
> z OCRxA registrom, ki drzi zeljeno vrednost do katere stejemo. Ko jo dosezemo se sprozi interrupt.

---

> [!IMPORTANT]
> 23. Razloži delovanje časovnika/števca v CTC načinu.

> V CTC nacinu casovnik deluje kot v compare match nacinu, le da se po dosezeni vrednosti OCRxA
> ne sprozi interrupta, ampak se stevec TCNTx nastavi na 0. Prav tako se vrednost OCxA ali OCxB
> registra (to je pin) nastavi na kar doloca TCCR register.
> [Source 1](https://www.electronicwings.com/avr-atmega/atmega1632-clear-timer-on-compare-match-ctc-mode)
> [Source 2](https://stackoverflow.com/questions/26599618/avr-timer-programming-ctc-mode-vs-normal-mode)

---

> [!IMPORTANT]
> 24. Razloži delovanje časovnika/števca v fast PWM načinu.

> V fast PWM nacinu casovnik deluje tako, da se vrednost na OCxA ali OCxB registru nastavi na 0
> dokler TCNTx ne doseze vrednosti OCRxA. Ko jo doseze se vrednost OCxA ali OCxB registra nastavi na 1,
> dokler se na TCNTx ne zgodi overflow, ki ga ponovo nastavimo na 0.
> [Source 1](https://www.electronicwings.com/avr-atmega/atmega1632-clear-timer-on-compare-match-ctc-mode)
> [Source 2](https://stackoverflow.com/questions/26599618/avr-timer-programming-ctc-mode-vs-normal-mode)
