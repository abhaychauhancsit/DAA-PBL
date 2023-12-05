# Spell-checker-using-trie-
Spell checking is an essential component of many software applications, including word processors, email clients, and web browsers.
# Python program to implement
# the above approach

# Structure of a Trie node
class TrieNode:
	def __init__(self):
	
		# Store address of a character
		self.trie = [None] * 256
		
		# Check if the character is
		# last character of a string or not
		self.isEnd = False

# Function to insert a string into Trie
def insert_trie(root, s):
	temp = root
	# Traverse the string, s
	for i in range(len(s)):
		if not temp.trie[ord(s[i])]:
			# Initialize a node
			temp.trie[ord(s[i])] = TrieNode()
		# Update temp
		temp = temp.trie[ord(s[i])]
	
	# Mark the last character of
	# the string to true
	temp.isEnd = True

# Function to print suggestions of the string
def print_suggestions(root, res):
	# If current character is
	# the last character of a string
	if root.isEnd:
		print(res,end=" ")
	
	# Iterate over all possible
	# characters of the string
	for i in range(256):
		# If current character
		# present in the Trie
		if root.trie[i]:
			# Insert current character
			# into Trie
			res_list = list(res)
			res_list.append(chr(i))
			print_suggestions(root.trie[i], "".join(res_list))

# Function to check if the string
# is present in Trie or not
def check_present(root, key):
	# Traverse the string
	for i in range(len(key)):
		# If current character not
		# present in the Trie
		if not root.trie[ord(key[i])]:
			print_suggestions(root, key[:i])
			return False
		# Update root
		root = root.trie[ord(key[i])]
	if root.isEnd:
		return True
	print_suggestions(root, key)
	return False

# Driver Code

# Given array of strings
strs = ["gee", "geeks", "ape", "apple", "geeksforgeeks"]
key = "geek"

# Initialize a Trie
root = TrieNode()

# Insert strings to trie
for s in strs:
	insert_trie(root, s)

if check_present(root, key):
	print("YES")


# This code is contributed by Aman Kumar
