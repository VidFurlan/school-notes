# Vprašanja za prvo ocenjevalno obdobje

> [!NOTE]
> 1. Nariši 4 bitni R-2R DAC pretvornik in razloži delovanje.

> [!CAUTION]
> Na sliki iz zvezka je narisan en upor prevec

> DAC pretvarja digitalne signale v analogne.
> Ta ima 4 upore priklopljene na izhode mikrokrmilnika. Vhod A ima najmanjši vpliv na izhod,
> vhod D pa ima največji vpliv (zaradi števila uporov).
> 4 bitni DAC lahko predstavlja le 2<sup>4</sup> vrednosti saj ima le 4 vhode.
> 
>```
> R - Upor
> A-D - Vhodi
>
>    o-------o-- R --o-- R --o-- R --o---o OUT
>    |       |       |       |       |
>   2R      2R      2R      2R      2R
>    |       |       |       |       |
>    o       A       B       C       D
>   GND    (LSB)                   (MSB)
>```

---

> [!NOTE]
> 2. Napiši formulo za 4 bitni DAC in izpelji splošno formulo za n-bitni R-2R DAC.

> Formula velja če ni ničesar na izhodu!
>
> Formula za 4 bitni DAC: 
>```math
> Vout = \frac{V_{a} + 2V_{b} + 4V_{c} + 8V_{d}}{16}
>```
>
> Splošna formula za n-bitni DAC:
>```math
> Vout = \frac{2^0V_{a} + 2^1V_{b} + 2^2V_{c} + 2^3V_{d} + ... + 2^{n-1}V_{x}}{2^n}
>```

---

> [!NOTE]
> 3. Zakaj je potrebno na izhod R-2R DAC priključiti diferencialni ojačevalnik?

> Ker formula velja če ni ničesar na izhodu. To se zgodi, ker ima končna naprava
> svojo vpornost ki vpliva na izhodno napetost. To rešimo vporabo diferencialnega ojačevalnika,
> saj ta lahko proporcijsko poveča izhodno napetost.
>
> [Diferencialni ojačevalnik](https://www.electronics-tutorials.ws/opamp/opamp_5.html)
> 
> [R-2R DAC](https://www.electronics-tutorials.ws/combination/r-2r-dac.html) (Od tukej je Krislov pdf narjen)

---

> [!NOTE]
> 4. Katere predpostavke uporabimo pri izpeljavi formule za ojačanje diferencialnega
> ojačevalnika?

> Predpostavimo:
> 1. Vhodni tok v operacijski ojačevalnik je enak 0:
> ```math
> I_{vh} \sim 0
> ```
> 2. Razlika napetosti na vhodih – in + je enaka 0:
> ```math
> U_{vh}(V^{+}-V^{-}) \sim 0
> ```
> 3. Ojačanje A je neskončno:
> ```math
> A \sim \infty
> ```

---

> [!NOTE]
> 5. Nariši vezavo operacijskega ojačevalnika z invertiranim vhodom in
> negativno povratne povezavo in izpelji formulo za ojačanje.

> Shema:
> 
> ![image](https://github.com/user-attachments/assets/9da7cfb9-ddb0-418c-8dca-adbd2ddea4ab)
>
> Izpeljava:
> ```math
> \begin{gather}
> U_{in} = I_{R1} * R_{1} \\
> U_{out} = I_{R1} * R_{f} \\
> A = \frac{U_{out}}{U_{in}} = \frac{I_{R1} * R_{f}}{-(I_{R1} * R_{1})} = -\frac{R_{f}}{R_{1}}
> \end{gather}
> ```

---

> [!NOTE]
> 6. Nariši vezavo operacijskega ojačevalnika z ne-invertiranim vhodom in
> negativno povratne povezavo in izpelji formulo za ojačanje.

> Shema:
>
> ![image](https://github.com/user-attachments/assets/a409ad70-fbf5-4c9c-b4c7-e55d652c0884)
>
> Izpeljava:
> ```math
> \begin{gather}
> U_{in} = I_{R1} * R_{1} \\
> U_{out} = I_{R1} * R_{1} + I_{R1} * R_{f} = I_{R1} (R_{1}+R_{F}) \\
> A = \frac{U_{out}}{U_{in}} = \frac{I_{R1} (R_{1}+R_{F})}{I_{R1} * R_{1}} = 1 + \frac{R_{f}}{R_{1}}
> \end{gather}
> ```

---

> [!NOTE]
> 7. Primerjaj vhodno upornost operacijskega ojačevalnika z invertiranim in
> ne-invertiranim vhodom.

> Pri invertiranem vhodu je upornost enaka R1, pri ne-invertiranem pa nimamo upora v vhodni zanki, kar
> pomeni da bo vhodna upornost bistveno večja.

---

> [!NOTE]
> 8. Ali smemo operacijski ojačevalnik uporabljati brez negativne povratne vezave?

> Načeloma ne, razen če ga uporabljamo kot komparator.

---

> [!NOTE]
> 9. Nariši shemo invertiranega operacijskega ojačevalnika z enojnim napajanjem.
> V čem je težava enojnega napajanja?

> V primerjavi s simetričnim napajanjem, imamo tu problem z ojačanjem izmeničnih signalov.
> Da problem odpravimo lahko uporabimo delilnik napetosti na + vhodu.
> 
> Shema:
> 
> ![](https://github.com/user-attachments/assets/07888de4-5984-4873-9b4b-638c79dcd6d3)

---

> [!NOTE]
> 10. Kdaj je smiselno uporabiti operacijski ojačevalnik v t.i. »buffer« načinu (ojačanje = 1)?

> *Za buffer način velja V<sub>in</sub> =  V<sub>out</sub>. Tako vezje nima ojačanja, posledično pa velja,
> da je vhodni tok zanemarljiv, impedenca pa je zelo majhna.* To vezavo uporabimo npr. ko imamo senzor,
> ki ne zagotavlja dovolj izhodnega toka. Z ojačevalnikom v tej situaciji reproduciramo vhodno napetost
> hkrati pa zagotavljanmo dovolj toka.

---

> [!NOTE]
> 11. Pri realnem operacijskim ojačevalniku je pasovna širina omejena z ojačenjem. Večje je
> ojačanje, manjša bo pasovna širina in obratno. Pri kakšnem ojačenju je frekvenčna pasovna
> širina maksimalna?

> Maksimalna pasovna širina je pri ojačanju 1. (Idealni operacijski ojačevalnik ima neskončno pasovno širino.)

---

> [!NOTE]
> 12. Imamo operacijski ojačevalec z negativno povratno zanko, ki določa ojačenje v vrednosti
> A=100. Kakšna bo pasovna širina tega ojačevalca, če uporabimo podatke iz spodnje krivulje.
> GBP=Ojačenje×Pasovna širina(Unity Gain).
> ![](https://github.com/user-attachments/assets/5edd78f9-e78d-4ed8-85ac-9bf0bd16ed65)

> [!IMPORTANT]
> Formule:
> 
> ```math
> \begin{gather}
> GBP = Ojačanje * PasovnaSirina(UnityGain) \\
> PasovnaSirina[Hz] = \frac{GBP}{Ojačanje} \\
> \end{gather}
> ```

> Da izračunamo vstavimo v log podano številko:
> ```math
> \begin{gather}
> A[dB] = 20log(\frac{U_{izh}}{U_{vh}}) = 40dB
> \end{gather}
> ```

---

> [!NOTE]
> 13. Nariši shemo mostičnega vezja H in razloži za kaj ga uporabljamo.

> Shema:
> 
> ![](https://github.com/user-attachments/assets/e482ce40-77fa-487d-a553-3e8c9afa1d5e)
>
> Uporablja se za kontrolo DC motorjev. Motor lahko:
> - vrtimo levo
> - vrtimo desno
> - ustavimo (s tem da sklenemo vzporedni stikali)

---

> [!NOTE]
> 14. Razloži delovanje servo motorja.

> (Stvar je tečna za razlagat ampak nekej v tem smislu)
> Motor sestavljajo potenciometer, DC motor in kontrolno vezje. Potencjometer lahko določi
> trenutno rotacijo motorja, to sporoči kotrolnemu vezju, to pa lahko nato DC motor zavrti,
> da izhod servo motorja dobi željeno rotacijo.
> ![image](https://github.com/user-attachments/assets/db42bc6a-854f-4c32-abf2-cba5d8e6465b)

---

> [!NOTE]
> 15. S kakšnim signalom krmilimo servo motor?

> Servo motor krimilimo s PWM signalom s periodo 20ms (50Hz).

---

> [!NOTE]
> 16. Nariši vezavo 2 polnega koračnega motorja in mostičnega vezja H.

> ![](https://github.com/user-attachments/assets/6be265d3-caf9-447a-a845-67ee2b540f0e)

---

> [!NOTE]
> 17. Razloži fizikalni princip delovanja LCD prikazovalnika.

> Ekran je osvetljen z neko svetlobo (od odzadaj ali spredaj). Ta svetloba gre najprej
> čez en sloj vertikano polariziranega stekla, ki prepušča le pravilno obrnjeno polarizirano svetlobo.
> Na tej točki ostane le vertikalno polarizirana svetloba. Ta gre nato čez LC (Liquid Crystal) elektrodo.
> Če je ta brez napetosti bo zaradi stanja kristalov povzročila 90° zasuka, če pa je napetost prisotna,
> polarizacija svetloba ni spremenjena. Temu sledi še sloj horizontalno polariziranega stekla, ki bo prepuščalo
> le svetlobo, katere polarizacija je bila obrnjena za  90°.

---

> [!NOTE]
> 18. Razloži sinhronizacijo asinhronega serijskega protokola UART.

> 

---

> [!NOTE]
> 19. Nariši povezavo mikrokrmilnika z 3 perifernimi enotami preko SPI vodila in razloži pomen
> posameznih SPI signalov.

> ![](https://github.com/user-attachments/assets/8062fe79-e182-4c4b-bc19-d3e1385ad7e1)
> - SCLK (Serial Clock) - Clock signal od master naprave
> - MOSI (Master Out Slave In) - Serijski podatki od master naprave za slave naprave
> - MISO (Master In Slave Out) - Serijski podatki od slave naprave za master naprave
> - SS (Slave Select) - Uporabljen da izberemo slave device za trenutno povezavo
> 
> __*Zna bit da vpračanje sprasuje po čem drugem zato si poglej [Moodle](https://moodle2.vegova.si/mod/resource/view.php?id=27720)*__

---

> [!NOTE]
> 20. Nariši povezavo mikrokrmilnika z 3 perifernimi enotami preko I2C vodila in razloži pomen
posameznih I2C signalov.

> ![](https://github.com/user-attachments/assets/6f17fac4-a7c7-4d1b-b70d-4314393068bd)
> - SDA - Podatkovna linija
> - SCL - Serijska ura
> 
> __*Zna bit da vpračanje sprasuje po čem drugem zato si poglej [Moodle](https://moodle2.vegova.si/mod/resource/view.php?id=27781)*__

---

![](https://cdn.discordapp.com/attachments/1221482994066264157/1357778077714747563/PXL_20250404_175931654.jpg?ex=67f170e0&is=67f01f60&hm=c77e157499468c9d0186c4fc86596c6521f7b8adab058fa5d9ab9fb8d8e8376a&)
![](https://cdn.discordapp.com/attachments/1221482994066264157/1357778076846522478/PXL_20250404_175937662.MP.jpg?ex=67f170df&is=67f01f5f&hm=d56fcdee8c5e84e9a65e1753a773050f23db1677efa35382e25e3cc4e2f7b1c6&)
![](https://cdn.discordapp.com/attachments/1221482994066264157/1357778075953139813/PXL_20250404_175942361.jpg?ex=67f170df&is=67f01f5f&hm=bbd33d763717722d98b954145d5702a56465f6dd2e11ea1c8e9da1e869471812&)
![](https://cdn.discordapp.com/attachments/1221482994066264157/1357778074950832138/PXL_20250404_175947784.MP.jpg?ex=67f170df&is=67f01f5f&hm=ed2c70e7a55bdeaf4e316f0227b1093537eee8f0247282864c2ba52261a127ce&)
![](https://cdn.discordapp.com/attachments/1221482994066264157/1357778073952452628/PXL_20250404_175952695.jpg?ex=67f170df&is=67f01f5f&hm=0fb8fe076057a328152ae9b97e11e4c8ec1c11a371646176720c14b0f11f7d38&)
