
# How to use application

When you access the main page of the application.
You can see a finder form on the right side.
There you can choose in which chemical database you search and then choose search parameter.
You can search in PubChem, ChemSpider (apikey needed, [how to obtain ChemspiderKey]()), ChEBI, Norine, and PDB.
The search parameter is restricted by a selected chemical database.
Next table shows search restrictions.
In the Norine database, you can download all database data and then search in by attributes that are not provided in API, but this is **slow**.


| Database   | API  | name    | SMILES  | formula | mass        | identifier |
| ---------- | ---- | ------- | ------- | ------- | ----------- | ---------- |
| Pubchem    | REST | **Yes** | **Yes** | **Yes** | No          | **Yes**    |
| ChemSpider | REST | **Yes** | **Yes** | **Yes** | No (atomic) | **Yes**    |
| ChEBI      | SOAP | **Yes** | **Yes** | **Yes** | **Yes**     | **Yes**    |
| Norine     | REST | **Yes** | No      | Slow    | No          | **Yes**    |
| PDB        | REST | No      | No      | No      | No          | **Yes**    |


When you fill source database and search param, the main remaining thing is to fill search param and click on the Find button.
Now there are 3 possibilities what will happen.
Search not found anything, find one result, find more results.
When the result is only one structure is automatically filed to form and when SMILES is found then the structure is drawn into the left side of the page.
When there are more results is show under the form and you can choose one of them.
In the list, you can click on reference identifier and then you show structure in the source database page.
When you click on a small preview then the structure is increase to a full page.

For example, you could search roseotoxin by name on Pubchem.

![roseotoxin_find](https://user-images.githubusercontent.com/36856494/113470341-2cd1a580-9455-11eb-9d5c-2b722e9eace1.png)

On buttons in the bottom part of the form are more actions other than find.
You can transfer isomeric SMILES to canonical (one-way transformation), you can transfer SMILES to unique SMILES representation. 
Or you can edit SMILES in JSME by click on Edit.
If you have an account and select a container with RW rights, you can save the sequence to this container.
The most important function is to find building blocks of sequence.
Before you do that you can see red bonds (edges) on sequence preview. These are the decay points of peptide or ester bonds.
You can (un)select these bonds by clicking the bond on the preview.
After that, you can click on the button Build Blocks and wait for the application to show building blocks under the preview.

![roseotoxin_blocks](https://user-images.githubusercontent.com/36856494/113470797-7f609100-9458-11eb-9b3a-6e5862d6d05e.png)

After that operation you can see information about sequence type (linear, cyclic, branched, branch-cyclic, linear-polyketide, cyclic-polyketide, other), sequence blocks notation, pre-filled family by similarity and you can set up organisms and end modifications.
Next, you can see a table with blocks. When you are not logged in, blocks are searched in the default Nonribosomal Peptides and Siderophores container.
If some block is not found then is find on Pubchem by similarity search. 
The first column in the table indicates if the block is loaded from the database or not, as a value is showed the block acronym.
The next column is block preview, you can increase it to a full page by click on it.
You can edit information in it by click on a row that you would like to edit (All tables in the application works like that).
To edit block structure you can edit SMILES directly or use the button Edit to open JSME. 
Now same blocks are all edit together at once, but if you would like to change this behavior, you can unclick the checkbox above the table.

# Containers

As i mentioned in previous section, there are containers.
Container is like an envelope for a sequences, blocks, modifications, organism, families and others grouped together.
There are PUBLIC containers: Nonribosomal Peptides and Siderophores, Proteinogenic Amino Acids and Siderophores and Secondary Metabolites.
Nonribosomal Peptides and Siderophores is selected by default, it contains NRPs and siderophores sequences.
Proteinogenic Amino Acids containes only 20 Proteinogenic Amino Acid blocks.
Siderophores and Secondary Metabolites is specific in that it doesn't contains SMILES.
It's used in CycloBranch program for mass spectrometry as a whole, without blocks.
You can manage containers on Containers page, whre you see your PRIVATE containers and PUBLIC containers.
Other pages like Sequences, Blocks and Modifications are list with data about that entities.
Data on pages are always showed from selected container.
To create your containers you need to be login in application.
PUBLIC containers is manage by admin.

There are 3 types of permissions: R, RW and RWM.
Where R and RW is work as expected from name.
RWM is to manage container.
You have RWM role, when you create new container.
with this role you can add/remove other users to access your container and assign them roles.
On container detail page you can manage users with access to container and work with families and organisms.

![containers](https://user-images.githubusercontent.com/36856494/113471676-3d3a4e00-945e-11eb-9882-7d5386f68129.png)
![container_detail](https://user-images.githubusercontent.com/36856494/113471686-54793b80-945e-11eb-8cd2-f66645df2448.png)
![blocks](https://user-images.githubusercontent.com/36856494/113471699-72df3700-945e-11eb-8604-aaff8ca910c9.png)



