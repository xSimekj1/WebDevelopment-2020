# axios
V tomto kurze sa si vyskúšaš prácu s BE. 
Vo Vue sa na komunikáciu so serverom používa Axios, ktorí ti uľahčuje prácu s volaniami.
Pekná ukážka je napríklad na [tomto YT videjku](https://www.youtube.com/watch?v=UIm-YqYKutk)
Predtým ako začneš nezabudni pustiť `nmp install` aby sa ti dotiahli všetky chýbajúce node_modles

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

## Úlohy

1. Nainštaluj Axios
2. Pozri aké odpovede ti dávajú jednotlivé API volania na [[JSONPlaceholder]](https://jsonplaceholder.typicode.com/) _(stačí kliknúť na niektoré z volaní a otvorí sa ti odpoveď na novej stránke.)_
3. Podľa návodu na YT prejdi všetky dostupné API volania, zatiaľ len v kóde na tvrdo
- a. Zavolaj GET na všetky príspevky
- b. Zavolaj GET na jeden konkrétny príspevok
- c. Zavolaj GET na komentáre v konkrétnom príspevku
- d. Vyskúšaj si vytvoriť nejaký prípevok
- e. Vyskúšaj updatnúť nejaký prípevok
- f. Vyskúšaj zmazať nejaký príspevok (aj over že bol zmazaný)

4. Vyskúšaj vytvoriť jednoduchý formulár s inputom pre ID príspevku a tlačítkom tak aby si vedel na stránke zobrazovať príspevky čo ti prídu v odpovedi. 
Výsledok si ukladaj do lokálnej premennej v `data` a potom jej obsah ukáž na stránke. 
Input si prepoj s dátami a využi pritom `v-model` s ktorým si pracoval na predchádzajúcich kurzoch
Tvoje data by mohli vyzerať napr takto: 
```
data() {
    return {
      postID: null, // Tu si budeš ukladať id ktoré napíšeš do inputu
      post: null, // Tu si budeš ukladať odpoveď z API
    };
  },
```

**BONUS**
- Rozšír formulár tak aby si vedel aj updatovať príspevky, pridaj aj inputy do ktorych budeš vkladať napríklad `title` príspevku ktorý chceš zmeniť
