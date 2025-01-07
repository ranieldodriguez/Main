# Code Solution 1: Distance Calculator for Employees

**Task**  
Create a solution that accepts three integer inputs representing the number of times an employee travels to a job site. Output the total distance traveled to two decimal places.

```python
em_a_dis = 15.62
em_b_dis = 41.85
em_c_dis = 32.67

em_a_trip = int(input())
em_b_trip = int(input())
em_c_trip = int(input())

total_miles_traveled = (em_a_dis * em_a_trip) + (em_b_dis * em_b_trip) + (em_c_dis * em_c_trip)

print(f'Distance: {total_miles_traveled:.2f} miles')
```

# Code Solution 2: Ounces to Tons, Pounds, and Ounces Converter

**Task**  
Convert a given number of ounces into tons, pounds, and remaining ounces.

```python
total_ounces = int(input())

ounces_in_pounds = 16
pounds_in_tons = 2000

tons = total_ounces // (pounds_in_tons * ounces_in_pounds)
remaining_ounces_after_tons = total_ounces % (pounds_in_tons * ounces_in_pounds)
pounds = remaining_ounces_after_tons // ounces_in_pounds
ounces = remaining_ounces_after_tons % ounces_in_pounds

print(f'Tons: {tons}')
print(f'Pounds: {pounds}')
print(f'Ounces: {ounces}')
```
# Code Solution 3: List Data Type Identifier

**Task**  
Identify the data type of an element at a specified index in a predefined list.

```python
various_data_types = [516, 112.49, True, "meow", ("Western", "Governors", "University"), {"apple": 1, "pear": 5}]
index_value = int(input())
data_type = type(various_data_types[index_value]).__name__

print(f'Element {index_value}: {data_type}')
```
# Code Solution 4: Trapezoid Area Calculator
**Task**  
Calculate the area of a trapezoid using base and height inputs.

```python
b1 = int(input())
b2 = int(input())
h = int(input())

A = ((b1 + b2) / 2) * h
print(f'Trapezoid area: {A} square meters')
```
# Code Solution 5: Sum of Inputs in Various Formats

**Task**  
Output the sum of five integer inputs as integer, float, and concatenated string values.

```python
num1 = int(input())
num2 = int(input())
num3 = int(input())
num4 = int(input())
num5 = int(input())

integer_sum = num1 + num2 + num3 + num4 + num5
float_sum = float(integer_sum)
string_sum = str(num1) + str(num2) + str(num3) + str(num4) + str(num5)

print(f'Integer: {integer_sum}')
print(f'Float: {float_sum}')
print(f'String: {string_sum}')
```
# Code Solution 6: Student ID Formatter

**Task**  
Format a 9-digit student identification number as a string with hyphens.

```python
student_id = input()
formatted_id = f'{student_id[:3]}-{student_id[3:5]}-{student_id[5:]}'

print(formatted_id)
```
# Code Solution 7: Maximum Comparison in a List

**Task**  
Check if an input number is greater than the maximum value in a predefined list.

```python
predef_list = [4, -27, 15, 33, -10]
input_value = int(input())
max_value = max(predef_list)
is_greater = input_value > max_value

print(f'Greater Than Max? {is_greater}')
```
# Code Solution 8: Framework Index Retrieval

**Task**  
Retrieve a framework name by index, with error handling for out-of-range indexes.

```python
frameworks = ["Django", "Flask", "CherryPy", "Bottle", "Web2Py", "TurboGears"]

try:
    index_value = int(input())
    print(frameworks[index_value])
except (IndexError, ValueError):
    print("Error")
```
# Code Solution 9: Water Temperature State

**Task**  
Determine water state based on temperature and provide a safety warning when appropriate.

```python
temperature = int(input())

if temperature < 33:
    print('Frozen')
    print('Watch out for ice!')
elif 33 <= temperature <= 80:
    print('Cold')
elif 81 <= temperature <= 115:
    print('Warm')
elif 116 <= temperature <= 211:
    print('Hot')
else:
    print('Boiling')
    if temperature == 212:
        print('Caution: Hot!')
```
# Code Solution 10: Stock Purchase Cost Calculator

**Task**  
Calculate the total cost of purchased stocks based on a predefined stock dictionary.

```python
stocks = {'TSLA': 912.86, 'BBBY': 24.84, 'AAPL': 174.26, 'SOFI': 6.92, 'KIRK': 8.72, 'AURA': 22.12, 'AMZN': 141.28, 'EMBK': 12.29, 'LVLU': 2.33}
num_shares = int(input())
total_cost = 0.0

for _ in range(num_shares):
    stock_symbol = input()
    total_cost += stocks[stock_symbol]

print(f'Total price: ${total_cost:.2f}')
```
