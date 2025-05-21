# discrete-practicals-
## practical 1 
```
class SET:
    def __init__(self, u_set):
        self.u_set = u_set

    def is_member(self, element):
        return "Element Found" if element in self.u_set else "Element Not Found"

    def powerset(self):
        lst = []
        length = len(self.u_set)
        u_list = list(self.u_set)  # Convert set to list for indexing
        for i in range(1 << length):
            lst.append({u_list[j] for j in range(length) if (i & (1 << j))})
        print("Your Required Powerset Is:", lst)

    def subset(self, subset_set):
        if subset_set.u_set.issubset(self.u_set):
            return "This Is A Subset"
        else:
            return "This Is Not A Subset"

    def union_intersection(self, set2):
        print("Intersection Of Your Sets Is:", self.u_set.intersection(set2.u_set))
        print("Union Of Your Sets Is:", self.u_set.union(set2.u_set))

    def complement(self, complement_set):
        print("Complement Of The Set Is:", self.u_set - complement_set.u_set)

    def difference_and_symmetric_difference(self, set2):
        print("Difference Of The Sets Is:", self.u_set.difference(set2.u_set))
        print("Symmetric Difference Is:", self.u_set.symmetric_difference(set2.u_set))

    def cartesian_product(self, set2):
        product = {(x, y) for x in self.u_set for y in set2.u_set}
        print("Cartesian Product Is:", product)


def set_create(uni="Set"):
    u_set = set(map(int, input(f"Enter elements of {uni} (space-separated): ").split()))
    print(f"{uni} is:", u_set)
    return u_set


def main():
    choice = input("""\nMain Menu:
1. Check whether an element belongs to the set or not
2. List all the elements of the powerset
3. Check whether one set is a subset of the other
4. Find union and intersection of two sets
5. Find complement of a set
6. Find difference and symmetric difference between sets
7. Find cartesian product of sets
Enter your choice (1–7): """)

    if choice == '1':
        set1 = SET(set_create())
        element = int(input("Enter the element to search: "))
        print(set1.is_member(element))
    elif choice == '2':
        set1 = SET(set_create())
        set1.powerset()
    elif choice == '3':
        universal_set = SET(set_create("Universal Set"))
        subset_set = SET(set_create("Subset"))
        print(universal_set.subset(subset_set))
    elif choice == '4':
        set1 = SET(set_create("First Set"))
        set2 = SET(set_create("Second Set"))
        set1.union_intersection(set2)
    elif choice == '5':
        universal_set = SET(set_create("Universal Set"))
        setA = SET(set_create("Subset"))
        universal_set.complement(setA)
    elif choice == '6':
        set1 = SET(set_create("First Set"))
        set2 = SET(set_create("Second Set"))
        set1.difference_and_symmetric_difference(set2)
    elif choice == '7':
        set1 = SET(set_create("First Set"))
        set2 = SET(set_create("Second Set"))
        set1.cartesian_product(set2)
    else:
        print("Invalid choice. Please try again.")
        main()

if __name__ == "__main__":
    for _ in range(8):
        main()
```


## practical2 
```
from numpy import array

class RELATION:
    def __init__(self, matrix):
        self.matrix = matrix
        self.length = len(matrix)

    def reflexive(self):
        for i in range(self.length):
            if not self.matrix[i][i]:
                return False
        return True

    def symmetric(self):
        for i in range(self.length):
            for j in range(self.length):
                if self.matrix[i][j] != self.matrix[j][i]:
                    return False
        return True

    def transitive(self):
        for i in range(self.length):
            for j in range(self.length):
                for k in range(self.length):
                    if self.matrix[i][j] and self.matrix[j][k] and not self.matrix[i][k]:
                        return False
        return True

    def anti_symmetric(self):
        for i in range(self.length):
            for j in range(self.length):
                if i != j and self.matrix[i][j] and self.matrix[j][i]:
                    return False
        return True


def enter_matrix():
    lst = list(map(int, input("Enter all relation matrix values (space-separated): ").split()))
    row = int(input("Enter the number of rows/columns (for square matrix): "))
    matrix = array(lst).reshape(row, row)
    print("Your matrix is:\n", matrix)
    return matrix


def main():
    rel = RELATION(enter_matrix())
    if rel.reflexive() and rel.symmetric() and rel.transitive():
        print("Your Relation is an Equivalence Relation.")
    elif rel.reflexive() and rel.anti_symmetric() and rel.transitive():
        print("Your Relation is a Partial Order Relation.")
    else:
        print("Your Relation is neither Equivalence nor Partial Order.")


if __name__ == "__main__":
    main()
```

## practical 3
```
from itertools import permutations, product

def generate_permutations(Set, repetition):
    if repetition:
        return list(product(Set, repeat=len(Set)))  # With repetition: use product
    else:
        return list(permutations(Set))  # Without repetition: use permutations

def main():
    Set = set(map(int, input("Enter all elements of the set (space-separated): ").split()))
    with_repetition = generate_permutations(Set, repetition=True)
    without_repetition = generate_permutations(Set, repetition=False)

    print("\nPermutations WITH repetition:")
    for perm in with_repetition:
        print(perm)

    print("\nPermutations WITHOUT repetition:")
    for perm in without_repetition:
        print(perm)

    print(f"\nTotal With Repetition: {len(with_repetition)}")
    print(f"Total Without Repetition: {len(without_repetition)}")

if __name__ == "__main__":
    main()
```

## prac 4
```
from itertools import product

def find_solutions(n, C):
    solutions = []
    # Generate all n-tuples with values from 0 to C (inclusive)
    for combo in product(range(C + 1), repeat=n):
        if sum(combo) == C:
            solutions.append(combo)
    return solutions

if __name__ == "__main__":
    n = int(input("Enter number of variables (n): "))
    C = int(input("Enter constant value (C ≤ 10): "))

    if C > 10 or C < 0:
        print("C must be between 0 and 10 (inclusive).")
    else:
        solutions = find_solutions(n, C)
        print(f"\nAll solutions for x1 + x2 + ... + x{n} = {C} are:")
        for sol in solutions:
            print(sol)
        print(f"\nTotal solutions found: {len(solutions)}")
```

## practical 5
```
def solve_function():
    func = list(map(int, input("Enter the coefficients of the function (highest to lowest power), separated by space: ").split()))
    num = int(input("Enter value of variable: "))
    
    value = 0
    degree = len(func) - 1
    
    for i in range(len(func)):
        value += func[i] * (num ** (degree - i))
    
    return value

# Call the function and print the result
print("Value of the function is:", solve_function())
```
## practical 6
```
def is_complete_graph(matrix):
    n = len(matrix)
    for i in range(n):
        for j in range(n):
            if i == j:
                if matrix[i][j] != 0:  # No self-loop
                    return False
            else:
                if matrix[i][j] != 1:  # All distinct pairs must be connected
                    return False
    return True

def main():
    n = int(input("Enter the number of vertices in the graph: "))
    print("Enter the adjacency matrix row by row (space-separated):")

    matrix = []
    for i in range(n):
        row = list(map(int, input(f"Row {i+1}: ").split()))
        if len(row) != n:
            print("Invalid row length. Matrix must be square.")
            return
        matrix.append(row)

    print("\nAdjacency Matrix:")
    for row in matrix:
        print(row)

    if is_complete_graph(matrix):
        print("\nThe graph is a COMPLETE graph.")
    else:
        print("\nThe graph is NOT a complete graph.")

if __name__ == "__main__":
    main()
```
## ppractical 7
```
def is_complete_graph(adj_list):
    n = len(adj_list)
    for vertex, neighbors in adj_list.items():
        if len(neighbors) != n - 1:
            return False
    return True

def main():
    n = int(input("Enter the number of vertices: "))
    adj_list = {}

    print("Enter the adjacency list for each vertex:")
    for i in range(n):
        neighbors = list(map(int, input(f"Enter neighbors of vertex {i} (space-separated): ").split()))
        adj_list[i] = neighbors

    print("\nAdjacency List:")
    for vertex in adj_list:
        print(f"{vertex}: {adj_list[vertex]}")

    if is_complete_graph(adj_list):
        print("\nThe graph is a COMPLETE graph.")
    else:
        print("\nThe graph is NOT a complete graph.")

if __name__ == "__main__":
    main()
```

## practical 8
```
class DirectedGraph:
    def __init__(self, vertices):
        self.vertices = vertices
        self.adj_list = [[] for _ in range(vertices)]

    def add_edge(self, u, v):
        # Add a directed edge from u to v
        self.adj_list[u].append(v)

    def compute_degrees(self):
        in_degree = [0] * self.vertices
        out_degree = [0] * self.vertices

        for u in range(self.vertices):
            out_degree[u] = len(self.adj_list[u])  # Count of outgoing edges
            for v in self.adj_list[u]:
                in_degree[v] += 1  # Count of incoming edges

        print("\nVertex\tIn-Degree\tOut-Degree")
        for i in range(self.vertices):
            print(f"{i}\t{in_degree[i]}\t\t{out_degree[i]}")

    def print_adj_list(self):
        print("\nAdjacency List:")
        for i in range(self.vertices):
            print(f"{i}: {self.adj_list[i]}")


# Main program
if __name__ == "__main__":
    n = int(input("Enter number of vertices: "))
    e = int(input("Enter number of directed edges: "))

    graph = DirectedGraph(n)

    for i in range(e):
        u, v = map(int, input(f"Enter edge {i+1} (from to): ").split())
        graph.add_edge(u, v)

    graph.print_adj_list()
    graph.compute_degrees()

```

outputs prac 1

![image](https://github.com/user-attachments/assets/586290f7-d4de-4989-99bb-dc1873a28471)

![image](https://github.com/user-attachments/assets/fe5e7801-c3a5-41a4-9a95-2142f8d7dfb6)


![image](https://github.com/user-attachments/assets/135866de-3c61-426f-93f5-915f55dd89de)


![image](https://github.com/user-attachments/assets/27f287d2-770c-44c8-b5f1-13ebec85f79b)


![image](https://github.com/user-attachments/assets/360bd3bc-84c8-4cf0-9bf3-5b582361de5d)


![image](https://github.com/user-attachments/assets/def49d88-1f4b-478e-944d-b1ac446fb886)


![image](https://github.com/user-attachments/assets/e1c0bd80-c643-4850-b03b-fbad918990ca)


![image](https://github.com/user-attachments/assets/ba706bdc-f785-4520-818e-24fda7b09dc6)

prac 2
![image](https://github.com/user-attachments/assets/26f60c62-3b62-4049-8812-d9119c93a80f)

![image](https://github.com/user-attachments/assets/71e048ed-93a8-4ae4-8f4e-0fec7d4c4729)

![image](https://github.com/user-attachments/assets/c39a7f31-5f1f-4225-8cda-1f47f976325f)

prac 3 
![image](https://github.com/user-attachments/assets/77e1e53b-224f-4c6c-a910-9ee9d1e11c7c)

practical 4
![image](https://github.com/user-attachments/assets/333542e9-e8e4-487e-be61-fc7cc5e32f39)

prac 5
![image](https://github.com/user-attachments/assets/ee009638-302e-4b25-96c6-9d3290ef2e28)

prac 6
![image](https://github.com/user-attachments/assets/bf612d83-c442-43ee-8461-78cfc27a1b43)
prac 7
![image](https://github.com/user-attachments/assets/f429fc4c-87f8-4732-9a21-895368cc84a4)
prac 8
![image](https://github.com/user-attachments/assets/d121fc22-d44d-41ce-ba30-12e11096e400)
