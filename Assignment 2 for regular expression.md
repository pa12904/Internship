import regex as re
import pandas as pd
#answer 1
input_str = "Python Excersises, PHP excersizes."

modified_string = re.sub(r'[ .,]', ':', input_str)

print(modified_string)
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
    #answer3
def get_words(input_string):
    text = re.compile(r'\b\w{4,}\b')  
    result = text.findall(input_string)  
   
    return result

input_text = "It is the set of the sails, not the direction of the wind that determines which way we will go."
result = get_words(input_text)
print("Words at least 4 characters long:", result)
#answer4
def find_specific_length_words(input_string):
    pattern = re.compile(r'\b\w{3,5}\b')  
    specific_length_words = pattern.findall(input_string)  
    return specific_length_words

input_text = "You can't buy happiness, but you can buy coffee, and that's pretty close."
result = find_specific_length_words(input_text)
print(result)
