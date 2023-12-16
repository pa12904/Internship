import regex as re
import pandas as pd
#answer 1
input_str = "Python Excersises, PHP excersizes."

modified_string = re.sub(r'[ .,]', ':', input_str)

print(modified_string)
Python:Excersises::PHP:excersizes:
#answer 2
data = {'SUMMARY': ['hello, world!', 'XXXX test', '123four, five:; six...']}

df = pd.DataFrame(data)

def format_string(text):
    exclude_words = {'XXXX'}
    formatted_text = re.sub(r'[^a-zA-Z\s]', '', text)
    formatted_text = ' '.join(filter(lambda word: word.lower() not in exclude_words, formatted_text.split()))
    return ' '.join(filter(None, formatted_text.split()))

df['SUMMARY'] = df['SUMMARY'].apply(format_string)

for index, row in df.iterrows():
    print(f"{index} {row['SUMMARY']}")
0 hello world
1 XXXX test
2 four five six
#answer3
def get_words(input_string):
    text = re.compile(r'\b\w{4,}\b')  
    result = text.findall(input_string)  
   
    return result

input_text = "It is the set of the sails, not the direction of the wind that determines which way we will go."
result = get_words(input_text)
print("Words at least 4 characters long:", result)
Words at least 4 characters long: ['sails', 'direction', 'wind', 'that', 'determines', 'which', 'will']
#answer4
def find_specific_length_words(input_string):
    pattern = re.compile(r'\b\w{3,5}\b')  
    specific_length_words = pattern.findall(input_string)  
    return specific_length_words

input_text = "You can't buy happiness, but you can buy coffee, and that's pretty close."
result = find_specific_length_words(input_text)
print(result)
['You', 'can', 'buy', 'but', 'you', 'can', 'buy', 'and', 'that', 'close']
#answer5
def remove_parentheses(strings_list):
    pattern = re.compile(r'\([^)]*\)')  
    formatted_texts = [pattern.sub('', string) for string in strings_list]
   
    return formatted_texts

input_list = [
    "example(.com)",
    "hr@fliprobo(.com)",
    "github(.com)",
    "Hello (Data Science World)",
    "Data(Scientist)"
]

result = remove_parentheses(input_list)
print(result)
['example', 'hr@fliprobo', 'github', 'Hello ', 'Data']
#answer 6
["example(.com)", "hr@fliprobo(.com)","github(.com)","Hello (Data Science World)","Data (Scientist)"]
df = 'input.csv'
with open(df, 'r') as file:
    text = file.read()

pattern = re.compile(r'\([^)]*\)')

modified_text = pattern.sub('', text)

print(modified_text)
["example", "hr@fliprobo","github","Hello ","Data "

#answer7
input_string = "ImportanceOfRegularExpressionsInPython"

result = re.findall('[A-Z][^A-Z]*', input_string)

print(result)
['Importance', 'Of', 'Regular', 'Expressions', 'In', 'Python']
#answer8
def insert_spaces_before_numbers(text):
   
    modified_text = re.sub(r'(?<=[^0-9])(?=[0-9])', ' ', text)
    return modified_text


input_text = "RegularExpression1IsAn2ImportantTopic3InPython"
result = insert_spaces_before_numbers(input_text)
print(result)
RegularExpression 1IsAn 2ImportantTopic 3InPython
#answer9
def insert_spaces(text):
    modified_text = re.sub(r'(?<=[a-z])(?=[A-Z0-9])|(?<=[A-Z])(?=[A-Z][a-z0-9])', ' ', text)
    return modified_text

# Example usage:
input_text = "RegularExpression1IsAn2ImportantTopic3InPython"
result = insert_spaces(input_text)
print(result)
Regular Expression 1Is An 2Important Topic 3In Python
#answer10
import requests
github_csv_url = 'https://raw.githubusercontent.com/dsrscientist/DSData/master/happiness_score_dataset.csv'

response = requests.get(github_csv_url)

if response.status_code == 200:
    df = pd.read_csv(github_csv_url)
    df['first_five_letters'] = df['Country'].str[:6]
    print(df[['Country', 'first_five_letters']].head())  
else:
    print(f"Failed to fetch data. Status code: {response.status_code}")
       Country first_five_letters
0  Switzerland             Switze
1      Iceland             Icelan
2      Denmark             Denmar
3       Norway             Norway
4       Canada             Canada
 
#answer11
def match_string(input_string):
    pattern = re.compile(r'^[a-zA-Z0-9_]*$')
    match = pattern.match(input_string)
    if match:
        print(f"The string '{input_string}' matches the pattern.")
    else:
        print(f"The string '{input_string}' does not match the pattern.")

strings_to_test = [
    "Hello_World123",
    "abcDEF456",
    "PythonIs_123_cool",
    "Hello world",
    "Hello@123.com"
]

for string in strings_to_test:
    match_string(string)
The string 'Hello_World123' matches the pattern.
The string 'abcDEF456' matches the pattern.
The string 'PythonIs_123_cool' matches the pattern.
The string 'Hello world' does not match the pattern.
The string 'Hello@123.com' does not match the pattern.
#answer12
def starts_with_number(string, number):
    pattern = re.compile(f'^{number}.+')
    match = re.match(pattern, string)
   
    if match:
        return True
    else:
        return False

# Example usage:
input_string = "123abcxyz"  
specified_number = "123"

result = starts_with_number(input_string, specified_number)
print(result)
True
#answer13
def remove_leading_zeroes(ip_address):
    pattern = re.sub(r'\b0+(\d)', r'\1', ip_address)
    return pattern

input_ip = "192.168.001.001"

result = remove_leading_zeroes(input_ip)
print(f"Original IP address: {input_ip}")
print(f"IP address after removing leading zeroes: {result}")
Original IP address: 192.168.001.001
IP address after removing leading zeroes: 192.168.1.1
#answer14
def find_date(text):
    pattern = re.compile(r'\b(?:January|February|March|April|May|June|July|August|September|October|November|December)\s+\d{1,2}(?:st|nd|rd|th)?\s+\d{4}\b')
    match = re.search(pattern, text)
    if match:
        return match.group()
    else:
        return None

input_string = 'On August 15th 1947 that India was declared independent from British colonialism, and the reins of control were handed over to the leaders of the Country'

result = find_date(input_string)

if result:
    print(result)
else:
    print("Date not found.")
August 15th 1947
#answer15
def search_words(text, words):
    for word in words:
        if re.search(word, text):
            print(f"'{word}' found in the text.")
        else:
            print(f"'{word}' not found in the text.")

input_string = 'The quick brown fox jumps over the lazy dog.'

searched_words = ['fox', 'dog', 'horse']

search_words(input_string, searched_words)
'fox' found in the text.
'dog' found in the text.
'horse' not found in the text.
 #answer16
def find_word_location(text, word):
    pattern = re.compile(re.escape(word))
    match = pattern.search(text)
   
    if match:
        start_index = match.start()
        end_index = match.end()
        print(f"'{word}' found in the text at index {start_index} to {end_index - 1}")
    else:
        print(f"'{word}' not found in the text.")

sample_text = 'The quick brown fox jumps over the lazy dog.'

searched_word = 'fox'

find_word_location(sample_text, searched_word)
'fox' found in the text at index 16 to 18
#answer17
def find_substrings(text, pattern):
    matches = re.finditer(pattern, text)
   
    if matches:
        print(f"Occurrences of '{pattern}' in the text:")
        for match in matches:
            start_index = match.start()
            end_index = match.end()
            print(f"Found '{pattern}' at index {start_index} to {end_index - 1}")
    else:
        print(f"No occurrences of '{pattern}' found in the text.")

input_String = 'Python exercises, PHP exercises, C# exercises'

substring_pattern = 'exercises'

find_substrings(input_String, substring_pattern)
Occurrences of 'exercises' in the text:
Found 'exercises' at index 7 to 15
Found 'exercises' at index 22 to 30
Found 'exercises' at index 36 to 44
#answer18
def find_substrings_with_positions(text, pattern):
    matches = re.finditer(pattern, text)
   
    if matches:
        print(f"Occurrences of '{pattern}' in the text:")
        for match in matches:
            start_index = match.start()
            end_index = match.end()
            print(f"Found '{pattern}' at index {start_index} to {end_index - 1}")
    else:
        print(f"No occurrences of '{pattern}' found in the text.")

sample_text = 'Python exercises, PHP exercises, C# exercises'

substring_pattern = 'exercises'

find_substrings_with_positions(sample_text, substring_pattern)
Occurrences of 'exercises' in the text:
Found 'exercises' at index 7 to 15
Found 'exercises' at index 22 to 30
Found 'exercises' at index 36 to 44
#answer19
def convert_date_format(date):
    pattern = re.compile(r'(\d{4})-(\d{2})-(\d{2})')
   
    modified_date = re.sub(pattern, r'\3-\2-\1', date)
    return modified_date

input_date = '2023-12-16'

result = convert_date_format(input_date)
print(f"Converted Date: {result}")
Converted Date: 16-12-2023
#answer20
def find_decimal_numbers(text):
    pattern = re.compile(r'\b\d+\.\d{1,2}\b')
    decimal_numbers = pattern.findall(text)
    return decimal_numbers

sample_text = "01.12 0132.123 2.31875 145.8 3.01 27.25 0.25"

result = find_decimal_numbers(sample_text)
print("Decimal numbers with precision of 1 or 2:", result)
Decimal numbers with precision of 1 or 2: ['01.12', '145.8', '3.01', '27.25', '0.25']
#answer21
def extract_numbers_with_positions(text):
    pattern = re.compile(r'\d+')
    matches = pattern.finditer(text)
   
    if matches:
        print("Numbers and their positions in the text:")
        for match in matches:
            number = match.group()
            start_index = match.start()
            end_index = match.end()
            print(f"Number '{number}' found at index {start_index} to {end_index - 1}")
    else:
        print("No numbers found in the text.")

new_input_text = 'The price is $25 for product A, $30 for product B, and $45 for product C.'

extract_numbers_with_positions(new_input_text)
Numbers and their positions in the text:
Number '25' found at index 14 to 15
Number '30' found at index 33 to 34
Number '45' found at index 56 to 57
#answer22
def extract_maximum_numeric_value(text):
    pattern = re.compile(r'\b\d+\b')
    numbers = [int(number) for number in pattern.findall(text)]
   
    if numbers:
        max_number = max(numbers)
        return max_number
    else:
        return None

sample_text = 'My marks in each semester are: 947, 896, 926, 524, 734, 950, 642'

max_value = extract_maximum_numeric_value(sample_text)

if max_value is not None:
    print(max_value)
else:
    print("No numeric values found in the text.")
950
#answer23
def insert_spaces(text):
    modified_text = re.sub(r'([a-z])([A-Z])', r'\1 \2', text)
    return modified_text

input_text = "RegularExpressionIsAnImportantTopicInPython"

result = insert_spaces(input_text)

print(result)
Regular Expression Is An Important Topic In Python
#answer24
sample_text = "Let the pink sky be your daily Reminder to chase your dreams Fearlessly."

pattern = re.compile(r'\b[A-Z][a-z]+\b')

matches = pattern.findall(sample_text)

print("Sequences of one uppercase letter followed by lowercase letters:")
print(matches)
Sequences of one uppercase letter followed by lowercase letters:
['Let', 'Reminder', 'Fearlessly']
#answer25
def remove_continuous_duplicates(text):
    pattern = re.compile(r'\b(\w+)(?:\s+\1\b)+', flags=re.IGNORECASE)
    modified_text = pattern.sub(r'\1', text)
    return modified_text

sample_text = "Hello hello world world"

result = remove_continuous_duplicates(sample_text)

print(result)
Hello world
#answer26
def ends_with_alphanumeric(string):
    pattern = re.compile(r'\w$')  
    match = pattern.search(string)
   
    if match:
        return True
    else:
        return False

test_strings = [
    "Hello123",  
    "world!",    
    "12345",      
    "This is a test string.",  
]

for string in test_strings:
    result = ends_with_alphanumeric(string)
    print(result)
True
False
True
False
#answer27
def extract_hashtags(text):
    pattern = re.compile(r'#\w+')
    hashtags = pattern.findall(text)
    return hashtags

sample_text = """RT @kapil_kausik: #Doltiwal I mean #xyzabc is "hurt" by #Demonetization as the same has rendered USELESS <ed><U+00A0><U+00BD><ed><U+00B1><U+0089> "acquired funds" No wo"""

hashtags = extract_hashtags(sample_text)

print(hashtags)
['#Doltiwal', '#xyzabc', '#Demonetization']
#answer28
def remove_U_symbols(text):
    pattern = re.compile(r'<U\+[0-9A-Fa-f]+>')
    clean_text = pattern.sub('', text)
    return clean_text

sample_text = "@Jags123456 Bharat band on 28??<ed><U+00A0><U+00BD><ed><U+00B8><U+0082>Those who are protesting #demonetization are all different party leaders"

result = remove_U_symbols(sample_text)

print(result)
@Jags123456 Bharat band on 28??<ed><ed>Those who are protesting #demonetization are all different party leaders
#answer29
def extract_dates_from_text(file_path):
    with open(file_path, 'r') as file:
        text = file.read()        
       
        pattern = re.compile(r'\b\d{2}-\d{2}-\d{4}\b')        
       
        dates = pattern.findall(text)
       
        return dates

file_path = 'sample.txt'

extracted_dates = extract_dates_from_text(file_path)

print(extracted_dates)
['12-09-1992', '15-12-1999']
#answer30
def remove_words_of_length_between_2_and_4(text):
    pattern = re.compile(r'\b\w{2,4}\b')
    modified_text = pattern.sub('', text)
    return modified_text

sample_text = "The following example creates an ArrayList with a capacity of 50 elements. 4 elements are then added to the ArrayList and the ArrayList is trimmed accordingly."

result = remove_words_of_length_between_2_and_4(sample_text)

print(result)
 following example creates  ArrayList  a capacity   elements. 4 elements   added   ArrayList   ArrayList  trimmed accordingly.
 
