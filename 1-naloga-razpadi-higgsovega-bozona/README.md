# Praktikum strojnega učenja

[Povezava](https://ucilnica.fmf.uni-lj.si/course/view.php?id=520) do spletne učilnice predmeta.

## 1. naloga: MODELIRANJE 1-D PORAZDELITEV: RAZPADI HIGGSOVEGA BOZONA 𝑯→𝝁𝝁

### Navodila in usmeritve

V nadaljevanju sledijo podrobnejša navodila in usmeritve za lažje reševanje naloge.
* Iz surovih ("raw") podatkov zgeneriraj svoje histograme s pomočjo predpripravljene skripte `create_histograms.py`, pri kateri lahko spreminjaš število predalov ("bin"-ov) in m<sub>𝝁𝝁</sub> interval, ki ga boš opazoval/-a.
Histogrami (mejne in sredinske `x` vrednosti predalov, vrednosti in napake) se shranijo v formatu `.npz`.
* Ko imaš zgenerirane svoje histograme, jih lahko izrišeš s pomočjo skripte `visualize_data.py` (ustrezno s prejšnjo točko spremeni ime datotek, ki jih nalagaš).
* Preveri, če so napake res pravilno upoštevane. Lahko jih namenoma pokvariš in ponoviš prva dva koraka, da vidiš vpliv.
* Da se spoznaš z osnovnim fitanjem, najprej zgladi histogram simuliranega ozadja ("simulated background") s pomočjo preprostejših matematičnih funkcij in nadaljuj do različnih teoretično podkrepljenih nastavkov (CMS, ATLAS nastavki). Dobiš funkcijo / vrednosti predalov `m(x_k)`.
* Prilagodi funkcijo CB histogramu simuliranega signala, pri čemer upoštevaj še dodatni normalizacijski faktor. Dobiš funkcijo / vrednosti predalov `s(x_k)`.
* Ker simulacija ozadja ni vedno najboljša, se po navadi za oceno ozadja raje vzame izmerjene podatke, pri čemer pa je potrebno izključiti območje, kjer pričakujemo signal ("blinding") - nočemo fitati še signala! Prilagodi torej funkcijo histogramu podatkov, da dobiš dobro oceno za ozadje ("background from data") in pri tem pazi, da pri fitu \textbf{ne} upoštevaš območja okrog mase Higgsovega bozona, npr. izključi interval 120 - 130 GeV. Dobiš funkcijo / vrednosti predalov `b(x_k)`.
* Od podatkov odštej čim bolje zglajeno ozadje, ki si ga dobil/-a v prejšnji točki, da dobiš ekstrahiran signal. Če so vrednosti podatkov `d(x_k)`, dobimo ekstrahiran signal `y(x_k)` kot `y(x_k) = d(x_k) - b(x_k)`.
* Na ekstrahiran signal fitaj CB funkcijo s prostimi parametri, ki si jih dobil/-a v točki 5 tako, da ji v resnici prilagodiš le nov normalizacijski faktor, npr.: `𝛂 * s(x_k)`. Optimalno je, da je le-ta blizu 1.
* Ker je izmerjenega signala še zelo malo, predlagamo, da postopek najprej narediš z umetno napihnjenim signalom - le tega množi z nekim faktorjem (npr. `𝜸 = 100`) in ga dodaj podatkom (`s_{new}(x_k) = 𝜸 * s(x_k)` in `d(x_k) = d(x_k) + s_{new}(x_k)`). Ker bo signal na ta način lepo izstopal iz ozadja, ga boš lažje izluščil/-a.
