# coding=UTF-8
from __future__ import division
import re



 
# Split text into sentences
def text_to_sentences(text):
    text = text.replace("\n", ". ")
    return text.split(". ")

 
# Split text into paragraphs
def text_to_paragraphs(text):
    return text.split("\n\n")

 
# Caculate the intersection between 2 sentences
def sentences_intersection(sent1, sent2):
 
    # split the sentence into words/tokens
    s1 = set(sent1.split(" "))  
    s2 = set(sent2.split(" "))
    if (len(s1) + len(s2)) == 0:
        return 0
    else: 
        return len(s1 & s2) / ((len(s1) + len(s2)) / 2)


 
# Remove all non-alphbetic characters from the sentence
def format_sentence(sentence):
    sentence = re.sub(r'\W+', '', sentence)
    return sentence


 
# Compute ranks of each sentence
def sentences_ranks(text):
 
    # Split into sentences
    sentences = text_to_sentences(text)
 
    # Calculate the intersection of every two sentences
    n = len(sentences)
    values = [[0 for x in xrange(n)] for x in xrange(n)]
    for i in range(0, n):
        for j in range(0, n):
            values[i][j] = sentences_intersection(sentences[i], sentences[j])
 
    # Build the sentence-rank dictionary
    # The score of a sentences is the sum of all its intersection
    sentences_dic = {}
    for i in range(0, n):
        score = 0
        for j in range(0, n):
            if i == j:
                continue
            score += values[i][j]
        sentences_dic[format_sentence(sentences[i])] = score
    return sentences_dic


 
# Return the best sentence in a paragraph
def best_sentence(paragraph, sentences_dic):
 
    # Split the paragraph into sentences
    sentences = text_to_sentences(paragraph)
 
    # Ignore short paragraphs
    if len(sentences) < 2:
        return ""
 
    # Get the best sentence according to the sentences dictionary
    best_sentence = ""
    max_value = 0
    for s in sentences:
        strip_s = format_sentence(s)
        if strip_s:
            if sentences_dic[strip_s] > max_value:
                max_value = sentences_dic[strip_s]
                best_sentence = s
 
    return best_sentence


 
# Build the summary
def get_summary(text):
 
    # Split the content into paragraphs
    paragraphs = text_to_paragraphs(text)
    sentences_dic = sentences_ranks(text)
    summary = []
    # Add the best sentence from each paragraph
    for p in paragraphs:
        sentence = best_sentence(p, sentences_dic).strip()
        if sentence:
            summary.append(sentence)
 
    return ("\n").join(summary)
 
 
paper = " "

print get_summary(paper)
