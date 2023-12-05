class TrieNode:
	def _init_(self):
	
		self.trie = [None] * 256
	self.isEnd = False


def insert_trie(root, s):
	temp = root
	for i in range(len(s)):
		if not temp.trie[ord(s[i])]:
			
			temp.trie[ord(s[i])] = TrieNode()
		
		temp = temp.trie[ord(s[i])]

	temp.isEnd = True

def print_suggestions(root, res):

	if root.isEnd:
		print(res,end=" ")
	
	for i in range(256):
		if root.trie[i]:
			res_list = list(res)
			res_list.append(chr(i))
			print_suggestions(root.trie[i], "".join(res_list))

def check_present(root, key):
	for i in range(len(key)):
		if not root.trie[ord(key[i])]:
			print_suggestions(root, key[:i])
			return False
		root = root.trie[ord(key[i])]
	if root.isEnd:
		return True
	print_suggestions(root, key)
	return False

strs = ["gee", "geeks", "ape", "apple", "geeksforgeeks"]	

key = "geek"
root = TrieNode()
for s in strs:
	insert_trie(root, s)

if check_present(root, key):
	print("YES")
