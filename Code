import numpy as np
import itertools 
import time
import matplotlib.pyplot as plt
from itertools import permutations
from itertools import product

num_consensus = 0
num_secure = 0
num_cap_secure = 0
num_abundant = 0
num_cap_abundant = 0
n = 4
m = 5


def generate_random_binary_matrix(rows, cols):
    return np.random.randint(2, size=(rows, cols))

def generate_allocations(n, m):
    items = list(range(0, m))  
    agents = list(range(0, n))  
    all_allocations = list(product(agents, repeat=m))
    all_allocations = set(all_allocations)
    return all_allocations

allocations = generate_allocations(n, m)
# print("Allocation:", allocations)

All_allocations = []
for allocation in allocations:
    dict = {}
    for i in range(0, n):
        indices = [index for index, value in enumerate(allocation) if value == i]
        if i in dict.keys():
            dict[i].append(indices)
        else:
            dict[i] = indices
    All_allocations.append(dict)

for item in All_allocations:
    print(item)

print("total no. of allocations, length of all_allocation;",len(All_allocations))
    

for i in range(100):

    M = generate_random_binary_matrix(n, m)
    print("M: \n", M)


    Valuations = []

    for allocation in All_allocations:
        Valuation_matrix =[[0] * len(M) for _ in range(len(M))]
        for i in range(len(Valuation_matrix)):
            for j in range(len(Valuation_matrix[i])):
                for k in allocation[j]:
                    Valuation_matrix[i][j] = Valuation_matrix[i][j] + M[i][k]
        Valuations.append(Valuation_matrix)

    # for element in Valuations:
    #     print(element)

    def is_bivalued(matrix):
        flat_list = [element for row in matrix for element in row]
        if len(set(flat_list))>2:
            return False
        return True

    Check_Consensus = []
    for element in Valuations:
        Check_Consensus.append(is_bivalued(element))

    if any(Check_Consensus):
        num_consensus=num_consensus+1

    def is_secure(matrix):
        secure = 0
        for i in range(len(matrix)):
            diagonal_entry = matrix[i][i]
            column_values = [row[i] for row in matrix]
            if diagonal_entry == max(column_values):
                secure = secure+1
        if secure == len(matrix):
            return True
        return False

    Check_Secure = []
    Secure_Allocations = []
    for element in Valuations:
        Check_Secure.append(is_secure(element))
        if is_secure(element):
            my_index = Valuations.index(element)
            Secure_Allocations.append(All_allocations[my_index])

    Check_Cap_Secure = []
    Capacitated_Secure_Allocations = []
    for element in Secure_Allocations:
        if all(len(value) < (m/n) + 1 for value in element.values()):
            Capacitated_Secure_Allocations.append(element)
            Check_Cap_Secure.append(True)



    def is_abundant(matrix):
        abundant = 0
        for i in range(len(matrix)):
            diagonal_entry = matrix[i][i]
            column_values = [row[i] for row in matrix]
            if diagonal_entry == min(column_values):
                abundant = abundant+1
        if abundant == len(matrix):
            return True
        return False
    
    Check_Abundant = []
    Abundant_Allocations = []
    for element in Valuations:
        Check_Abundant.append(is_secure(element))
        if is_abundant(element):
            my_index = Valuations.index(element)
            Abundant_Allocations.append(All_allocations[my_index])

    Check_Cap_Abundant = []
    Capacitated_Abundant_Allocations = []
    for element in Abundant_Allocations:
        if all(len(value) < (m/n) + 1 for value in element.values()):
            Capacitated_Abundant_Allocations.append(element)
            Check_Cap_Abundant.append(True)

    
    
    
    print("Capacitated_Secure_Allocations are as follows:")
    for item in Capacitated_Secure_Allocations:
        print(item)
    print("secure len:", len(Secure_Allocations))
    print("cap secure len:", len(Capacitated_Secure_Allocations))
        

    if any(Check_Secure):
        num_secure = num_secure+1  

    if any(Check_Cap_Secure):
        num_cap_secure = num_cap_secure+1    

    if any(Check_Abundant):
        num_abundant = num_abundant + 1

    if any(Check_Cap_Abundant):
        num_cap_abundant = num_cap_abundant+1 

print("no. of consensus allocation:", num_consensus)
print("no. of secure allocation:", num_secure)
print("no. of cap. secure allocation:",num_cap_secure)
print("no. of abundant allocation:", num_abundant)
print("no. of cap. abundant allocation:", num_cap_abundant)
print("total no of allocations/instance:", len(All_allocations))








    
