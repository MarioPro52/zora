# zoraimport hashlib
import time

class Block:
    def __init__(self, index, previous_hash, data, timestamp=None):
        self.index = index
        self.previous_hash = previous_hash
        self.data = data
        self.timestamp = timestamp or time.time()
        self.hash = self.calculate_hash()

    def calculate_hash(self):
        block_string = f"{self.index}{self.previous_hash}{self.data}{self.timestamp}"
        return hashlib.sha256(block_string.encode()).hexdigest()

# Create the first block (genesis block)
genesis_block = Block(0, "0", "Zora Block - Genesis", time.time())

# Create a new block, linked to the genesis block
new_block = Block(1, genesis_block.hash, "This is a simple Zora block", time.time())

# Display the blocks
print("Genesis Block:")
print(f"Index: {genesis_block.index}")
print(f"Hash: {genesis_block.hash}")
print(f"Previous Hash: {genesis_block.previous_hash}\n")

print("New Block:")
print(f"Index: {new_block.index}")
print(f"Hash: {new_block.hash}")
print(f"Previous Hash: {new_block.previous_hash}")
