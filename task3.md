import random
import string

print("=== Password Generator ===")

length = int(input("Enter password length: "))

print("\nChoose character types:")
use_letters = input("Use letters? (y/n): ")
use_numbers = input("Use numbers? (y/n): ")
use_symbols = input("Use symbols? (y/n): ")

characters = ""

if use_letters == "y":
    characters += string.ascii_letters

if use_numbers == "y":
    characters += string.digits

if use_symbols == "y":
    characters += string.punctuation


if characters == "":
    print("You must select at least one character type!")
else:
    password = ""

    for i in range(length):
        password += random.choice(characters)

    print("\nGenerated Password:", password)
