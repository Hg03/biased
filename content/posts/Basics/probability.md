+++
title = "Probability"
date = "2025-08-08"
+++

`The Chance of Something Happening. 1 stands for Certain it will occur and 0 stands for Certain it won't occur.`

# Basics

- **P(A)**: Probability of occurring an event **A**.
$$P(A) = \frac{\text{Preferred Event}}{\text{All Events}}$$
- Ex: Probability of a flipping coin and coming out as a head is:
$$P(A) = \frac{\text{Heads}}{\text{2}} = 0.5$$
	- Reason is that, Coming head is 1 out of two possible outcomes i.e. Heads or Tails hence 1/2 = 0.5.
- **Set**: Collection of possible outcomes.
- **Union**: A = `{1, 3, 5}` & B = `{1, 2, 3}`
$$A \cup B = \{ 1,\, 2,\, 3,\, 5 \}$$
	- **Union** is concerned with values in 1 OR Another set.
- **Intersection**: - Union: A = `{1, 3, 5}` & B = `{1, 2, 3}`, `A u B` = `{1, 2, 3, 5}`
$$A \cap B = \{ 1,\, 3\}$$
	- **Intersection** is concerned with Values in 1 AND Another set.
- **Complement** of `A = {1, 3, 5}` if Set = `{1, 2, 3, 4, 5}` is `{2, 4}`

# Conditional Probability

`Probability Changes given another event occurs.`

- **P(A | B)**: Probability of A Given B.
- Probability of 5 (A) Given the value is Odd (B) in die roll.

$$P (A | B) = \frac{P (A \cap B)}{P(B)} = \frac{1/6}{1/2} = \frac{1}{3}$$
	- P(B): Probability of occuring odd on a die roll i.e. 3/6 = 1/2.
	- P(A intesection B): Probability of 5 in a die roll i.e. 1/6.

Example Problem: Calculate a probability of selecting a women given that person selected will do exercise ?


| -     | No Exericise | Did Exercise | Total |
| ----- | ------------ | ------------ | ----- |
| Men   | 78           | 22           | 100   |
| Women | 83           | **17**       | 100   |
| Total | 161          | **39**       | 200   |

$$P(A|B) = \frac{P (A \cap B)}{P(B)} = \frac{17/200}{39/200} = 0.436 = 43.6\%$$

# Addition Rule

Take the same table above and calculate the probability of selecting a person is exerciser or a women ?

| -     | No Exericise | Did Exercise | Total   |
| ----- | ------------ | ------------ | ------- |
| Men   | 78           | 22           | 100     |
| Women | 83           | **17**       | **100** |
| Total | 161          | **39**       | 200     |


`If two probabilities are exclusive (independent), we can add it`

$$P(A \cup B) = P(A) + P(B)$$
`If two probabilites are not exclusive (dependent), As above question asked`

$$P(A \cup B) = P(A) + P(B) - P(A \cap B)$$
$$P(A \cup B) = 100/200 + 39/200 - 17/200 = 0.61 = 61\%$$
This is called **Joint Probability**, hence we are looking two characteristics probability.

# Dependent vs Independent

- Event is **Dependent** if: `P(A|B) = P(A) & P(B|A) = P(B)` else it is **Independent** event.
- E.g.
	- **Dependent** Case
		- P(Die is Odd) = 0.5 , P(Roll 2) = 0.167
		- P(Odd | 2) = 0
	- **Independent** Case
		- P(1 or 2) = 0.33 (1/3), P(Die is Odd) = 0.5
		- P(1 or 2 | Odd) = 0.5




## Probability of Independent Events

- Probability of Rolling a 1 and then a 2 (Both event are **independent** of each other), hence multiply probabilities.

$$1/6 \times 1/6 = 0.028 = 2.8 \%$$
- Probability of `mutually exclusive events`, hence add them. You can't roll an even 1.
$$A \cup B = P(A) + P(B)$$
- E.g.
	- Roll 1 u Roll even = 1/6 + 1/2 = 2/3

# Venn Diagrams

`Representation in terms of probabilities.`

![[Pasted image 20250804144654.png]]


# Total Probability

`Probability based on Several Events.`

$$P(A) = \sum_{i=1}^n P(A | B_i) \times P(B_i)$$
- E.g.
	- X breaks: 40,000 Miles, 95 %, 60% of market.
	- Y breaks: 40,000 Miles, 92%, 40% of market
	- Probability Break pads last 40,000 Miles
$$P(A) = 95/100 X 6/10 + 92/100 + 4/10 = (570 + 368)/1000 = 938/1000 = 0.938$$

# Bayes' Theorem

`Helps to find a probability when we know other probabilities.`

$$P(A|B) = \frac{P(A) \times P(B|A)}{P(B)}$$
$$P(A|B) = \frac{P(A) \times P(B|A)}{\sum_{i=n}^n P(A) \times P(B|A)}$$

Take a look on same table:

| -     | No Exericise | Did Exercise | Total   |
| ----- | ------------ | ------------ | ------- |
| Men   | 78           | 22           | 100     |
| Women | 83           | **17**       | **100** |
| Total | 161          | **39**       | 200     |

- Calculate probability that it is a man given that you have an exerciser ?
	- P(Man): 0.5
	- P(Exerciser): 0.195
	- P(Exerciser | Man) = 0.22
	- P(A | B) = (0.5 x 0.22)/ 0.195 = 0.564

