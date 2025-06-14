# password-strength-checker
# a simple python script to check password strength

import re

def check_password_strength(password):
    length_error = len(password) < 8
    digit_error = re.search(r"\d", password) is None
    uppercase_error = re.search(r"[A-Z]", password) is None
    lowercase_error = re.search(r"[a-z]", password) is None
    symbol_error = re.search(r"[!@#$%^&*(),.?\":{}|<>]", password) is None
    errors = {
        'length': length_error,
        'digit': digit_error,
        'uppercase': uppercase_error,
        'lowercase': lowercase_error,
        'symbol': symbol_error
    }
    strength_score = 5 - sum(errors.values())
    if strength_score == 5:
        strength = "Strong 💪"
    elif 3 <= strength_score < 5:
        strength = "Moderate 😐"
    else:
        strength = "Weak 😟"
    return strength, errors
def main():
    password = input("Enter your password: ")
    strength, errors = check_password_strength(password)
    print(f"\nPassword strength: {strength}")
    if any(errors.values()):
        print("Issues:")
        if errors['length']:
            print("- Too short (min 8 characters)")
        if errors['digit']:
            print("- Should include at least one digit")
        if errors['uppercase']:
            print("- Should include at least one uppercase letter")
        if errors['lowercase']:
            print("- Should include at least one lowercase letter")
        if errors['symbol']:
            print("- Should include at least one special character")
            
if __name__ == "__main__":
    main()
