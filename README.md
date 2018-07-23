# Authorship-Attribution
Authorship Attribution system is a system which attempts to determine who wrote a given document, based on analysis of the language used and style of that document.
The first step in our authorship attribution system will be to take a document, separate it out into its component words, and construct/return a dictionary of word frequencies. As we are focused on the English language, we will assume that "words" are separated by whitespace, in the form of spaces (' '), tabs ('\t') and newline characters ('\n').

AA1

We will also do something slightly unconventional in considering each "standalone" non-alphabetic character (i.e. any character other than whitespace, or upper- or lower-case alphabetic characters) to be a single word. For example, given the document 'Dynamic-typed variables, Python; really?!!', the component words, in sequence, would be 'Dynamic-typed' (noting that '-' here is not considered to be a word despite being non-alphabetic, as it is surrounded by alphabetic characters), 'variables', ',', 'Python', ';', 'really', '?', '!', '!'. Note here that, in the case of the document starting with 'Dynamic--typed', the breakdown into words would instead be 'Dynamic', '-', '-', and 'typed', as both of the hyphens neighbour a non-alphabetic letter. Note also that case should be preserved in the output (i.e. if a word is upper case in the original, it should remain in upper case).

Write a function authattr_worddict(doc) that takes a single string argument doc and returns a dictionary (dict) of words contained in doc (as defined above), with the frequency of each word as an int. Note that, as the output is a dict, the order of those words may not correspond exactly to that indicated below, and that the testing will accept any word ordering within the dictionary.

AA2

The next step in our authorship attribution system will be to take two dictionaries of word counts and count the similarity between them. We will do this by:

1. ranking the two sets of words in descending order of frequency, and;
2. for corresponding word pairs, calculate the absolute difference in rank between the two.

If a word is found in one ranking but not the other, we will set the ranking for the second to the value maxrank (provided as part of the function call). In the case of a tie in the word frequency ranking (due to multiple words having the same frequency), we will assign all items the same value, calculated as follows: tied ranking + (number of tied items - 1)/2

For example, if two items were tied for second, we would assign each of them the rank . The ranking of the next item would then be 4 rather than 3, as two places in the ranking have been taken.

The final step is to calculate the "out-of-place" distance between the two rankings, by calculating the total absolute difference between the respective rankings for each word contained in the union of the rankings ... which is just a complicated way of saying, for each row in the table above calculate the absolute difference between the two ranking values 

Write a function authattr_oop(dictfreq1, dictfreq2, maxrank) that takes three arguments:

dictfreq1: a dictionary of words, with the (positive integer) frequency of each
dictfreq2: a second dictionary of words, with the (positive integer) frequency of each
maxrank: the positive int value to set the ranking to in the case that the word isn't in the dictionary of words in question
and returns a float out-of-place distance between the two (where the smaller the number, the more similar the two rankings are).

AA3

The final step in our authorship attribution system will be to perform authorship attribution based on a selection of sample documents from a range of authors, and a document of unknown origin.

You will be given a selection of sample documents from a range of authors (from which we will learn our word frequency dictionaries), and a document of unknown origin. Given these, you need to return a list of authors in ascending order of out-of-place distance between the document of unknown origin and the combined set of documents from each of the authors. You should do this according to the following steps:

compute a single dictionary of word frequencies for each author based on the combined set of documents from that author (provided in the form of a list of strings)
compute a dictionary of word frequencies for the document of unknown origin
compare the document of unknown origin with the combined works of each author, based on the out-of-place distance metric
calculate and return a ranking of authors, from most similar (smallest distance) to least similar (greatest distance), resolving any ties in the ranking based on an alphabetic sort

Write a function authattr_authorpred(authordict, unknown, maxrank) that takes three arguments:

authordict: a dictionary of authors (each of which is a str), associated with a non-empty list of documents (each of which is a str)
unknown: a str contained the document of unknown origin
maxrank: the positive int value to set maxrank to in the call to authattr_oop
and returns a list of (author, oop) tuples, where author is the name of an author from authordict, and oop is the out-of-place distance between unknown and the combined works of author, in the form of a float.
