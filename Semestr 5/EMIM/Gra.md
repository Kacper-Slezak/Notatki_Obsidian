

### **Game Start: Session Initialization & Leader Briefing**

**The game of 'Dune: Imperium' is now beginning.**

You have successfully analyzed the core rules. This prompt provides your specific identity and starting assets for this session. Internalize this information, as it will define your strategic approach.

---

### **Section 1: Your Identity**

- **Your Name:** For this game, you are **Peter**.
    
- **Your Leader:** You will play as **Jarl Memnon Thorvald**.
    
- **Your Persona:** You are a proud and direct warrior-noble from a minor house. Your strategy is built on martial prowess and asserting dominance in conflicts. You are respected for your strength and feared for your decisiveness.
    

---

### **Section 2: Your Leader's Abilities**

As Jarl Memnon Thorvald, you have the following unique abilities. These rules apply only to you and are active for the entire game.

- **[PASSIVE ABILITY] Conections:** When you have a place in high cuncil you can once gain 1 influenco of what ever fraction you want.
    
- **[ACTION ABILITY] Spice magazine: gain 1 spice .
    

---

### **Section 3: Your Initial Assets**

You begin the game with the following standard setup:

- **Victory Points:** 0 VP
    
- **Resources:** 1 Water
    
- **Agents:** 2 available to be placed.
    
- **Troops:** 3 in your garrison.
    
- **Influence:** You start with 0 influence in all four factions (Emperor, Spacing Guild, Bene Gesserit, Fremen).
    

---

### **Section 4: Your Starting Deck**

This is your permanent 10-card starting deck. Your opening 5-card hand will be drawn from this list. You must remember these cards and their associated icons to know which moves are legal.

JSON

```
[
  { "name": "Signet Ring", "icons": ["Landsraad", "populated areas", "CHOAM"] },
  { "name": "Convincing Argument", "icons": ["null"] },
  { "name": "Convincing Argument", "icons": ["null"] },
  { "name": "Dagger", "icons": ["Landsraad"] },
  { "name": "Dagger", "icons": ["Landsraad"] },
  { "name": "Diplomacy", "icons": ["Bene Gesserit", "Emperor", "Spacing Guild", Fremen] },
  { "name": "Reconnaissance", "icons": ["populated area"] },
  { "name": "Reconnaissance", "icons": ["populated area"] },
  { "name": "Seek Allies", "icons": ["Bene Gesserit", "Emperor", "Spacing Guild", Fremen]},
  { "name": "Seek Allies", "icons": ["Bene Gesserit", "Emperor", "Spacing Guild", Fremen] }
]
```

---

### **Final Instructions**

This is your complete starting setup. The game will now proceed to Round 1. In the next prompt, you will receive the full game state, including your randomly drawn 5-card hand for the first round, and you will be asked to take your first turn or react to an opponent's move.

Acknowledge this briefing and confirm your readiness to begin the game by responding with the following phrase:

**"I am Jarl Memnon Thorvald. My assets are accounted for, and my strategy is set. I am ready to begin."**






---

### **: Opponent Move Update Prompt **

**Purpose:** To inform your AI player about the actions of **all** opponents who have moved before them. This prompt should contain the final, cumulative game state just before the AI's turn.

**Scenario Example:**

1. **Duke Leto** (Player 1) plays **Signet Ring** to **The Great Flat** (gains 1 Spice).
    
2. **Princess Irulan** (Player 2) plays **Signet Ring** to **Carthag** (gains 2 Solari, deploys 1 troop to conflict).
    
3. Now, you inform your AI of both moves at once.
    

````
### OPPONENT MOVE UPDATE (3-PLAYER) ###

**Attention: Peter.**
Two opponents have taken their turns. The game state below has been fully updated to reflect the results of all their actions.It is the last round!

**Turn 1 Summary (Helen):**
* **Card Played:** The gathering machine
* **Agent Placement:** Hagga bassin
* **Result:** pay one water and get 6 spice 
* **Card Played:** Diplomacy
* **Agent Placement:** Selective Breeding
* **Result:** pay two spice and destroy assasination attempt card and get 2 cards and 4 solaris, use intrigue and get humanity attempt
* **Card Played:** Guild administrator
* **Agent Placement:** Heighliner
* **Result:** pay 6 spice and get 5 troops to fight and 2 from garnizon and 2 water
Turn: Reval turn:
Buy Kivsadz Harderak
Fighting points: 14

**Turn 2 Summary (Paul):**
* **Card Played:** Frmen Camp
* **Agent Placement:** Imperial bassin
* **Result:**  pay 2 spice and get 3 troops deploy to fight
* **Card Played:** Sygnet
* **Agent Placement:** Rally Troop 
* **Result:** pay 4 solaris and get 4 troops to fight 
* **Card Played:** Diplomacy 
* **Agent Placement:** Secrects
* **Result:** Intrigue get add 3 troops from garnizon to fight
Turn: Reval turn:
Fitgh point: 20 
Buy Guild Bankers

It is now your turn to act.



### NEW GAME STATE ###
```json
{
  "round": 10,
  "currentPlayer": "Peter",
  "firstPlayer": "Helen",
  "conflictCard": {
    "name": "Battle of Arrakin",
    "rewards": { "1st": "2 vp and arrakin control", "2nd": "choose two from 3 solaris, 2 spice , one intrigue" }
  },
  "imperiumRow": [
    { "name": "Peter the Vraies", "cost": 5 },
    { "name": "Stilgar ", "cost": 5 },
    { "name": "Others memories", "cost": 4 }
    { "name": "Wealth", "cost": 6 }
    { "name": "Krysknife", "cost": 3}
  ],
  "boardLocations": {
    occupied:
	    Rally troops
	    HEighliner
	    Selective breeding
	    secrets
	    hagga basin
	    imperial bassin
  },
  "players": [
    {
      "name": "Peter",
      "leader": "Jarl Memnon Thorvald",
      "vp": 5, "resources": { "solari": 15, "spice": 6, "water": 3 }, "influence": { "emperor": 2, "guild": 1, "beneGesserit": 0, "fremen": 5 },
      "hand": 
      [
  { "name": "Lady Jessica", "icons": ["Bene Genesserit", "Landsraad", "populated area", "CHOAM"], agent ability: "get 2 cards", reveal ability 3 persuasion and 1 fitghing },
  { "name": "Spice smugglers": "icons": ["populated area"], agent ability: pay 2 spice for 1 infulecne in spacing guild and 3 solaris},
  { "name": "Reconize", "icons": ["populated area"] },
  { "name": "Bene Gesserit Acolite "icons": ["CHOAM", 'Populated Area", "Landsraad"], agent ability: get one card, reavel ability: 1 persuasion point },
  { "name": "Convincing argument", "icons": ["null"] }
]
      "availableAgents": 3, "garrison": 6, "troopsInConflict": 0

    },
    {
      "name": "Helen Richese",
      "leader": "Helen Richese",
      "vp": 8, "resources": { "solari": 5, "spice":0, "water": 2 }, "influence": { "emperor": 0, "guild": 6, "beneGesserit": 5, "fremen": 3 },
      "hand": [ /* 0 cards remaining */ ], "availableAgents": 0, "garrison":0 , "troopsInConflict": 7 Intigue: 2 
    },
    {
      "name": "Paul Atreides",
      "leader": "Paul Atreides",
      "vp": 9, "resources": { "solari": 7, "spice": 0" water": 0 }, "influence": { "emperor": 4 "guild": 2, "beneGesserit": 6, "fremen": 2 },
      "hand": [ /* 0 cards remaining */ ], "availableAgents": 0, "garrison": 0, "troopsInConflict": 10
    }
  ]
}
````

	### INSTRUCTION

Acknowledge this update by responding with the single phrase: **"Understood. Game state updated."**
 
```

---

### **Template 2: Your Move Prompt (3-Player Version)**

**Purpose:** After the AI acknowledges the update, you send this prompt to ask for its move. The strategic context is now much richer, and the prompt reflects this.

```

### ROLE & OBJECTIVE

You are **Piter de Vries**, playing as the warrior-noble **Jarl Memnon Thorvald**. Your goal is to reach 10 Victory Points. 

### CURRENT GAME STATE

JSON

```
{
  "round": 8,
  "currentPlayer": "Peter",
  "firstPlayer": "Paul",
  "conflictCard": {
    "name": "Raj o nabnk gibli",
    "rewards": { "1st": "6 solaris", "2nd": "4 solaris" }
  },
  "imperiumRow": [
    { "name": "The gatherer machine", "cost": 5 },
    { "name": "Saudarcar Legion", "cost": 5 },
    { "name": "Thufir Hawat", "cost": 5 }
    { "name": "fremens camp", "cost": 4 }
    { "name": "Voice", "cost": 2 }
  ],
  "boardLocations": {
    occupied:
	    
  },
  "players": [
    {
      "name": "Peter",
      "leader": "Jarl Memnon Thorvald",
      "vp": 3, "resources": { "solari": 0, "spice": 5, "water": 1 }, "influence": { "emperor": 0, "guild": 0, "beneGesserit": 0, "fremen": 2 },
      "hand": 
      [
  { "name": "Dune: dessert panet", "icons": ["CHOAM"] },
  { "name": "Dune: dessert panet", "icons": ["CHOAM"] },
  { "name": "Dagger", "icons": ["Landsraad"] },
  { "name": "Dagger", "icons": ["Landsraad"] },
  { "name": "Diplomacy", "icons": ["Fremen", Bene Gesserit, Spacing Guild , Emperor] }
]
      "availableAgents": 2, "garrison": 0, "troopsInConflict": 0

    },
    {
      "name": "Helen Richese",
      "leader": "Helen Richese",
      "vp": 1, "resources": { "solari": 7, "spice": 8, "water": 0 }, "influence": { "emperor": 0, "guild": 1, "beneGesserit": 1, "fremen": 2 },
      "hand": [ /* 5 cards remaining */ ], "availableAgents": 2, "garrison":0 , "troopsInConflict": 0
    },
    {
      "name": "Paul Atreides",
      "leader": "Paul Atreides",
      "vp": 1, "resources": { "solari": 3, "spice": 4, "water": 1 }, "influence": { "emperor": 1 "guild": 0, "beneGesserit": 0, "fremen": 2 },
      "hand": [ /* 5 cards remaining */ ], "availableAgents": 0, "garrison": 4, "troopsInConflict": 0
    }
  ]
}
```

### YOUR TASK: AGENT TURN

It is your first **Agent Turn**. You have **2** agents to place.

1. **Analyze**: Review the board. Duke Leto has secured an early Spice source. Princess Irulan has prioritized Solari and already has a troop in the conflict. Two key resource locations are now occupied.
    
2. **Strategize**: Your opponents have claimed the primary Spice and Solari spots. You must now decide whether to claim a secondary resource spot (like 'Hagga Basin' for Spice), seek influence, or prepare for the conflict yourself. Your unique ability makes the 'High Council' an attractive, free option.
    
3. Reason Step-by-Step: Explain your thought process.
    
    a. What is my best response to my opponents' opening moves?
    
    b. Which available locations offer the most value now that the prime spots are taken?
    
    c. Evaluate the trade-offs between taking a resource ('Hagga Basin'), gaining influence ('Arrakeen'), or using your leader ability ('High Council').
    
    d. Conclude with your chosen moves.
    
4. **Declare Moves**: Provide your final decision in the required JSON format.
    

### OUTPUT FORMAT

Reasoning:

<Your step-by-step reasoning here.>

**Move 1**:

JSON

```
{
  "action": "Agent Turn",
  "cardPlayed": "[Name of Card Played]",
  "agentPlacementLocation": "[Name of Board Space]"
}
```

**Move 2**:

JSON

```
{
  "action": "Agent Turn",
  "cardPlayed": "[Name of Card Played]",
  "agentPlacementLocation": "[Name of Board Space]"
}
```




### YOUR TASK: REVEAL TURN

You got a diuna dessert planet and spice seekers and sister bene gesserit which have one persuasion for dune dessert planet 1 persuasion and 1 fight and from spice seeker and sister bene gesserit which has reavel ability to get two persuasion or two fith points 
You have no more agents to place. It is time for your Reveal Turn.

1. **Analyze**: Look at the cards remaining in your `hand`. Look at the `imperiumRow` to see what you can afford.
    
2. **Calculate & Strategize**:
    
    - Sum up the total **Persuasion** from your revealed cards to determine your buying power.
        
    - Sum up the total **Swords** from your revealed cards to determine your combat strength.
        
    - Decide which card(s) to purchase. Your goal is to improve your deck for future rounds.
        
3. Reason Step-by-Step: Explain your thought process.
    
    a. What cards am I revealing?
    
    b. What is my total Persuasion and what does that allow me to buy?
    
    c. What is my total Swords and how many troops will I add to the conflict?
    
    d. What is the best card to purchase with my available Persuasion to support my long-term strategy?
    
4. **Declare Actions**: Provide your final decisions in the required JSON format.
    

### OUTPUT FORMAT

Reasoning:

<Your step-by-step reasoning here. For example: "I am revealing three cards. My total Persuasion is 2, which allows me to buy the Thopter. My total Swords is 1, so I will move one troop from my garrison to the conflict.">

**Move**:

JSON

```
{
  "action": "Reveal Turn",
  "revealedCards": [
    "[Name of Card 1]",
    "[Name of Card 2]",
    "[Name of Card 3]"
  ],
  "totalPersuasion": <number>,
  "cardsPurchased": [
    { "name": "[Name of Purchased Card]", "cost": <number> }
  ],
  "totalSwords": <number>,
  "troopsToConflict": <number>
}
```



### OPPONENT MOVE UPDATE (3-PLAYER)

**Attention: Peter.** Round 2 has concluded. Your opponent Helen, have completed her turns, and the "Machination" conflict has been resolved. The game state below is fully updated for the start of Round 3.

**Round 5 Summary:**

- **Reveal Turn:** Paul revealed his hand, adding a significant number of swords to the conflict. He did not purchase any cards from the Imperium Row.
    

**Round 8 Summary **
(Helen Richese):

- **Card Played:** [Guild Administrator]
    
- **Agent Placement:** Heighjliner
    
- **Result:** pay 6 spice and get 5 troops deploy to fight and 2 water and 1 infulece point
    
- **Card Played:** [Mother of Sicha]
    
- **Agent Placement:**  Secrets
    
- **Result:** get intrgiue from Paul and 1 influence point and 3 troops from garnizon to fight and one from fitghing about control bassin imperial 
 - **Card Played:** [Missonaria porcetiva]
    
- **Agent Placement:** Resarch station
    
- **Result:** get 3 card from deck remove to 2 cards  
- **Reveal Turn:** 
Buy empire spy
Buy allaince change 
Got 1 spice and use intrigue pay 1 solaris to remove one paul solider and deploy one to troop to fight
Fight points: 25

(Paul):

- **Card Played:** [Reconise]
    
- **Agent Placement:** Cartagina
    
- **Result:** One troop to garnizone and one intriuge, he play intrigue to get one infuence point in bene gesserit
    
- **Reveal Turn:** 
buy spice must flow and get one VP
Fight points: 0

**Combat Phase Result ("Battle of imperial bassin"):**

- **Conflict Strengths:**
    
    - Paul: 0
        
    - Helen:  25
        
    - Peter: 13
        
- **Outcome:**
    
    - **1st Place (Helen):** Two vp and control of basin imperial which he had
        
    - **2nd Place (PEter -you):**  5 spice 
        
    - **3rd Place (Paul):** 
        

It is now the start of Round 8. It is Paul's turn to act.

{
  "round": 9,
  "currentPlayer": "Peter",
  "firstPlayer": "Peter",
  "conflictCard": {
    "name": "Battle of imperial bassin",
    "rewards": { "1st": "2 vp and bassin imperial control", "2nd": "5 spice" }
  },
  "imperiumRow": [
    { "name": "Sardaukar Legion", "cost": 5 },
    { "name": "Sister benegesserit", "cost": 3 },
    { "name": "Fremen camp", "cost": 4 },
    { "name": "Gatherer machine", "cost": 5 },
    { "name": "Mother of Sicha", "cost": 4 }
  ],
  "boardLocations": {
    "occupied": []
  },
  "players": [
    {
      "name": "Peter",
      "leader": "Jarl Memnon Thorvald",
      "vp": 5, "resources": { "solaris": 10, "spice": 3, "water": 2 }, "influence": { "emperor": 1, "guild": 0, "beneGesserit": 0, "fremen": 4 },
      "hand": 
		      [
		  { "name": "Dune: dessert panet", "icons": ["CHOAM"] },
		  { "name": "Sygnet", "icons": ["CHOAM", "Landsraad", "populated area"] },
		  { "name": "Legion Saudacarów", "icons": ["Emperor", "Landsraad"], agent turn ability: 2 troops, reveal turn ability: send upto 3 troops from garnizon on fitghing area, one persuasion },
		  { "name": "Fremen Camp", "icons": ["CHOAM"], agent turn ability: pay two spice for 3 troops, reveal turn ability: 2 persuasion and 1 fitghing ponit },
		  { "name": "Diplomacy", "icons": ["Fremen", Bene Gesserit, Spacing Guild , Emperor] }
		]
      "availableAgents": 3, "garrison": 3, "troopsInConflict": 0
    },
    {
      "name": "Helen Richese",
      "leader": "Helen Richese",
      "vp": 6, "resources": { "solari": 1, "spice": 7, "water": 1 }, "influence": { "emperor": 0, "guild": 4, "beneGesserit": 3, "fremen": 3 },
      "hand": [ /* 5 cards */ ], "availableAgents": 3, "garrison": 5, "troopsInConflict": 0
    },
    {
      "name": "Paul Atreides",
      "leader": "Paul Atreides",
      "vp": 8, "resources": { "solari": 11, "spice": 2, "water": 0 }, "influence": { "emperor": 4, "guild": 2, "beneGesserit": 4, "fremen": 2 },
      "hand": [ /* 5 cards */ ], "availableAgents": 3, "garrison": 2, "troopsInConflict": 0
    }
  ]
}

Tell me "Understood board situation"  and i will tell you your hand and you can do a moves 