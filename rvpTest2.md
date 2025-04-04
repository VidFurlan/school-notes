# Vprašanja za prvo ocenjevalno obdobje

> [!NOTE]
> 1. Nariši 4 bitni R-2R DAC pretvornik in razloži delovanje.

> DAC pretvarja digitalne signale v analogne.
> Ta ima 4 upore priklopljene na vhode. Vhod A ima najmanjši vpliv na izhod,
> vhod D pa ima največji vpliv (zaradi števila uporov).
> 4 bitni DAC lahko predstavlja le 2<sup>4</sup> vrednosti saj ima le 4 vhode.
> 
>```
> R - Upor
> A-D - Vhodi
>
>    o-- R --o-- R --o-- R --o-- R --o---o OUT
>    |       |       |       |       |
>    R       R       R       R       R
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
> V \sim \infty
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

![](https://cdn.discordapp.com/attachments/1221482994066264157/1357778077714747563/PXL_20250404_175931654.jpg?ex=67f170e0&is=67f01f60&hm=c77e157499468c9d0186c4fc86596c6521f7b8adab058fa5d9ab9fb8d8e8376a&)
![](https://cdn.discordapp.com/attachments/1221482994066264157/1357778076846522478/PXL_20250404_175937662.MP.jpg?ex=67f170df&is=67f01f5f&hm=d56fcdee8c5e84e9a65e1753a773050f23db1677efa35382e25e3cc4e2f7b1c6&)
![](https://cdn.discordapp.com/attachments/1221482994066264157/1357778075953139813/PXL_20250404_175942361.jpg?ex=67f170df&is=67f01f5f&hm=bbd33d763717722d98b954145d5702a56465f6dd2e11ea1c8e9da1e869471812&)
![](https://cdn.discordapp.com/attachments/1221482994066264157/1357778074950832138/PXL_20250404_175947784.MP.jpg?ex=67f170df&is=67f01f5f&hm=ed2c70e7a55bdeaf4e316f0227b1093537eee8f0247282864c2ba52261a127ce&)
![](https://cdn.discordapp.com/attachments/1221482994066264157/1357778073952452628/PXL_20250404_175952695.jpg?ex=67f170df&is=67f01f5f&hm=0fb8fe076057a328152ae9b97e11e4c8ec1c11a371646176720c14b0f11f7d38&)
