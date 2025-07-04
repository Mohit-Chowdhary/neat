# pong-neat-ai

> 🧠 A neural network learns to play Pong — trained via NEAT (NeuroEvolution of Augmenting Topologies) with Pygame.  
> The AI competes against itself or the player, using only paddle/ball position inputs to learn strategy over time.

---

## 🎮 Project Overview

This project trains an AI to play **Pong** using **NEAT-Python**, a genetic algorithm that evolves neural networks.  
Two AIs can battle each other, or one can be tested against a human-controlled paddle.

---

## 🧠 How It Works

- The AI receives only:
  - Its own paddle Y position
  - The ball Y position
  - The X distance between paddle and ball

- The network outputs:
  - 0: Do nothing
  - 1: Move paddle up
  - 2: Move paddle down

- Fitness is based on **number of hits** (not wins) — incentivizing longer rallies and better reaction.

- Training is done using **NEAT's population evolution**.
- Networks are saved via **pickle** checkpoints to resume or test.

---

## 🚀 Features

- Human vs AI mode (`test_ai`)
- AI vs AI mode (`train_ai`)
- Real-time paddle movement and ball physics via `Pygame`
- Save/load best network using `pickle`
- Checkpoints every generation via `neat.Checkpointer`
- Toggle training/test mode from `__main__` block

---

## 🛠 Technologies

- Python
- [Pygame](https://www.pygame.org/)
- [NEAT-Python](https://neat-python.readthedocs.io/en/latest/)
- Pickle for model persistence

---

## ⚙️ How to Run

### 1. Install requirements

```bash
pip install pygame neat-python
```

2. Run training (optional)
Uncomment the line in __main__:

```python
run_neat(config)
```
Then run:

```bash
python main.py
```
This trains the AI over generations and saves checkpoints + best.pickle.

3. Run test mode (play AI)
```python
test_ai(config)
```
This loads best.pickle and runs a visual game:

You play left paddle (W/S)

AI controls right paddle

🧪 Inputs and Fitness
Input to NN	Description
self.right_paddle.y	Current Y of paddle
self.ball.y	Y position of ball
abs(paddle.x - ball.x)	Horizontal distance to ball

Output from NN	Action
0	Do nothing
1	Move up
2	Move down

Fitness function:
Each genome earns +1 fitness per paddle hit. Long rallies = smarter AIs.

💾 Checkpointing
Saves state with neat-checkpoint-*

You can resume from a specific generation with:

```python
p = neat.Checkpointer.restore_checkpoint('neat-checkpoint-16')
```
📁 File Structure
bash
Copy
Edit
pong/
├── main.py               # Training & testing logic
├── pong.py               # Game logic (paddles, ball, scores)
├── config.txt            # NEAT configuration file
├── best.pickle           # Trained genome (AI)


📚 What I Learned
How to structure a NEAT training loop for a game environment

How to assign fitness in a way that leads to strategic behavior

Using pickle to serialize a neural network for real-time testing

Combining classic game loops with evolutionary AI
