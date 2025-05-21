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
outputs 

![image](https://github.com/user-attachments/assets/586290f7-d4de-4989-99bb-dc1873a28471)

![image](https://github.com/user-attachments/assets/fe5e7801-c3a5-41a4-9a95-2142f8d7dfb6)


![image](https://github.com/user-attachments/assets/135866de-3c61-426f-93f5-915f55dd89de)


![image](https://github.com/user-attachments/assets/27f287d2-770c-44c8-b5f1-13ebec85f79b)


![image](https://github.com/user-attachments/assets/360bd3bc-84c8-4cf0-9bf3-5b582361de5d)


![image](https://github.com/user-attachments/assets/def49d88-1f4b-478e-944d-b1ac446fb886)


![image](https://github.com/user-attachments/assets/e1c0bd80-c643-4850-b03b-fbad918990ca)


![image](https://github.com/user-attachments/assets/ba706bdc-f785-4520-818e-24fda7b09dc6)


