## Role: Fintech engineer who’s working at one of the five largest banks in the world.

## Goal: The task is to build a blockchain-based ledger system, complete with a user-friendly web interface. This ledger should allow partner banks to conduct financial transactions (that is, to transfer money between senders and receivers) and to verify the integrity of the data in the ledger.

------

# Creating 

* Create a new data class named Record. This class will serve as the blueprint for the financial transaction records that the blocks of the ledger will store.

* Change the existing Block data class by replacing the generic data attribute with a record attribute that’s of type Record.

* Create additional user input areas in the Streamlit application. These input areas should collect the relevant information for each financial record that you’ll store in the PyChain ledger.

* Test your complete PyChain ledger.

------

### Overview 

The steps for this Challenge are divided into the following sections:

Create a Record Data Class

Modify the Existing Block Data Class to Store Record Data

Add Relevant User Inputs to the Streamlit Interface

Test the PyChain Ledger by Storing Records

------

### Types Of Technology used
This Blockchain was built on the python platform using streamlit. 

* Streamlit is an open-source Python library that makes it easy to create and share beautiful, custom web apps for machine learning and data science. 

https://docs.streamlit.io/en/stable/


![pythonblockchain](https://media.onlinecoursebay.com/2019/07/30020503/2454264_fd7c-750x405.jpg)

![streamlitblockchain](https://blog.jcharistech.com/wp-content/uploads/2020/11/workingwithstfileuploads_streamlit_jcharistech.png)

-----

## Sample code 
```
@dataclass
class Block:

    # @TODO
    # Rename the `data` attribute to `record`, and set the data type to `Record`
    record: Record

    creator_id: int
    prev_hash: str = 0
    timestamp: str = datetime.datetime.utcnow().strftime("%H:%M:%S")
    nonce: str = 0

    def hash_block(self):
        sha = hashlib.sha256()

        record = str(self.record).encode()
        sha.update(record)

        creator_id = str(self.creator_id).encode()
        sha.update(creator_id)

        timestamp = str(self.timestamp).encode()
        sha.update(timestamp)

        prev_hash = str(self.prev_hash).encode()
        sha.update(prev_hash)

        nonce = str(self.nonce).encode()
        sha.update(nonce)

        return sha.hexdigest()


@dataclass
class PyChain:
    chain: List[Block]
    difficulty: int = 4

    def proof_of_work(self, block):

        calculated_hash = block.hash_block()

        num_of_zeros = "0" * self.difficulty

        while not calculated_hash.startswith(num_of_zeros):

            block.nonce += 1

            calculated_hash = block.hash_block()

        print("Wining Hash", calculated_hash)
        return block

    def add_block(self, candidate_block):
        block = self.proof_of_work(candidate_block)
        self.chain += [block]

    def is_valid(self):
        block_hash = self.chain[0].hash_block()

        for block in self.chain[1:]:
            if block_hash != block.prev_hash:
                print("Blockchain is invalid!")
                return False

            block_hash = block.hash_block()

        print("Blockchain is Valid")
        return True
```
# demonstration video 

https://user-images.githubusercontent.com/73854785/117518120-73825600-af53-11eb-94d6-70560a997303.mp4

