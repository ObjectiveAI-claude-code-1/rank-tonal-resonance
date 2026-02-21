# rank-tonal-resonance

A vector function that ranks candidate video game titles by how well each one matches the emotional register, mood, and tone of the game as conveyed by its description.

## Purpose

A title is the first thing a player encounters, and it sets an expectation — not about what the game is about, but about how the game will feel. Two games can share a theme (survival, exploration, war) and yet feel entirely different: one bleak and harrowing, the other lighthearted and comedic. Their titles should not be interchangeable.

`rank-tonal-resonance` evaluates **tonal resonance** — the degree to which a title sounds the way a game feels. It distinguishes between thematic relevance (what a game is about) and tonal fit (how a game feels), focusing exclusively on the latter. Titles that create tonal dissonance, such as a whimsical name for a grim game or a somber name for a playful one, are ranked lower. Titles whose tone is pitch-perfect for the game's emotional character are ranked higher.

## Input

The function accepts an object with two required fields:

| Field | Type | Description |
|---|---|---|
| `game_description` | `string` | A description of the video game conveying its mood, tone, and emotional character. This serves as the emotional source of truth. |
| `titles` | `string[]` (min: 2) | An array of candidate titles to rank by tonal resonance. |

### Example Input

```json
{
  "game_description": "A solitary astronaut drifts through the ruins of a collapsed space station, piecing together audio logs from a crew that slowly turned on each other. The atmosphere is claustrophobic and heavy with dread. Every corridor feels like a held breath. There is no combat — only the growing certainty that something went terribly wrong, and the quiet horror of understanding what it was.",
  "titles": [
    "Starfield Adventures",
    "Dead Frequency",
    "Cosmic Buddies",
    "The Silence After"
  ]
}
```

## Output

The function returns an array of scores corresponding to each title in the input array. Higher scores indicate stronger tonal resonance with the game's emotional character. The scores sum to approximately 1, forming a probability distribution across the candidates.

### Example Output

```json
[0.05, 0.38, 0.02, 0.55]
```

In this example, "The Silence After" scores highest because its quiet, heavy tone precisely matches the game's atmosphere of dread and slow revelation. "Dead Frequency" also scores well — its mood is appropriately dark and tense. "Starfield Adventures" and "Cosmic Buddies" score poorly because their buoyant, playful tones create stark dissonance with the game's claustrophobic horror.

## What It Evaluates

The function evaluates three core qualities of tonal resonance:

### 1. Emotional Weight Alignment

Every title carries a sense of gravity or lightness — a feeling of heft or buoyancy that registers before the reader has fully processed the title's meaning. "Abyssal" lands heavy; "Sprout" lifts upward. This quality assesses whether the title's emotional weight matches the game's emotional intensity. A psychologically dense game needs a title that arrives with weight. A breezy, carefree game needs a title that feels unburdened. When a title's weight contradicts the game's intensity, the mismatch registers instinctively — something feels wrong before the player can articulate what.

### 2. Mood Congruence

Where emotional weight concerns intensity and gravity, mood concerns color and atmosphere. Mood is the specific emotional climate a title evokes — whether it feels eerie, jubilant, melancholic, tense, serene, mischievous, or desperate. A survival horror game steeped in isolation needs a title that breathes uneasy air. A cozy farming sim needs a title that feels warm and inviting. This quality assesses whether the title projects the same emotional atmosphere as the game — whether it makes the reader feel, even for a moment, the way the game intends to make the player feel for hours.

### 3. Expressive Precision

The subtlest and most demanding of the three. It is not enough for a title to land in the right emotional neighborhood — it must find the exact address. Two games can both be dark, but one might be gothic and brooding while the other is nihilistic and cold. Two games can both be whimsical, but one might be warmly nostalgic while the other is absurdist and sharp. This quality assesses whether the title captures the specific shade of feeling that defines this particular game. A title with high expressive precision feels inevitable — as though no other combination of words could so exactly name the texture of this experience.

## Use Cases

- **Studio brainstorming.** A game development team with a list of candidate titles can rank them by tonal fit, quickly surfacing which options feel right for their game before investing in focus groups or market testing.
- **Indie developer gut-check.** A solo developer choosing between a handful of names can use the function as a creative sounding board — a way to confirm or challenge their instincts about which title best captures their game's feel.
- **Title generation filtering.** A naming tool or AI generator that produces many candidate titles can use the function as a filtering layer, winnowing a large set down to those that actually sound like the game they name.
- **Publisher review.** When evaluating title proposals for a game in development, a publisher can use the function to objectively assess which titles prepare the player for the emotional experience ahead.