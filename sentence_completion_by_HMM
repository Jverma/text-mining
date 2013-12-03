"""
A bigram langauge model for completing a sentence using Hidden Markov Methods.
Author : Janu Verma
http://www.math.ksu.edu/~jv291/
Twitter : @januverma
"""


import re
from collections import *
import random
import sys




########## Load the Data #########
"""
The data is a collections of text documents or a corpus of sentences.
We'll store the data as a list of text documents or a list of sentences. 
"""

text = []
input = open(sys.argv[1])
for line in input:
    text.append(line)




###############################################################
###### Word Tokenization #####################################
def word_tokens(text):
    words = text.split()
    words = [x.lower() for x in words]
    formated_text = [re.sub('[^a-z]', '', word) for word in words]
    return formated_text

#############################################################
######### Extracting Bigrams #######

def bigrams(text):
    words = word_tokens(text)
    n = len(words)
    bigrams = []
    i = 0
    while (i < n-1):
        bigram = words[i], words[i + 1]
        if (bigram != None):
            bigrams.append(bigram)
            i = i + 1
        else:
            i = i + 1
    return bigrams



################################ Training 
print "training....."



#################################################################
##### Compute all the words in the Training set ########
all_words = []        
for line in text:
    words = word_tokens(line)
    all_words.extend(words)



################################################################    
##### Compute the frequencies of occurences of possible transitions ###########

pair_counts = defaultdict(float)
for x in text:
    for pairs in bigrams(x):
        pair_counts[pairs] = pair_counts[pairs] + 1



#########################################################################
#### Count the total number of possible transactions #####
count_dict = {}
for x in all_words:
    count = 0
    for pair in pair_counts.keys():
        if (pair[0] == x):
            count = count  + 1
    count_dict[x] = count          


#####################################################################        
##### Compute the transition probabilities #########

transition_prob = defaultdict(float)
for pair in pair_counts.keys():
    transition_prob[pair] = pair_counts[pair]/count_dict[pair[0]]


   
######################################################
######### Compute the most probable next word ####

def next_word(x):
    max_prob = 0.0
    for pair in transition_prob.keys():
        if (pair[0] == x):
            if (transition_prob[pair] > max_prob):
                most_probable = pair[1]
                max_prob = transition_prob[pair]
    if (max_prob != 0):            
        return most_probable
    else:
        return None



##########################################################################
######## Completion of a sentence ###############################    
def complete_sentence(sentence, threshold):
    words = word_tokens(sentence)
    n = len(words)
    last_word = words[n-1]
    i = n
    while (i < threshold): #and (last_word != None):
        last_word = next_word(last_word)
        words.append(last_word)
        i = i + 1
    return words

        
##################################################
###Validity of a distribution#####################
def distribution(x):
    for pair in transition_prob.keys():
        if pair[0] == x:
            guess = random.random()
            count = 0
            if (guess <= transition_prob[pair]):
                return pair[1]
            guess -= transition_prob[pair]
    assert False, "not a valid prob"    
            


################################################################
######## Query ##############


q = sys.argv[1]
print complete_sentence(q, 5)
    
    
    
        
