# Solution outputs are

## Imports
```python
import numpy as np
from functools import reduce
import matplotlib.pyplot as plt
plt.style.use('seaborn')
```
## Solution 1
```python
def solution1():
    def adds_n(n):
        return lambda x, y=n: x + y

    adds1 = adds_n(1)
    test = 4
    assert (test + 1 == adds1(test))
    print "Output of", solution1.__name__
    print "'Adding 1 function' i.e., 'adds1(x)' returns: ", adds1(test), " for ", test, " as input"
```
* Output of solution1
'Adding 1 function' i.e., 'adds1(x)' returns:  5  for  4  as input

## Solution 2
```python
def solution2():
    def reverse_string(input):
        return reduce(lambda x, y: x + y, list(reversed(input)))

    test = 'Hello'
    assert ('olleH' == reverse_string(test))
    print "Output of", solution2.__name__
    print "Reverse of '{}' is '{}' ".format(test, reverse_string(test))
```
* Output of solution2
Reverse of 'Hello' is 'olleH' 

## Solution 3
```python
def solution3():
    def tic_tac_toe(board):
        diag1 = [tup for tup in zip(range(3), range(3))]
        diag2 = [tup for tup in zip(range(3), reversed(range(3)))]
        for row in range(3):
            for box in range(row, 3):
                if board[row][box] == 'X':
                    if board[row][:] == ['X', 'X', 'X']:
                        return 'X'
                    elif [board[n][box] for n in range(3)] == ['X', 'X', 'X']:
                        return 'X'
                    elif row == box:
                        if [board[d[0]][d[1]] for d in diag1] == ['X', 'X', 'X']:
                            return 'X'
                        if row == 1 and box == 1:
                            if [board[d[0]][d[1]] for d in diag2] == ['X', 'X', 'X']:
                                return 'X'
                    else:
                        break
                elif board[row][box] == 'O':
                    if board[row][:] == ['O', 'O', 'O']:
                        return 'O'
                    elif [board[n][box] for n in range(3)] == ['O', 'O', 'O']:
                        return 'O'
                    elif row == box:
                        if [board[d[0]][d[1]] for d in diag1] == ['O', 'O', 'O']:
                            return 'O'
                        if row == 1 and box == 1:
                            if [board[d[0]][d[1]] for d in diag2] == ['O', 'O', 'O']:
                                return 'O'
                    else:
                        break
                else:
                    break
        return 'Draw'

    assert (tic_tac_toe([
        ["X", "O", "X"],
        ["O", "X", "O"],
        ["E", "E", "X"]]) == "X")

    assert (tic_tac_toe([
        ["X", "X", "O"],
        ["O", "O", "X"],
        ["X", "X", "O"]]) == "Draw")

    assert (tic_tac_toe([
        ["O", "O", "O"],
        ["O", "X", "X"],
        ["E", "X", "X"]]) == "O")

    print "All asserts of ", solution3.__name__, " passed"
```
* All asserts of  solution3  passed

## Solution 4
```python
    np.random.seed(22)
    VARIANCE = 10

    def random():
        return int(4 * np.random.rand(1))

    class Person:
        def __init__(self, destination):
            self.pos = [0, 0]  # list((np.random.randn(2) * VARIANCE).astype(np.int16))
            self.color = np.random.rand(3)
            self.destination = destination

        def move(self):
            direction = random()
            x_old, y_old = self.pos
            # Left
            if direction == 0:
                self.pos[0] -= 1
            # Right
            elif direction == 1:
                self.pos[0] += 1
            # Up
            elif direction == 2:
                self.pos[1] += 1
            # Down
            elif direction == 3:
                self.pos[1] -= 1

            plt.plot([x_old, self.pos[0]], [y_old, self.pos[1]], c=self.color)
            if self.destination == self.pos:
                return True

    def initialise():
        return list((np.random.randn(2) * VARIANCE/2).astype(np.int8))

    if __name__ == '__main__':
        destination = initialise()
        persons = 10
        treasure_found = False

        people = [Person(destination) for _ in range(persons)]

        plt.figure()
        # plt.grid(True)
        plt.xlim(-30, 30)
        plt.ylim((-30, 30))
        plt.scatter(destination[0], destination[1], marker='*', c='r', label="Treasure")
        plt.annotate("({}, {})".format(destination[0], destination[1]), (destination[0], destination[1]))
        plt.title("Number of people searching are: {}".format(persons))
        plt.legend()

        while not treasure_found:
            for person_instance in people:
                treasure_found = person_instance.move()
                if treasure_found:
                    break
            plt.pause(0.00001)

    plt.show()
```
* ![working_solution](../imgs/random_walk.png)

## Calling part
```python
if __name__ == '__main__':
    solution1()
    solution2()
    solution3()
    solution4()
```