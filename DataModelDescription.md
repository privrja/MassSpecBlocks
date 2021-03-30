
## User [msb_user]

Necessary user data for login.

| name              | Type           | Properties       | Description                                                                                    |
| ----------------- | -------------- | ---------------- | ---------------------------------------------------------------------------------------------- |
| id                | INT            | PRIMARY KEY      | Unique identifier                                                                              |
| nick              | VARCHAR(180)   | UNIQUE, NOT NULL | Name for login                                                                                 | 
| roles             | JSON           | NOT NULL         | Application roles, ROLE_ADMIN can edit the visibility of containers and assign users to containers |
| password          | VARCHAR(255)   | NOT NULL         | Password stored as hash                                                                        |
| mail              | VARCHAR(255)   |                  | Email for reset password                                                                       |
| api_token         | VARCHAR(255)   | UNIQUE           | Token authentication                                                                           |
| conditions        | TINYINT(1)     | NOT NULL         | If user agree with terms and conditions                                                       |
| chem_spider_token | VARCHAR(255)   |                  | Apikey from ChemSpider to perform queries against it                                           |
| last_activity     | DATETIME       |                  | Time with last user activity, used for logout user when is inactive                            |

## Container [msb_container]

Users can create containers with sequences, blocks, etc. 

| name           | Type           | Properties          | Description                             |
| -------------- | -------------- | ------------------- | --------------------------------------- |
| id             | INT            | PRIMARY KEY         | Unique identifier                       |
| container_name | VARCHAR(255)   | NOT NULL            | Name of container                       |
| visibility     | VARCHAR(10)    | NOT NULL            | Visibility values: 'PRIVATE', 'PUBLIC'  |

## U2C [msb_u2c]

Relational table between User and Container M:N relationship.
Users can view/edit many Containers and Container may be view/edited by many users.

| name           | Type           | Properties                 | Description                                              |
| -------------- | -------------- | -------------------------- | -------------------------------------------------------- |
| id             | INT            | PRIMARY KEY                | Unique identifier                                        |
| user_id        | INT            | FOREIGN KEY, NOT NULL      | Reference to User                                        |
| container_id   | INT            | FOREIGN KEY, NOT NULL      | Reference to Container                                   |
| mode           | VARCHAR(10)    | NOT NULL                   | User rights to container, values: 'R', 'RW'              |  

## Sequence [msb_sequence]

The sequence consists of many Blocks and Modifications (Up to 3 - n, c, b).
The sequence is in the given Container and may have a SequenceFamily tag.

| name              | Type         | Properties            | Description                                 |
| ----------------- | ------------ | --------------------- | ------------------------------------------- |
| id                | INT          | PRIMARY KEY           | Unique identifier                           |
| n_modification_id | INT          | FOREIGN KEY           | Reference to n terminal Modification        |
| b_modification_id | INT          | FOREIGN KEY           | Reference to branch terminal Modification   |
| c_modification_id | INT          | FOREIGN KEY           | Reference to c terminal Modification        |
| container_id      | INT          | FOREIGN KEY, NOT NULL | Reference to Container                      |
| sequence_type     | VARCHAR(255) | NOT NULL, DEFAULT 'other' | Values: linear, cyclic, branched, branch-cyclic, linear-polyketide, cyclic-polyketide, other |
| sequene           | VARCHAR(500) | NOT NULL              | Comptuted sequence of block acronnyms       |
| sequence_original | VARCHAR(500) | NOT NULL              | Sequence with numbers not acronyms, used for deleting acronyms from sequence |
| sequence_name     | VARCHAR(255) | NOT NULL              | Name of sequence ex.: ```Cyclosporin A```   |
| sequence_formula  | VARCHAR(255) | NOT NULL              | Chemical formmula ex.: ```C62H111N11O12```  |
| sequence_mass     | DOUBLE       |                       | Mass of molecule ex.: ```1201.841368```     |
| sequence_smiles   | VARCHAR(4000)|                       | Description of molecula by SMILES format ex.: ```CCC1C(=O)N(CC(=O)N(C(C(=O)NC(C(=O)N(C(C(=O)NC(C(=O)NC(C(=O)N(C(C(=O)N(C(C(=O)N(C(C(=O)N(C(C(=O)N1)C(C(C)CC=CC)O)C)C(C)C)C)CC(C)C)C)CC(C)C)C)C)C)CC(C)C)C)C(C)C)CC(C)C)C)C``` |
| usmiles           | VARCHAR(4000)|                       | Unique SMILES representation                |
| source            | SMALLINT     |                       | Reference to other databases (can be extended), defined: PUBCHEM = 0, CHEMSPIDER = 1, NORINE = 2, const PDB = 3, CHEBI = 4 |
| identifier        | VARCHAR(255) |                      | Unique identifier of molecula in another database |
| decays            | VARCHAR(255) |                      | Auxiliary variable for coloring decay points      |
| unique_block_count| INT          | NOT NULL             | Unique number of blocks used in sequence, used for similarity search |
| block_count       | INT          | NOT NULL             | Number of blocks used in sequence (duplicit blocks are count in), used for similarity search |

**UNIQUE INDEX** on sequence_name and container_id columns.

## Modification [msb_modification]

| name                 | Type         | Properties              | Description                                 |
| -------------------- | ------------ | ----------------------- | ------------------------------------------- |
| id                   | INT          | PRIMARY KEY             | Unique identifier                           |
| container_id         | INT          | FOREIGN KEY, NOT NULL   | Reference to Container                      |
| modification_name    | VARCHAR(255) | NOT NULL                | Name of modification ex.: ```Acetyl```      |
| modification_formula | VARCHAR(255) | NOT NULL                | Chemical formmula ex.: ```H2C2O```          |
| modification_mass    | DOUBLE       |                         | Mass of molecule ex.: ```42.0105646863```   |
| n_terminal           | BOOLEAN      | NOT NULL, DEFAULT 0     | is n terminal?                              |
| c_terminal           | BOOLEAN      | NOT NULL, DEFAULT 0     | is c terminal?                              |

**UNIQUE INDEX** on modification_name and container_id columns.

## Block [msb_block]

| name              | Type         | Properties            | Description                                 |
| ----------------- | ------------ | --------------------- | ------------------------------------------- |
| id                | INT          | PRIMARY KEY           | Unique identifier                           |
| container_id      | INT          | FOREIGN KEY, NOT NULL | Reference to Container                      |
| block_name        | VARCHAR(255) | NOT NULL              | Name of modification ex.: ```Valine```      |
| acronym           | VARCHAR(30)  | NOT NULL              | Name of modification ex.: ```Val```         |
| residue           | VARCHAR(255) | NOT NULL              | Chemical formmula ex.: ```C5H9NO```         |
| block_mass        | DOUBLE       |                       | Mass of molecule ex.: ```99.068414```       |
| losses            | VARCHAR(255) |                       | Potencional losses ex.: ```NH3;CONH```      |
| block_smiles      | VARCHAR(255) |                       | Description of molecula by SMILES format ex.: ```CC(C)C(C(=O)O)N``` |
| usmiles           | VARCHAR(255) |                       | Description of molecula by SMILES format but in unique format       |
| source            | SMALLINT     |                       | Reference to other databases (can be extended), defined: PUBCHEM = 0, CHEMSPIDER = 1, NORINE = 2, const PDB = 3, CHEBI = 4 (same as values in Sequence)|
| identifier        | VARCHAR(255) |                       | Unique identifier of molecula in another database |
| is_polyketide     | TINYINT(1)   | NOT NULL, DEFAULT 0   | Flag if block is polyketide or not, when block is polyketide, his name should starts with (-2H) |

**UNIQUE INDEX** on block_name and container_id columns.


## B2S [msb_b2s]

Relational table between Sequence and Block M:N relationship.
The sequence can consist of many Blocks and Block can be in many Sequences.

| name                 | Type         | Properties            | Description                                 |
| -------------------- | ------------ | --------------------- | ------------------------------------------- |
| id                   | INT          | PRIMARY KEY           | Unique identifier                           |
| sequence_id          | INT          | FOREIGN KEY           | Reference to Sequence                       |
| block_id             | INT          | FOREIGN KEY           | Reference to Block                          |
| next_block_id        | INT          | FOREIGN KEY           | Reference to next block in sequence         |
| branch_reference_id  | INT          | FOREIGN KEY           | Reference to next block in branch           |
| is_branch            | TINYINT(1)   | NOT NULL, DEFAULT 0    | Flag if block is on branch                  |
| block_original_id    | INT          | NOT NULL              | Original id from SmilesDrawer               |
| sort                 | INT          | NOT NULL              | Order of blocks in Sequence                 |

## Block Family [msb_block_family]

| name              | Type         | Properties            | Description                                 |
| ----------------- | ------------ | --------------------- | ------------------------------------------- |
| id                | INT          | PRIMARY KEY           |  Unique identifier                          |
| container_id      | INT          | FOREIGN KEY, NOT NULL | Reference to Container                      |
| block_family_name | VARCHAR(255) | NOT NULL              | Name of block family tag                    |

**UNIQUE INDEX** on block_family_name and container_id columns.

## B2F [msb_b2f]

Relational table between Block and BlockFamily M:N relationship.
Block can have many BlockFamily tags and BlockFamily tags can be used on many Blocks.

| name              | Type         | Properties            | Description                                 |
| ----------------- | ------------ | --------------------- | ------------------------------------------- |
| id                | INT          | PRIMARY KEY           | Unique identifier                           |
| block_id          | INT          | FOREIGN KEY, NOT NULL | Reference to Block                          |
| family_id         | INT          | FOREIGN KEY, NOT NULL | Reference to BlockFamily                    |

## Sequence Family [msb_sequence_family]

| name                 | Type         | Properties            | Description                                 |
| -------------------- | ------------ | --------------------- | ------------------------------------------- |
| id                   | INT          | PRIMARY KEY           | Unique identifier                           |
| container_id         | INT          | FOREIGN KEY, NOT NULL | Reference to Container                      |
| sequence_family_name | VARCHAR(255) | NOT NULL              | Name of sequence family tag                 |

**UNIQUE INDEX** on sequence_family_name and container_id columns.

## S2F [msb_s2f]

Relational table between Sequence and SequenceFamily M:N relationship.
The sequence can have many SequenceFamily tags and the SequenceFamily tags can be used on many Sequences.

| name              | Type         | Properties            | Description                                 |
| ----------------- | ------------ | --------------------- | ------------------------------------------- |
| id                | INT          | PRIMARY KEY           | Unique identifier                           |
| sequence_id       | INT          | FOREIGN KEY, NOT NULL | Reference to Sequence                       |
| family_id         | INT          | FOREIGN KEY, NOT NULL | Reference to SequenceFamily                 |

## Organism [msb_organism]

| name                 | Type         | Properties            | Description                                 |
| -------------------- | ------------ | --------------------- | ------------------------------------------- |
| id                   | INT          | PRIMARY KEY           | Unique identifier                           |
| container_id         | INT          | FOREIGN KEY, NOT NULL | Reference to Container                      |
| organism             | VARCHAR(255) | NOT NULL              | Name of organism                            |

**UNIQUE INDEX** on the organism and container_id columns.

## S2O [msb_s2o]

Relational table between Sequence and Organism M:N relationship.
The sequence can have many Organism tags and the Organism tags can be used on many Sequences.

| name                 | Type         | Properties            | Description                                 |
| -------------------- | ------------ | --------------------- | ------------------------------------------- |
| id                   | INT          | PRIMARY KEY           | Unique identifier                           |
| organism_id          | INT          | FOREIGN KEY, NOT NULL | Reference to Organism                       |
| sequence_id          | INT          | FOREIGN KEY, NOT NULL | Reference to Sequence                       |

## Setup [msb_setup]

Independent table for application setup. Should have only one row forever.

| name                 | Type         | Properties                |  Description                                                 |
| -------------------- | ------------ | ------------------------- | ------------------------------------------------------------ |
| id                   | INT          | PRIMARY KEY               | Unique identifier                                            |
| similarity           | VARCHAR(10)  | NOT NULL, DEFAULT 'name'  | Values (name, tanimoto) tells which similarity search to use |

## Condition [msb_condition]

Independent table for terms and conditions as a blob text. In Application is used terms with the highest id.

| name                 | Type         | Properties                |  Description                                                 |
| -------------------- | ------------ | ------------------------- | ------------------------------------------------------------ |
| id                   | INT          | PRIMARY KEY               | Unique identifier                                            |
| text                 | TEXT         | NOT NULL                  | Terms and conditions text                                    |
