# Povinné ručení v Koopii

## Modelování stornovosti a optimalizace prolongovaného pojistného

Vítejte v Koopii, malé fiktivní zemi s přibližně jedním milionem obyvatel. Více než třetina z nich žije v hlavním městě Koopolis, perle džungle. Kooperativa je největším poskytovatelem povinného ručení pro expediční vozy, kterými místní obyvatelé brázdí džungle a louky své země.

Smlouvy povinného ručení se uzavírají vždy na jeden rok. Při výročí smlouvy klientovi posíláme nabídku nového pojistného, které zohledňuje inflaci a očekávanou škodovost. Klient může novou cenu přijmout, nebo smlouvu stornovat.

Vaším úkolem je vytvořit model, který pro každou smlouvu odhadne pravděpodobnost storna, a odhadnout celkovou stornovost portfolia v příštím roce.

## Modelování stornovosti

Pro každou smlouvu započatou v roce 2026 vytvořte odhad pravděpodobnosti storna:

$$
\hat{p}_i = P(\mathrm{storno}_i = 1 \mid X_i),
$$

kde $X_i$ jsou informace dostupné při nabídce prolongace, například údaje o smlouvě, klientovi, vozidle, pojistném a tržní ceně.

Pro rok 2026 není ve vstupních datech znám skutečný výsledek `storno`. Historická data můžete použít pro návrh, trénink a validaci modelu.

## Optimalizace slevy

Při prolongaci lze klientovi nabídnout slevu 5 % z předepsaného pojistného. Cílem není jen snížit počet storen, ale maximalizovat očekávaný profit portfolia.

Pro smlouvu $i$ definujeme očekávaný profit bez slevy:

$$
\widehat{\pi}_{i,0} = (1 - \hat{p}_{i,0}) \left(PP_{i,0} - \widehat{S}_i\right),
$$

a očekávaný profit po nabídnutí slevy:

$$
\widehat{\pi}_{i,1} = (1 - \hat{p}_{i,1}) \left(0.95 \cdot PP_{i,0} - \widehat{S}_i\right).
$$

Kde:

- $PP_{i,0}$ je původně nabízené předepsané pojistné smlouvy $i$.
- $\hat{p}_{i,0}$ je predikovaná pravděpodobnost storna bez slevy.
- $\hat{p}_{i,1}$ je predikovaná pravděpodobnost storna po aplikaci 5% slevy.
- $\widehat{S}_i$ je odhad očekávaných škod na smlouvě.

Slevu doporučte tehdy, když je očekávaný profit se slevou vyšší než očekávaný profit bez slevy:

$$
\widehat{\pi}_{i,1} > \widehat{\pi}_{i,0}.
$$

## Očekávané výstupy

1. Odhad pravděpodobnosti storna pro každou smlouvu započatou v roce 2026.
2. Odhad celkové stornovosti portfolia v roce 2026.
3. Seznam smluv roku 2026, u kterých doporučujete nabídnout 5% slevu.
4. Stručné zdůvodnění zvolené modelové a optimalizační strategie.
5. Odhad očekávaného přínosu doporučené slevové strategie k profitu.

## Vyhodnocení a určení vítěze

Po odevzdání budou týmy hodnoceny ve dvou samostatných disciplínách:

1. **Přesnost predikce stornovosti** - vyhodnotíme kvalitu predikovaných pravděpodobností storna pro smlouvy roku 2026. Nižší hodnota metriky pravděpodobnostní predikce znamená lepší výsledek.
2. **Přínos slevové strategie k profitu** - vyhodnotíme skutečný celkový profit portfolia po aplikaci navržených slev. Vyšší dosažený profit znamená lepší výsledek.

V každé disciplíně týmy obdrží pořadí. Celkové skóre je aritmetický průměr pořadí z obou disciplín:

$$
\mathrm{celkové\ skóre} = \frac{\mathrm{pořadí\ za\ predikci} + \mathrm{pořadí\ za\ optimalizaci}}{2}.
$$

Vyhrává tým s nejnižším celkovým skóre. Při shodném výsledku rozhoduje lepší pořadí v optimalizační úloze, tedy vyšší dosažený profit po aplikaci slev.

## Doporučený formát odevzdání

```text
smlo_pk | pravdepodobnost_storna | doporucit_slevu
```

Sloupec `doporucit_slevu` obsahuje hodnotu `0` nebo `1`.
