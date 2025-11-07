### 1. Baza Lokacji (`locations.json`)

**Główne zasady projektowe:**

1. **Koszty (`cost`)** to lista obiektów. Dlaczego lista? Bo niektóre lokacje mają złożony koszt (np. 1 Woda I 1 Solari).
    
2. **Efekty (`effects`)** to też lista obiektów. Dlaczego? Bo lokacje dają wiele rzeczy (np. 1 Wpływ I 2 Solari).
    
3. **Wybory (`choice`)** są najtrudniejsze. Proponuję obiekt `{"type": "choice", "options": [ ... ]}`, gdzie `options` to lista... list efektów.
    

#### Przykład `locations.json`:

JSON

```
{
  "arrakeen": {
    "name": "Arrakeen",
    "area": "Fremen",
    "symbol_required": "fremen",
    "cost": [
      { "type": "resource", "resource": "woda", "amount": 2 }
    ],
    "effects": [
      { "type": "resource", "resource": "przyprawa", "amount": 3 },
      { "type": "influence", "faction": "fremen", "amount": 1 }
    ]
  },
  "carthag": {
    "name": "Carthag",
    "area": "Fremen",
    "symbol_required": "fremen",
    "cost": [],
    "effects": [
      { "type": "resource", "resource": "woda", "amount": 1 },
      { "type": "influence", "faction": "fremen", "amount": 1 },
      { "type": "special", "effect_id": "place_influence_any" }
    ]
  },
  "zbiorniki_wody": {
    "name": "Zbiorniki z wodą",
    "area": "Fremen",
    "symbol_required": "fremen",
    "cost": [],
    "effects": [
      {
        "type": "choice",
        "options": [
          // Opcja 1: Weź 2 Wody
          [
            { "type": "resource", "resource": "woda", "amount": 2 }
          ],
          // Opcja 2: Weź 1 Wodę i 1 Wpływ
          [
            { "type": "resource", "resource": "woda", "amount": 1 },
            { "type": "influence", "faction": "fremen", "amount": 1 }
          ]
        ]
      }
    ]
  },
  "wysoka_rada": {
    "name": "Wysoka Rada",
    "area": "Landsraad",
    "symbol_required": "imperium",
    "cost": [
      { "type": "resource", "resource": "solari", "amount": 5 }
    ],
    "effects": [
      { "type": "influence", "faction": "landsraad", "amount": 2 },
      { "type": "special", "effect_id": "gain_council_seat" }
    ]
  }
}
```

**Objaśnienie typów efektów:**

- `{"type": "resource", "resource": "...", "amount": X}`: Do zasobów (woda, solari, przyprawa).
    
- `{"type": "influence", "faction": "...", "amount": X}`: Do wpływu (fremen, gildia, etc.).
    
- `{"type": "troop", "amount": X, "target": "garrison"}`: Do żołnierzy (do garnizonu).
    
- `{"type": "special", "effect_id": "..."}`: Na specjalne akcje (jak "weź Miejsce w Radzie"), które skrypt musi zinterpretować.
    
- `{"type": "choice", "options": [ [efekt1], [efekt2, efekt3] ]}`: Gracz musi wybrać jeden z elementów listy `options`.
    

---

### 2. Baza Kart (`cards.json`)

**Główne zasady projektowe:**

1. **`agent_symbols`**: Lista symboli, jakie daje karta (np. `["fremen"]`, `["gildia", "imperium"]`, lub `["fremen", "bene_gesserit", "gildia", "imperium"]` dla "dowolnego").
    
2. **`agent_effects`**: Efekty tekstowe z GÓRNEJ części karty (np. "Zapłać 2 Solari...").
    
3. **`reveal_effects`**: Efekty z DOLNEJ części karty (Perswazja, Solari, dobranie karty itp.).
    

#### Przykład `cards.json`:


```
{
  "sztylet": {
    "name": "Sztylet",
    "deck_type": "startowa",
    "cost_spice": 0,
    "vp": 0,
    "agent_symbols": ["fremen", "bene_gesserit", "gildia", "imperium"],
    "agent_effects": [
      {
        "type": "conditional_action",
        "cost": [
          { "type": "resource", "resource": "solari", "amount": 2 }
        ],
        "effect": [
          { "type": "combat", "strength": 1 }
        ]
      }
    ],
    "reveal_effects": [
      { "type": "persuasion", "amount": 1 }
    ]
  },
  "diuna_pustynna_planeta": {
    "name": "Diuna, Pustynna Planeta",
    "deck_type": "rynkowa",
    "cost_spice": 3,
    "vp": 1,
    "agent_symbols": ["fremen"],
    "agent_effects": [],
    "reveal_effects": [
      { "type": "resource", "resource": "solari", "amount": 2 }
    ]
  },
  "wyslannik_gildii": {
    "name": "Wysłannik Gildii",
    "deck_type": "rynkowa",
    "cost_spice": 4,
    "vp": 0,
    "agent_symbols": ["gildia", "imperium"],
    "agent_effects": [
      {
        "type": "choice",
        "options": [
          [
            { "type": "resource", "resource": "woda", "amount": 1 }
          ],
          [
            { "type": "troop", "amount": 2, "target": "garrison" }
          ]
        ]
      }
    ],
    "reveal_effects": [
      { "type": "persuasion", "amount": 2 },
      { "type": "draw_card", "amount": 1 }
    ]
  }
}
```

**Objaśnienie typów efektów (karty):**

- `{"type": "persuasion", "amount": X}`: Siła kupna.
    
- `{"type": "draw_card", "amount": X}`: Dobranie kart.
    
- `{"type": "combat", "strength": X}`: Siła w konflikcie.
    
- `{"type": "conditional_action", "cost": [...], "effect": [...]}`: Kluczowe dla efektów "Zapłać X aby dostać Y".
    

### Podsumowanie

1. Gracz wpisuje: `karta: sztylet`, `lokacja: arrakeen`.
    
2. Skrypt sprawdza `cards.json` -> `sztylet` -> `agent_symbols`. Czy zawiera `fremen`? Tak.
    
3. Skrypt sprawdza `locations.json` -> `arrakeen` -> `cost`. Czy gracz ma 2 Wody?
    
4. Jeśli tak, skrypt sam aktualizuje stan gry: odejmuje 2 Wody, dodaje 3 Przyprawy i 1 Wpływ u Fremenów.
    
5. Następnie pyta gracza: "`Sztylet` ma akcję warunkową. Czy chcesz zapłacić 2 Solari za +1 Siły? (T/N)".
