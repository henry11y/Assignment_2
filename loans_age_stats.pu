import csv
import sys
import os

def find_age_column(header):
    """Find the age column name from possible options."""
    possible_names = ['age', 'Age', 'client_age', 'applicant_age']
    for name in possible_names:
        if name in header:
            return name
    return None

def read_ages_from_csv(filename):
    """Read ages from the CSV file, skipping empty or non-numeric values."""
    if not os.path.exists(filename):
        print(f"Error: File '{filename}' does not exist.")
        return None

    ages = []
    try:
        with open(filename, newline='', encoding='utf-8') as csvfile:
            reader = csv.DictReader(csvfile)
            age_col = find_age_column(reader.fieldnames)
            if not age_col:
                print("Error: Age column not found in CSV file.")
                return None
            for row in reader:
                age_val = row.get(age_col, '').strip()
                if age_val.isdigit():
                    ages.append(int(age_val))
    except Exception as e:
        print(f"Error reading CSV file: {e}")
        return None
    return ages

def calculate_statistics(ages):
    """Calculate min, max, range, and median of ages."""
    if not ages:
        return None
    ages.sort()
    min_age = ages[0]
    max_age = ages[-1]
    age_range = max_age - min_age
    n = len(ages)
    if n % 2 == 1:
        median = ages[n // 2]
    else:
        median = (ages[n // 2 - 1] + ages[n // 2]) / 2
    return min_age, max_age, age_range, median

def print_results(min_age, max_age, age_range, median):
    """Print the results in a clear format."""
    print("Loan Applicant Age Statistics:")
    print(f"Minimum Age: {min_age}")
    print(f"Maximum Age: {max_age}")
    print(f"Age Range: {age_range}")
    print(f"Median Age: {median}")

def main():
    filename = input("Enter CSV filename: ").strip()
    ages = read_ages_from_csv(filename)
    if ages is None or not ages:
        print("No valid age data found.")
        return
    stats = calculate_statistics(ages)
    if stats:
        print_results(*stats)
    else:
        print("Could not calculate statistics.")

if __name__ == "__main__":
