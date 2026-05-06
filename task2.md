weight = float(input("Enter your weight in kg: "))
height = float(input("Enter your height in meters: "))

bmi = weight / (height * height)

print("\nYour BMI is:", round(bmi, 2))

if bmi < 18.5:
    print("Category: Underweight")

elif 18.5 <= bmi < 25:
    print("Category: Normal weight")

elif 25 <= bmi < 30:
    print("Category: Overweight")

else:
    print("Category: Obese")
