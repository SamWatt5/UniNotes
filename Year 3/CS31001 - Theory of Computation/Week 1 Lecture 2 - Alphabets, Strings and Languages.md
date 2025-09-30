# Motivational Considerations
## Natural and Computer Languages
>[!definition] Natural Languages
>- Three different entities: letters, words and sentences
>- Groups of letters make up words, group of words (together with punctuation symbols) make up sentences
>- Not all groups of letters form a valid word!

>[!definition] Computer Languages
>- The same happens in computer languages!
>- Some character strings form keywords in programming languages (`int`, `return`, ...)
>- Some strings of words are valid statements (`int x = 4;`)
>- But not all character strings form keywords and not all sequences of keywords form valid commands (`int 4 x =;`)

We need a way of representing languages, where the decision of whether something belongs to the language is based on explicitly stated rules, and not guesswork!
## Theory of Formal Languages
- The **Theory of Formal Languages** is the field of mathematics that studies *syntactical* aspects of languages.
- Rules for languages (in terms of what words belong to them) are explicitly stated
- We are interested in the *form* of the words that belong to a language, not their *meaning*
- Using the English language analogue, "Today is a warm day" is as good a construct for our purposes as is "I ate three Thursdays"
# Alphabets, Strings and Languages
## Alphabet and String
>[!definition] Alphabet
>- **Alphabet** is a *finite* set of units (symbols) out of which structures are build
>- Elements of alphabet will sometimes be called **letters** or **characters**

>[!definition] Word or String
>- Finite sequences of characters from an alphabet are called **words** or **strings**.
>- Rather than writing strings using the sequence notation, we will write them using a juxtaposition. We will write, for example, the string (D, o, o, r) as door
>- **Empty string** or **null string** is a string that has no letters
>- We denote the empty string by $\epsilon$
>- For clarity, $\epsilon$ will not be a part of any alphabet we deal with
>- Two words are considered *equal* if all their letters are the same and they are in the same order
>	- Note: It is imprecise to say that two words are equal if they consist of the same letters (consider the words *door* and *rod*)

## Language
>[!definition] Language
>- A **language** is some set of words over some alphabet
## Example: Words of English Language
>[!example] Words of English Language
>- *Alphabet* of the words of English language is a set of all English letters, plus characters - and '$$\sum = \{a,b,c,d,e,...,-,'\}$$
>- Language of all english words $L$ is a set of all the words that comprise letters from $\sum$ for which there is an entry in a standard dictionary.$$L = \{\text{all the main entries in a standard dictionary}\}$$
>- For example, door $\in L$, while bmmfxx $\notin L$
>- Here we could theoretically list *all* the strings that belong to the language (it is a *finite* language).

## Example: Sentences of English Language
>[!example] Sentences of English Language
>- *Alphabet* of the sentences of the English language is a set of all words in the English language, plus a blank space, plus the usual punctuation symbols.
>- *Language* of the sentences in the English language is a set of all strings of the above alphabet that are valid sentences in English.
>- **We cannot list all the strings of this language, as this set is infinite**
>	- I bought one apple
>	- I bought two apples
>	- I bought three apples
>	- ...
>- To describe the language, we could list all the grammar rules for deriving sentences

### Syntax vs Semantics
- What about a sentence "*I bought three Fridays*"?
- It is grammatically (syntactically) correct!
- Its meaning (semantics) doesn't make any sense
- But in this module, we are purely interested in determining whether a given string belongs to a given language (syntax). We do not care about the meaning.
- What about "If I very does"?

## Some Examples of Binary Languages
- The most common alphabet that we will use in this module is the binary alphabet $\sum = \{0,1\}$.
- Some examples (and non-examples) of languages over this alphabet:
	- $L_1 = \{00,11,01,1110\}$
	- $L_2 = \{\epsilon,0,1,00,110\}$
	- $L_3 = \{0^n1^n|n\leq{0}\} = \{\epsilon,01,0011,000111,...\}$
	- $L_4 = \{\epsilon\}$
	- $L_5 = \{\{\epsilon\}\}$
		- This is not a language!
	- $L_6 = \emptyset$
## Specifying a Language Over Some Alphabet
There are two ways in which we can specify a language over some alphabet
- List all of the strings that belong to a language
- Specify a set of rules that allows us to determine, in finite time, whether a string belongs to a language
>[!example]
>Let $\sum = \{x\}$ and $$L_1 = \{x,xx,xxxxx,xxxxxx\},$$ $$L_2 = \{x,xx,xxx,xxxx,xxxxx,...\}$$
>which we also write as $$L_2 = \{x^n|n = 1,2,3,...\}$$
- This language does not include the empty word $\epsilon$
- If we wanted to include it, we would write $L_2\{\epsilon,x,xx,xxx,xxxx,...\}$
- Or alternatively, $L_2 = \{x^n|n = 0,1,2,3,...\}$
- Note that $x^0$ = $\epsilon$
# String and Language Operations
>[!definition] String Concatenation (Informal)
>Given two strings, their concatenation is a new string obtained when one of them is appended to the other

- Suppose $\sum = \{0\}$ is an alphabet and $v = 00$ and $w = 000$ are two strings over that alphabet. then $$vw = 00000$$
- In this case, $vw = 00000$ also.
- Suppose $\sum = \{0,1\}$ is an alphabet and $v = 00$ and $w = 111$ are two strings over that alphabet. Then $$vw=00111, wv=1110$$
>[!definition] Convention
>- We will denote by $w^2$ a concatenation of the string $w$ with itself
>- In general, $w^k$ will be $w$ appended to itself $k-1$ times
>- $w^0$ will always be $\epsilon$, for every string $w$

- Let $w = 00$, then $w^2 - 0000$, $w^3=000000$, $w^5=0000000000$ and so on

>[!definition] Notation Convention
>- We will, in general, use the letters towards the beginning of English alphabet for individual symbols (e.g. $a$,$b$,$c$).
>- The letters towards the end of the English alphabet, such as $v$,$w$,$x$ will be used for strings.

### String Length
>[!definition] String Length (Informal)
>The length of a string is the number of positions of letters in that string

- Let $w=0000$. Then length of a string $w$ is $4$.
- We also write length($w$) or $|w| = 4$ 
- The length of the empty string is $0$.
- Note: It is not correct to define the length of a string as the number of letters in it. In the case above, the length of string $w$ would then be $1$.
### Closure of An Alphabet
>[!definition] Closure of an Alphabet
>Let $\sum$ be an alphabet. **Closure** of the alphabet $\sum$, denoted by $\sum^*$ is the set of all strings (of any length, including $0$) over the alphabet $\sum$

- Operator $*$ is sometimes called **Kleene star**
- $\sum^*$ is always infinite, for any (nonempty) alphabet $\sum$
- $\sum^*$ always includes the empty word
- Note: The closure of alphabet is also an example of a language over that alphabet

>[!example]
>- Let $\sum = \{0\}$. Then $\sum^* = \{\epsilon,0,00,000,0000,00000,...\}$. Or we can write $\sum^* = \{0^n|n=0,1,2,3,...\}$.
>- Let $\sum=\{0,1\}$. Then $\sum^* = \{\epsilon,0,1,00,11,01,10,000,001,...\}$ .
>- Let $\sum=\{0,1,2\}$. Then $\sum^*=\{\epsilon,0,1,2,00,01,02,10,11,12,20,21,22,...\}$.

### Language Concatenation
>[!definition] Language Concatenation (informal)
>Given two languages $L_1$ and $L_2$, their concatenation is a language comprised of all strings that are obtained as a concatenation of some string of $L_1$ and some strings of $L_2$

>[!definition] Language Concatenation (formal)
>Given two languages $L_1$ and $L_2$, their concatenation is the language $L_1L_2$ defined as $$L_1L_2=\{vw|v\in L_1, w\in $L_2\}$$

>[!example]
>Let $L_1 = \{00,1\}$ and $L_2 = \{2,20\}$. Then $$L_1L_2 = \{002,0020,12,120\}$$

>[!example]
>Let $L_1 = \{00,1\}$ . Then $$L_1L_1 = \{0000,001,100,11\}$$

### Power of a Language
- For a language $L$, we define $L^2$ as $LL$ (concatenation of the language with itself)
- $L^3 = L^2L$
- $L^4 = L^3L$
- ...
- $L^1 = L$
- $L^0 = \{\epsilon\}$
- $L^n$ is a set of all strings that are themselves a concatenation of any $n$ strings from $L$
### Closure of a Language
>[!definition] Closure of a Language
>Let $L$ be a language. The closure of the language $L$, denoted by $L^*$ is the set of all strings that are concatenations of any number of words (including $0$) from $L$.

>[!example]
>Let $L = \{00,1\}$. The closure of $L$ is$$L^*=\{\epsilon,00,1,0000,001,100,11,00001,00100,10000,...\}$$

- $*$ is (again) sometimes called Kleene star.
- $L^*$ is almost always infinite
- There are only two languages whose closure is not infinite:
	- $L = \{\epsilon\}$
	- $L= \{\{\epsilon\}\}$
- $L^*$ always includes the empty word.
### Why Study Formal Languages?
- Everything in this module revolves around languages and membership of strings to languages
	- We will design mathematical models that "recognise" languages (i.e. are able to decide in finite time whether a given string belongs to the language or not).
	- We will also find languages that cannot be recognised by the given models
- One might think that, considering our grand goal to discover the limits of computers, focusing on such a simple model as languages is too naive and limiting
- However, this is not true.





