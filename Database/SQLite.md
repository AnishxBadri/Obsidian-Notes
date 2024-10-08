- [Architecture of SQLite](https://www.sqlite.org/arch.html)
	- SQLite works by compiling SQL text into bytecode, and then running that bytecode using a virtual machine.
	- ![[Screenshot 2024-09-11 at 1.26.46 PM.png]]
	 - Tokenizer breaks the SQL text into tokens and hands those tokens one by one to the parser. The tokenizer then calls the parser/
	 - Parser assigns meaning to tokens based on their context. Lemon parser generator is a thread safe
	 - After parser assembles tokens into a parse tree, code generator generates bytecode around this. For any SQL statement, the query planner is an AI that selects the best algorithm from these millions of choices.
	 - The bytecode program created by the code generator is run by a virtual machine.
	 - The database is maintained on disk using a B-tree implementation. Separate B-trees are used for each table and each index in the database.
	 - Page Cache is responsible for reading, writing, caching pages. The B-tree module requests information from the disk in such fix sized pages. The cache provides rollback and atomic commit abstraction and takes care of locking of the database file.
	 - For SQLite to be portable across operating systems, it uses an abstract object called VFS. Each VFS provides methods for opening, reading, writing and closing files on disk.
- [Why SQLite uses Bytecode](https://sqlite.org/draft/whybytecode.html)
	- 