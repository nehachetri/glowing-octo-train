import string

# Defining the ranges for each category
uppercase_range = range(1, 27)
lowercase_range = range(27, 53)
punctuation_range = range(53, 66)

# Creating dictionaries to map characters to numbers
uppercase_dict = {char: str(i) for i, char in zip(uppercase_range, string.ascii_uppercase)}
lowercase_dict = {char: str(i) for i, char in zip(lowercase_range, string.ascii_lowercase)}
punctuation_dict = {char: str(i) for i, char in zip(punctuation_range, string.punctuation)}

# Combining the dictionaries into one
mapping_dict = {**uppercase_dict, **lowercase_dict, **punctuation_dict}


# Defining function to convert a string to numbers
def convert_string_to_numbers(string):
    result = ""
    for char in string:
        if char in mapping_dict:
            result += mapping_dict[char] + " "
    return result.strip()

# Example
message = input("Enter the message: ")
number = convert_string_to_numbers(message)
print("The equivalent index numbers are: " + number)

binary_list = []
for num in number.split():
    binary_list.append(format(int(num), "07b"))  # format each number as 7-bit binary

print("The binary representation is:")
print(binary_list)

# Joining the binary digits
binary_string = "".join(binary_list)
print("The binary string is:")
print(binary_string)

# Breaking the binary string into chunks of 60 bits
chunks = [binary_string[i:i+60] for i in range(0, len(binary_string), 60)]

# Padding the last chunk with zeros if necessary
if len(chunks[-1]) < 60:
    chunks[-1] += '0' * (60 - len(chunks[-1]))

# XORing the chunks
result = int(chunks[0], 2)
for chunk in chunks[1:]:
    result ^= int(chunk, 2)

# Converting the result to a 60-bit binary string
result_binary = format(result, "060b")
print("The final 60-bit binary result is:")
print(result_binary)

#Asking for a key value less than 66
a = input("Enter a key less than 66 : ")
binary_a = bin(int(a))[2:]

print("The Binary Representation of the Key is :" + binary_a)

# Counting
count_ones = binary_a.count('1')
count_zeroes = binary_a.count('0')
r = count_ones - count_zeroes

print(f"Number of ones: {count_ones}")
print(f"Number of zeroes: {count_zeroes}")

# Function to create a 3x3 matrix from a binary string
def create_matrix(binary_string):
    # Determine the number of elements needed to fill the matrix
    elements_needed = 9 - (len(binary_string) % 9)
    # Pad the binary string with '2' to reach the desired length
    binary_string += '2' * elements_needed

    # Split the binary string into 3-bit elements
    elements = [binary_string[i:i+1] for i in range(0, len(binary_string), 1)]

    # Create the matrix
    matrix = [elements[i:i+3] for i in range(0, len(elements), 3)]

    return matrix

# Create the matrix from the binary string
matrix = create_matrix(result_binary)

# Print the matrix
print("The original matrix is:")
for row in matrix:
    print(row)


# Converting matrix to B
B = []
n = len(matrix)
m = len(matrix[0])

for i in range(n):
    row = []
    for j in range(m):
        inp = matrix[i][j]
        row.append(inp)
    B.append(row)

def shift(r):
    if r > 0:
        for i in range(n):
            for j in range(m):
                if j - r < 0:
                    B[i][j] = matrix[i][j - r + m]
                else:
                    B[i][j] = matrix[i][j - r]
    else:
        r = abs(r)
        for i in range(n):
            for j in range(m):
                if j + r >= m:
                    b = (j + r) % m
                    B[i][j] = matrix[i][b]
                else:
                    B[i][j] = matrix[i][j + r]

    print("The Shifted Encrypted matrix is:")
    for row in B:
        print(row)

def reverse_shift(matrix):
    original_binary = ""
    for row in matrix:
        for element in row:
            original_binary += element
    return original_binary.replace('2', '')

# Reverse the shift operation on the shifted matrix
reversed_matrix = create_matrix(reverse_shift(B))

# Obtain the original 60-bit binary output
original_binary = reverse_shift(reversed_matrix)

print("The reversed matrix is:")
for row in reversed_matrix:
    print(row)

print("The original 60-bit binary Hash Code is:")
print(original_binary)
